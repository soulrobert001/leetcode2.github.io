### 最大间距（LeetCode 题目 164）

#### 题目描述
给定一个无序数组 `nums`，找出数组在排序之后，相邻元素之间最大的差值。如果数组元素个数小于2，则返回0。

#### 说明
- 所有元素都是非负整数，且数值在32位有符号整数范围内。
- 请尝试在线性时间复杂度和空间复杂度的条件下解决此问题。

#### 示例

**示例 1**:
```
输入: nums = [3, 6, 9, 1]
输出: 3
解释: 排序后的数组是 [1, 3, 6, 9]，其中相邻元素 (3,6) 和 (6,9) 之间都存在最大差值 3。
```

**示例 2**:
```
输入: nums = [10]
输出: 0
解释: 数组元素个数小于2，因此返回0。
```

#### 解题思路
要找到数组中相邻元素之间的最大差值，可以使用桶排序的思想来在线性时间复杂度和空间复杂度的条件下解决此问题。以下是详细步骤：

1. **确定桶的数量**：
   - 使用每个桶的大小 `bucket_size = max(1, (max_val - min_val) // (len(nums) - 1))`。
   - 使用 `(max_val - min_val) // bucket_size + 1` 计算桶的数量。

2. **将元素放入桶中**：
   - 计算每个元素所属的桶索引 `bucket_index = (num - min_val) // bucket_size`。
   - 记录每个桶中的最小值和最大值。

3. **计算最大间距**：
   - 遍历所有的桶，计算相邻非空桶之间的差值，并更新最大间距。

#### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

int max(int a, int b) {
    return a > b ? a : b;
}

int min(int a, int b) {
    return a < b ? a : b;
}

int maximumGap(int* nums, int numsSize) {
    if (numsSize < 2) {
        return 0;
    }

    int min_val = INT_MAX, max_val = INT_MIN;
    for (int i = 0; i < numsSize; i++) {
        min_val = min(min_val, nums[i]);
        max_val = max(max_val, nums[i]);
    }

    int bucket_size = max(1, (max_val - min_val) / (numsSize - 1));
    int bucket_count = (max_val - min_val) / bucket_size + 1;

    int* bucket_min = (int*)malloc(bucket_count * sizeof(int));
    int* bucket_max = (int*)malloc(bucket_count * sizeof(int));

    for (int i = 0; i < bucket_count; i++) {
        bucket_min[i] = INT_MAX;
        bucket_max[i] = INT_MIN;
    }

    for (int i = 0; i < numsSize; i++) {
        int bucket_index = (nums[i] - min_val) / bucket_size;
        bucket_min[bucket_index] = min(bucket_min[bucket_index], nums[i]);
        bucket_max[bucket_index] = max(bucket_max[bucket_index], nums[i]);
    }

    int max_gap = 0, prev_max = min_val;
    for (int i = 0; i < bucket_count; i++) {
        if (bucket_min[i] == INT_MAX) {
            continue;
        }
        max_gap = max(max_gap, bucket_min[i] - prev_max);
        prev_max = bucket_max[i];
    }

    free(bucket_min);
    free(bucket_max);

    return max_gap;
}

int main() {
    int nums1[] = {3, 6, 9, 1};
    int numsSize1 = sizeof(nums1) / sizeof(nums1[0]);
    int result1 = maximumGap(nums1, numsSize1);
    printf("示例 1 最大间距: %d\n", result1);

    int nums2[] = {10};
    int numsSize2 = sizeof(nums2) / sizeof(nums2[0]);
    int result2 = maximumGap(nums2, numsSize2);
    printf("示例 2 最大间距: %d\n", result2);

    return 0;
}
```

### 代码解释：

1. **最大值和最小值函数**：
   ```c
   int max(int a, int b) {
       return a > b ? a : b;
   }
   
   int min(int a, int b) {
       return a < b ? a : b;
   }
   ```

2. **主函数 `maximumGap`**：
   ```c
   int maximumGap(int* nums, int numsSize) {
       if (numsSize < 2) {
           return 0;
       }
   
       int min_val = INT_MAX, max_val = INT_MIN;
       for (int i = 0; i < numsSize; i++) {
           min_val = min(min_val, nums[i]);
           max_val = max(max_val, nums[i]);
       }
   
       int bucket_size = max(1, (max_val - min_val) / (numsSize - 1));
       int bucket_count = (max_val - min_val) / bucket_size + 1;
   
       int* bucket_min = (int*)malloc(bucket_count * sizeof(int));
       int* bucket_max = (int*)malloc(bucket_count * sizeof(int));
   
       for (int i = 0; i < bucket_count; i++) {
           bucket_min[i] = INT_MAX;
           bucket_max[i] = INT_MIN;
       }
   
       for (int i = 0; i < numsSize; i++) {
           int bucket_index = (nums[i] - min_val) / bucket_size;
           bucket_min[bucket_index] = min(bucket_min[bucket_index], nums[i]);
           bucket_max[bucket_index] = max(bucket_max[bucket_index], nums[i]);
       }
   
       int max_gap = 0, prev_max = min_val;
       for (int i = 0; i < bucket_count; i++) {
           if (bucket_min[i] == INT_MAX) {
               continue;
           }
           max_gap = max(max_gap, bucket_min[i] - prev_max);
           prev_max = bucket_max[i];
       }
   
       free(bucket_min);
       free(bucket_max);
   
       return max_gap;
   }
   ```

3. **测试函数 `main`**：
   ```c
   int main() {
       int nums1[] = {3, 6, 9, 1};
       int numsSize1 = sizeof(nums1) / sizeof(nums1[0]);
       int result1 = maximumGap(nums1, numsSize1);
       printf("示例 1 最大间距: %d\n", result1);
   
       int nums2[] = {10};
       int numsSize2 = sizeof(nums2) / sizeof(nums2[0]);
       int result2 = maximumGap(nums2, numsSize2);
       printf("示例 2 最大间距: %d\n", result2);
   
       return 0;
   }
   ```

---

### 相关链接
- [LeetCode 题目 164](https://leetcode.com/problems/maximum-gap/)
- [桶排序简介](https://en.wikipedia.org/wiki/Bucket_sort)