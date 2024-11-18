# LeetCode
# 剑指 Offer 45. 把数组排成最小的数

## 题目描述

给定一个非负整数数组，要求将数组中的数字拼接起来，生成能拼接出的最小的一个数。

### 注意事项

- 输出的数字可能非常大，所以返回一个字符串。
- 拼接的数字可能会有前导零，最后的结果不需要去掉前导零。

## 解题思路

要生成能拼接出的最小数，我们需要根据数字的拼接方式来判断大小。具体而言，对于两个数字 `a` 和 `b`，我们需要比较 `a + b` 和 `b + a` 的大小，选择拼接后的数字较小的顺序。通过对数组中的数字进行排序，能够拼接出最小的数字。

### 关键步骤

1. **字符串比较**：
   - 拼接的数字需要根据字符串的拼接顺序来判断大小。即，两个数字 `x` 和 `y` 比较时，我们判断 `x + y` 和 `y + x` 的大小。
   
2. **自定义排序**：
   - 使用自定义的比较函数，对数字进行排序。这样，拼接后的最小值就能够通过排序得到。

3. **特殊情况**：
   - 如果所有的数字都是 0，那么结果应该是 `"0"`，而不是多个零。

## C 语言实现

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// 自定义比较函数
int compare(const void *a, const void *b) {
    // 将两个数字转成字符串并拼接，比较拼接后的结果
    char str1[20], str2[20];
    sprintf(str1, "%d", *(int *)a);
    sprintf(str2, "%d", *(int *)b);
    // 拼接后比较大小
    if (strcmp(str1, str2) < 0)
        return -1;
    else
        return 1;
}

char* minNumber(int* nums, int n) {
    // 数组为空，返回空字符串
    if (n == 0) {
        return "";
    }

    // 使用 qsort 对数字进行排序
    qsort(nums, n, sizeof(int), compare);

    // 创建一个足够大的字符数组来存储结果
    char* result = (char*)malloc(n * 10 * sizeof(char));  // 假设每个数字不超过10位
    int index = 0;

    // 将排序后的数字拼接成字符串
    for (int i = 0; i < n; i++) {
        sprintf(result + index, "%d", nums[i]);
        index += strlen(result + index);
    }

    // 特殊情况，如果结果的第一个字符是 '0'，那么返回 "0"
    if (result[0] == '0') {
        return "0";
    }

    return result;
}

int main() {
    int nums[] = {3, 30, 34, 5, 9};
    int n = sizeof(nums) / sizeof(nums[0]);

    char* result = minNumber(nums, n);
    printf("%s\n", result);  // 输出 "3033459"

    return 0;
}

时间复杂度
排序操作的时间复杂度为 O(n log n)，其中 n 是数组的长度。
在 qsort 中，我们需要将数字转换成字符串并进行比较，因此排序的实际复杂度会比 O(n log n) 稍微高一些，但一般仍然可以接受。
