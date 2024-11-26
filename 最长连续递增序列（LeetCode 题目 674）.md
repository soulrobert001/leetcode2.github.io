### 最长连续递增序列（LeetCode 题目 674）

#### 2.1 题目大意
描述：给定一个未经排序的数组 `nums`。

要求：找到最长且连续递增的子序列，并返回该序列的长度。

#### 说明
- 连续递增的子序列：可以由两个下标 `l` 和 `r`（`l < r`）确定，如果对于每个 `l ≤ i < r`，都有 `nums[i] < nums[i + 1]`，那么子序列 `[nums[l], nums[l + 1], ..., nums[r - 1], nums[r]]` 就是连续递增子序列。
- 1 ≤ `nums.length` ≤ 10^4。
- -10^4 ≤ `nums[i]` ≤ 10^4。

#### 示例
**示例 1**:
```python
输入：nums = [1, 3, 5, 4, 7]
输出：3
解释：最长连续递增序列是 [1, 3, 5]，长度为 3。尽管 [1, 3, 5, 7] 也是升序的子序列，但它不是连续的，因为 5 和 7 在原数组里被 4 隔开。
```

**示例 2**:
```python
输入：nums = [2, 2, 2, 2, 2]
输出：1
解释：最长连续递增序列是 [2]，长度为 1。
```

### 解题思路
我们可以使用遍历的方法来找到最长连续递增子序列的长度。我们保持一个 `current_length` 变量来跟踪当前的递增序列长度，并使用 `max_length` 变量来记录最大的序列长度。

### 代码实现（C语言）

```c
#include <stdio.h>

// 找到最长连续递增序列的长度
int findLengthOfLCIS(int* nums, int numsSize) {
    if (numsSize == 0) return 0;

    int max_length = 1, current_length = 1;

    for (int i = 1; i < numsSize; i++) {
        if (nums[i] > nums[i - 1]) {
            current_length++;
            if (current_length > max_length) {
                max_length = current_length;
            }
        } else {
            current_length = 1;
        }
    }

    return max_length;
}

int main() {
    // 示例 1
    int nums1[] = {1, 3, 5, 4, 7};
    printf("最长连续递增序列的长度: %d\n", findLengthOfLCIS(nums1, sizeof(nums1) / sizeof(nums1[0])));

    // 示例 2
    int nums2[] = {2, 2, 2, 2, 2};
    printf("最长连续递增序列的长度: %d\n", findLengthOfLCIS(nums2, sizeof(nums2) / sizeof(nums2[0])));

    return 0;
}
```

### 总结
通过遍历数组，我们可以有效地找到最长且连续递增的子序列长度。这个方法的时间复杂度为 O(n)，能够在较短时间内处理大规模数据。

### 相关资料
- [LeetCode 674 题目页面](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)
- [数组操作详解 - GeeksforGeeks](https://www.geeksforgeeks.org/array-data-structure/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)