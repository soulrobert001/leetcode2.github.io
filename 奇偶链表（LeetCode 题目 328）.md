### 奇偶链表（LeetCode 题目 328）

#### 1.1 题目大意
描述：给定一个单链表的头节点 `head`。

要求：将链表中的奇数位置上的节点排在前面，偶数位置上的节点排在后面，返回新的链表节点。

#### 说明
- 要求空间复杂度为 `O(1)`。
- `n` 等于链表中的节点数。
- 1 ≤ `n` ≤ 10^4。
- -10^6 ≤ `Node.val` ≤ 10^6。

#### 示例
```c
输入：head = [1, 2, 3, 4, 5]
输出：[1, 3, 5, 2, 4]

输入：head = [2, 1, 3, 5, 6, 4, 7]
输出：[2, 3, 6, 7, 1, 5, 4]
```

### 解题思路
通过维护两个指针，一个用于奇数位置的节点，一个用于偶数位置的节点。将奇数位置的节点链接在一起，同时将偶数位置的节点链接在一起，最后将奇数链表的末尾连接到偶数链表的头部即可。

### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>

// 定义链表节点结构
struct ListNode {
    int val;
    struct ListNode *next;
};

// 奇偶链表
struct ListNode* oddEvenList(struct ListNode* head) {
    if (head == NULL) return NULL;

    struct ListNode *odd = head, *even = head->next;
    struct ListNode *evenHead = even;

    while (even != NULL && even->next != NULL) {
        odd->next = even->next;
        odd = odd->next;
        even->next = odd->next;
        even = even->next;
    }
    odd->next = evenHead;
    return head;
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

    head = oddEvenList(head);

    printf("奇偶链表: ");
    printList(head);

    return 0;
}
```

### 总结
通过将链表的奇数位置节点和偶数位置节点分开并重新组合，可以高效地实现奇偶链表的重排。该方法保证了时间复杂度和空间复杂度的最优化。

### 相关资料
- [LeetCode 328 题目页面](https://leetcode.com/problems/odd-even-linked-list/)
- [链表操作详解 - GeeksforGeeks](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)