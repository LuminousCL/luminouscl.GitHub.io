---
title:  Plane Production Problem
tags:
  - 算法
---



### Paint N pieces of wood

Paint N pieces of wood with two colors white and black, the only constraint is that there cannot be more than two adjacent woods with the same color. Please find out how many possible ways to paint the wood.

**Example 1:**

```
Input: N = 3
Output: 6
Explanation: possible ways: BBW, BWB, BWW, WBW, WBB, WWB
```

**Example 2:**

```
Input: 4
Output: 8
Explanation: BWBW, BWWB, BBWW, BBWB, WBWB, WBBW, WWBB, WWBW
```



**Clarification:** 

N  > 0.



**Base case :** 

MB[0] = 1, MW[0] = 1.  

以黑色结尾的一段木头，方法数就是1；以白色结尾的一段木头，方法数也是1

MB[1] = 2, MW[1] = 2.  

以黑色结尾的两段木头，方法数是2（白黑，黑黑）；以白色结尾的两段木头，方法数是2（黑白，白白）



**Induction rule: **

MB[i]表示以黑色结尾，对从0到i-1段的木材的着色方法数；
MW[i]表示以白色结尾，对从0到i-1段的木材的着色方法数；

考察以黑色结尾的方法数：

1.我们可以很明显的看出以B结尾的方法数 = case1方法数 + case2方法数 + case3方法数

2.case1方法数 + case2方法数 = MW[i - 1]

3.case3方法数不好表示，但是我们可以转换思路，case3方法数 = MB[i - 1] - MB[i - 2]

**MB[i] = MW[i - 1] + (MB[i - 1] - MB[i - 2])**

**MW[i] = MB[i - 1] + (MW[i - 1] - MW[i - 2])**

(i为黑色前提下，i-1结尾为黑色且i-2结尾为白色的方法数 = i-1结尾为黑色的总方法数 - i-2结尾为黑色总方法数)

|  Case  | i - 2 | i - 1 | i    |
| :----: | :---: | :---: | ---- |
| Case 1 |   B   |   W   | B    |
| Case 2 |   W   |   W   | B    |
| Case 3 |   W   |   B   | B    |

最后输出结果为MB[N - 1] + MW[N - 1]



**Solution：** 

```java
package DP;

public class Color_Wood {
    public static int color(int N) {
        // MB[i] represents the ways to color the wood ending with black from 0 to i-1;
        // MW[i] represents the ways to color the wood ending with white from 0 to i-1;
        int[] MB = new int[N];
        int[] MW = new int[N];
        MB[0] = 1;
        MB[1] = 2;
        MW[0] = 1;
        MW[1] = 2;

        for (int i = 2; i < N; i++) {
            MB[i] = MW[i - 1] + (MB[i - 1] - MB[i - 2]);
            MW[i] = MB[i - 1] + (MW[i - 1] - MW[i - 2]);
        }
        return MB[N - 1] + MW[N - 1];
    }

    public static void main(String[] args) {
        Color_Wood  solution = new Color_Wood();
        int a = solution.color(4);
        System.out.println(a);
    }
}
```

| Time Complexity |     Space Complexity      |
| :-------------: | :-----------------------: |
|      O(N)       |           O(2N)           |
|  一遍for loop   | 只要用一个有限的int array |
