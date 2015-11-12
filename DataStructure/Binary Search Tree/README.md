# 二元搜尋樹 Binary Search Tree | 黃鈺程

## 前置知識

1. 遞迴

2. 基本 Tree 的認識與實作。

3. 基本指標(pointer)的操作。

## 定義

BST 是一棵空樹或是一棵二元樹 (Binary Tree)，每個節點 `N` 都符合以下性質：

```
1. 若該節點的左節點 N->left 不為空，則 N 的比較序大於 N->left 的比較序

2. 若該節點的右節點 N->right 不為空，則 N 的比較序小於 N->right 的比較序

3. 該節點的左、右節點各是一個二元樹。（左子樹、右子樹）

4. 無任何兩個節點的比較序相同。
```

定義比較序為比較節點值的大小：
[圖1]

以下皆以此為例：
```cpp
struct Node_ {
    int value;
    struct Node_* left;
    struct Node_* right;
};
typedef struct Node_ Node;
```

根據定義，可以發現 BST 的 **中序遍歷(Inorder Traversal)** 的結果就是
節點按照比較序，**由小到大遍歷** 的結果。

BST 支援查找、插入、刪除、遍歷等操作。

使用範例：
```cpp
int main() {
    Node* root = NULL;
    root = bst_insert(root, 4);
    root = bst_insert(root, 2);
    root = bst_insert(root, 5);
    root = bst_insert(root, 6);
    root = bst_insert(root, 3);

    //     4     
    //    / \    
    //   2   5   
    //    \   \  
    //     3   6

    if (bst_find(root, 7)) // false
        puts("7 exists in BST.");
    if (bst_find(root, 3)) // true
        puts("3 exists in BST.");

    if (bst_find(root, 4))
        root = bst_remove(bst, 4);
    if (bst_find(root, 3))
        root = bst_remove(bst, 3);
    //
    //
    //
    inorder_traversal(root); // ...

    printf("%d\n", root->right); // ...

    return 0;
}
```

使用方法：
```cpp
Node* root;
// ...
if (bst_find(root, x)) {
    // ...
}
```

## 查找

利用 BST 的定義，來快速的搜尋 `x` 存不存在。
若 `Node* root` 是 BST 的根節點。

```
1. 若 root = NULL（代表該 BST 為空），則回傳 false(不存在) 。

   若 root 不為 NULL，則 x 與 root->value 比較，三種情況：

2. x < root->value: x 若存在，必在 root 的左子樹中，對左子樹遞迴，回到步驟 1

3. x > root->value: x 若存在，必在 root 的右子樹中，對右子樹遞迴，回到步驟 1

4. x = root->value: 找到值，回傳 true(存在)
```

[圖2]

```cpp
// 搜尋 x 存不存在於以 p 為 root 的 BST 中。
bool bst_find(Node* p, int x) {
    if (p == NULL) // 該子樹是空的。
        return false;

    if (x < p->value)
        return bst_find(p->left, x);
    else if (x > p->value)
        return bst_find(p->right, x);
    else // x = p->value
        return true;
}
```

## 插入

類似於搜尋，欲插入 `x` 這個值，我們尋找它該所在的位置（是一個 `NULL` 的節點）：
```
1. 若 root = NULL，則這個位置就是我們要插入的位置。新增節點，節點的值 = x。

   若 root 不為 NULL，則尋找 x 的位置 x 與 root->value 比較，三種情況：

2. x < root->value: x 的位置在 root 的左子樹中，對左子樹遞迴，回到步驟 1

3. x > root->value: x 的位置在 root 的右子樹中，對右子樹遞迴，回到步驟 1

4. x = root->value: 看題目是要做什麼，有些要記錄 x 的出現次數，此時就可以修改。
   若不想這個 case 發生，可在 insert 前就先用 bst_find 來判斷掉這個情況。
```

[圖3]

要實作這個東西，方法有很多，其中之一就是使用雙重指標…
但用雙重指標一不小時就寫出 bug，還常常找不出來…

這裡使用一個 **利用回傳值重新將變數賦值** 的方法。

呼叫此函式要寫成：
```cpp
Node* root;
// ...
root = bst_insert(root, x);
```
而不是
```cpp
Node* root;
// ...
bst_insert(root, x);
```

```cpp
// 在 以 p 為 root 的 BST 中，插入值 x
// 若節點 p 有更動（新增），回傳更動後的結果（新的節點）；
// 若節點 p 無更動，回傳 p
Node* bst_insert(Node* p, int x) {
    if (p == NULL) { // 新增節點
        new_node = (Node*) malloc (sizeof(Node));
        new_node->left = NULL;
        new_node->right = NULL;
        new_node->value = x;
        return new_node;
    }

    if (x < p->value)
        p->left = bst_insert(p->left, x); // 注意是 p->left = recursion...
    else if (x > p->value)
        p->right = bst_insert(p->right, x); // 注意是 p->right = recursion...
    else
        // ... x already in BST，依題意實作這裡。

    return p; // 這行別忘了
}
```

## 刪除

這應該是 BST 裡最難的…

### 原理

直接舉例，欲刪除值為 7 的那個節點。

圖4

刪除掉 7 後，這個空出來的位置，該怎麼處理呢？
很明顯地，這個空格只能從剩餘的節點裡 **移** 一個節點上來，
並且，放到這個位置的節點仍需滿足 BST 的性質：這節點的值需大於 5，小於 8。

在這個例子中，我們可以發現 與 這兩個節點都可以，選其中之一即可。
至於為什麼是這兩個節點？
因為他們是分別是 7 的 **左子樹中值最大的節點**，與 **右子樹中值最小的節點** 。

圖5

也只有這兩個節點，其值可以使 BST 的定義被滿足。不懂？證給你看~
```
假設欲刪除的節點為 n，其值為 v[n]。左子樹中值最大的節點為 k，值為 v[k]。

因為 k 在 n 的左子樹中，所以
v[k] < v[n] < v[n->right]

因為 k 是左子樹中最大的，所以
v[k] > v[n->left] (n->left 在 n 的左子樹中，當然~)

綜合起來：
v[n->left] < v[k] < v[n->right]

這即是 BST 的定義（性質）。
所以把 k 補到 n 的位置是正確的，沒有破壞 BST 的定義（性質）。
```
同理可證右子樹中值最小的節點也是可以的。

在這篇教學裡，我們使用 **左子樹中值最大的節點** 。

### 實作

至於是怎麼實作的呢？

首先得知道，因為 `k` 的定義，`k` 必為其 parent（設為 `r`）的右子節點，並且 `k` 沒有右子節點。
若要讓 `k` 是左子樹裡值最大的節點，`k` 必落在 `n` 左子節點的右子樹上，並且是此右子樹的最右端。
只有在此，`k` 才會是 `n` 的左子樹裡值最大的節點。

圖6（k 的位置）

```
1. 切開 k 與 r 的連結、切開 k 與其左子樹的連結，左子樹上移 ...... 式 1

2. 將 k 移到 n 的位置： k->left = n->left, k->right = n->right ...... 式 2

3. n 的 parent 原本連到 n 的那個連結改成連到 k ...... 式 3

4. 釋放 n 的空間。...... 式 4
```

圖7.1, 7.2

-------------------------

但在以下情形中，`k` 將不存在，因此做 special case 判斷：

```
1. n 左子樹為空，此時直接將 n 的右子樹全部往上移。...... 式 5

2. n 的左子節點的右子樹為空，此時直接將 n 的左子樹往上移。...... 式 6
   ※ 右子樹裡最大值存在，但不符合前面對 k 的定義（k 為 r 的右子節點），視為 special case
```

圖8

圖9


至此就是整個 BST 刪除的想法，整理如下：

```
1. 定位 n

2. 式 5：n->left = NULL

3. 式 6：n->left->right = NULL

4. 式 1, 2, 4：找 r, k

※ 式 3 被實作在遞迴中。
```

### 程式碼

與插入時相同，不想使用雙重指標，我們就利用回傳值：

```cpp
// 若節點 p 有更動，回傳更動後的結果（=新的節點=補上來的結點）；
// 若節點 p 無更動，回傳 p
Node* bst_remove(Node* p, int x) {
    if (p == NULL) return NULL; // 此值不存在

    if (x < p->value)
        p->left = bst_remove(p->left, x); // 這裡實作了 式 3
    else if (x > p->value)
        p->right = bst_remove(p->right, x); // 這裡實作了 式 3
    else { // 定位出來了，此時 p = n
        if (p->left == NULL) { // 式 5： n 左子樹為空
            Node* q = p->right; // 右子樹直接上移
            free(p);
            return q;
        }
        else if (p->left->right == NULL) { // 式 6：n 的左子樹是一個左偏樹
            Node* q = p->left; // 左偏樹上移
            q->right = p->right;
            free(p);
            return q;
        }
        else {
            Node* r; // parent of k
            for (r = p->left; r->right->right != NULL; r = r->right); // find r
            Node* k = r->right;

            r->left = k->left; // 左子樹上移

            k->left = p->left; // 式 2：將 k 移到 n 的位置
            k->right = p->right;

            free(p);
            return k;
        }
    }

    return p; // 記得要寫~
}
```

呼叫記得是寫成這樣：
```cpp
Node* root;
...
root = bst_remove(root, x);
```

## Traversal

### Inorder Traversal

Preorder, Postorder 就不寫了，自己改。

```cpp
void inorder_traversal(Node* p) {
    if (p == NULL) return;

    inorder_traversal(p->left);
    printf("%d ", p->value);
    inorder_traversal(p->right);
}
```

### Level Order Traversal

就是簡化版 BFS，不解釋，用 queue

```cpp
void level_order_traversal(Node* root) {
    queue<Node*> q;
    // 不用像 Graph 上的 BFS 記錄每個點有沒有 visit 過，
    // 因為 BST 是 tree (沒有環)，不會出現點重覆 visit 的情況。

    if (root != NULL)
        q.push(root);

    while (!q.empty()) {
        Node* cur = q.top(); q.pop();
        printf("%d ", cur->value);
        if (cur->left != NULL) q.push(cur->left);
        if (cur->right != NULL) q.push(cur->right);
    }
}
```

## 釋放 BST 的空間

利用遞迴：

```cpp
void free_bst(Node* p) {
    if (p == NULL) return;

    free_bst(p->left);
    free_bst(p->right);

    // free(p->data); // 如果 struct 裡有需釋放的資料，記得要先釋放
    free(p);
}
```

## 時間複雜度

當樹是平衡的，時間複雜度為 `O(lg(N))`，即樹的高度，`N` 是 BST 中節點的數量。

在一些測資中（例如進來的資料是單調的），樹會變成歪斜的，
相當於退化成 **長度為 `N` 的 linkedlist**，此時查找、插入、刪除等操作的複雜度都上升到 `O(N)`。

[圖10]

於是有一些資料結構 AVL Tree, Red Black Tree 等，就是利用左旋與右旋等操作，來讓 BST 維持平衡，
致使不會發生那些使 BST 退化的情況。

## 題目
