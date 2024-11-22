# LeetCode 33：搜索旋转排序数组

## 题目描述

给定一个整数数组 `nums`，数组中值互不相同。`nums` 是经过升序排列后进行「旋转」操作的数组。要求在数组中找到 `target` 的位置，找到返回下标，否则返回 -1。

## 解题思路

### 1. 核心算法：改进二分查找

关键在于确定目标值在哪一部分有序区间。

### 2. 算法实现

```c
int search(int* nums, int numsSize, int target) {
    int left = 0, right = numsSize - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        // 找到目标值
        if (nums[mid] == target) return mid;
        
        // 判断左半部分是否有序
        if (nums[left] <= nums[mid]) {
            // target在左半部分
            if (target >= nums[left] && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } 
        // 右半部分有序
        else {
            // target在右半部分
            if (target > nums[mid] && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    
    return -1;
}
```

### 3. 算法原理

1. 首先判断中间元素是否为目标值
2. 确定哪一部分是有序的
3. 判断 `target` 是否在有序部分
4. 根据条件缩小搜索范围

### 4. 复杂度分析

- **时间复杂度**：O(log n)
- **空间复杂度**：O(1)

## 关键代码解析

### 判断左半部分有序

```c
if (nums[left] <= nums[mid]) {
    // 左半部分有序
}
```

### 目标值范围判断

```c
if (target >= nums[left] && target < nums[mid]) {
    right = mid - 1;  // 在左半部分
}
```

## 典型测试用例

```c
int main() {
    int nums[] = {4,5,6,7,0,1,2};
    int target = 0;
    printf("结果：%d\n", search(nums, sizeof(nums)/sizeof(nums[0]), target));
    return 0;
}
```

## 解题技巧

1. 始终保持二分查找的对数时间复杂度
2. 准确判断有序区间
3. 精确处理边界条件

## 常见问题

### Q1：为什么使用 `nums[left] <= nums[mid]`？
确保正确判断左半部分是否有序。

### Q2：如何处理旋转数组的特殊性？
通过比较 `left`、`mid`、`right` 三个位置的值。

## 相关题目

- [LeetCode 81. 搜索旋转排序数组 II](https://leetcode.cn/problems/search-in-rotated-sorted-array-ii/)
- [LeetCode 153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)

## 总结

旋转数组的查找是二分查找的变种，关键在于准确判断有序区间并据此缩小搜索范围。

## 版权声明

原创内容，遵循 MIT 开源协议。