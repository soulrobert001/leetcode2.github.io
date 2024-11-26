### 子数组最大平均数（LeetCode 题目 643）

#### 1.1 题目大意
描述：给定一个由 `n` 个元素组成的整数数组 `nums` 和一个整数 `k`。

要求：找出平均数最大且长度为 `k` 的连续子数组，并输出该最大平均数。

#### 说明
- 任何误差小于 `10^-5` 的答案都将被视为正确答案。
- `n == nums.length`。
- `1 ≤ k ≤ n ≤ 10^5`。
- `-10^4 ≤ nums[i] ≤ 10^4`。

#### 示例
**示例 1**:
```python
输入：nums = [1, 12, -5, -6, 50, 3], k = 4
输出：12.75
解释：最大平均数 (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
```

**示例 2**:
```python
输入：nums = [5], k = 1
输出：5.00000
```

### 解题思路
要找到平均数最大的长度为 `k` 的连续子数组，我们可以使用滑动窗口技术。通过滑动窗口，可以在一次遍历中计算所有长度为 `k` 的子数组的和，并更新最大值。

### 代码实现（C语言）

```c
#include <stdio.h>

// 子数组最大平均数函数
double findMaxAverage(int* nums, int numsSize, int k) {
    double sum = 0;
    // 计算第一个窗口的和
    for (int i = 0; i < k; i++) {
        sum += nums[i];
    }
    double maxSum = sum;
    
    // 计算后续窗口的和，采用滑动窗口技术
    for (int i = k; i < numsSize; i++) {
        sum += nums[i] - nums[i - k];
        if (sum > maxSum) {
            maxSum = sum;
        }
    }
    
    return maxSum / k;
}

int main() {
    // 示例 1
    int nums1[] = {1, 12, -5, -6, 50, 3};
    int k1 = 4;
    printf("最大平均数: %.5f\n", findMaxAverage(nums1, sizeof(nums1) / sizeof(nums1[0]), k1));
    
    // 示例 2
    int nums2[] = {5};
    int k2 = 1;
    printf("最大平均数: %.5f\n", findMaxAverage(nums2, sizeof(nums2) / sizeof(nums2[0]), k2));
    
    return 0;
}
```

### 总结
通过使用滑动窗口技术，我们可以在一次遍历中找到长度为 `k` 的连续子数组的最大平均数，从而有效地解决这个问题。

### 相关资料
- [LeetCode 643 题目页面](https://leetcode.com/problems/maximum-average-subarray-i/)
- [滑动窗口技术详解 - GeeksforGeeks](https://www.geeksforgeeks.org/window-sliding-technique/)
- [数据结构与算法基础知识](https://www.coursera.org/learn/data-structures)