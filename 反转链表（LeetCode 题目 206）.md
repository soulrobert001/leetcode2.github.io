### 反转链表（LeetCode 题目 206）

#### 2.1 题目大意
描述：给定一个单链表的头节点 `head`。

要求：将该单链表进行反转。可以迭代或递归地反转链表。

#### 说明
- 链表中节点的数目范围是 `[0, 5000]`。
- -5000 ≤ Node.val ≤ 5000

#### 示例
```c
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```
解释：
- 翻转前：1 -> 2 -> 3 -> 4 -> 5 -> NULL
- 反转后：5 -> 4 -> 3 -> 2 -> 1 -> NULL

### 解题思路
我们可以使用迭代或递归的方法来反转链表。

### 代码实现（C语言）

#### 迭代方法
迭代的方法通过逐个节点的翻转来实现链表的反转。

```c
#include <stdio.h>
#include <stdlib.h>

// 定义链表节点结构
struct ListNode {
    int val;
    struct ListNode *next;
};

// 迭代方法反转链表
struct ListNode* reverseList(struct ListNode* head) {
    struct ListNode *prev = NULL;
    struct ListNode *curr = head;
    while (curr != NULL) {
        struct ListNode *nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev;
}

// 打印链表（用于测试）
void printList(struct ListNode *head) {
    struct ListNode *temp = head;
    while (temp != NULL) {
        printf("%d ", temp->val);
        temp = temp->next;
    }
    printf("\n");
}

// 创建新节点（用于测试）
struct ListNode* createNode(int val) {
    struct ListNode* newNode = (struct ListNode*)malloc(sizeof(struct ListNode));
    newNode->val = val;
    newNode->next = NULL;
    return newNode;
}

int main() {
    // 创建链表 1 -> 2 -> 3 -> 4 -> 5
    struct ListNode* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(3);
    head->next->next->next = createNode(4);
    head->next->next->next->next = createNode(5);

    printf("原链表: ");
    printList(head);

    head = reverseList(head);

    printf("反转后的链表: ");
    printList(head);

    return 0;
}
```

#### 递归方法
递归的方法通过递归地反转子链表来实现整个链表的反转。

```c
#include <stdio.h>
#include <stdlib.h>

// 定义链表节点结构
struct ListNode {
    int val;
    struct ListNode *next;
};

// 递归方法反转链表
struct ListNode* reverseListRecursive(struct ListNode* head) {
    if (head == NULL || head->next == NULL) {
        return head;
    }
    struct ListNode *newHead = reverseListRecursive(head->next);
    head->next->next = head;
    head->next = NULL;
    return newHead;
}

// 打印链表（用于测试）
void printList(struct ListNode *head) {
    struct ListNode *temp = head;
    while (temp != NULL) {
        printf("%d ", temp->val);
        temp = temp->next;
    }
    printf("\n");
}

// 创建新节点（用于测试）
struct ListNode* createNode(int val) {
    struct ListNode* newNode = (struct ListNode*)malloc(sizeof(struct ListNode));
    newNode->val = val;
    newNode->next = NULL;
    return newNode;
}

int main() {
    // 创建链表 1 -> 2 -> 3 -> 4 -> 5
    struct ListNode* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(3);
    head->next->next->next = createNode(4);
    head->next->next->next->next = createNode(5);

    printf("原链表: ");
    printList(head);

    head = reverseListRecursive(head);

    printf("反转后的链表: ");
    printList(head);

    return 0;
}
```

### 总结
通过实现链表的反转，我们不仅学习了链表的基本操作，还熟悉了迭代和递归两种方法在链表操作中的应用。这些技能对于处理复杂的数据结构问题非常有用。

### 相关资料
- [LeetCode 206 题目页面](https://leetcode.com/problems/reverse-linked-list/)
- [链表反转详解 - GeeksforGeeks](https://www.geeksforgeeks.org/reverse-a-linked-list/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)