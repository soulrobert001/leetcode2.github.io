# LeetCode 1011：在 D 天内送达包裹的能力 

## 题目描述

传送带上的包裹必须在 D 天内从一个港口运送到另一个港口。给定所有包裹的重量数组 `weights`，货物必须按照给定的顺序装运，且每天船上装载的重量不会超过船的最大运载重量。

**要求**：求能在 D 天内将所有包裹送达的船的最低运载量。

## 解题思路

### 1. 二分查找算法

本题的核心解题思路是使用**二分查找**，通过不断缩小查找范围来确定最低运载量。

#### 查找范围
- 左边界：数组中的最大元素（保证可以装载最重的包裹）
- 右边界：所有包裹的总重量（一次性运输所有包裹）

#### 查找策略
1. 取中间值作为船的载重能力
2. 模拟运输过程，计算所需天数
3. 根据所需天数与目标天数的比较调整载重范围

### 2. 代码实现

```c
int shipWithinDays(int* weights, int weightsSize, int days) {
    int left = 0, right = 0;
    
    // 确定初始查找范围
    for (int i = 0; i < weightsSize; i++) {
        left = fmax(left, weights[i]);  // 最小载重
        right += weights[i];  // 最大载重
    }
    
    // 二分查找
    while (left < right) {
        int mid = left + (right - left) / 2;
        int current_days = 1;  // 初始天数
        int current_load = 0;
        
        // 模拟运输过程
        for (int i = 0; i < weightsSize; i++) {
            if (current_load + weights[i] > mid) {
                current_days++;  // 需要新的一天
                current_load = weights[i];
            } else {
                current_load += weights[i];
            }
        }
        
        // 根据所需天数调整载重范围
        if (current_days <= days) {
            right = mid;  // 尝试减小载重
        } else {
            left = mid + 1;  // 增加载重
        }
    }
    
    return left;
}
```

### 3. 算法复杂度

- **时间复杂度**：O(n * log(sum(weights)))
  - n 为包裹数量
  - log(sum(weights)) 为二分查找的次数
- **空间复杂度**：O(1)，只使用常数额外空间

### 4. 测试用例

```c
int main() {
    // 测试用例1
    int weights1[] = {1,2,3,4,5,6,7,8,9,10};
    int days1 = 5;
    printf("测试用例1结果：%d\n", shipWithinDays(weights1, sizeof(weights1)/sizeof(weights1[0]), days1));

    // 测试用例2
    int weights2[] = {3,2,2,4,1,4};
    int days2 = 3;
    printf("测试用例2结果：%d\n", shipWithinDays(weights2, sizeof(weights2)/sizeof(weights2[0]), days2));

    return 0;
}
```

## 解题技巧

1. 使用二分查找可以将时间复杂度从指数级降低到对数级
2. 通过模拟运输过程精确控制载重
3. 注意处理边界条件和特殊情况

## 常见问题

### Q1：为什么选择二分查找？
二分查找可以快速缩小查找范围，对于这类优化问题非常高效。

### Q2：如何确定初始查找范围？
- 左边界：确保可以装载最重的单个包裹
- 右边界：所有包裹的总重量

## 总结

这是一道考察二分查找和贪心算法思想的经典题目。通过模拟运输过程，我们可以精确地找到最低运载量。

## 扩展阅读

- [二分查找算法详解](https://leetcode.cn/link)
- [贪心算法原理](https://leetcode.cn/link)

## 版权声明

本文由 [Your Name] 原创，遵循 MIT 开源协议。