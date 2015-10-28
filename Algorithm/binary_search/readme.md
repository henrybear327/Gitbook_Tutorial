# 二分搜：講解 (by: 黃鈺程)

以下出現 `A[l, r]` 代表 `A` 陣列中 `[l, r]` 這個區間。
同理 `A[l, r)` 代表 `A` 陣列中 `[l, r)` 這個區間。

以下範例皆不處理 IO 的部份，都假設變數皆已被讀入。

## 基本使用

大一時學過，我們可以用二分搜在一個單調（遞增或遞減）的陣列中，尋找某個值在哪裡：

> 給定一長度為 `N` 的遞增整數陣列 `A[]`，與一整數 `K`，請問是否有任一項 `A[x] = K`？

> 若有，請輸出 `x`；若無請輸出 `-1`

> Sample Input 1: `A[] = [1, 4, 6, 8, 9, 17], K = 6`

> Sample Output 1: `2`

> Sample Input 2: `A[] = [1, 4, 6, 8, 9, 17], K = 18`

> Sample Output 2: `-1`

```cpp
int solve() {
    int l = 0, r = N - 1; // 解可能所在的範圍為 [l, r]
    while (l <= r) {
        int mid = (l + r) / 2;

        if (A[mid] > K) // 解可能所在的範圍縮減為 [l, mid-1]
            r = mid - 1;
        else if (A[mid] < K) // 解可能所在的範圍縮減為 [mid+1, r]
            l = mid + 1;
        else // A[mid] == K
            return mid;
    }
    return -1; // 找不到
}
```

## lower_bound/upper_bound

如果題目變成：
> 給定一個長度為 `N` 的遞增整數序列 `A[]` 與一個整數 `K`，

> 求 `A` 中，第一個大於等於 `K` 的項是哪一項。

> 請輸出它的 index，若不存在（所有數皆小於 `K`），請輸出 `N`

> Sample Input 1: `A[] = [1, 4, 6, 8, 9, 17], K = 2`

> Sample Output 1: `1`

> Sample Input 2: `A[] = [1, 4, 6, 8, 9, 17], K = 18`

> Sample Output 2: `6`

前面使用封閉區間 `[l, r]` 的寫法就得改寫成這樣：
```cpp
int solve() {
    int l = 0, r = N-1;

    while (l <= r) {
        int mid = (l + r) / 2;

        if (A[mid] < K) // 解在 mid 的右邊
            l = mid + 1;
        else if (A[mid] > K) // 解在 mid 的左邊
            r = mid - 1;
        else // A[mid] = K，已找到解，但其左邊可能會有相同值的項。
            r = mid - 1;

        // 即然 A[mid] > K, A[mid] = K 是做同樣事，可簡寫成
        // if (A[mid] < K) l = mid + 1;
        // else r = mid - 1;
    }
    // 有解時，上面迴圈結束，保證了 l = r，即為答案
    // 無解時，l 會一直右移直到超過 N-1 為止，即 l = N
    return l;
}
```

但這裡介紹使用半封閉區間 `[l, r)` 的寫法，這個寫法是以後所有二分搜的基礎：
```cpp
int solve() {
    int l = 0, r = N; // 解的範圍是 [l, r)

    while (r - l > 1) { // 如果 A[l], A[r] 尚不是相臨項
        int mid = (l + r) / 2;
        if (A[mid] < K) l = mid; // 解的範圍變成 [mid, r)
        else r = mid; // 解的範圍變成 [l, mid)
    }
    // 迴圈結束時，保證了 A[l] < K，且 A[r] >= Ｋ
    // 所以直接回傳 r 即為答案。
    return r;
}
```

這樣寫應該感覺好想多了是吧？！

如果題目改成求 **大於** `K` 的第一項呢？只需要把
```cpp
if (A[mid] < K)
```
這裡改成
```cpp
if (A[mid] <= K)
```
即可。

------------------

這兩個題目就是常見的求下界 (`lower_bound`) 與上界 (`upper_bound`)。
C++ 的函式庫 `algorithm` 底下的有提供這兩個函數，但搜索的空間僅限在陣列上。
（解的範圍常常大到無法存成陣列的型式，後面會講解）

### 基本應用

這裡給出一個著名的利用 `lower_bound`, `upper_bound` 的題目：
> 給定一個遞增的整數序列 `A[]`，與一整數 `K`，求 `K` 在此序列中的出現次數。

> 要求時間複雜度須在 `O(N)` 以下，不含 `O(N)`，所以不能從頭到尾掃一遍

> Sample Input 1: `A = [1, 1, 2, 2, 2, 3], K = 2`

> Sample Output 1: `3`

> Sample Input 2: `A = [1, 1, 2, 2, 2, 3], K = 4`

> Sample Output 2: `0`

`lower_bound` 是求解序列中第一個 **大於等於** `K` 的項。

`upper_bound` 是求解序列中第一個 **大於** `K` 的項。

以 Sample Input 1 為例，`lower_bound = A[2], upper_bound = A[5]`，
這兩項之間 `A[2, 5)` 的每一項不就是全部都等於 `K` 嗎！共有 `5 - 2 = 3` 項，即為答案。
所以只需做一次 `lower_bound`, 再做一次 `upper_bound，即可求到答案，`
時間複雜度為 `O(log(N)) + O(log(N)) = O(log(N))` 。
（在資工領域裡看到 `log()` 通常是指以 2 為底的對數，即 `lg()`）

```cpp
int solve() {
    // algorithm 底下的 lower_bound, upper_bound
    // 會回傳 iterator 這個型態，你可以把它想像成 C 中的指標
    // 就像我可以用這樣來得到指標是指向第幾項，iterator 也可以這麼做
    // int A[] = {...};
    // int* ptr = &A[3];
    // printf("%ld", ptr - A); // 3
    int idx_of_lb = lower_bound(A, A + N, K) - A;
    int idx_of_ub = upper_bound(A, A + N, K) - A;
    return idx_of_ub - idx_of_lb;
}
```

## 模板（時間複雜度皆為 O(lg(N))）

假使把 `A[mid] < K` 視為一個函數 `C(mid)`，這個函式回傳 0（不成立） 或 1 （成立）

我們可以發現，如果有解的話，在解的範圍上，`C(x)` 是這樣分佈的：
```no-highlight
... 1 1 1 1 0 0 0 ...
```
如果沒解的話，就是
```no-highlight
... 0 0 0 0 0 0 0 ...
```

所以函數在 `C(x)` 解的空間 `[a, b]` 分佈為
```no-highlight
... 1 1 1 1 0 0 0 ...
```
這種情形時，我們可以寫出以下模板來計算 `0`, `1` 是在哪一項分隔的。

```cpp
// 使用 [l, r)
int lb = a, ub = b + 1; // 初使時，若 C(lb) = 1, C(ub) = 0，則保證有解

while (ub - lb > 1) {
    int mid = (lb + ub) / 2;
    if (C(mid)) lb = mid;
    else ub = mid;
}
// 結束時，若有解，則 C(lb) = 1, C(ub) = 0
```

-----------------

同理可推出，如果 `C(x)` 表是
```no-highlight
... 0 0 0 1 1 1 1 ...
```
這種形式時，可以寫成

```cpp
// 使用 (lb, ub]
int lb = a - 1, ub = b; // 初使時，若 C(lb) = 0, C(ub) = 1，則保證有解。

while (ub - lb > 1) {
    int mid = (lb + ub) / 2;
    if (C(mid)) ub = mid;
    else lb = mid;
}
// 結束時，若有解，則 C(lb) = 0, C(ub) = 1
```

### 解的空間為浮點數時

當解的空間為浮點數時，就不能使用 `while (ub - lb > 1)` 這種寫法了。
這時就改用定量資數的二分搜，只要保證搜索的次數夠多，
誤差就可以縮小至題目要求的誤差以內。
搜尋 50 次，就相當於把解的空間除以 2^50，精度通常來說就已經足夠了。
這次你把 lb 當答案，把 ub 當答案都可。

```cpp
while (ub - lb > 1)
```
換成
```cpp
for (int i = 0; i < 50; i++)
```

### 例題

> 給定 `i, j (0 < i < j < 10^20)`、一整數 `K (0 < K < 10^40)`

> 在 `[i, j]` 中，保證存在 `x` ，使得 `f(x) <= K`，其中 `f(n) = n * n`

> 請問 `x` 最大是多少？

> Sample Input 1: `[i, j) = [1, 10^9), K = 10`

> Sample Output 1: `x = 3`

> Sample Input 2: `[i, j] = [10^9, 10^10), K = 10^20`

> Sample Output 2: `x = 10^10`


很明顯地，陣列是一定開不出來的，不過我們也不需要開陣列啊。：
```no-highlight
Let C(x) = whether f(x) <= K
```
`C(x)` 在 `[i, j]` 明顯會形成
```no-highlight
... 1 1 1 1 0 0 0 ...
```
這種形式，直接用模板。完整程式碼：
```cpp
typedef long long ll; // 用 long long，簡寫成 ll

bool C(int x) { return x * x <= K; }

int solve() {
    // 使用 [lb, ub)
    ll lb = i, ub = j + 1;
    while (ub - lb > 1) {
        ll mid = (lb + ub) / 2;
        if (C(mid)) lb = mid;
        else ub = mid;
    }
    return lb;
}
```

二分搜時間複雜度 `O(lg(N))` 的威力由此可見，測資的範圍最大會是一個長 `10^20` 的區間，
但在此情況下，我們也只需約 `lg(10 ^ 20) = 66` 次查詢，即可得知結果。
其中每次查詢，就是呼叫 `C(x)`，在這題中，`C(x)` 只是做一個簡單的比較，`O(1)` 的時間。

# 二分搜：解題

以下 poj 是指 pku online judge

二分搜常被用來解這幾種題目：

1. 最大值最小化

2. 最小值最大化

3. 平均最大化

4. 其他

下面的題目，都是書上的題目，我基本上都解過了，可以去翻我的 gists，
但需注意的是，那些題解是寫在這篇教學之前，我剛學習二分搜之時，可能會有一些錯誤。

## 題目

### poj 3258（最大值最小化）

`N` 個石頭排成一列，移除 `M` 個石頭後，相鄰石頭間的最小距離最大是多少？

```no-highlight
C(d) = 移除 M 個石頭後，能否使相鄰石頭間的最短距離 >= d
     = 計算相鄰石頭間距離小於 d 的有幾個，是否 <= M
C(d) 表：1 1 1 1 0 0 0，找最後一個 1
```

### poj 3273（最小值最大化）

給定長度為 `N` 的數列，分成連續的 `M` 段，使每段的和中的最大值最小，求此最小值？
```no-highlight
C(s) = 可否在分解成 M 段後，最大的和 <= s
     = 計算當每段的最大值 = s 時，可分解出幾段，此個數是否 <= M
C(s) 表：0 0 0 1 1 1 1，找第一個 1
```

### poj 3111（平均最大化）

重量與價值分別為 `w[i]`, `v[i]` 的 `N` 個物品，從中選出 `K` 個，
使單位重量的價值最大，求此值？
```no-highlight
C(a) = 選 K 個，可能使單位重量的價值 >= a
設 S 是解的集合，
單位重量的價值 = sum(v[i] for i in S) / sum(w[i] for i in S) >= a
移項可得 sum(v[i] for i in S) - a * sum(w[i] for i in S) >= 0
即我們只需找出 v - a * w 最大的 K 個物品（排序），看他們的單位重量價值是否 >= a
C(a) 表：1 1 1 1 0 0 0，找最後一個 1
```

### poj 3662（其他）

給定一個有權無向圖，欲從點 `0` 鋪電纜到點 `N-1`，電纜鋪在邊上面
其中 `K` 條電纜免費，其它自費，求須自費的電纜中最長的是多少？
```no-highlight
C(L) = 可否使路徑上長於 L 的邊少於等於 K 條
     = (使用 Dijkstra, d[x] = 從 0 走到 x 最少需要幾條 > L 的邊) d[N-1] <= K
C(L) 表：0 0 0 1 1 1 1，找第一個 1
```

其它的題目為 `poj1064`, `poj2456`, `poj3104`, `poj3045`, `poj2976`, `poj3579`, `poj3685`,
`poj3662`, `poj1759`, `poj3484`。
