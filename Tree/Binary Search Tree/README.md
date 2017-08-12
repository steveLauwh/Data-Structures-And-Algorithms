## 二分查找法

二分查找法用于查找问题，对于有序数列，才能使用二分查找法。

顺序查找：用链表实现，无法索引数据，查找时间复杂度 O(n)，无法保证数据有序。

二分查找：用数组保存数据，查找时间复杂度 O(logn)，保证有序。

二分查找法的实现方法：迭代 和 递归。

![](https://github.com/steveLauwh/Data-Structures-And-Algorithms/raw/master/Tree/image/Binary%20Search%20Method.PNG)

`int mid = low + (high - low) / 2;`

## 二叉搜索树

### 二叉搜索树的特点

* 每个节点的键值大于左孩子，小于右孩子
* 不一定是完全二叉树
* 高效地查找、插入、删除元素
* 使用递归，可以方便处理
* 链式结构，每个节点有一个键和关联的值

```cpp
// 二叉搜索树的节点
struct BSTNode
{
    Value value;
    BSTNode *left;
    BSTNode *right;

    BSTNode(Value value)
    {
        this->value = value;
        this->left = this->right = NULL;
    }        
};
```

|         | 查找元素 |  插入元素  | 删除元素|
| --------| :-----: | :----:  |:----:  |
| 普通数组 | O(n) |  O(n) |O(n)|
| 顺序数组 |   O(logn)   |  O(n)   |O(n)|
| 二叉搜索树|    O(logn)     |  O(logn)  |O(logn) |

### 二叉搜索树的缺点

当数据是顺序或者倒序，那么构造的二叉搜索树出现一边倒的情况，这样查找的时间复杂度达到 O(n)。

### 二叉搜索树—插入「insert」

结合二叉搜索树的特点，对于第一个要存入的值，设置为根节点；当插入节点的值小于根节点的值，将其移动到左子树上，与左孩子节点比较；当插入节点的值大于根节点的值，将其移动到右子树上，与右孩子节点比较。

插入新节点操作有 递归 和 非递归 两种实现方式。

**递归版的插入**

```cpp
// insert 内部使用递归实现
BSTNode* recursionInsertNode(BSTNode *node, Value value)
{
    if (!node)
    {
        count++;
        return new BSTNode(value);
    }

    if (value < node->value)  // 待插入节点的值小于当前节点的值
    {
        node->left = recursionInsertNode(node->left, value);
    }
    else if (value > node->value) // 待插入节点的值大于当前节点的值
    {
        node->right = recursionInsertNode(node->right, value);
    }
    else
    {
        //node->value = value; // 已存在
        cout << "insert the element is exist!" << endl;
    }

    return node;
}
```

**非递归版的插入**

```cpp
// insert 内部使用非递归实现
BSTNode* nonrecursionInsertNode(BSTNode *node, Value value)
{
    if (!node)
    {
        count++;
        return new BSTNode(value);
    }

    BSTNode *bstNode = node; // 保证函数返回是二叉搜索树的根节点

    while (bstNode)
    {
        // 待插入节点的值小于当前节点的值
        if (value < bstNode->value)
        {
            if (!(bstNode->left))
            {
                count++;
                bstNode->left = new BSTNode(value);
                break;
            }
            else
            {
                bstNode = bstNode->left;
            }              
        }
        else if (value > bstNode->value)         // 待插入节点的值大于当前节点的值
        {
            if (!(bstNode->right))
            {
                count++;
                bstNode->right = new BSTNode(value);
                break;
            }
            else
            {
                bstNode = bstNode->right;
            }
        }
        else
        {
            //bstNode->value = value;
            cout << "insert the element is exist!" << endl;
            break;
        }
    }

    return node;
}
```

### 二叉搜索树—查找「search」

查找是查找某一个节点是否在二叉搜索树中，如果存在，返回 true，否则 false。

查找操作有 递归 和 非递归 两种实现方式。

查找 和 包含 操作本质是一样的。

**递归版的查找**

```cpp
// search 内部使用递归实现
bool recursionSearch(BSTNode *node, Value value)
{
    if (!node)
    {
        return false;
    }

    if (node->value == value)
    {
        return true;
    }
    else if (value < node->value)
    {
        return recursionSearch(node->left, value);
    }
    else
    {
        return recursionSearch(node->right, value);
    }
}
```

**非递归版的查找**

```cpp
// search 内部使用非递归实现
bool nonrecursionSearch(BSTNode *node, Value value)
{
    if (!node)
    {
        return false;
    }

    while (node)
    {
        if (node->value == value)
        {
            return true;
        }
        else if (value < node->value)
        {
            node = node->left;
        }
        else
        {
            node = node->right;
        }
    }

    return false;
}
```

### 二叉搜索树—删除「remove」

如何删除二叉搜索树中的任意节点

### 二叉搜索树—遍历「order」

> **前序遍历「preOrder」**

`根-->左-->右`

递归方式：先访问当前节点，再依次递归访问左子树和右子树。

非递归方式：为了把一个递归过程改为非递归过程，就需要自己维护一个辅助栈(队列)结构，记录遍历时的回退路径。

```cpp
stack<BSTNode*> s;
s.empty(); // 当前堆栈为空，返回true，否则不为空，返回 false
```

**递归版的前序遍历**

```cpp
// preOrder 内部使用递归实现
void recursionPreOrder(BSTNode *node)
{
    if (node)
    {
        cout << node->value << endl;
        recursionPreOrder(node->left);
        recursionPreOrder(node->right);
    }
}
```

**非递归版的前序遍历**

首先让根节点进栈，只要栈不为空，就可以做弹出操作，每次弹出一个结点，记得把它的左右结点都进栈，由于栈是先进后出，前序遍历是根左右遍历，那么右子树先进栈，这样可以保证右子树在栈中总处于左子树的下面。

```cpp
// preOrder 内部使用非递归实现，这里借用栈结构
void nonrecursionPreOrder(BSTNode *node)
{
    if (!node)
    {
        return;
    }

    stack<BSTNode*> s;
    s.push(node);  // 当前节点进栈

    while (!s.empty())  // 栈不为空
    {
        BSTNode *current = s.top();   
        cout << current->value << endl;

        s.pop();  // 先把当前节点出栈

        if (current->right) // 先右孩子节点进栈
        {
            s.push(current->right);
        }

        if (current->left) // 再左孩子节点进栈
        {
            s.push(current->left);
        }
    }        
}
```

> **中序遍历「inOrder」**

左-->根-->右

递归方式：先递归访问左子树，再访问自身，再递归访问右子树。

非递归方式：

> **后序遍历「postOrder」**

> **层序遍历「levelOrder」**

### 二叉搜索树—应用

> **查找二叉搜索树中的最小值**

> **查找二叉搜索树中的最大值**

> **删除二叉搜索树中的最小值**

> **删除二叉搜索树中的最大值**