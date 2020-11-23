---
title:  【Leetcode】1088 Confusing Number II
tags:
  - 算法
---



### Leetcode 1088.Confusing Number II

We can rotate digits by 180 degrees to form new digits. When 0, 1, 6, 8, 9 are rotated 180 degrees, they become 0, 1, 9, 8, 6 respectively. When 2, 3, 4, 5 and 7 are rotated 180 degrees, they become invalid.

A *confusing number* is a number that when rotated 180 degrees becomes a **different** number with each digit valid.(Note that the rotated number can be greater than the original number.)

Given a positive integer `N`, return the number of confusing numbers between `1` and `N` inclusive.



**Clarification:** 

```
Input: 20
Output: 6
Explanation: 
The confusing numbers are [6,9,10,16,18,19].
6 converts to 9.
9 converts to 6.
10 converts to 01 which is just 1.
16 converts to 91.
18 converts to 81.
19 converts to 61.
```

```
Input: 100
Output: 19
Explanation: 
The confusing numbers are [6,9,10,16,18,19,60,61,66,68,80,81,86,89,90,91,98,99,100].
```



**Assumption:**  

1 <= N <= 10^9.



**Test:** As before.



**Solution 1:  常规**

```java
import java.util.*;

public class Confusing_Number_II {
    public int confusingNumberII(int N) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(6, 9);
        map.put(9, 6);
        map.put(0, 0);
        map.put(1, 1);
        map.put(8, 8);

        int count = 0;
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
                count++;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Confusing_Number_II solution = new Confusing_Number_II();

        // test cases to cover all the possible situations.
        int a = solution.confusingNumberII(100000);
        System.out.println(a);
    }
}
```

|     Time Complexity     |                Space Complexity                |
| :---------------------: | :--------------------------------------------: |
|          O(N)           |                      O(5)                      |
| (本思路在Leetcode上TLE) | 只要用一个有限的hashmap存对应的rotating number |



**Solution 2: DFS**

```java
import java.util.*;

public class Confusing_Number_II {
    Map<Integer, Integer> map = new HashMap<>();
    int result = 0;

    public int confusingNumberII(int N) {
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
            result++;
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
        Confusing_Number_II solution = new Confusing_Number_II();

        // test cases to cover all the possible situations.
        int a = solution.confusingNumberII(100000);
        System.out.println(a);
    }
}
```

| Time Complexity |     Space Complexity      |
| :-------------: | :-----------------------: |
|    O(N / ?)     | O(5 + recursion tree高度) |
|        -        |             -             |

本题在思路上和上一题主体一致，唯一注意的是需要使用DFS来实现（基于confusing number必定由confusing number变换而来），时间复杂度上的分析不是很确定，等待后续完善。