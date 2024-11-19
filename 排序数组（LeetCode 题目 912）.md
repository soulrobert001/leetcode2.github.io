### 排序数组（LeetCode 题目 912）

#### 题目描述
给定一个整数数组 `nums`，要求将该数组升序排列。

#### 示例

**示例 1**:
```
输入：nums = [5, 2, 3, 1]
输出：[1, 2, 3, 5]
```

**示例 2**:
```
输入：nums = [5, 1, 1, 2, 0, 0]
输出：[0, 0, 1, 1, 2, 5]
```

#### 解题思路
我们可以使用经典的排序算法，例如快速排序、归并排序或者内置的排序函数来实现数组排序。下面是使用C语言的代码示例，采用内置的 `qsort` 函数来进行排序。

#### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>

// 比较函数
int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

void sortArray(int* nums, int numsSize) {
    qsort(nums, numsSize, sizeof(int), compare);
}

int main() {
    // 示例 1
    int nums1[] = {5, 2, 3, 1};
    int numsSize1 = sizeof(nums1) / sizeof(nums1[0]);
    sortArray(nums1, numsSize1);

    printf("示例 1 排序结果: ");
    for (int i = 0; i < numsSize1; i++) {
        printf("%d ", nums1[i]);
    }
    printf("\n");

    // 示例 2
    int nums2[] = {5, 1, 1, 2, 0, 0};
    int numsSize2 = sizeof(nums2) / sizeof(nums2[0]);
    sortArray(nums2, numsSize2);

    printf("示例 2 排序结果: ");
    for (int i = 0; i < numsSize2; i++) {
        printf("%d ", nums2[i]);
    }
    printf("\n");

    return 0;
}
```

### 代码解释：

1. **比较函数 `compare`**：
   ```c
   int compare(const void *a, const void *b) {
       return (*(int *)a - *(int *)b);
   }
   ```
   - 这是用于 `qsort` 函数的比较函数。它比较两个整数的大小，并返回它们的差值。

2. **排序函数 `sortArray`**：
   ```c
   void sortArray(int* nums, int numsSize) {
       qsort(nums, numsSize, sizeof(int), compare);
   }
   ```
   - 使用 `qsort` 函数对数组进行排序。`qsort` 是标准库中的快速排序函数。

3. **主函数 `main`**：
   ```c
   int main() {
       // 示例 1
       int nums1[] = {5, 2, 3, 1};
       int numsSize1 = sizeof(nums1) / sizeof(nums1[0]);
       sortArray(nums1, numsSize1);
   
       printf("示例 1 排序结果: ");
       for (int i = 0; i < numsSize1; i++) {
           printf("%d ", nums1[i]);
       }
       printf("\n");
   
       // 示例 2
       int nums2[] = {5, 1, 1, 2, 0, 0};
       int numsSize2 = sizeof(nums2) / sizeof(nums2[0]);
       sortArray(nums2, numsSize2);
   
       printf("示例 2 排序结果: ");
       for (int i = 0; i < numsSize2; i++) {
           printf("%d ", nums2[i]);
       }
       printf("\n");
   
       return 0;
   }
   ```
   - 定义并初始化两个示例数组。
   - 调用 `sortArray` 函数对数组进行排序。
   - 输出排序后的数组结果。

### 示例输出

```
输出结果: 1 2 3 5 
输出结果: 0 0 1 1 2 5 
```

通过以上代码，你可以用C语言实现数组的升序排序。如果有任何问题或需要进一步的帮助，请随时告诉我！ 😊

---

### 相关链接
- [LeetCode 题目 912](https://leetcode.com/problems/sort-an-array/)
- [快速排序简介](https://en.wikipedia.org/wiki/Quicksort)