### 复制带随机指针的链表（LeetCode 题目 138）

#### 3.1 题目大意
描述：给定一个链表的头节点 `head`，链表中每个节点除了 `next` 指针之外，还包含一个随机指针 `random`，该指针可以指向链表中的任何节点或者空节点。

要求：将该链表进行深拷贝。返回复制链表的头节点。

#### 说明
- 链表中的节点数目在范围 `[0, 1000]` 内。
- -10^4 ≤ `Node.val` ≤ 10^4。
- `Node.random` 为 `null` 或指向链表中的节点。

#### 示例
```c
输入：head = [[7, null], [13, 0], [11, 4], [10, 2], [1, 0]]
输出：[[7, null], [13, 0], [11, 4], [10, 2], [1, 0]]

输入：head = [[1, 1], [2, 1]]
输出：[[1, 1], [2, 1]]
```

### 解题思路
要复制一个带随机指针的链表，我们可以使用两次遍历来实现：

1. 第一次遍历创建所有的新节点，并将新节点插入到原链表节点之后。
2. 第二次遍历设置新链表的 `random` 指针。

最后，我们将原链表和新链表分离。

### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>

// 定义链表节点结构
struct Node {
    int val;
    struct Node* next;
    struct Node* random;
};

// 复制带随机指针的链表
struct Node* copyRandomList(struct Node* head) {
    if (head == NULL) return NULL;

    struct Node* curr = head;

    // 第一次遍历：创建新节点并插入到原节点之后
    while (curr != NULL) {
        struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
        newNode->val = curr->val;
        newNode->next = curr->next;
        curr->next = newNode;
        curr = newNode->next;
    }

    // 第二次遍历：设置新链表的 random 指针
    curr = head;
    while (curr != NULL) {
        if (curr->random != NULL) {
            curr->next->random = curr->random->next;
        }
        curr = curr->next->next;
    }

    // 第三次遍历：分离原链表和新链表
    curr = head;
    struct Node* newHead = head->next;
    while (curr != NULL) {
        struct Node* newNode = curr->next;
        curr->next = newNode->next;
        if (newNode->next != NULL) {
            newNode->next = newNode->next->next;
        }
        curr = curr->next;
    }

    return newHead;
}

// 打印链表（用于测试）
void printList(struct Node *head) {
    struct Node *temp = head;
    while (temp != NULL) {
        printf("Node value: %d", temp->val);
        if (temp->random) {
            printf(", Random points to: %d", temp->random->val);
        } else {
            printf(", Random points to: NULL");
        }
        printf("\n");
        temp = temp->next;
    }
}

// 创建新节点（用于测试）
struct Node* createNode(int val) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->val = val;
    newNode->next = NULL;
    newNode->random = NULL;
    return newNode;
}

int main() {
    // 创建链表 [7, null], [13, 0], [11, 4], [10, 2], [1, 0]
    struct Node* head = createNode(7);
    head->next = createNode(13);
    head->next->next = createNode(11);
    head->next->next->next = createNode(10);
    head->next->next->next->next = createNode(1);

    head->random = NULL;
    head->next->random = head;
    head->next->next->random = head->next->next->next->next;
    head->next->next->next->random = head->next->next;
    head->next->next->next->next->random = head;

    printf("原链表: \n");
    printList(head);

    struct Node* newHead = copyRandomList(head);

    printf("复制链表: \n");
    printList(newHead);

    return 0;
}
```

### 总结
通过实现带随机指针的链表深拷贝，我们学习了链表的遍历、节点复制和指针处理等操作。链表在实际编程中非常常用，通过动手实践，可以更好地应对复杂的数据处理任务。

### 相关资料
- [LeetCode 138 题目页面](https://leetcode.com/problems/copy-list-with-random-pointer/)
- [C语言链表操作详解 - GeeksforGeeks](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)