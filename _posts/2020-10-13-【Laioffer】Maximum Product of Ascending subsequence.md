---
title:  【Laioffer】Maximum Product of Ascending subsequence
tags:
  - 算法
---



### Maximum Product of Ascending subsequence

Given an array of positive/negative integers, return the maximum product of numbers that forms an ascending subsequnce.



**Clarification:** 

There are positive and negative numbers randomly in the array;

Ascending subsequence.

Input: input array;

Output: integer which represents the maximum product of ascending subsequnce.



**Assumption:** 

Null.



**Result:** 

**Base case:**

M1[0] = M2[0] = input[0];

**Induction rule:**

 M1[i] represents the maximum product of an ascending subsequence that ends at i (includes ith element);
 M2[i] represents the minimum product of an ascending subsequence that ends at i (includes ith element).

M1[i] = find the maximum M1[j] * input[i], M2[j] * input[i] and input[i] itself when input[j] < input[i];

M1[i] = find the minimum M1[j] * input[i], M2[j] * input[i] and input[i] itself when input[j] < input[i].



**Test:** 

Input[N] = {-10, -4, -1, -3, 3, -2}

output = -10 * -4 * -3 * -2 = 240.

```java
package DP;

public class Maximum_product_of_Ascending_Subsequence {
    public static int maximumProduct(int[] input) {
        // M1[i] represents the maximum product of an ascending subsequence that ends at i (includes ith element);
        // M2[i] represents the minimum product of an ascending subsequence that ends at i (includes ith element);
        int[] M1 = new int[input.length];
        int[] M2 = new int[input.length];

        M1[0] = M2[0] = input[0];

        for (int i = 1; i < input.length; i++) {
            M1[i] = M2[i] = input[i];
            for (int j = 0; j < i; j++) {
                if (input[j] < input[i]) {
                    M1[i] = Math.max(M1[j] * input[i], M2[j] * input[i]);
                    M1[i] = Math.max(M1[i], input[i]);
                    M2[i] = Math.min(M1[j] * input[i], M2[j] * input[i]);
                    M2[i] = Math.min(M2[i], input[i]);
                }
            }
        }
        return M1[input.length - 1];
    }

    public static void main(String[] args) {
        Maximum_product_of_Ascending_Subsequence solution = new Maximum_product_of_Ascending_Subsequence();

        // test case
        int[] input = new int[]{-10, -4, 1, -3, 3, -2};

        int a = solution.maximumProduct(input);
        System.out.println(a);
    }
}
```

|    Time Complexity    |              Space Complexity              |
| :-------------------: | :----------------------------------------: |
|        O(n^2)         |                   O(2n)                    |
| 两个for循环go over DP | DP的问题需要记录下之前的结果；可以优化空间 |
