### 相对名次（LeetCode 题目 506）

#### 题目描述
给定一个长度为 `n` 的数组 `score`，其中 `score[i]` 表示第 `i` 名运动员在比赛中的成绩。所有成绩互不相同。

#### 要求
找出他们的相对名次，并授予前三名对应的奖牌。前三名运动员将分别授予「金牌（"Gold Medal"）」，「银牌（"Silver Medal"）」和「铜牌（"Bronze Medal"）」。

#### 示例

**示例 1**:
```
输入：score = [5, 4, 3, 2, 1]
输出：["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
解释：名次为 [1st, 2nd, 3rd, 4th, 5th] 。
```

**示例 2**:
```
输入：score = [10, 3, 8, 9, 4]
输出：["Gold Medal", "5", "Bronze Medal", "Silver Medal", "4"]
解释：名次为 [1st, 5th, 3rd, 2nd, 4th] 。
```

#### 解题思路
1. 创建一个包含原始索引的成绩列表，并按成绩降序排序。
2. 遍历排序后的成绩列表，根据索引位置更新名次和奖牌。
3. 返回最终结果列表。

#### 代码实现（C语言）

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 定义一个结构体来保存成绩和原始索引
typedef struct {
    int score;
    int index;
} Athlete;

// 比较函数，用于qsort排序
int compare(const void *a, const void *b) {
    return ((Athlete *)b)->score - ((Athlete *)a)->score;
}

char** findRelativeRanks(int* score, int scoreSize, int* returnSize) {
    Athlete athletes[scoreSize];
    char **result = (char **)malloc(scoreSize * sizeof(char *));
    *returnSize = scoreSize;

    // 初始化运动员数组
    for (int i = 0; i < scoreSize; i++) {
        athletes[i].score = score[i];
        athletes[i].index = i;
    }

    // 按成绩降序排序
    qsort(athletes, scoreSize, sizeof(Athlete), compare);

    // 分配奖牌和名次
    for (int i = 0; i < scoreSize; i++) {
        result[athletes[i].index] = (char *)malloc(20 * sizeof(char));
        if (i == 0) {
            strcpy(result[athletes[i].index], "Gold Medal");
        } else if (i == 1) {
            strcpy(result[athletes[i].index], "Silver Medal");
        } else if (i == 2) {
            strcpy(result[athletes[i].index], "Bronze Medal");
        } else {
            sprintf(result[athletes[i].index], "%d", i + 1);
        }
    }

    return result;
}

int main() {
    int score1[] = {5, 4, 3, 2, 1};
    int scoreSize1 = sizeof(score1) / sizeof(score1[0]);
    int returnSize1;
    char **result1 = findRelativeRanks(score1, scoreSize1, &returnSize1);

    printf("示例 1 输出结果: ");
    for (int i = 0; i < returnSize1; i++) {
        printf("%s ", result1[i]);
        free(result1[i]); // 释放内存
    }
    free(result1); // 释放内存
    printf("\n");

    int score2[] = {10, 3, 8, 9, 4};
    int scoreSize2 = sizeof(score2) / sizeof(score2[0]);
    int returnSize2;
    char **result2 = findRelativeRanks(score2, scoreSize2, &returnSize2);

    printf("示例 2 输出结果: ");
    for (int i = 0; i < returnSize2; i++) {
        printf("%s ", result2[i]);
        free(result2[i]); // 释放内存
    }
    free(result2); // 释放内存
    printf("\n");

    return 0;
}
```

### 代码解释：

1. **定义结构体 `Athlete`**：
   ```c
   typedef struct {
       int score;
       int index;
   } Athlete;
   ```
   - 结构体 `Athlete` 用于保存运动员的成绩和原始索引。

2. **比较函数 `compare`**：
   ```c
   int compare(const void *a, const void *b) {
       return ((Athlete *)b)->score - ((Athlete *)a)->score;
   }
   ```
   - `compare` 函数用于 `qsort` 的排序，它比较两个 `Athlete` 结构体的成绩，用于降序排序。

3. **函数 `findRelativeRanks`**：
   ```c
   char** findRelativeRanks(int* score, int scoreSize, int* returnSize) {
       Athlete athletes[scoreSize];
       char **result = (char **)malloc(scoreSize * sizeof(char *));
       *returnSize = scoreSize;
   
       // 初始化运动员数组
       for (int i = 0; i < scoreSize; i++) {
           athletes[i].score = score[i];
           athletes[i].index = i;
       }
   
       // 按成绩降序排序
       qsort(athletes, scoreSize, sizeof(Athlete), compare);
   
       // 分配奖牌和名次
       for (int i = 0; i < scoreSize; i++) {
           result[athletes[i].index] = (char *)malloc(20 * sizeof(char));
           if (i == 0) {
               strcpy(result[athletes[i].index], "Gold Medal");
           } else if (i == 1) {
               strcpy(result[athletes[i].index], "Silver Medal");
           } else if (i == 2) {
               strcpy(result[athletes[i].index], "Bronze Medal");
           } else {
               sprintf(result[athletes[i].index], "%d", i + 1);
           }
       }
   
       return result;
   }
   ```
   - 创建并初始化 `Athlete` 数组，将每个运动员的成绩和索引存储起来。
   - 使用 `qsort` 函数按成绩降序排序。
   - 根据排序后的结果分配奖牌和名次，将结果存储在 `result` 数组中。

4. **主函数 `main`**：
   ```c
   int main() {
       int score1[] = {5, 4, 3, 2, 1};
       int scoreSize1 = sizeof(score1) / sizeof(score1[0]);
       int returnSize1;
       char **result1 = findRelativeRanks(score1, scoreSize1, &returnSize1);
   
       printf("示例 1 输出结果: ");
       for (int i = 0; i < returnSize1; i++) {
           printf("%s ", result1[i]);
           free(result1[i]); // 释放内存
       }
       free(result1); // 释放内存
       printf("\n");
   
       int score2[] = {10, 3, 8, 9, 4};
       int scoreSize2 = sizeof(score2) / sizeof(score2[0]);
       int returnSize2;
       char **result2 = findRelativeRanks(score2, scoreSize2, &returnSize2);
   
       printf("示例 2 输出结果: ");
       for (int i = 0; i < returnSize2; i++) {
           printf("%s ", result2[i]);
           free(result2[i]); // 释放内存
       }
       free(result2); // 释放内存
       printf("\n");
   
       return 0;
   }
   ```
   - 定义并初始化两个示例数组。
   - 调用 `findRelativeRanks` 函数获取每个示例的结果。
   - 输出并释放结果数组。


---

### 相关链接
- [LeetCode 题目 506](https://leetcode.com/problems/relative-ranks/)
- [C语言 `qsort` 函数](https://en.cppreference.com/w/c/algorithm/qsort)
