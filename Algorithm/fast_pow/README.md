# 快速冪 Exponentiation by squaring | 黃鈺程

> 給定整數 `x` (0 < x < 10^9) 、整數 `n` (0 <= n < 10^9)，求取 `x ^ n`

> Sample Input 1: x = 2, n = 22

> Sample Output 1: 4194304

> Sample Input 2: x = 1, n = 0

> Sample Output 2: 1

通常這類題目還會給定一個較小的數 `M`，然後要求輸出 `(x ^ n) % M`。
因為這樣解題者就不用使用大數了，這題要考的也不是大數。

另外，這種題目時限會被壓的極短（或測資量極大），讓你用 `O(n)` 的解法會 TLE。

快速冪是矩陣加速的基礎，矩陣加速是好物。因此請務必學會快速冪~

## Naive Solution

就把 `x` 乘 `n` 次，看是多少……時間複雜度 `O(n)`

## 建表

當 `n` 的範圍大到 10^9，陣列是開不出來的。只能改用 map/dict 之類的資料結構來做，
這樣查詢的時間複雜度是 `O(lg(MAX_N))`，還不錯，但預處理為 `O(MAX_N * lg(MAX_N))`，
實在太花時間了，而且這樣做會需要極大的空間。

## 快速冪

正式名稱叫 Exponentiation by squaring，不過許多人簡稱它為快速冪。

顯而易見的，我們可以在 `O(lg(n))` 的時間計算出
```no-highlight
x, x^2, x^4, x^8, x^16, ..., x^(2^m) (2 ^ m <= n) ... 式 1
```
這些數（每一項都是前一項的平方）。我們可以利用這些數組合出 `x^n`。

例如
```no-highlight
x^22 = (x^16) * (x^4) * (x^2)
x^9 = (x^8) * (x^1)
```
有沒有發現什麼？這根本就是 `n` 的二進位拆解啊！

沒看出來？以 `x^22` 為例

| 22 的二進位 |   1  |  0  |  1  |  1  |  0  |
|:-----------:|:----:|:---:|:---:|:---:|:---:|
|      i      |   4  |  3  |  2  |  1  |  0  |
|     2^i     |  2^4 | 2^3 | 2^2 | 2^1 | 2^0 |
|   x^(2^i)   | x^16 | x^8 | x^4 | x^2 | x^1 |

只要二進位中對應的位置 `i` 是 1，我們就要乘上對應的 `x^(2^i)`。

於是，要計算 `x^22`，我們只要計算出 `(x^16)`, `(x^4)`, `(x^2)`。
而這些東西，我們知道可以快速地在 `O(lg(n))` 計算出。

於是，我們設計出一個演算法：

> 我們依序計算出 `式 1`，針對第 `i` 項，即 `x^(2^i)`，如果 `n` 的二進位中的第 `i` 項是 `1` 的話，
> `x^(2^i)` 就是解的一部分。當我們把所有這種 `x^(2^i)` 找出來後，全部乘起來就是 `x^n` 了。

```cpp
// 用 unsigned int 防止 n 左移時跑到負數去（這行你看不懂的話，去複習 2's complement 吧）
int fast_pow(int x, unsigned int n) {
    int result = 1; // 解
    int base = x; // x ^ (2^i)

    for (unsigned int i = 0; (1 << i) <= n; base = base * base) {
        if (n & (1 << i)) { // 如果位置 i 是 1
            result = result * base;
        }
    }

    return result;
}
```

※ `(1 << i)` 就是 0000...001 這個數左移 `i` 位，變成 000...1...000，
讓它跟 `n` 做 AND（bitwise AND），即可知道 `n` 的二進位中第 `i` 位是不是 1。

回憶一下：
```no-highlight
0 & 0 = 0
0 & 1 = 0
1 & 0 = 0
1 & 1 = 1
```
任何位元與 1 做 AND 就會得到它本身。

另一種寫法，不用 `unsigned int`：
```cpp
int fast_pow(int x, int n) {
    int result = 1;
    int base = x;

    while (n != 0) { // 從尾端一個一個拆解出位元
        if (n & 1)
            result = result * base;
        base = base * base;
        n >>= 1; // 即 n /= 2
    }

    return result;
}
```

------------------

這個演算法還可以這麼想：

> 針對 x^n，

> 如果 n 是偶數，則 x^n = (x ^ 2) ^ (n / 2)；

> 如果 n 是奇數，則 x^n = (x ^ 2) ^ ((n-1) / 2) * x;

用遞迴寫成程式：
```cpp
int fast_pow(int x, int n) {
    if (n == 0)
        return 1;

    if (n & 1) // n 是奇數，也可寫 if (n % 2 == 1)
        return fast_pow(x * x, (n-1) / 2) * x;
    else
        return fast_pow(x * x, n / 2);
}
```
完全等價於前面用迴圈的寫法。

------------------------------

如果題目是要求，輸出的結果為 `x^n mod M`，我們不可能把 `x^n` 計算出來後再 `mod M`，
因為這樣很可能會在計算過程中，值超出 int 的範圍，所以利用
```no-highlight
(a * b) mod M = ((a mod M) * (b mod M)) mod M
```
我們每次乘 `base` 到 `result` 時與 `base` 平方時，mod 一下， 最後的結果就是所求了。

```cpp
int fast_pow(int x, int n, int M) {
    int result = 1;
    int base = x;

    while (n != 0) { // 從尾端一個一個拆解出位元
        if (n & 1)
            result = result * base % M;
        base = base * base % M;
        n >>= 1; // 即 n /= 2
    }

    return result;
}
```

```cpp
int fast_pow(int x, int n, int M) {
    if (n == 0)
        return 1;

    if (n & 1) // n 是奇數，也可寫 if (n % 2 == 1)
        return fast_pow((x * x) % M, (n-1) / 2) * x % M;
    else
        return fast_pow((x * x) % M, n / 2) % M;
}
```

## 題目

[poj 3641](http://poj.org/problem?id=3641)

[poj 1995](http://poj.org/problem?id=1995)

基本上，單獨考快速冪的題目並不多，更多的是混合矩陣加速（矩陣快速冪）一起考…
