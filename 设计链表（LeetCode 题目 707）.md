### 设计链表（LeetCode 题目 707）

#### 1.1 题目大意
要求：设计实现一个链表，需要支持以下操作：

- **get(index)**：获取链表中第 `index` 个节点的值。如果索引 `index` 无效，则返回 `-1`。
- **addAtHead(val)**：在链表的第一个元素之前添加一个值为 `val` 的节点。插入后，新节点将成为链表的第一个节点。
- **addAtTail(val)**：将值为 `val` 的节点追加到链表的最后一个元素。
- **addAtIndex(index, val)**：在链表中的第 `index` 个节点之前添加值为 `val` 的节点。如果 `index` 等于链表的长度，则该节点将附加到链表的末尾。如果 `index` 大于链表长度，则不会插入节点。如果 `index` 小于 `0`，则在头部插入节点。
- **deleteAtIndex(index)**：如果索引 `index` 有效，则删除链表中的第 `index` 个节点。

#### 说明
- 所有 `val` 值都在 `[1, 1000]` 之内。
- 操作次数将在 `[1, 1000]` 之内。
- 请不要使用内置的 `LinkedList` 库。

#### 示例
```c
MyLinkedList linkedList;
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1, 2);  // 链表变为 1 -> 2 -> 3
int value = linkedList.get(1); // 返回 2
linkedList.deleteAtIndex(1);   // 现在链表是 1 -> 3
value = linkedList.get(1);     // 返回 3
```

### 解题思路
我们可以通过设计一个单链表来实现上述操作。单链表由一系列节点组成，每个节点包含一个值和一个指向下一个节点的指针。

### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>

// 定义节点结构
struct ListNode {
    int val;
    struct ListNode* next;
};

// 定义链表结构
struct MyLinkedList {
    struct ListNode* head;
    int size;
};

// 初始化链表
struct MyLinkedList* myLinkedListCreate() {
    struct MyLinkedList* obj = (struct MyLinkedList*)malloc(sizeof(struct MyLinkedList));
    obj->head = NULL;
    obj->size = 0;
    return obj;
}

// 获取链表中第 index 个节点的值
int myLinkedListGet(struct MyLinkedList* obj, int index) {
    if (index < 0 || index >= obj->size) {
        return -1;
    }
    struct ListNode* current = obj->head;
    for (int i = 0; i < index; i++) {
        current = current->next;
    }
    return current->val;
}

// 在链表的第一个元素之前添加一个值为 val 的节点
void myLinkedListAddAtHead(struct MyLinkedList* obj, int val) {
    struct ListNode* node = (struct ListNode*)malloc(sizeof(struct ListNode));
    node->val = val;
    node->next = obj->head;
    obj->head = node;
    obj->size++;
}

// 将值为 val 的节点追加到链表的最后一个元素
void myLinkedListAddAtTail(struct MyLinkedList* obj, int val) {
    struct ListNode* node = (struct ListNode*)malloc(sizeof(struct ListNode));
    node->val = val;
    node->next = NULL;
    if (obj->head == NULL) {
        obj->head = node;
    } else {
        struct ListNode* current = obj->head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = node;
    }
    obj->size++;
}

// 在链表中的第 index 个节点之前添加值为 val 的节点
void myLinkedListAddAtIndex(struct MyLinkedList* obj, int index, int val) {
    if (index > obj->size) {
        return;
    }
    if (index <= 0) {
        myLinkedListAddAtHead(obj, val);
    } else {
        struct ListNode* node = (struct ListNode*)malloc(sizeof(struct ListNode));
        node->val = val;
        struct ListNode* current = obj->head;
        for (int i = 0; i < index - 1; i++) {
            current = current->next;
        }
        node->next = current->next;
        current->next = node;
        obj->size++;
    }
}

// 删除链表中的第 index 个节点
void myLinkedListDeleteAtIndex(struct MyLinkedList* obj, int index) {
    if (index < 0 || index >= obj->size) {
        return;
    }
    struct ListNode* temp;
    if (index == 0) {
        temp = obj->head;
        obj->head = obj->head->next;
    } else {
        struct ListNode* current = obj->head;
        for (int i = 0; i < index - 1; i++) {
            current = current->next;
        }
        temp = current->next;
        current->next = current->next->next;
    }
    free(temp);
    obj->size--;
}

// 释放链表占用的内存
void myLinkedListFree(struct MyLinkedList* obj) {
    struct ListNode* current = obj->head;
    struct ListNode* next;
    while (current != NULL) {
        next = current->next;
        free(current);
        current = next;
    }
    free(obj);
}

int main() {
    struct MyLinkedList* linkedList = myLinkedListCreate();
    myLinkedListAddAtHead(linkedList, 1);
    myLinkedListAddAtTail(linkedList, 3);
    myLinkedListAddAtIndex(linkedList, 1, 2);  // 链表变为 1-> 2 -> 3
    printf("%d\n", myLinkedListGet(linkedList, 1)); // 返回 2
    myLinkedListDeleteAtIndex(linkedList, 1);  // 现在链表是 1-> 3
    printf("%d\n", myLinkedListGet(linkedList, 1)); // 返回 3
    myLinkedListFree(linkedList);
    return 0;
}
```

### 总结
通过实现链表数据结构，我们不仅掌握了链表操作的基本方法，还提升了对数据结构的理解。链表在实际编程中非常常用，通过动手实践，可以更好地应对复杂的数据处理任务。

### 相关资料
- [LeetCode 707 题目页面](https://leetcode.com/problems/design-linked-list/)
- [C语言单链表实现教程](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)