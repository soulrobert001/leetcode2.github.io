# LeetCode 第二次打卡

## 日期：2024年11月17日

### 今天的题目

1. **题目名称**：[两数之和](https://leetcode.com/problems/two-sum/)

   - **题目难度**：简单
   - **用时**：30分钟
   - **解题思路**：
     1. 使用哈希表存储已经访问过的元素。
     2. 对于每一个元素，检查目标值减去当前元素的差是否在哈希表中。
     3. 如果是，返回两个元素的索引；否则，将当前元素加入哈希表。
   - **代码实现**：

   ```python
   def twoSum(nums, target):
       seen = {}
       for i, num in enumerate(nums):
           complement = target - num
           if complement in seen:
               return [seen[complement], i]
           seen[num] = i
   ```
