## 基本数据结构——链表

对表的所有操作都可以使用数组来实现。由于插入和删除的线性开销，引入另一种实现方式：链表。

## LeetCode Linked List

* [Linked List Cycle](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Linked%20List%20Cycle)
* [Delete Node in a Linked List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Delete%20Node%20in%20a%20Linked%20List)
* [Add Two Numbers](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Add%20Two%20Numbers)
* [Merge Two Sorted Lists](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Merge%20Two%20Sorted%20Lists)
* [Remove Duplicates from Sorted List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Remove%20Duplicates%20from%20Sorted%20List)
* [Reverse Linked List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Reverse%20Linked%20List)
* [Remove Linked List Elements](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Remove%20Linked%20List%20Elements)
* [Intersection of Two Linked Lists](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Intersection%20of%20Two%20Linked%20Lists)
* [Palindrome Linked List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Palindrome%20Linked%20List)
* [Partition List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Partition%20List)
* [Rotate List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Rotate%20List)
* [Sort List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Sort%20List)
* [Insertion Sort List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Insertion%20Sort%20List)
* [Swap Nodes in Pairs](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Swap%20Nodes%20in%20Pairs)
* [Odd Even Linked List ](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Odd%20Even%20Linked%20List)
* [Remove Nth Node From End of List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Remove%20Nth%20Node%20From%20End%20of%20List)
* [Reorder List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Reorder%20List)
* [Convert Sorted List to Binary Search Tree](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree)
* [Copy List with Random Pointer](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Copy%20List%20with%20Random%20Pointer)
* [Plus One Linked List](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Plus%20One%20Linked%20List)
* [Design Phone Directory](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Design%20Phone%20Directory)
* [Reverse Nodes in k-Group](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Reverse%20Nodes%20in%20k-Group)
* [Merge k Sorted Lists](https://github.com/steveLauwh/Data-Structures-And-Algorithms/tree/master/Linked%20List/Merge%20k%20Sorted%20Lists)

![](https://github.com/steveLauwh/Data-Structures-And-Algorithms/raw/master/image/Linked%20List(I).PNG)

![](https://github.com/steveLauwh/Data-Structures-And-Algorithms/raw/master/image/Linked%20List(II).PNG)

![](https://github.com/steveLauwh/Data-Structures-And-Algorithms/raw/master/image/Linked%20List(III).PNG)

## 链表的测试

LinkedListTest.cpp
```cpp
#include <iostream>

using namespace std;

/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class LinkedList {
public:
    ListNode* createLinkedList(int* arr, int n) {
        if (n == 0) {
            return NULL;
        }
       
        ListNode *head = new ListNode(arr[0]);
        ListNode *cur = head;
        
        for (int i = 1; i < n; i++) {
            cur->next = new ListNode(arr[i]);
            cur = cur->next;
        }
        
        return head;
    }
    
    void deleteLinkedList(ListNode* head) {
        ListNode *cur = head;
        
        while (cur) {
            ListNode *deleteNode = cur;
            cur = cur->next;
            delete deleteNode;
        }
        
        return;
    }
    
    void printLinkedList(ListNode* head) {
        ListNode *cur = head;
        
        while (cur) {
            cout << cur->val << " -> ";
            cur = cur->next;
        }
        
        cur << "NULL" << endl;
        
        return;
    }
}
```
