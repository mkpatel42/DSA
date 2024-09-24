# Binary Search Notes

## Table of Contents
1. [Introduction](#introduction)
   - [Example](#real-time-example-of-binary-search)
   - [Master Template](#general-binary-search-template)
2. [Basic Problems](#basic-problems)
   - [First Bad Version](#278-first-bad-versionhttpsleetcodecomproblemsfirst-bad-version)
   - [Sqrt of Number](#69-sqrtx-easyhttpsleetcodecomproblemssqrtx)
   - [Search Insertion Point](#35-search-insert-position-easyhttpsleetcodecomproblemssearch-insert-position)
3. [Advanced Problems](#advanced-problems)
   - [Capacity To Ship Packages Within D Days](#1011-capacity-to-ship-packages-within-d-dayshttpsleetcodecomproblemscapacity-to-ship-packages-within-d-days-medium)
   - [Split Array Largest Sum](#410-split-array-largest-sum-hardhttpsleetcodecomproblemssplit-array-largest-sumdescription)
   - [Koko Eating Bananas](#875-koko-eating-bananas-mediumhttpsleetcodecomproblemskoko-eating-bananasdescription)
   - [Minimum Number of Days to Make m Bouquets](#1482-minimum-number-of-days-to-make-m-bouquets-mediumhttpsleetcodecomproblemsminimum-number-of-days-to-make-m-bouquetsdescription)
   - [Kth Smallest Number in Multiplication Table](#668-kth-smallest-number-in-multiplication-table-hardhttpsleetcodecomproblemskth-smallest-number-in-multiplication-tabledescription)
   - [Find K-th Smallest Pair Distance](#719-find-k-th-smallest-pair-distance-hardhttpsleetcodecomproblemsfind-k-th-smallest-pair-distancedescription)
   - [Ugly Number III](#1201-ugly-number-iii-mediumhttpsleetcodecomproblemsugly-number-iiidescription)
   - [Find the Smallest Divisor Given a Threshold](#1283-find-the-smallest-divisor-given-a-threshold-mediumhttpsleetcodecomproblemsfind-the-smallest-divisor-given-a-thresholddescription)
4. [Practice Problems](#practice-problems)

## Introduction

Binary Search is an efficient algorithm used to find a target element in a sorted array or search space. It works by repeatedly dividing the search space in half, making it much faster than a linear search, especially for large datasets.
## Real-Time Example of Binary Search

### Scenario: Searching for a Name in a Phonebook

Imagine you have a **phonebook** sorted alphabetically, and you want to find the phone number of **Emily Green**. Instead of checking names one by one (linear search), you can use **binary search** to speed up the process by halving the search space at each step.

### Steps:
1. **Open the middle page** of the phonebook.
    - If the name is **"Emily Green"**, you're done!
    - If the name is **earlier** than "Emily Green" (e.g., "Charlie Brown"), search the **second half**.
    - If the name is **later** than "Emily Green" (e.g., "George White"), search the **first half**.

2. **Discard half of the phonebook** and focus on the remaining half.

3. **Repeat** the process, halving the search space, until you find **Emily Green**.

### Why It's Effective:
- Binary search reduces the search time from O(n) linear search to O(log n).
- In a large phonebook, this means finding the name much faster than checking every entry.


####However, implementing it correctly can be tricky due to common pitfalls like:

- Choosing the right loop exit condition (`left < right` vs. `left <= right`)
- Initializing boundary variables (`left` and `right`)
- Updating boundaries correctly (`left = mid`, `left = mid + 1`, etc.)

Binary Search can be applied to a wide range of problems beyond simple array searches.

## General Binary Search Template

To generalize binary search, we can often frame problems as:

**Minimize** k, **subject to** `condition(k)` is True.

### Binary Search Template Code

```Java
public class Solution {
    public static int binarySearch(int[] array) {

        // We need to identify left and right condition based on problem
        int left = 0;
        int right = array.length - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            // Define the condition, for example checking if array[mid] >= target
            if (condition(array[mid])) {
                right = mid;  // Shrink the right boundary
            } else {
                left = mid + 1;  // Shrink the left boundary
            }
        }

        return left;  // Return the smallest index satisfying the condition
    }
}
```


## Key Points
1. **Initialize boundaries**: Ensure the boundaries encompass all possible values. Usually, `left` starts at the minimum value and `right` at the maximum.
2. **Return value**: After the loop, return `left`. The `left` pointer will hold the smallest value that satisfies the condition.
3. **Design the condition function**: This is the critical part and requires practice. The condition checks whether the current `mid` value satisfies the desired property (problem-specific).

## Basic Problems

### [278. First Bad Version](https://leetcode.com/problems/first-bad-version/)
**Problem**: You are a product manager and need to find the first bad version among `n` versions using the API `isBadVersion(version)`.

- **Solution**: Use binary search to minimize `k` such that `isBadVersion(k)` is true.

#### Code:

```java
public class Solution {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

# [69. Sqrt(x) (Easy)](https://leetcode.com/problems/sqrtx/)

### Problem
Implement `int sqrt(int x)`. Compute and return the square root of `x` where `x` is a non-negative integer. Since the return type is an integer, the decimal digits are truncated, and only the integer part of the result is returned.

### Example
**Input:** `4`  
**Output:** `2`

**Input:** `8`  
**Output:** `2` (since the integer part of `sqrt(8)` is `2`)

### Solution
We use binary search to find the minimal value `k` such that `k^2 > x`. Once found, `k - 1` is the result since we are only concerned with the integer part of the square root.

### Java Code
```java
public class Solution {
    public int mySqrt(int x) {
        int left = 0, right = x + 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (mid * mid > x) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left - 1;
    }
}
```

# [35. Search Insert Position (Easy)](https://leetcode.com/problems/search-insert-position/)

### Problem
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You may assume no duplicates in the array.

### Example
**Input:** `[1, 3, 5, 6], 5`  
**Output:** `2`

**Input:** `[1, 3, 5, 6], 2`  
**Output:** `1`

### Solution
This problem is a classic application of binary search. We are looking for the minimal index `k` such that `nums[k] >= target`. The right boundary is initialized to `len(nums)` to accommodate cases where the target is larger than all elements.

### Java Code
```java
public class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
    }
}
```

## Advanced Problems

# [1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) [Medium]

## Problem
A conveyor belt has packages that must be shipped from one port to another within `D` days. Each package has a weight represented by `weights[i]`. We need to determine the least weight capacity of the ship that will allow all packages to be shipped within `D` days, following the order of the weights.

### Example
**Input:** `weights = [1,2,3,4,5,6,7,8,9,10], D = 5`  
**Output:** `15`  
**Explanation:** A ship capacity of 15 is the minimum to ship all packages in 5 days.

## Explanation
To solve this problem using binary search, we need to identify the monotonicity present:

1. If we can successfully ship all packages within `D` days with a given capacity `m`, then we can definitely ship them with any capacity larger than `m`. This establishes that we are looking for the minimal feasible capacity.

2. **Condition Function**: We define a function `feasible(capacity)` that returns whether it is possible to ship all packages within `D` days for a given capacity. This function operates greedily:
    - Accumulate weights until the current day's capacity is exceeded.
    - If exceeded, increment the day count and reset the total weight to the current package's weight.
    - If the total days exceed `D`, return `False`; otherwise, return `True`.

3. **Boundary Initialization**:
    - The minimum capacity (`left`) should be at least the maximum weight of the packages, `max(weights)`.
    - The maximum capacity (`right`) can be the sum of all weights, `sum(weights)`, as that would allow shipping all packages in one day.

With these components, we can apply the binary search template.

## Java Code

```java
class Solution {
   private int[] weights;
   private int days;

   private boolean feasible(int capacity) {
      int daysNeeded = 1;
      int currentLoad = 0;
      for (int weight : weights) {
         if (currentLoad + weight > capacity) {
            daysNeeded++;
            currentLoad = weight;
         } else {
            currentLoad += weight;
         }
         if (daysNeeded > days) return false;
      }
      return true;
   }

   public int shipWithinDays(int[] weights, int days) {
      this.weights = weights;
      this.days = days;

      int left = 0;
      int right = 0;
      for (int weight : weights) {
         left = Math.max(left, weight);
         right += weight;
      }

      while (left < right) {
         int mid = left + (right - left) / 2;
         if (feasible(mid)) {
            right = mid;
         } else {
            left = mid + 1;
         }
      }
      return left;
   }
}
```

# [410. Split Array Largest Sum (Hard)](https://leetcode.com/problems/split-array-largest-sum/description/)

## Problem
Given an array of non-negative integers and an integer `m`, you can split the array into `m` non-empty continuous subarrays. The goal is to minimize the largest sum among these `m` subarrays.

### Example
**Input:**  
`nums = [7,2,5,10,8]`  
`m = 2`

**Output:**  
`18`

**Explanation:**  
The best way to split `nums` into two subarrays is `[7,2,5]` and `[10,8]`, where the largest sum among the two subarrays is 18.

## Explanation
This problem can be approached using binary search, similar to LC 1011. We can define a feasible function that checks if we can split the array into `m` subarrays such that each subarray's sum does not exceed a given threshold.

### Steps:
1. **Feasibility Function**: Given a threshold, determine if it's possible to split the array such that no subarray has a sum greater than the threshold.
    - Maintain a count of subarrays and a total sum for the current subarray.
    - If adding a number exceeds the threshold, increment the subarray count and reset the total sum.

2. **Binary Search**:
    - Initialize `left` as the maximum element in `nums` and `right` as the sum of all elements in `nums`.
    - Perform binary search to find the minimal feasible capacity.

### Java Code

```java

class Solution {
   private int[] nums;
   private int k;

   private boolean feasible(int threshold) {
      int count = 1;
      int total = 0;
      for (int num : nums) {
         if (total + num > threshold) {
            total = num;
            count++;
            if (count > k) return false;
         } else {
            total += num;
         }
      }
      return true;
   }

   public int splitArray(int[] nums, int k) {
      this.nums = nums;
      this.k = k;

      int left = 0;
      int right = 0;
      for (int num : nums) {
         left = Math.max(left, num);
         right += num;
      }

      while (left < right) {
         int mid = left + (right - left) / 2;
         if (feasible(mid)) {
            right = mid;
         } else {
            left = mid + 1;
         }
      }
      return left;
   }
}

```

# [875. Koko Eating Bananas (Medium)](https://leetcode.com/problems/koko-eating-bananas/description/)

Koko loves to eat bananas. There are N piles of bananas, the i-th pile has piles[i] bananas. The guards have gone and will come back in H hours. Koko can decide her bananas-per-hour eating speed of K. Each hour, she chooses some pile of bananas, and eats K bananas from that pile. If the pile has less than K bananas, she eats all of them instead, and won't eat any more bananas during this hour.

Koko likes to eat slowly, but still wants to finish eating all the bananas before the guards come back. Return the minimum integer K such that she can eat all the bananas within H hours.

## Example :

Input: piles = [3,6,7,11], H = 8
Output: 4

Input: piles = [30,11,23,4,20], H = 5
Output: 30

Input: piles = [30,11,23,4,20], H = 6
Output: 23

Very similar to LC 1011 and LC 410 mentioned above. Let's design a feasible function, given an input speed, determine whether Koko can finish all bananas within H hours with hourly eating speed speed. Obviously, the lower bound of the search space is 1, and upper bound is max(piles), because Koko can only choose one pile of bananas to eat every hour.

```java
class Solution {
   public int minEatingSpeed(int[] piles, int h) {
      int left = 1, right = getMax(piles);

      while (left < right) {
         int mid = left + (right - left) / 2;
         if (feasible(piles, h, mid)) {
            right = mid;
         } else {
            left = mid + 1;
         }
      }

      return left;
   }

   private boolean feasible(int[] piles, int h, int speed) {
      int time = 0;
      for (int banana : piles) {
         time += banana/speed;
         if(banana % speed != 0) {
            time++;
         }
         if(time > h){
            return false;
         }
      }
      return true;
   }

   private int getMax(int[] piles) {
      int max = piles[0];
      for (int pile : piles) {
         max = Math.max(max, pile);
      }
      return max;
   }
   
}
```


# [1482. Minimum Number of Days to Make m Bouquets (Medium)](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/description/)

Given an integer array bloomDay, an integer m and an integer k. We need to make m bouquets. To make a bouquet, you need to use k adjacent flowers from the garden. The garden consists of n flowers, the ith flower will bloom in the bloomDay[i] and then can be used in exactly one bouquet. Return the minimum number of days you need to wait to be able to make m bouquets from the garden. If it is impossible to make m bouquets return -1.


## Examples :

Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3

Explanation: Let's see what happened in the first three days. x means flower bloomed and _ means flower didn't bloom in the garden.
We need 3 bouquets each should contain 1 flower.

After day 1: [x, _, _, _, _]   // we can only make one bouquet.

After day 2: [x, _, _, _, x]   // we can only make two bouquets.

After day 3: [x, _, x, _, x]   // we can make 3 bouquets. The answer is 3.


Input: bloomDay = [1,10,3,10,2], m = 3, k = 2

Output: -1

Explanation: We need 3 bouquets each has 2 flowers, that means we need 6 flowers. We only have 5 flowers so it is impossible to get the needed bouquets and we return -1.

Now that we've solved three advanced problems above, this one should be pretty easy to do. The monotonicity of this problem is very clear: if we can make m bouquets after waiting for d days, then we can definitely finish that as well if we wait for more than d days.

```java
class Solution {
    public int minDays(int[] bloomDay, int m, int k) {
        if (m * k > bloomDay.length) return -1;

        int left = 1, right = 1000000000;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (canMakeBouquets(bloomDay, m, k, mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }

    private boolean canMakeBouquets(int[] bloomDay, int m, int k, int days) {
        int bouquets = 0, flowers = 0;
        for (int bloom : bloomDay) {
            if (bloom <= days) {
                flowers++;
                if (flowers == k) {
                    bouquets++;
                    flowers = 0;
                }
            } else {
                flowers = 0;
            }
        }
        return bouquets >= m;
    }
}
```

# [668. Kth Smallest Number in Multiplication Table (Hard)](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/)

Nearly everyone has used the Multiplication Table. But could you find out the k-th smallest number quickly from the multiplication table? Given the height m and the length n of an m * n Multiplication Table, and a positive integer k, you need to return the k-th smallest number in this table.

## Example:

Input: m = 3, n = 3, k = 5
Output: 3
Explanation:
The Multiplication Table:
1	2	3
2	4	6
3	6	9

The 5-th smallest number is 3 (1, 2, 2, 3, 3).

## Solution Approach

For Kth-Smallest problems like this, what comes to mind first is a Heap. Usually, we can maintain a Min-Heap and just pop the top of the Heap for k times. However, that doesn't work out in this problem. We don't have every single number in the entire Multiplication Table; instead, we only have the height and the length of the table.

This is when binary search comes in. We can design an `enough` function that, given an input `num`, determines whether there are at least k values less than or equal to `num`. The minimal `num` satisfying the `enough` function is the answer we're looking for.

## Implementation

```java
class Solution {
    public int findKthNumber(int m, int n, int k) {
        int left = 1;
        int right = m * n;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (enough(mid, m, n, k)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
    }
    
    private boolean enough(int num, int m, int n, int k) {
        int count = 0;
        for (int i = 1; i <= m; i++) {
            int add = Math.min(num / i, n);
            if (add == 0) {
                break;
            }
            count += add;
        }
        return count >= k;
    }
}
```

# [719. Find K-th Smallest Pair Distance (Hard)](https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/)

Given an integer array, return the k-th smallest distance among all the pairs. The distance of a pair (A, B) is defined as the absolute difference between A and B.

## Example:

Input:
nums = [1,3,1]
k = 1
Output: 0
Explanation:
Following are all the pairs. The 1st smallest distance pair is (1,1), and its distance is 0.

(1,3) -> 2

(1,1) -> 0

(3,1) -> 2

## Solution

We can use binary search to find the k-th smallest distance. The key is to design an `enough` function that determines whether there are at least k pairs with a distance less than or equal to a given value.

```java
class Solution {
   public int smallestDistancePair(int[] nums, int k) {
      Arrays.sort(nums);
      int n = nums.length;
      int left = 0;
      int right = nums[n - 1] - nums[0];

      while (left < right) {
         int mid = left + (right - left) / 2;
         if (enough(nums, mid, k)) {
            right = mid;
         } else {
            left = mid + 1;
         }
      }

      return left;
   }

   private boolean enough(int[] nums, int distance, int k) {
      int count = 0;
      int i = 0;
      for (int j = 0; j < nums.length; j++) {
         while (nums[j] - nums[i] > distance) {
            i++;
         }
         count += j - i;
      }
      return count >= k;
   }
}
```

# [1201. Ugly Number III (Medium)](https://leetcode.com/problems/ugly-number-iii/description/)

Write a program to find the n-th ugly number. Ugly numbers are positive integers which are divisible by a or b or c.

## Examples:

Example 1:
Input: n = 3, a = 2, b = 3, c = 5
Output: 4
Explanation: The ugly numbers are 2, 3, 4, 5, 6, 8, 9, 10... The 3rd is 4.

Example 2:
Input: n = 4, a = 2, b = 3, c = 4
Output: 6
Explanation: The ugly numbers are 2, 3, 4, 6, 8, 9, 10, 12... The 4th is 6.

## Solution

We can use binary search to find the n-th ugly number. The key is to design an `enough` function that determines whether there are at least n ugly numbers less than or equal to a given value.

```java
class Solution {
    public int nthUglyNumber(int n, int a, int b, int c) {
        long ab = lcm(a, b);
        long ac = lcm(a, c);
        long bc = lcm(b, c);
        long abc = lcm(a, bc);
        
        long left = 1, right = 2_000_000_000;
        while (left < right) {
            long mid = left + (right - left) / 2;
            if (enough(mid, a, b, c, ab, ac, bc, abc, n)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return (int) left;
    }
    
    private boolean enough(long num, int a, int b, int c, long ab, long ac, long bc, long abc, int n) {
        long count = num / a + num / b + num / c - num / ab - num / ac - num / bc + num / abc;
        return count >= n;
    }
    
    private long gcd(long a, long b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }
    
    private long lcm(long a, long b) {
        return a * b / gcd(a, b);
    }
}
```

# [1283. Find the Smallest Divisor Given a Threshold (Medium)](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/description/)

Given an array of integers `nums` and an integer `threshold`, we will choose a positive integer divisor and divide all the array by it and sum the result of the division. Find the smallest divisor such that the result mentioned above is less than or equal to `threshold`.

Each result of division is rounded to the nearest integer greater than or equal to that element. (For example: 7/3 = 3 and 10/2 = 5). It is guaranteed that there will be an answer.

## Example:

Input: nums = [1,2,5,9], threshold = 6
Output: 5
Explanation: We can get a sum to 17 (1+2+5+9) if the divisor is 1.
If the divisor is 4 we can get a sum to 7 (1+1+2+3) and if the divisor is 5 the sum will be 5 (1+1+1+2).

## Solution

We can use binary search to find the smallest divisor. The condition function checks if the sum of divisions is less than or equal to the threshold.

```java
class Solution {
    public int smallestDivisor(int[] nums, int threshold) {
        int left = 1;
        int right = getMaxElement(nums);
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (condition(nums, mid, threshold)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
    }
    
    private boolean condition(int[] nums, int divisor, int threshold) {
        int sum = 0;
        for (int num : nums) {
            sum += (num - 1) / divisor + 1;
        }
        return sum <= threshold;
    }
    
    private int getMaxElement(int[] nums) {
        int max = nums;
        for (int num : nums) {
            max = Math.max(max, num);
        }
        return max;
    }
}
```

## Practice Problems:
1. [Guess Number Higher or Lower (Easy)](https://leetcode.com/problems/guess-number-higher-or-lower/)
2. [Binary Search (Easy)](https://leetcode.com/problems/binary-search/)
3. [Search in Rotated Sorted Array (Medium)](https://leetcode.com/problems/search-in-rotated-sorted-array/)
4. [Find Minimum in Rotated Sorted Array (Medium)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
5. [Peak Index in a Mountain Array (Medium)](https://leetcode.com/problems/peak-index-in-a-mountain-array/)
6. [Find Peak Element (Medium)](https://leetcode.com/problems/find-peak-element/)
7. [Search a 2D Matrix (Medium)](https://leetcode.com/problems/search-a-2d-matrix/)
8. [Find the Duplicate Number (Medium)](https://leetcode.com/problems/find-the-duplicate-number/)
9. [Find Smallest Letter Greater Than Target (Easy)](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)
10. [Single Element in a Sorted Array (Medium)](https://leetcode.com/problems/single-element-in-a-sorted-array/)
11. [Count Negative Numbers in a Sorted Matrix (Easy)](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/)
12. [Time Based Key-Value Store (Medium)](https://leetcode.com/problems/time-based-key-value-store/)
13. [Find First and Last Position of Element in Sorted Array (Medium)](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
14. [Search in Rotated Sorted Array II (Medium)](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)
15. [Find Minimum in Rotated Sorted Array II (Hard)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)
16. [Kth Smallest Element in a Sorted Matrix (Medium)](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
17. [Median of Two Sorted Arrays (Hard)](https://leetcode.com/problems/median-of-two-sorted-arrays/)