### 合并两个有序数组（LeetCode 题目 88）

#### 题目描述
给定两个有序数组 `nums1` 和 `nums2`。

要求：将 `nums2` 合并到 `nums1` 中，使 `nums1` 成为一个有序数组。

#### 说明
- 给定数组 `nums1` 的空间大小为 `m + n`，其中前 `m` 个为 `nums1` 的元素，后面 `n` 个为 `0`。
- 给定数组 `nums2` 的空间大小为 `n`。
- 0 ≤ m, n ≤ 200。
- 1 ≤ m + n ≤ 200。
- -10^9 ≤ nums1[i], nums2[j] ≤ 10^9。

#### 示例

**示例 1**:
```
输入：nums1 = [1, 2, 3, 0, 0, 0], m = 3, nums2 = [2, 5, 6], n = 3
输出：[1, 2, 2, 3, 5, 6]
解释：需要合并 [1, 2, 3] 和 [2, 5, 6] 。
合并结果是 [1, 2, 2, 3, 5, 6] 。
```

**示例 2**:
```
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
解释：需要合并 [1] 和 [] 。
合并结果是 [1] 。
```

#### 解题思路
我们可以使用双指针法来解决这个问题。具体步骤如下：
1. 使用两个指针分别指向 `nums1` 和 `nums2` 的末尾位置。
2. 从后向前遍历，将较大的元素放入 `nums1` 的末尾，直到所有元素都合并完毕。

#### 代码实现（C语言）

```c
#include <stdio.h>

void merge(int* nums1, int m, int* nums2, int n) {
    int i = m - 1;
    int j = n - 1;
    int k = m + n - 1;
    
    // 从后向前遍历，将较大的元素放入 nums1 的末尾
    while (i >= 0 && j >= 0) {
        if (nums1[i] > nums2[j]) {
            nums1[k--] = nums1[i--];
        } else {
            nums1[k--] = nums2[j--];
        }
    }

    // 如果 nums2 有剩余，直接放入 nums1
    while (j >= 0) {
        nums1[k--] = nums2[j--];
    }
}

int main() {
    // 示例 1
    int nums1_1[] = {1, 2, 3, 0, 0, 0};
    int nums2_1[] = {2, 5, 6};
    merge(nums1_1, 3, nums2_1, 3);

    printf("示例 1 合并结果: ");
    for (int i = 0; i < 6; i++) {
        printf("%d ", nums1_1[i]);
    }
    printf("\n");

    // 示例 2
    int nums1_2[] = {1};
    int nums2_2[] = {};
    merge(nums1_2, 1, nums2_2, 0);

    printf("示例 2 合并结果: ");
    for (int i = 0; i < 1; i++) {
        printf("%d ", nums1_2[i]);
    }
    printf("\n");

    return 0;
}
```

### 代码解释：

1. **函数 `merge` 的定义**：
   ```c
   void merge(int* nums1, int m, int* nums2, int n) {
       int i = m - 1;
       int j = n - 1;
       int k = m + n - 1;
       
       // 从后向前遍历，将较大的元素放入 nums1 的末尾
       while (i >= 0 && j >= 0) {
           if (nums1[i] > nums2[j]) {
               nums1[k--] = nums1[i--];
           } else {
               nums1[k--] = nums2[j--];
           }
       }
   
       // 如果 nums2 有剩余，直接放入 nums1
       while (j >= 0) {
           nums1[k--] = nums2[j--];
       }
   }
   ```
   - 使用双指针分别指向 `nums1` 和 `nums2` 的末尾。
   - 从后向前遍历，将较大的元素放入 `nums1` 的末尾。
   - 如果 `nums2` 有剩余元素，将其直接放入 `nums1`。

2. **主函数 `main`**：
   ```c
   int main() {
       // 示例 1
       int nums1_1[] = {1, 2, 3, 0, 0, 0};
       int nums2_1[] = {2, 5, 6};
       merge(nums1_1, 3, nums2_1, 3);
   
       printf("示例 1 合并结果: ");
       for (int i = 0; i < 6; i++) {
           printf("%d ", nums1_1[i]);
       }
       printf("\n");
   
       // 示例 2
       int nums1_2[] = {1};
       int nums2_2[] = {};
       merge(nums1_2, 1, nums2_2, 0);
   
       printf("示例 2 合并结果: ");
       for (int i = 0; i < 1; i++) {
           printf("%d ", nums1_2[i]);
       }
       printf("\n");
   
       return 0;
   }
   ```
   - 定义并初始化两个示例数组。
   - 调用 `merge` 函数合并数组。
   - 输出合并后的数组结果。


---

### 相关链接
- [LeetCode 题目 88](https://leetcode.com/problems/merge-sorted-array/)
- [双指针法简介](https://en.wikipedia.org/wiki/Two-pointer_technique)
