# LeetCode 153：寻找旋转排序数组中的最小值

## 题目描述

给定一个由升序数组经过「旋转」得到的数组 `nums`，数组中不存在重复元素。要求找出数组中的最小元素。

## 解题思路

### 1. 二分查找算法

核心思路是通过比较中间元素和边界元素，确定最小值所在区间。

### 2. 代码实现

```c
int findMin(int* nums, int numsSize) {
    int left = 0, right = numsSize - 1;
    
    while (left < right) {
        // 如果已经有序，直接返回第一个元素
        if (nums[left] < nums[right]) {
            return nums[left];
        }
        
        int mid = left + (right - left) / 2;
        
        // 中间元素大于左边界，说明最小值在右半部分
        if (nums[mid] >= nums[left]) {
            left = mid + 1;
        } 
        // 中间元素小于左边界，说明最小值在左半部分（包括mid）
        else {
            right = mid;
        }
    }
    
    return nums[left];
}
```

### 3. 算法分析

#### 关键判断逻辑
- 如果整个数组有序，返回第一个元素
- 通过比较 `mid` 与 `left` 的大小关系确定最小值位置

#### 复杂度
- **时间复杂度**：O(log n)
- **空间复杂度**：O(1)

## 典型测试用例

```c
int main() {
    int nums1[] = {3, 4, 5, 1, 2};
    printf("最小值：%d\n", findMin(nums1, sizeof(nums1)/sizeof(nums1[0])));
    
    int nums2[] = {4, 5, 6, 7, 0, 1, 2};
    printf("最小值：%d\n", findMin(nums2, sizeof(nums2)/sizeof(nums2[0])));
    
    return 0;
}
```

## 解题技巧

1. 利用二分查找快速定位最小值
2. 准确判断有序区间
3. 处理边界条件

## 常见问题

### Q1：为什么使用 `left < right`？
- 确保最终找到最小值
- 避免无限循环

### Q2：如何处理旋转数组的特殊性？
通过比较 `left`、`mid`、`right` 的大小关系。

## 相关题目

- [LeetCode 33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)
- [LeetCode 81. 搜索旋转排序数组 II](https://leetcode.cn/problems/search-in-rotated-sorted-array-ii/)

## 总结

寻找旋转排序数组的最小值是二分查找的一个经典变体，通过巧妙的区间判断，可以在对数时间复杂度内找到最小元素。

## 版权声明

原创内容，遵循 MIT 开源协议。