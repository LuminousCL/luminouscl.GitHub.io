---
title: 【Laioffer】Plane Production Problem
tags:
  - 算法
---



### Plane Production Problem

Given twp production lines that can produce the same plane, and each line has n stations. For each station of each production line can produce a specific part od the machine, for example, Prod_1 means the ith station of Production line 1 can produce the ith part of the plane. Both station Prod_1 and station Prod_2 can produce the same part_0 of the plane with different time cost Prod1[0] and Prod2[0].

The plane can be produced after each part is produced one by one. Note that, when the ith part of the plane is made, the incomplete plane can be transferred to another production line at extra time cost. For example, T12[i] means after the ith part is done, the time cost to transfer the plane from production line 1 to line 2, and T21[i] means after the ith part is done, the time cost to transfer the plane from production line2 to line1. Return the minimum time needed to produce the plane with two production lines.



**Clarification:** 

All integers in the array are positive which represents the time cost;

Input: int[] Prod_1, int[] Prod_2, int[] T12, int[] T21;

Output: integer which represents the minimum time needed to produce the plane.



**Assumption:**  

Follow up :

N pipelines ? (for loop to finish the 2D matrix)

Prod_1.length != Prod_2.length? ...(firstly DP finish the shorter pipeline)



**Result:** 

**Base case:**

M1[0] = Prod_1[0];

M2[0] = Prod_2[0];

**Induction rule:**

M1[i] represents the minimum time cost needed when the plane is at 1st production line and ith part is finished;

M2[i] represents the minimum time cost needed when the plane is at 2nd production line and ith part is finished;

M1[i] = case1: M1[i - 1] + Prod_1[i]

​			  case2: M2[i - 1] + Prod_1[i] + T21[i - 1]

M2[i] = case1: M2[i - 1] + Prod_2[i]

​			  case2: M1[i - 1] + Prod_2[i] + T12[i - 1]



**Test:** 

Prod_1[N] = {4, 5, 2, 7, 8, 19};

Prod_1[N] = {3, 6, 3, 2, 9, 20};

T12[N] = {3, 1, 4, 1, 5, 9};

T21[N] = {2, 6, 9, 7, 9, 3};

Minumum time: 43.

```java
package DP;

public class Plane_Production_Problem {
    public static int planeProduction(int[] Prod_1, int[] Prod_2, int[] T12, int[] T21) {
        // M1[i] represents the minimum time cost needed when the plane is at 1st production line and ith part is finished;
        // M2[i] represents the minimum time cost needed when the plane is at 2nd production line and ith part is finished;
        int[] M1 = new int[Prod_1.length];
        int[] M2 = new int[Prod_1.length];
        M1[0] = Prod_1[0];
        M2[0] = Prod_2[0];

        for (int i = 1; i < Prod_1.length; i++) {
            M1[i] = Math.min(M1[i - 1] + Prod_1[i], M2[i - 1] + Prod_1[i] + T21[i - 1]);
            M2[i] = Math.min(M2[i - 1] + Prod_2[i], M1[i - 1] + Prod_2[i] + T12[i - 1]);
        }
        return Math.min(M1[Prod_1.length - 1], M2[Prod_1.length - 1]);
    }

    public static void main(String[] args) {
        Plane_Production_Problem solution = new Plane_Production_Problem();

        // test case
        int[] Prod_1 = new int[]{4, 5, 2, 7, 8, 19};
        int[] Prod_2 = new int[]{3, 6, 3, 2, 9, 20};
        int[] T12 = new int[]{3, 1, 4, 1, 5, 9};
        int[] T21 = new int[]{2, 6, 9, 7, 9, 3};

        int a = solution.planeProduction(Prod_1, Prod_2, T12, T21);
        System.out.println(a);
    }
}
```

|    Time Complexity    |              Space Complexity              |
| :-------------------: | :----------------------------------------: |
|         O(N)          |                   O(2n)                    |
| 一个for循环go over DP | DP的问题需要记录下之前的结果；可以优化空间 |

