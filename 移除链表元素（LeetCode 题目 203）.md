### 移除链表元素（LeetCode 题目 203）

#### 3.1 题目大意
描述：给定一个链表的头节点 `head` 和一个值 `val`。

要求：删除链表中值为 `val` 的节点，并返回新的链表头节点。

#### 说明
- 列表中的节点数目在范围 `[0, 10^4]` 内。
- `1 ≤ Node.val ≤ 50`。
- `val` 的范围是 `[1, 50]`。

#### 示例
```c
输入：head = [1, 2, 6, 3, 4, 5, 6], val = 6
输出：[1, 2, 3, 4, 5]

输入：head = [], val = 1
输出：[]
```

### 解题思路
我们可以通过遍历链表，逐个节点检查其值是否等于 `val`，如果是则删除该节点。我们需要特别处理头节点的情况，因为头节点本身可能也需要被删除。

### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>

// 定义链表节点结构
struct ListNode {
    int val;
    struct ListNode *next;
};

// 移除链表元素
struct ListNode* removeElements(struct ListNode* head, int val) {
    struct ListNode dummy;
    dummy.next = head;
    struct ListNode* current = &dummy;
    
    while (current->next != NULL) {
        if (current->next->val == val) {
            struct ListNode* temp = current->next;
            current->next = current->next->next;
            free(temp);
        } else {
            current = current->next;
        }
    }
    
    return dummy.next;
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
    // 创建链表 1 -> 2 -> 6 -> 3 -> 4 -> 5 -> 6
    struct ListNode* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(6);
    head->next->next->next = createNode(3);
    head->next->next->next->next = createNode(4);
    head->next->next->next->next->next = createNode(5);
    head->next->next->next->next->next->next = createNode(6);

    printf("原链表: ");
    printList(head);

    head = removeElements(head, 6);

    printf("移除后的链表: ");
    printList(head);

    return 0;
}
```

### 总结
通过移除链表中的指定元素，我们熟悉了链表的基本操作，如节点遍历、删除和处理边界情况。链表在实际编程中非常常用，通过动手实践，可以更好地应对复杂的数据处理任务。

### 相关资料
- [LeetCode 203 题目页面](https://leetcode.com/problems/remove-linked-list-elements/)
- [C语言链表操作详解 - GeeksforGeeks](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)