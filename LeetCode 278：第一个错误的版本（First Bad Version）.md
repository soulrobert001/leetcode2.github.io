# LeetCode 278：第一个错误的版本（First Bad Version）

## 题目描述

给定一个整数 `n`，代表已发布的版本号，以及一个用于检测版本是否出错的接口 `isBadVersion(version)`。要求找出第一个出错的版本号。

## 解题思路

### 1. 问题本质

本题是一个经典的**二分查找变体**问题，目标是在最少的API调用次数内找到第一个错误版本。

### 2. 算法设计

#### 二分查找策略
- 初始查找范围：[1, n]
- 每次计算中间版本号
- 根据 `isBadVersion()` 结果调整查找范围

### 3. 代码实现

```c
// LeetCode 提供的API
bool isBadVersion(int version);

int firstBadVersion(int n) {
    int left = 1, right = n;
    
    while (left < right) {
        // 防止整数溢出的写法
        int mid = left + (right - left) / 2;
        
        if (isBadVersion(mid)) {
            // mid 可能是第一个错误版本
            right = mid;
        } else {
            // 错误版本在 mid 之后
            left = mid + 1;
        }
    }
    
    return left;
}
```

### 4. 关键代码解析

#### 防溢出写法
```c
int mid = left + (right - left) / 2;
```
- 避免 `(left + right) / 2` 可能的整数溢出
- 等价于传统的中点计算方式

#### 范围收缩
- `isBadVersion(mid)` 为 `true`：可能为第一个错误版本，将 `right` 移动到 `mid`
- `isBadVersion(mid)` 为 `false`：错误版本在 `mid` 之后，将 `left` 移动到 `mid + 1`

### 5. 复杂度分析

- **时间复杂度**：O(log n)
- **空间复杂度**：O(1)

## 解题技巧

1. 二分查找的核心是**每次缩小一半的查找范围**
2. 注意边界条件处理
3. 避免整数溢出

## 常见问题

### Q1：为什么使用 `left < right`？
- 确保最终找到唯一的错误版本
- 避免无限循环

### Q2：如何最小化 API 调用？
- 每次二分查找将搜索范围减半
- 只在必要时调用 `isBadVersion()`

## 应用场景

1. 软件版本回溯
2. 大规模系统版本追踪
3. 持续集成与部署(CI/CD)检测

## 相关题目

- [LeetCode 34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)
- [LeetCode 33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

## 总结

二分查找是解决有序数组查找问题的高效算法，通过每次排除一半的搜索空间，显著降低了时间复杂度。

## 版权声明

本文原创内容，遵循 MIT 开源协议。

## 关于作者

算法爱好者，专注于数据结构与算法研究。