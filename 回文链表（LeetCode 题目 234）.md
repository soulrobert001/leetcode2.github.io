### 回文链表（LeetCode 题目 234）

#### 2.1 题目大意
描述：给定一个链表的头节点 `head`。

要求：判断该链表是否为回文链表。

#### 说明
- 链表中节点数目在范围 `[1, 10^5]` 内。
- `0 ≤ Node.val ≤ 9`。

#### 示例
```c
输入：head = [1, 2, 2, 1]
输出：True

输入：head = [1, 2]
输出：False
```

### 解题思路
要判断一个链表是否为回文链表，可以使用以下两种方法之一：

1. **将链表的值存入数组然后检查是否为回文**。
2. **使用快慢指针找到链表中点，反转后半部分链表，然后比较前半部分和反转后的后半部分**。

### 代码实现（C语言）

#### 方法一：将链表的值存入数组然后检查是否为回文

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// 定义链表节点结构
struct ListNode {
    int val;
    struct ListNode *next;
};

// 将链表的值存入数组然后检查是否为回文
bool isPalindrome(struct ListNode* head) {
    if (head == NULL) return true;

    // 用于存储链表值的数组
    int values[100000];
    int size = 0;

    struct ListNode* current = head;
    while (current != NULL) {
        values[size++] = current->val;
        current = current->next;
    }

    // 检查数组是否为回文
    for (int i = 0; i < size / 2; i++) {
        if (values[i] != values[size - 1 - i]) {
            return false;
        }
    }
    return true;
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
    // 创建链表 1 -> 2 -> 2 -> 1
    struct ListNode* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(2);
    head->next->next->next = createNode(1);

    printf("原链表: ");
    printList(head);

    bool result = isPalindrome(head);

    printf("是否为回文链表: %s\n", result ? "True" : "False");

    return 0;
}
```

#### 方法二：使用快慢指针找到链表中点，反转后半部分链表，然后比较前半部分和反转后的后半部分

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// 定义链表节点结构
struct ListNode {
    int val;
    struct ListNode *next;
};

// 反转链表
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

// 使用快慢指针找到链表中点，反转后半部分链表，然后比较前半部分和反转后的后半部分
bool isPalindrome(struct ListNode* head) {
    if (head == NULL) return true;

    // 使用快慢指针找到链表的中点
    struct ListNode *slow = head, *fast = head;
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // 反转后半部分链表
    struct ListNode* secondHalf = reverseList(slow);
    struct ListNode* firstHalf = head;

    // 比较前半部分和反转后的后半部分
    while (secondHalf != NULL) {
        if (firstHalf->val != secondHalf->val) {
            return false;
        }
        firstHalf = firstHalf->next;
        secondHalf = secondHalf->next;
    }
    return true;
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
    // 创建链表 1 -> 2 -> 2 -> 1
    struct ListNode* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(2);
    head->next->next->next = createNode(1);

    printf("原链表: ");
    printList(head);

    bool result = isPalindrome(head);

    printf("是否为回文链表: %s\n", result ? "True" : "False");

    return 0;
}
```

### 总结
通过判断链表是否为回文链表，我们熟悉了链表的遍历、反转和比较操作。这些技能对于处理链表相关的问题非常有用。

### 相关资料
- [LeetCode 234 题目页面](https://leetcode.com/problems/palindrome-linked-list/)
- [C语言链表操作详解 - GeeksforGeeks](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)