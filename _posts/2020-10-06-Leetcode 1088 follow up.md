---
title:  Leetcode 1088 follow up
tags:
  - 算法
---



### Leetcode 1088. Minimum Add to Make Parentheses Valid(follow up)

We can rotate digits by 180 degrees to form new digits. When 0, 1, 6, 8, 9 are rotated 180 degrees, they become 0, 1, 9, 8, 6 respectively. When 2, 3, 4, 5 and 7 are rotated 180 degrees, they become invalid.

A *confusing number* is a number that when rotated 180 degrees becomes a **different** number with each digit valid.(Note that the rotated number can be greater than the original number.)

Given a positive integer `N`, return all confusing numbers between `1` and `N` inclusive.



**Clarification:** 

```
Input: 20
Output: [6,9,10,16,18,19]
Explanation: 
The confusing numbers are [6,9,10,16,18,19].
6 converts to 9.
9 converts to 6.
10 converts to 01 which is just 1.
16 converts to 91.
18 converts to 81.
19 converts to 61.
```



**Assumption:**  

1 <= N <= 10^9.



**Test:** As before.



**Solution 1: 常规 ** 

```java
import java.util.*;

public class Confusing_Number_III {
    public List<Integer> confusingNumberIII(int N) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(6, 9);
        map.put(9, 6);
        map.put(0, 0);
        map.put(1, 1);
        map.put(8, 8);

        List<Integer> result = new ArrayList<>();
        for (int i = 1; i <= N; i++) {
            int newNum = 0;
            int tmp = i;
            while (tmp != 0) {
                if (!map.containsKey(tmp % 10)) {
                    newNum = i;
                    break;
                }
                newNum = 10 * newNum + map.get(tmp % 10);
                tmp /= 10;
            }
            if (i != newNum) {
                result.add(i);
            }
        }
        return result;
    }

    public static void main(String[] args) {
        Confusing_Number_III solution = new Confusing_Number_III();

        // test cases to cover all the possible situations.
        List<Integer> a = solution.confusingNumberIII(100);
        System.out.println(a);
    }
}
```

| Time Complexity |                       Space Complexity                       |
| :-------------: | :----------------------------------------------------------: |
|      O(N)       |                    O(n + length(result))                     |
|        -        | 只要用一个有限的hashmap存对应的rotating number；加上result的长度 |



**Solution 2: DFS** 

```java
import java.util.*;

public class Confusing_Number_III {
    Map<Integer, Integer> map = new HashMap<>();
    List<Integer> result = new ArrayList<>();

    public List<Integer> confusingNumberIII(int N) {
        map.put(6, 9);
        map.put(9, 6);
        map.put(0, 0);
        map.put(1, 1);
        map.put(8, 8);
        dfs(N, 0);
        return result;
    }

    private void dfs(int N, int cur) {
        if (isConfusingNumber(cur)) {
            result.add(cur);
        }
        for (Integer i : map.keySet()) {
            if (cur * 10 + i <= N && cur * 10 + i != 0) {
                dfs(N, cur * 10 + i);
            }
        }
    }

    private boolean isConfusingNumber(int num) {
        int newNum = 0;
        int tmp = num;
        while (tmp != 0) {
            if (!map.containsKey(tmp % 10)) {
                return false;
            }
            newNum = 10 * newNum + map.get(tmp % 10);
            tmp /= 10;
        }
        return num == newNum ? false : true;
    }

    public static void main(String[] args) {
        Confusing_Number_III solution = new Confusing_Number_III();

        // test cases to cover all the possible situations.
        List<Integer> a = solution.confusingNumberIII(100);
        System.out.println(a);
    }
}
```

| Time Complexity |              Space Complexity              |
| :-------------: | :----------------------------------------: |
|      O(N)       | O(5 + length(result) + recursion tree高度) |
|        -        |                     -                      |
