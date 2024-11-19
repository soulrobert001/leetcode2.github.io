### 剑指 Offer 51. 数组中的逆序对

#### 题目描述
给定一个数组 `nums`，计算数组中的逆序对的总数。

#### 说明
- **逆序对**：在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。
- 0 < `nums.length` < 50000。

#### 示例

**示例 1**:
```
输入: [7, 5, 6, 4]
输出: 5
```

#### 解题思路
计算数组中的逆序对的总数可以使用归并排序的方法。在归并排序的过程中，统计逆序对的数量。

#### 代码实现（C语言）

```c
#include <stdio.h>

int mergeAndCount(int* nums, int* temp, int left, int mid, int right) {
    int i = left, j = mid + 1, k = left, inv_count = 0;

    while (i <= mid && j <= right) {
        if (nums[i] <= nums[j]) {
            temp[k++] = nums[i++];
        } else {
            temp[k++] = nums[j++];
            inv_count += (mid - i + 1); // 统计逆序对
        }
    }

    while (i <= mid)
        temp[k++] = nums[i++];

    while (j <= right)
        temp[k++] = nums[j++];

    for (i = left; i <= right; i++)
        nums[i] = temp[i];

    return inv_count;
}

int mergeSortAndCount(int* nums, int* temp, int left, int right) {
    int mid, inv_count = 0;
    if (right > left) {
        mid = (right + left) / 2;

        inv_count += mergeSortAndCount(nums, temp, left, mid);
        inv_count += mergeSortAndCount(nums, temp, mid + 1, right);
        inv_count += mergeAndCount(nums, temp, left, mid, right);
    }
    return inv_count;
}

int reversePairs(int* nums, int numsSize) {
    int* temp = (int*)malloc(numsSize * sizeof(int));
    int result = mergeSortAndCount(nums, temp, 0, numsSize - 1);
    free(temp);
    return result;
}

int main() {
    int nums[] = {7, 5, 6, 4};
    int numsSize = sizeof(nums) / sizeof(nums[0]);

    int result = reversePairs(nums, numsSize);
    printf("数组中的逆序对总数: %d\n", result);

    return 0;
}
```

### 代码解释

1. **函数 `mergeAndCount`**：
   ```c
   int mergeAndCount(int* nums, int* temp, int left, int mid, int right) {
       int i = left, j = mid + 1, k = left, inv_count = 0;
   
       while (i <= mid && j <= right) {
           if (nums[i] <= nums[j]) {
               temp[k++] = nums[i++];
           } else {
               temp[k++] = nums[j++];
               inv_count += (mid - i + 1); // 统计逆序对
           }
       }
   
       while (i <= mid)
           temp[k++] = nums[i++];
   
       while (j <= right)
           temp[k++] = nums[j++];
   
       for (i = left; i <= right; i++)
           nums[i] = temp[i];
   
       return inv_count;
   }
   ```
   - `mergeAndCount` 函数在归并排序的过程中，统计逆序对的数量。

2. **函数 `mergeSortAndCount`**：
   ```c
   int mergeSortAndCount(int* nums, int* temp, int left, int right) {
       int mid, inv_count = 0;
       if (right > left) {
           mid = (right + left) / 2;
   
           inv_count += mergeSortAndCount(nums, temp, left, mid);
           inv_count += mergeSortAndCount(nums, temp, mid + 1, right);
           inv_count += mergeAndCount(nums, temp, left, mid, right);
       }
       return inv_count;
   }
   ```
   - `mergeSortAndCount` 函数使用归并排序的递归方式，分治法计算逆序对的总数。

3. **函数 `reversePairs`**：
   ```c
   int reversePairs(int* nums, int numsSize) {
       int* temp = (int*)malloc(numsSize * sizeof(int));
       int result = mergeSortAndCount(nums, temp, 0, numsSize - 1);
       free(temp);
       return result;
   }
   ```
   - `reversePairs` 函数是主函数，调用 `mergeSortAndCount` 函数计算逆序对，并返回结果。

4. **主函数 `main`**：
   ```c
   int main() {
       int nums[] = {7, 5, 6, 4};
       int numsSize = sizeof(nums) / sizeof(nums[0]);
   
       int result = reversePairs(nums, numsSize);
       printf("数组中的逆序对总数: %d\n", result);
   
       return 0;
   }
   ```
   - 定义并初始化示例数组。
   - 调用 `reversePairs` 函数计算逆序对的总数。
   - 输出逆序对的总数。


---

### 相关链接
- [LeetCode 题目 51](https://leetcode.com/problems/reverse-pairs/)
- [归并排序简介](https://en.wikipedia.org/wiki/Merge_sort)
