### 存在重复元素 III（LeetCode 题目 220）

#### 题目描述
给定一个整数数组 `nums`，以及两个整数 `k` 和 `t`。

#### 要求
判断数组中是否存在两个不同下标 `i` 和 `j`，其对应元素满足 `abs(nums[i] - nums[j]) ≤ t`，同时满足 `abs(i - j) ≤ k`。如果满足条件则返回 `True`，不满足条件返回 `False`。

#### 说明
- 0 < `nums.length` < 2 × 10^4
- -2^31 < `nums[i]` < 2^31 - 1
- 0 ≤ `k` ≤ 10^4
- 0 ≤ `t` ≤ 2^31 - 1

#### 示例

**示例 1**:
```
输入: nums = [1, 2, 3, 1], k = 3, t = 0
输出: True
```

**示例 2**:
```
输入: nums = [1, 0, 1, 1], k = 1, t = 2
输出: True
```

#### 解题思路
为了满足题目的要求，我们需要在数组中找到两个不同下标 `i` 和 `j`，满足两个条件：`abs(nums[i] - nums[j]) ≤ t` 和 `abs(i - j) ≤ k`。我们可以使用滑动窗口和二叉搜索树来解决这个问题。

1. 使用一个滑动窗口来维护当前窗口中的元素。
2. 在每次迭代中，使用一个二叉搜索树来检查是否存在符合条件的元素。
3. 更新滑动窗口中的元素，以确保窗口大小不超过 `k`。

#### 代码实现（Python）

```python
from sortedcontainers import SortedList

def containsNearbyAlmostDuplicate(nums, k, t):
    if t < 0: return False
    sorted_list = SortedList()
    for i in range(len(nums)):
        if i > k:
            sorted_list.remove(nums[i - k - 1])
        pos1 = SortedList.bisect_left(sorted_list, nums[i] - t)
        pos2 = SortedList.bisect_right(sorted_list, nums[i] + t)
        if pos1 != pos2 and pos1 != len(sorted_list):
            return True
        sorted_list.add(nums[i])
    return False

# 示例测试
print(containsNearbyAlmostDuplicate([1, 2, 3, 1], 3, 0)) # 输出: True
print(containsNearbyAlmostDuplicate([1, 0, 1, 1], 1, 2)) # 输出: True
```

### 代码解释：

1. **导入 `SortedList` 模块**：
   ```python
   from sortedcontainers import SortedList
   ```
   - `SortedList` 是一个保持元素有序的列表，用于高效地执行插入和查找操作。

2. **定义函数 `containsNearbyAlmostDuplicate`**：
   ```python
   def containsNearbyAlmostDuplicate(nums, k, t):
       if t < 0: return False
       sorted_list = SortedList()
       for i in range(len(nums)):
           if i > k:
               sorted_list.remove(nums[i - k - 1])
           pos1 = SortedList.bisect_left(sorted_list, nums[i] - t)
           pos2 = SortedList.bisect_right(sorted_list, nums[i] + t)
           if pos1 != pos2 and pos1 != len(sorted_list):
               return True
           sorted_list.add(nums[i])
       return False
   ```

3. **滑动窗口和检查条件**：
   - `SortedList.bisect_left` 和 `SortedList.bisect_right` 用于找到符合条件的范围。
   - `sorted_list.remove` 和 `sorted_list.add` 用于维护滑动窗口。
   - 检查条件是否满足，若满足则返回 `True`。

4. **示例测试**：
   ```python
   print(containsNearbyAlmostDuplicate([1, 2, 3, 1], 3, 0)) # 输出: True
   print(containsNearbyAlmostDuplicate([1, 0, 1, 1], 1, 2)) # 输出: True
   ```

---

### 相关链接
- [LeetCode 题目 220](https://leetcode.com/problems/contains-duplicate-iii/)
- [滑动窗口技术简介](https://en.wikipedia.org/wiki/Sliding_window_protocol)