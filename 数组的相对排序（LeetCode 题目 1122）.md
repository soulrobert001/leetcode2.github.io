### 数组的相对排序（LeetCode 题目 1122）

#### 题目描述
给定两个数组 `arr1` 和 `arr2`，其中 `arr2` 中的元素各不相同，且 `arr2` 中的每个元素都出现在 `arr1` 中。

#### 要求
对 `arr1` 中的元素进行排序，使 `arr1` 中项的相对顺序和 `arr2` 中的相对顺序相同。未在 `arr2` 中出现过的元素需要按照升序放在 `arr1` 的末尾。

#### 说明
- 1 ≤ `arr1.length`, `arr2.length` < 1000
- 0 ≤ `arr1[i]`, `arr2[i]` < 1000

#### 示例

**示例 1**:
```
输入: arr1 = [2, 3, 1, 3, 2, 4, 6, 7, 9, 2, 19], arr2 = [2, 1, 4, 3, 9, 6]
输出: [2, 2, 2, 1, 4, 3, 3, 9, 6, 7, 19]
```

**示例 2**:
```
输入: arr1 = [28, 6, 22, 8, 44, 17], arr2 = [22, 28, 8, 6]
输出: [22, 28, 8, 6, 17, 44]
```

#### 解题思路
我们可以使用计数排序的思想来解决这个问题。具体步骤如下：
1. 遍历 `arr1`，使用哈希表记录每个元素的频次。
2. 按照 `arr2` 的顺序填充 `arr1`。
3. 将 `arr2` 中没有出现的元素按升序填充到 `arr1` 的末尾。

#### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>

// 比较函数，用于排序未出现在 arr2 中的元素
int compare(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

void relativeSortArray(int* arr1, int arr1Size, int* arr2, int arr2Size) {
    int count[1001] = {0}; // 根据题意，0 <= arr1[i], arr2[i] < 1000

    // 记录 arr1 中每个元素的出现频次
    for (int i = 0; i < arr1Size; i++) {
        count[arr1[i]]++;
    }

    // 按照 arr2 的顺序填充 arr1
    int index = 0;
    for (int i = 0; i < arr2Size; i++) {
        while (count[arr2[i]] > 0) {
            arr1[index++] = arr2[i];
            count[arr2[i]]--;
        }
    }

    // 填充 arr2 中没有出现的元素
    for (int i = 0; i < 1001; i++) {
        while (count[i] > 0) {
            arr1[index++] = i;
            count[i]--;
        }
    }
}

int main() {
    // 示例 1
    int arr1_1[] = {2, 3, 1, 3, 2, 4, 6, 7, 9, 2, 19};
    int arr2_1[] = {2, 1, 4, 3, 9, 6};
    int arr1Size1 = sizeof(arr1_1) / sizeof(arr1_1[0]);
    int arr2Size1 = sizeof(arr2_1) / sizeof(arr2_1[0]);

    relativeSortArray(arr1_1, arr1Size1, arr2_1, arr2Size1);

    printf("示例 1 排序结果: ");
    for (int i = 0; i < arr1Size1; i++) {
        printf("%d ", arr1_1[i]);
    }
    printf("\n");

    // 示例 2
    int arr1_2[] = {28, 6, 22, 8, 44, 17};
    int arr2_2[] = {22, 28, 8, 6};
    int arr1Size2 = sizeof(arr1_2) / sizeof(arr1_2[0]);
    int arr2Size2 = sizeof(arr2_2) / sizeof(arr2_2[0]);

    relativeSortArray(arr1_2, arr1Size2, arr2_2, arr2Size2);

    printf("示例 2 排序结果: ");
    for (int i = 0; i < arr1Size2; i++) {
        printf("%d ", arr1_2[i]);
    }
    printf("\n");

    return 0;
}
```

### 代码解释：

1. **比较函数，用于排序未出现在 `arr2` 中的元素**：
   ```c
   int compare(const void* a, const void* b) {
       return (*(int*)a - *(int*)b);
   }
   ```

2. **函数 `relativeSortArray`**：
   ```c
   void relativeSortArray(int* arr1, int arr1Size, int* arr2, int arr2Size) {
       int count[1001] = {0}; // 根据题意，0 <= arr1[i], arr2[i] < 1000
   
       // 记录 arr1 中每个元素的出现频次
       for (int i = 0; i < arr1Size; i++) {
           count[arr1[i]]++;
       }
   
       // 按照 arr2 的顺序填充 arr1
       int index = 0;
       for (int i = 0; i < arr2Size; i++) {
           while (count[arr2[i]] > 0) {
               arr1[index++] = arr2[i];
               count[arr2[i]]--;
           }
       }
   
       // 填充 arr2 中没有出现的元素
       for (int i = 0; i < 1001; i++) {
           while (count[i] > 0) {
               arr1[index++] = i;
               count[i]--;
           }
       }
   }
   ```

3. **主函数 `main`**：
   ```c
   int main() {
       // 示例 1
       int arr1_1[] = {2, 3, 1, 3, 2, 4, 6, 7, 9, 2, 19};
       int arr2_1[] = {2, 1, 4, 3, 9, 6};
       int arr1Size1 = sizeof(arr1_1) / sizeof(arr1_1[0]);
       int arr2Size1 = sizeof(arr2_1) / sizeof(arr2_1[0]);
   
       relativeSortArray(arr1_1, arr1Size1, arr2_1, arr2Size1);
   
       printf("示例 1 排序结果: ");
       for (int i = 0; i < arr1Size1; i++) {
           printf("%d ", arr1_1[i]);
       }
       printf("\n");
   
       // 示例 2
       int arr1_2[] = {28, 6, 22, 8, 44, 17};
       int arr2_2[] = {22, 28, 8, 6};
       int arr1Size2 = sizeof(arr1_2) / sizeof(arr1_2[0]);
       int arr2Size2 = sizeof(arr2_2) / sizeof(arr2_2[0]);
   
       relativeSortArray(arr1_2, arr1Size2, arr2_2, arr2Size2);
   
       printf("示例 2 排序结果: ");
       for (int i = 0; i < arr1Size2; i++) {
           printf("%d ", arr1_2[i]);
       }
       printf("\n");
   
       return 0;
   }
   ```
---
### 相关链接
- [LeetCode 题目 1122](https://leetcode.com/problems/relative-sort-array/)
- [计数排序简介](https://en.wikipedia.org/wiki/Counting_sort)