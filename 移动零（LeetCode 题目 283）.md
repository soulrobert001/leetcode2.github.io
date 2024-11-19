### 移动零（LeetCode 题目 283）

#### 题目描述
给定一个数组 `nums`，要求将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序不变。

#### 说明
- 必须在原数组上操作，不能拷贝额外的数组。
- 尽量减少操作次数。

#### 示例

**示例 1**:
```
输入: nums = [0, 1, 0, 3, 12]
输出: [1, 3, 12, 0, 0]
```

**示例 2**:
```
输入: nums = [0]
输出: [0]
```

#### 解题思路
这道题可以通过双指针法来解决。具体步骤如下：
1. 使用一个指针遍历数组，找到所有非零元素，并将它们移动到数组的前部。
2. 遍历结束后，将数组剩余位置全部填上 `0`。

#### 代码实现（C语言）
下面是C语言的代码实现：

```c
#include <stdio.h>

void moveZeroes(int* nums, int numsSize) {
    int left = 0; // 用于记录非零元素的位置

    // 遍历数组，将非零元素移动到数组前部
    for (int right = 0; right < numsSize; right++) {
        if (nums[right] != 0) {
            nums[left] = nums[right];
            left++;
        }
    }

    // 将剩余位置填上零
    for (int i = left; i < numsSize; i++) {
        nums[i] = 0;
    }
}

int main() {
    int nums[] = {0, 1, 0, 3, 12};
    int numsSize = sizeof(nums) / sizeof(nums[0]);

    moveZeroes(nums, numsSize);

    // 输出结果
    printf("输出结果: ");
    for (int i = 0; i < numsSize; i++) {
        printf("%d ", nums[i]);
    }

    return 0;
}
```

### 代码解释

1. **函数 `moveZeroes` 的定义**：
   ```c
   void moveZeroes(int* nums, int numsSize) {
       int left = 0; // 用于记录非零元素的位置
   
       // 遍历数组，将非零元素移动到数组前部
       for (int right = 0; right < numsSize; right++) {
           if (nums[right] != 0) {
               nums[left] = nums[right];
               left++;
           }
       }
   
       // 将剩余位置填上零
       for (int i = left; i < numsSize; i++) {
           nums[i] = 0;
       }
   }
   ```

   - `moveZeroes` 函数接收一个数组指针 `nums` 和数组的大小 `numsSize`。
   - 使用一个指针 `left` 来记录非零元素的位置。
   - 遍历数组，将所有非零元素移动到数组前部，同时使用 `left` 指针跟踪位置。
   - 遍历结束后，将剩余位置填上零。

2. **主函数 `main`**：
   ```c
   int main() {
       int nums[] = {0, 1, 0, 3, 12};
       int numsSize = sizeof(nums) / sizeof(nums[0]);
   
       moveZeroes(nums, numsSize);
   
       // 输出结果
       printf("输出结果: ");
       for (int i = 0; i < numsSize; i++) {
           printf("%d ", nums[i]);
       }
   
       return 0;
   }
   ```

   - 定义并初始化一个数组 `nums`。
   - 计算数组的大小 `numsSize`。
   - 调用 `moveZeroes` 函数将零移动到数组末尾。
   - 输出处理后的数组结果。

### 示例输出

```
输出结果: 1 3 12 0 0 
```


---

### 相关链接
- [LeetCode 题目 283](https://leetcode.com/problems/move-zeroes/)
- [双指针法简介](https://en.wikipedia.org/wiki/Two-pointer_technique)
