# LeetCode 剑指 Offer 45：把数组排成最小的数

## 题目描述

### 问题定义
给定非负整数数组 `nums`，将数组中的数字拼接成最小的数。

### 输入输出要求
- 输入：非负整数数组
- 输出：拼接成的最小数字字符串
- 数组长度：`0 < nums.length ≤ 100`

### 示例展示

#### 示例 1
- 输入: `[10, 2]`
- 输出: `"102"`

#### 示例 2
- 输入: `[3, 30, 34, 5, 9]`
- 输出: `"3033459"`

## 解题思路

### 核心算法：特殊排序

#### 关键洞察
- 传统数字大小比较不适用
- 需要根据拼接后的字符串大小排序

### 排序规则
1. 将数字转换为字符串
2. 比较 `a + b` 与 `b + a` 的大小
3. 按此规则升序排序
4. 拼接排序后的数组

## C语言实现

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 自定义比较函数
int compare(const void* a, const void* b) {
    char num1[20], num2[20];
    sprintf(num1, "%d%d", *(int*)a, *(int*)b);
    sprintf(num2, "%d%d", *(int*)b, *(int*)a);
    return strcmp(num1, num2);
}

char* minNumber(int* nums, int numsSize) {
    // 使用 qsort 排序
    qsort(nums, numsSize, sizeof(int), compare);
    
    // 分配结果内存
    char* result = (char*)malloc(11 * numsSize + 1);
    result[0] = '\0';
    
    // 拼接数字
    for (int i = 0; i < numsSize; i++) {
        char temp[20];
        sprintf(temp, "%d", nums[i]);
        strcat(result, temp);
    }
    
    return result;
}
```

## 算法详解

### 比较函数设计

```c
int compare(const void* a, const void* b) {
    char num1[20], num2[20];
    // 尝试两种拼接顺序
    sprintf(num1, "%d%d", *(int*)a, *(int*)b);
    sprintf(num2, "%d%d", *(int*)b, *(int*)a);
    // 比较拼接后的字符串大小
    return strcmp(num1, num2);
}
```

#### 比较示例
- `3` 和 `30`
  - `330` vs `303`
  - 选择 `303`，即 `30` 在前

### 关键函数解析

1. `qsort()`
   - 系统快速排序函数
   - 自定义比较逻辑

2. `sprintf()`
   - 整数转字符串
   - 拼接数字

3. `strcmp()`
   - 字符串字典序比较

## 复杂度分析

### 时间复杂度
- `O(nlogn)`
- 排序算法主要耗时

### 空间复杂度
- `O(n)`
- 额外字符串存储空间

## 边界情况处理

1. 数组为空
2. 数组只有一个元素
3. 数组包含 0
4. 数字范围很大

## 代码测试

```c
int main() {
    int nums[] = {3, 30, 34, 5, 9};
    int numsSize = sizeof(nums) / sizeof(nums[0]);
    
    char* result = minNumber(nums, numsSize);
    printf("最小数字: %s\n", result);
    
    free(result);
    return 0;
}
```

## 可能的优化方向

1. 预分配内存优化
2. 使用更高效的字符串处理
3. 针对特定数据范围的定制算法

## 相似问题

- LeetCode 179. 最大数
- 字符串排序
- 数字重排问题

## 学习总结

本题考察：
- 排序算法
- 自定义比较函数
- 字符串处理
- 数学思维转换

**关键在于：改变思维，用字符串拼接大小代替数字大小比较**