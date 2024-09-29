
## Table of Contents

1. [Running from Both Ends of Array](#runnig-from-both-ends-of-array)
    - [Template](#template)
    - [2 Sum Pattern](#2-sum-problem)
        - [15. 3Sum](#15-3sum)
        - [18. 4Sum](#18-4sum)
        - [1498. Number of Subsequences That Satisfy the Given Sum Condition](#1498-number-of-subsequences-that-satisfy-the-given-sum-condition)
        - [653. Two Sum IV - Input is a BST](#653-two-sum-iv---input-is-a-bst)
        - [881. Boats to Save People](#881-boats-to-save-people)
        - [1877. Minimize Maximum Pair Sum in Array](#1877-minimize-maximum-pair-sum-in-array)
        - [923. 3Sum With Multiplicity](#923-3sum-with-multiplicity)
    - [Trapping Water](#trapping-water)
        - [Trapping Rain Water](#trapping-rain-water)
    - [Next Permutation](#next-permutation)
    - [Reversing / Swapping](#reversing--swapping)
        - [Valid Palindrome](#valid-palindrome)
        - [344. Reverse String](#344-reverse-string)
        - [345. Reverse Vowels of a String](#345-reverse-vowels-of-a-string)
        - [680. Valid Palindrome II](#680-valid-palindrome-ii)
        - [917. Reverse Only Letters](#917-reverse-only-letters)
        - [27. Remove Element](#27-remove-element)
        - [75. Sort Colors](#75-sort-colors)
        - [977. Squares of a Sorted Array](#977-squares-of-a-sorted-array)
        - [905. Sort Array By Parity](#905-sort-array-by-parity)
        - [922. Sort Array By Parity II](#922-sort-array-by-parity-ii)
        - [969. Pancake Sorting](#969-pancake-sorting)
        - [2000. Reverse Prefix of Word](#2000-reverse-prefix-of-word)
        - [541. Reverse String II](#541-reverse-string-ii)
        - [557. Reverse Words in a String III](#557-reverse-words-in-a-string-iii)
    - [Others](#others)
        - [948. Bag of Tokens](#948-bag-of-tokens)
        - [942. DI String Match](#942-di-string-match)
        - [1750. Minimum Length of String After Deleting Similar Ends](#1750-minimum-length-of-string-after-deleting-similar-ends)
        - [1813. Sentence Similarity III](#1813-sentence-similarity-iii)
        - [658. Find K Closest Elements](#658-find-k-closest-elements)
        - [821. Shortest Distance to a Character](#821-shortest-distance-to-a-character)
2. [Slow & Fast Pointers](#slow--fast-pointers)
   - [Template](#template-slow--fast)
   - [Linked List Operations](#linked-list-operations)
   - [Cyclic Detection](#cyclic-detection)
       - [457. Circular Array Loop](#457-circular-array-loop)
   - [Sliding Window/Caterpillar Method](#sliding-windowcaterpillar-method)
       - [795. Number of Subarrays with Bounded Maximum](#795-number-of-subarrays-with-bounded-maximum)
       - [1040. Moving Stones Until Consecutive II](#1040-moving-stones-until-consecutive-ii)
       - [1782. Count Pairs Of Nodes](#1782-count-pairs-of-nodes)
       - [696. Count Binary Substrings](#696-count-binary-substrings)
       - [532. K-diff Pairs in an Array](#532-k-diff-pairs-in-an-array)
   - [Rotation](#rotation)
       - [1861. Rotating the Box](#1861-rotating-the-box)
       - [189. Rotate Array](#189-rotate-array)
   - [String Operations](#string)
       - [String Compression](#443-string-compression)
       - [Last Substring in lexicographical order](#1163-last-substring-in-lexicographical-order)
   - [Remove Duplicates](#remove-duplicate)
       - [26. Remove Duplicates from Sorted Array](#26-remove-duplicates-from-sorted-array)
       - [80. Remove Duplicates from Sorted Array II](#80-remove-duplicates-from-sorted-array-ii)
       - [82. Remove Duplicates from Sorted List II](#82-remove-duplicates-from-sorted-list-ii)
       - [1089. Duplicate Zeros](#1089-duplicate-zeros)
   - [Others](#others-slow--fast-pointers)
       - [1093. Statistics from a Large Sample](#1093-statistics-from-a-large-sample)
       - [763. Partition Labels](#763-partition-labels)
       - [481. Magical String](#481-magical-string)
       - [825. Friends Of Appropriate Ages](#825-friends-of-appropriate-ages)
       - [845. Longest Mountain in Array](#845-longest-mountain-in-array)
       - [1574. Shortest Subarray to be Removed to Make Array Sorted](#1574-shortest-subarray-to-be-removed-to-make-array-sorted)
     

# Runnig from both ends of array

### Template
```Java
class Solution {
    template(int[] arr){
        int left = 0;
        int right = arr.length - 1;
        
        while(left<right){
            // computation
            if(someCondition()){
                left++;
            }else{
                right--;
            }
        }
    }

}
```

## 2 Sum Problem
### [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.



**Example 1:**

Input: numbers = [2,7,11,15], target = 9

Output: [1,2]

Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

**Example 2:**


Input: numbers = [2,3,4], target = 6

Output: [1,3]

Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

#### Intuition

- The array is sorted, allowing the use of a two-pointer approach.
- Initialize one pointer (p1) at the start and the other (p2) at the end of the array.
- If the sum of elements at p1 and p2 equals the target, return their indices.
- If the sum is greater than the target, move p2 left; if less, move p1 right.
- This approach efficiently finds the solution in O(n) time.

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int p1 = 0;
        int p2 = nums.length-1;
        int[] ans = new int[2];
        
        while(p1 < p2){
            int sum = nums[p1]+nums[p2];     
            if(sum == target){
                ans[0] = p1+1;
                ans[1] = p2+1;
                break;
            }
            else if(sum > target){
                p2--;
            }
            else{
                p1++;
            }
        }
        return ans;
    }
}
```

### [15. 3Sum](https://leetcode.com/problems/3sum/description/)

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.



**Example 1:**

Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]

Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.

nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.

nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.

The distinct triplets are [-1,0,1] and [-1,-1,2]. 

Notice that the order of the output and the order of the triplets does not matter.



**Example 2:**

Input: nums = [0,1,1]

Output: []

Explanation: The only possible triplet does not sum up to 0.

**Example 3:**

Input: nums = [0,0,0]

Output: [[0,0,0]]

Explanation: The only possible triplet sums up to 0.

#### Intuition

- Sorting: First, we sort the array to make it easier to avoid duplicates and efficiently find triplets.
- Two-pointer approach: For each element nums[i], we use two pointers (k and l) to find pairs that, along with nums[i], sum up to zero.
- Avoiding duplicates: We skip duplicate elements while iterating to ensure unique triplets in the result.
- Sum comparison: If the sum of nums[i] + nums[k] + nums[l] equals zero, we add the triplet to the result; otherwise, adjust the pointers to find a valid triplet.

```Java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        // calculating the quadruplets:
        for (int i = 0; i < n; i++) {
            // avoid the duplicates while moving i:
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            // 2 pointers:
            int k = i + 1;
            int l = n - 1;
            while (k < l) {
                long sum = nums[i];
                sum += nums[k];
                sum += nums[l];
                if (sum == 0) {
                    List<Integer> temp = new ArrayList<>();
                    temp.add(nums[i]);
                    temp.add(nums[k]);
                    temp.add(nums[l]);
                    ans.add(temp);
                    k++;
                    l--;

                    // skip the duplicates:
                    while (k < l && nums[k] == nums[k - 1]) k++;
                    while (k < l && nums[l] == nums[l + 1]) l--;
                } else if (sum < 0) k++;
                else l--;
            }
        }

        return ans;
    }

}
```

### [18. 4Sum](https://leetcode.com/problems/4sum/description/)

Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n

a, b, c, and d are distinct.

nums[a] + nums[b] + nums[c] + nums[d] == target

You may return the answer in any order.

#### Intuition
- Sorting: Start by sorting the array to make it easier to use the two-pointer approach and avoid duplicates.
- Iterate with two loops: Use two nested loops to fix the first two numbers (nums[i] and nums[j]), and for each pair, find two more numbers to complete the quadruplet.
- Two-pointer approach: Use two pointers (k and l) to search for the other two numbers that sum up with nums[i] and nums[j] to the target.
- Check for duplicates: Skip duplicate numbers for both the first two loops and the two-pointer step to ensure only unique quadruplets are included in the result.
- Sum comparison: If the sum equals the target, add the quadruplet to the result; if the sum is less, move the left pointer (k) right, otherwise move the right pointer (l) left.
```Java
class Solution {



    public List<List<Integer>> fourSum(int[] nums, int target) {
       int n = nums.length; // size of the array
        List<List<Integer>> ans = new ArrayList<>();

        // sort the given array:
        Arrays.sort(nums);

        // calculating the quadruplets:
        for (int i = 0; i < n-3; i++) {
            // avoid the duplicates while moving i:
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < n-2; j++) {
                // avoid the duplicates while moving j:
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;

                // 2 pointers:
                int k = j + 1;
                int l = n - 1;
                while (k < l) {
                    long sum = nums[i];
                    sum += nums[j];
                    sum += nums[k];
                    sum += nums[l];
                    if (sum == target) {
                        List<Integer> temp = new ArrayList<>();
                        temp.add(nums[i]);
                        temp.add(nums[j]);
                        temp.add(nums[k]);
                        temp.add(nums[l]);
                        ans.add(temp);
                        k++;
                        l--;

                        // skip the duplicates:
                        while (k < l && nums[k] == nums[k - 1]) k++;
                        while (k < l && nums[l] == nums[l + 1]) l--;
                    } else if (sum < target) k++;
                    else l--;
                }
            }
        }

        return ans;
    }

  
}
```

### [1498. Number of Subsequences That Satisfy the Given Sum Condition](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/description/)

#### Intuition
- Sorting: We first sort the array so we can easily find pairs of numbers that add up to the target.
- Two Pointers: We use two pointers—one starting at the beginning (left) and the other at the end (right) of the array—to check pairs of numbers.
- Valid Pairs: If the sum of the numbers at these pointers is less than or equal to the target, we can form many valid subsequences with numbers between these two pointers. We keep track of these using precomputed powers of 2.
- Count Subsequences: When we find a valid pair, we add the number of valid subsequences to our total count.
- Adjust Pointers: If the sum is greater than the target, we move the right pointer to the left to try a smaller number, allowing us to check all possible pairs.

**We will precompute power of 2, so it would be efficient and within MOD range**
```Java
class Solution {
    public int numSubseq(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        int left = 0, right = n - 1;
        int mod = 1000000007;
        int res = 0;

        // Precompute powers of 2 up to n to avoid recalculating
        int[] powerOfTwo = new int[n + 1];
        powerOfTwo[0] = 1; // 2^0 = 1
        for (int i = 1; i <= n; i++) {
            powerOfTwo[i] = (int)((1L * powerOfTwo[i - 1] * 2) % mod);
        }

        while (left <= right) {
            if (nums[left] + nums[right] <= target) {
                res = (res + powerOfTwo[right - left]) % mod; // Use precomputed power
                left++;
            } else {
                right--;
            }
        }
        return res;
    }
}

```
### [653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/description/)

#### Intuition
- traverse tree and can we convefrt tree into sorted array?
- Once we find sorted array then it is 2 sum problem

```Java
class Solution {
    public void dfs(TreeNode root,ArrayList<Integer> list){
        if(root == null) return;
        
        dfs(root.left,list);
        list.add(root.val);
        dfs(root.right,list);
        
    }
    public boolean findTarget(TreeNode root, int k) {
        ArrayList<Integer> list = new ArrayList<>();
        dfs(root,list);
        int i = 0;
        int j = list.size()-1;
        while(i<j){
            int sum = list.get(i) + list.get(j);
            if(sum == k){
                return true;
            }
            if(sum < k){
                i++;
            }else{
                j--;
            }
        }
        return false;
    }
}
```
### [633. Sum of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers/description/)

**Problem:** Given a non-negative integer c, decide whether there're two integers a and b such that a² + b² = c.

#### Intuition
- Can we consider n as straight line left to right boundary?
- Can we create condition in a way it shrinks our search space?

```Java
class Solution {
    public boolean judgeSquareSum(int c) {
        long left = 0, right = (long) Math.sqrt(c);
        while (left <= right) {
            if (left * left + right * right == c) return true;
            else if (left * left + right * right > c) right--;
            else left++;
        }
        return false;
    }
}
```

### [881. Boats to Save People](https://leetcode.com/problems/boats-to-save-people/description/)

You are given an array people where people[i] is the weight of the ith person, and an infinite number of boats where each boat can carry a maximum weight of limit. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most limit.

Return the minimum number of boats to carry every given person.

#### Intuition
- Sort an array
- Maximum 2 people possible, so best pick is minimum and maximum weight combination
- for that combination we will need one boat

```Java
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        Arrays.sort(people);
        int i = 0;
        int j = people.length - 1;
        int boat = 0;
        while(i<=j){
             boat++;
            if(people[i] + people[j] <= limit){
               
                i++;
                j--;
            }else{
                 j--;
            }
        }
        return boat;
    }
}
```

### [1877. Minimize Maximum Pair Sum in Array](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/description/)

#### Intuition

- Sort the array.
- Minimize the pair by using the first and last elements of the sorted array.
- Meanwhile, we need to store the maximum sum.

```Java
class Solution {
    
    public int minPairSum(int[] nums) {

        Arrays.sort(nums);

        int left = 0;
        int right = nums.length - 1;
        int max = 0;
        while(left < right){
            max = Math.max(max, nums[left] + nums[right]);
            left++;
            right--;

        }
        return max;
    }
}
```

### [923. 3Sum With Multiplicity](https://leetcode.com/problems/3sum-with-multiplicity/description/)
**ADVANCED 3Sum**
#### Intuition
When we find the three array element values, x, y, and z; how do we make sure their corresponding index values meet the requirement where indexes are i < j < k? More precisely, in the if and elif statements, we compare the array element values, but not the array index values. If the LeetCode problem itself say the array is sorted, then it makes more sense. But it doesn't say if the array is sorted or not.
A1: The problems states: ...return the number of tuples i, j, k such that i < j < k and arr[i] + arr[j] + arr[k] == target....
The above actually means return the number of tuples of 3 elements with a sum of target.
i < j < k in this problem actually means i, j and k are 3 different indices.

```Java
class Solution {
        public int threeSumMulti(int[] A, int target) {
        Arrays.sort(A);
        long res = 0;
        for (int i = 0; i < A.length - 2; ++i) {
            int j = i + 1;
            int k = A.length - 1;
            while (j < k) {
                if (A[j] + A[k] < target - A[i]) { 
                    ++j;
                }else if (A[j] + A[k] > target - A[i]) {
                    --k;
                }else {
                    int l = 1, r = 1;
                    while (j + l < k && A[j + l] == A[j]) { ++l; } // l: number of elements equal to A[j].
                    while (j + l <= k - r && A[k - r] == A[k]) { ++r; } // r: number of elements equal to A[k].
                    // If A[j...k] are all equal, then there are C(k - j + 1, 2) cases
                    // that meet the requirement;
                    // Otherwise, there are l * r cases that meet the requirement.
                    res += A[j] == A[k] ? (k - j + 1) * (k - j) / 2 : l * r ;
                    j += l; // forward j by l steps.
                    k -= r; // backward k by r steps.
                }
            }
        }
        return (int)(res % 1_000_000_007);
    }
}
```

## Trapping Water
### [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)
# PENDING

## Next Permutation
# PENDING

## Reversing / Swapping

### [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

#### Intuition
- palindrom needs to match from start and end
- can we skip non alpha numberic and convert upper case to lowercase?

```Java
/**
 * One Pass Solution using two pointers
 *
 * Time Complexity: O(N)
 *
 * Space Complexity: O(1)
 *
 * N = Length of input string.
 */
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

### [344. Reverse String](https://leetcode.com/problems/reverse-string/description/)

```Java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;

        while(left < right){
            s[left] = (char)((int)(s[left])  ^ (int)(s[right]));
            s[right] = (char)((int)(s[left])  ^ (int)(s[right]));
            s[left] = (char)((int)(s[left])  ^ (int)(s[right]));
            left++;
            right--;
        }

    }
}
```

### [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)

```Java
class Solution {
    public String reverseVowels(String s) {
        char[] arr = s.toCharArray();
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            char leftChar = Character.toLowerCase(arr[left]);
            char rightChar = Character.toLowerCase(arr[right]);

            if (!isVowel(leftChar)) {
                left++;
                continue;
            }

            if (!isVowel(rightChar)) {
                right--;
                continue;
            }

            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;

            left++;
            right--;
        }

        return new String(arr);
    }

    private boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u';
    }
}

```
    
### [680. Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/description/)

Given a string s, return true if the s can be palindrome after deleting at most one character from it.

#### Intuition
- If character does not match can we skip from right or left?
- let's assume first we will try to delete from left
- but if we don't find answer from left then we need to reset left and right; delete from right

```Java

class Solution {
    public boolean validPalindrome(String s) {
        
        int left = 0;
        int right = s.length() - 1;

        boolean leftSkip = false;
        int leftDeleted = -1;
        int rightPointerWhenLeftDeleted = -1;
        boolean rigthSkip = false;

        while(left< right){
            if(s.charAt(left) == s.charAt(right)){
                left++;
                right--;
            }else if(!leftSkip){
                leftSkip = true;
                leftDeleted = left;
                rightPointerWhenLeftDeleted = right;
                left++;
            }else if(!rigthSkip){
                rigthSkip = true;
                left = leftDeleted;
                right = rightPointerWhenLeftDeleted;
                right--;
            }else{
                return false;
            }
        }
        return true;
    }
}

```
### [917. Reverse Only Letters](https://leetcode.com/problems/reverse-only-letters/description/)

```Java
class Solution {
    public String reverseOnlyLetters(String s) {
        char temp[] = s.toCharArray();      
        int low = 0 , high = s.length()-1;
        while(low < high){
            if(!Character.isAlphabetic(temp[low]))  low++;
            else if(!Character.isAlphabetic(temp[high]))  high--;   
            else if(Character.isAlphabetic(temp[low]) && Character.isAlphabetic(temp[high])){
                char i = temp[low];temp[low] = temp[high];
                temp[high] = i;
                low++; high--;
            }
        }
        return String.valueOf(temp);
    }
}
```

### [27. Remove Element](https://leetcode.com/problems/remove-element/description/)

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
- Return k.

#### Intuition
- one pointer iterates over the array.
- second pointer keeps track of where to place the next element that is not equal to val.

```Java
class Solution {
    public int removeElement(int[] nums, int val) {
        int left=0;
        int right = 0;
        while(right < nums.length){
            if(nums[right]== val){
                left++;
            }else{
                nums[right-left] = nums[right];

            }
            right++;
        }
        return nums.length - left;
    }
}
```

### [75. Sort Colors](https://leetcode.com/problems/sort-colors/description/)
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

### Intuition
- Move 0 left side
- Move 2 right side
- After completing above operation, automatically all 1s will be placed in the centre

```Java
class Solution {
    public void sortColors(int[] nums) {
        int start = 0;
        int end = nums.length - 1;
        int i = 0;
        //this is tricky
        while( i<=end){
            if(nums[i] == 0){
                swap(start++, i,nums);
                i++;
            }else if (nums[i] == 1){

            i++;
            }
             else if(nums[i] == 2){
                 // Here we will not increase i because swapped element could be 2 on ith position
                swap(end--, i, nums);
            }
        }
    }

    public void swap(int i, int j,int[] nums){
        int temp = nums[i];
        nums[i]= nums[j];
        nums[j] =  temp;
    }
}
```

### [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)

#### Intuition)
- It can have negative number and it is sorted; how can we do in O(n)?
- Negative numbers in the array will become positive after squaring.
- The absolute value of negative numbers might be larger than positive numbers, so their squared values might be larger and need to be placed later in the sorted result.
- To handle this efficiently, we use two pointers: one starting at the beginning (left) and one at the end (right) of the array.

```Java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int n = nums.length;
        int left = 0;
        int right = n - 1;
        int[] ans = new int[n];
        int index = n - 1;

        while (left <= right) {
            int leftSquare = nums[left] * nums[left];
            int rightSquare = nums[right] * nums[right];

            if (leftSquare > rightSquare) {
                ans[index--] = leftSquare;
                left++;
            } else {
                ans[index--] = rightSquare;
                right--;
            }
        }

        return ans;
    }
}

```


### [905. Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/description/)
Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

**Order doesn't matter**
```Java
class Solution {
    public int[] sortArrayByParity(int[] nums) {
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            if (nums[left] % 2 == 0) {
                left++;
            } else if (nums[right] % 2 == 1) {
                right--;
            } else {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }
        
        return nums;
    }
}

```
### [922. Sort Array By Parity II](https://leetcode.com/problems/sort-array-by-parity-ii/description/)

#### Intuition
- 2 Pointers can be start from any place
- Here, we need odd and even pointer

```Java
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        int i = 0, j = 1;
        int n = nums.length;

        while (i < n && j < n) {
            while (i < n && nums[i] % 2 == 0) i += 2;
            while (j < n && nums[j] % 2 == 1) j += 2;

            if (i < n && j < n) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }
        }

        return nums;
    }
}

// TC: O(N), SC: O(1)
```

### [969. Pancake Sorting](https://leetcode.com/problems/pancake-sorting/description/)

# PENDING

### [2000. Reverse Prefix of Word](https://leetcode.com/problems/reverse-prefix-of-word/description/)

Given a 0-indexed string word and a character ch, reverse the segment of word that starts at index 0 and ends at the index of the first occurrence of ch (inclusive). If the character ch does not exist in word, do nothing.

- For example, if word = "abcdefd" and ch = "d", then you should reverse the segment that starts at 0 and ends at 3 (inclusive). The resulting string will be "dcbaefd".

Return the resulting string.

#### Intuition
- Find Index, it will be left=0 and right= index boundary
- Do Swapping
```Java
public class Solution {
    public String reversePrefix(String word, char ch) {
        // Add characters to the result in the original order
        char[] result = word.toCharArray();
        int left = 0;

        for (int right = 0; right < word.length(); right++) {
            // We found ch - reverse characters up to ch by swapping
            if (result[right] == ch) {
                while (left < right) {
                    swap(result, left, right);
                    left++;
                    right--;
                }
                return new String(result);
            }
        }
        return word;
    }

    private void swap(char[] characters, int index1, int index2) {
        char temp = characters[index2];
        characters[index2] = characters[index1];
        characters[index1] = temp;
    }
}
```

### [541. Reverse String II](https://leetcode.com/problems/reverse-string-ii/description/)

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

#### Intuition
- Simplify task first
- We have number k; We need to reverse k character among 2k character; menas we have k=5 then we will reverse 5 characters among 10 characters
- Then at one point we will not have enough characters in the string (<k character); then we will reverse those remaining characters

```Java
class Solution {
    public String reverseStr(String s, int k) {
        char[] chars = s.toCharArray();
        
        for (int i = 0; i < s.length() - 1; i += 2 * k) {
            int start = i;
            int end = Math.min(i + k - 1, s.length() - 1);
            
            while (start < end) {
                char temp = chars[start];
                chars[start++] = chars[end];
                chars[end--] = temp;
            }
        }
        
        return new String(chars);
    }
}

// TC: O(n), SC: O(n)
```

### [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)

#### Intuition
- get last string, 
- how can we do that? 
- remove extra space
- Two pointers, left and right, are initialized. right starts from the end of the string and left will be used to track the beginning of each word as we traverse backward.
```Java
class Solution {
    public String reverseWords(String s) {
        s = s.trim();
        int left = 0;int n = s.length();
        int right = n-1;
        
        char[] chars = s.toCharArray();
        StringBuilder ans  = new StringBuilder();
        while(right>=0){
            while(right>=0&&chars[right]==' '){
                right--;
            }
            if(right<0) break;
             left = right;
            while(left>=0&&chars[left]!=' '){
                left--;
            }
            ans.append(s,left+1,right+1);
            ans.append(" ");
        right = left;
        }
        
        return ans.toString().trim();
    }
}
```

### [557. Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/description/)

#### Intuition
- move end pointer till char is empty or end of string
- once we get that point, need to reverse string from start to end position

```Java
class Solution {
    public String reverseWords(String s) {
        char[] c = s.toCharArray();
        int start = 0;
        int end = 0;

        while (end < c.length) {
            if (c[end] == ' ') {
                reverseWord(c, start, end - 1);
                start = end + 1;
            }
            end++;
        }
        
        reverseWord(c, start, end - 1);
        
        return new String(c);
    }
    
    private void reverseWord(char[] c, int start, int end) {
        while (start < end) {
            char temp = c[start];
            c[start++] = c[end];
            c[end--] = temp;
        }
    }
}

```

## Others

### [948. Bag of Tokens](https://leetcode.com/problems/bag-of-tokens/description/)

#### Intuition
- **Two Operations:** The method utilizes two operations, gaining a score by playing tokens face-up and losing a score to regain power by playing tokens face-down.
- **Initial Focus on Face-Up:** The algorithm prioritizes playing tokens face-up first since at least one score is needed to perform face-down operations.
- **Using Sorted Array:** The sorted array allows for a strategic approach where the smallest tokens can be played first to maximize score, while still keeping larger tokens available for potential face-down operations.
- **Check Remaining Token:** After exiting the main loop, the last token is checked if it can be played face-up to gain an additional score.

```Java
class Solution {
    public int bagOfTokensScore(int[] tokens, int power) {
        if(tokens.length == 0){
            return 0;
        }
        Arrays.sort(tokens);

        int i=0;
        int j = tokens.length - 1;
        int score = 0;
        while(i<j){
            if(tokens[i]<= power){
                power -= tokens[i++];
                score++;
            }else{
                if(score > 0){
                    power+= tokens[j];
                    score--;
                }
                j--;
            }
        }

        if(tokens[i]<= power){
                score++;
        }

        return score;
    }
}
```

### [942. DI String Match](https://leetcode.com/problems/di-string-match/description/)
A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where:

s[i] == 'I' if perm[i] < perm[i + 1], and
s[i] == 'D' if perm[i] > perm[i + 1].
Given a string s, reconstruct the permutation perm and return it. If there are multiple valid permutations perm, return any of them.

#### Intuition
- We will have range of number from 0 to s.length()
- when we have I, pick smaller
- when we have D, pick largest

```Java
class Solution {
    public int[] diStringMatch(String s) {
        int start = 0;
        int end = s.length();
        int[] ans = new int[end+1];
        
        for(int i=0;i< s.length();i++){
            if(s.charAt(i)=='I'){
                ans[i] = start++;
            }else{
                ans[i] = end--;
            }
        }
         ans[s.length()] = start;
         return ans;
    }
}
```

### [1750. Minimum Length of String After Deleting Similar Ends](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/description/)

Given a string s consisting only of characters 'a', 'b', and 'c'. You are asked to apply the following algorithm on the string any number of times:

1) Pick a non-empty prefix from the string s where all the characters in the prefix are equal.
2) Pick a non-empty suffix from the string s where all the characters in this suffix are equal.
3) The prefix and the suffix should not intersect at any index.
4) The characters from the prefix and suffix must be the same.
5) Delete both the prefix and the suffix.
Return the minimum length of s after performing the above operation any number of times (possibly zero times).

#### Intuition
- If we have same character in prefix and suffix then skip that
- count does not matter.. character needs to be same

```Java
class Solution {
    public int minimumLength(String s) {
        int i = 0;
        int j = s.length() - 1;

        while (i < j && s.charAt(i) == s.charAt(j)) {
            char currentChar = s.charAt(i);

            while (i <= j && s.charAt(i) == currentChar) {
                i++;
            }

            while (i <= j && s.charAt(j) == currentChar) {
                j--;
            }
        }

        return j - i + 1;
    }
}

```

### [1813. Sentence Similarity III](https://leetcode.com/problems/sentence-similarity-iii/description/)

### Intuition
- Compare front elements and move pointer till they match
- Compare back elements and move pointer till they match
- If one of the string is empty then we can say second string has additional words

```Java
class Solution {
    public boolean areSentencesSimilar(String sentence1, String sentence2) {
        if(sentence1.length()==sentence2.length()){
            if(sentence1.equals(sentence2)) return true;
            else return false;
        }
        
        String[] arr1 = sentence1.split(" ");
        String[] arr2 = sentence2.split(" ");
        
        int l1 = arr1.length;  // l1 = length of the 1st array arr1.
        int l2 = arr2.length;  // l2 = length of the 2st array arr2.
        
        int f1 =0, f2 =0;        // f1 and f2 are the front of the array arr1 and arr2;
        int b1 =l1-1, b2 = l2-1; // b1 and b2 are the back of the array arr1 and arr2;
        
        // If the front element of both array are equal we delete them and increment the front.
        while(l1!=0 && l2!=0 && arr1[f1].equals(arr2[f2])){
            l1--;
            l2--;
            f1++;
            f2++;
        }
        
        // If the back element of both array are equal we delete them and decrement the back.
        while(l1!=0 && l2!=0 && arr1[b1].equals(arr2[b2])){
            l1--;
            l2--;
            b1--;
            b2--;
        }
        
        return l1==0 || l2==0;  
    }
}

```

### [658. Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/description/)
#PENDING

### [821. Shortest Distance to a Character](https://leetcode.com/problems/shortest-distance-to-a-character/description/)

#### Intuition
- Can we initialize start and end pointer from 0th position and move end pointer till character found
- then update all start to end position and keep prev character position as well and update minimum one
- after entire loop, process remaining elements

```Java
class Solution {
    public int[] shortestToChar(String s, char c) {
        int n = s.length();
        int[] result = new int[n];
        int prevMatchPosition = Integer.MAX_VALUE;
        int start = 0;
        int end = 0;
        
        while (end < n) {
            if (s.charAt(end) == c) {
                for (int i = start; i <= end; i++) {
                    result[i] = Math.min(Math.abs(i-prevMatchPosition), Math.abs(i - end));
                }
                prevMatchPosition = end;
                start = end + 1;
            }
            end++;
        }

        for (int i = start; i < end; i++) {
            result[i] = Math.abs(i-prevMatchPosition);
        }

        return result;
    }
}

```

# Slow & Fast Pointers

### Template (Slow & Fast)
```Java
class Solution {
    template(int[] arr){
        int left = 0;
        int right = 0;
        // right will reach to the end first
        while(right< arr.length){
            // computation
            // both chnaged in different condition
            if(someCondition()){
                left++;
            }

            if(someCondition()){
                right--;
            }
        }
    }

}
```

## Linked List Operations

**Below linked list problem will be covered in Linked list Notes**
### [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)
### [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
### [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)
### [61. Rotate List](https://leetcode.com/problems/rotate-list/description/)
### [143. Reorder List](https://leetcode.com/problems/reorder-list/description/)
### [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/)
### [82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)

## Cyclic Detection
###[457. Circular Array Loop](https://leetcode.com/problems/circular-array-loop/description/)
# PENDING

## Sliding Window/Caterpillar Method
### [795. Number of Subarrays with Bounded Maximum](https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/description/)


#### Intuition
- Count subarray, It should have only one number which is in given range
- add count in all iteration

```Java
class Solution {
    public int numSubarrayBoundedMax(int[] nums, int left, int right) {
        
        int i=0;
        int j=0;
        int ans = 0;
        int count = 0;
        while(j< nums.length){
            // valid case
            if(nums[j] >= left && nums[j]<= right){
               count = j - i + 1;
            }else if(nums[j] > right){
                // reset count
                count = 0;
                i = j+1;
            }
            ans += count;
            j++;
        }

      
        return ans;
    }
}
```
###[1040. Moving Stones Until Consecutive II](https://leetcode.com/problems/moving-stones-until-consecutive-ii/description/)

# PENDING

### [1782. Count Pairs Of Nodes](https://leetcode.com/problems/count-pairs-of-nodes/description/)

# PENDING

###[696. Count Binary Substrings](https://leetcode.com/problems/count-binary-substrings/description/)

#### Intuition
We can convert the string s into an array groups that represents the length of same-character contiguous blocks within the string. For example, if s = "110001111000000", then groups = [2, 3, 4, 6].

For every binary string of the form '0' * k + '1' * k or '1' * k + '0' * k, the middle of this string must occur between two groups.

Let's try to count the number of valid binary strings between groups[i] and groups[i+1]. If we have groups[i] = 2, groups[i+1] = 3, then it represents either "00111" or "11000". We clearly can make min(groups[i], groups[i+1]) valid binary strings within this string. Because the binary digits to the left or right of this string must change at the boundary, our answer can never be larger.

```Java
class Solution {
    public int countBinarySubstrings(String s) {
        int ans = 0;
        int prevGroupLength = 0;
        int currGroupLength = 1;

        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) {
                currGroupLength++;
            } else {
                ans += Math.min(prevGroupLength, currGroupLength);
                prevGroupLength = currGroupLength;
                currGroupLength = 1;
            }
        }
        
        ans += Math.min(prevGroupLength, currGroupLength);

        return ans;
    }
}

```

###[532. K-diff Pairs in an Array](https://leetcode.com/problems/k-diff-pairs-in-an-array/description/)
To start I think its easier to look at, what IS NOT a valid answer.

If the left pointer has caught up to our right pointer. This is between two different values so if left == right, this will never be a valid answer.
1) If we have previously used this value to accurately determine that two values compute a valid answer.
2) For this problem I used a previous variable and set it whenever we find a value where nums[r] - nums[l] == k. This stops any sort of duplicates from happening.
3) As mentioned earlier we must also check that nums[r]-nums[l] == k. We use the while loop to get as close as possible for each iteration but we need the final if statement to check accuracy.

```Java
class Solution {
    public int findPairs(int[] nums, int k) {
        if (nums == null || nums.length < 1) return 0;
        
        Arrays.sort(nums);
        int left = 0, pairCount = 0, previous = Integer.MAX_VALUE;
        
        for (int right = 1; right < nums.length; right++) {
            // Move the left pointer to maintain the difference <= k
            while (left < right && nums[right] - nums[left] > k) {
                left++;
            }
            
            // Check for valid pair
            if (left != right && previous != nums[left] && nums[right] - nums[left] == k) {
                pairCount++;
                previous = nums[left]; // Mark this number as used
            }
        }
        
        return pairCount;
    }
}

```

## Rotation
###[1861. Rotating the Box](https://leetcode.com/problems/rotating-the-box/description/)

# PENDING

###[189. Rotate Array](https://leetcode.com/problems/rotate-array/description/)

#### Intuition
- Make sure k is within range
- Reverse entire array
- Reverse 0 to k array length
- Reverse k to array length

```Java
class Solution {
    
    public void rotate(int[] nums, int k) {
        // Ensure k is within array bounds
        k %= nums.length;
        // Reverse entire array
        reverse(nums, 0, nums.length - 1);
        // Reverse first k elements
        reverse(nums, 0, k - 1);
        // Reverse remaining elements
        reverse(nums, k, nums.length - 1);
    }
    
    public static void reverse(int nums[], int start, int end){
    while(start < end){
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
}
```

## String
###[443. String Compression](https://leetcode.com/problems/string-compression/description/)

#### Intuition
- Here we are using two pointers, one for iterating through the original character array and one for keeping track of the current position in the compressed array. The two pointer variables used are i and ans.
- Now also use a variable to keep track of the count of consecutive characters.
- First set the current letter to the first character in the array and initializes the count to 0.
- Then iterate through the array until you find a different character or reach the end of the array.
- For each iteration, increment the count and the index i.

```Java
class Solution {
    public int compress(char[] chars) {
        int i = 0, k = 0;
        
        while (i < chars.length) {
            int j = i;
            
            while (j < chars.length && chars[i] == chars[j]) {
                j++;
            }
            
            chars[k++] = chars[i];
            
            int count = j - i;
            if (count > 1) {
                String countStr = Integer.toString(count);
                for (char c : countStr.toCharArray()) {
                    chars[k++] = c;
                }
            }
            
            i = j;
        }
        
        return k;
    }
}

```

### [1163. Last Substring in Lexicographical Order](https://leetcode.com/problems/last-substring-in-lexicographical-order/description/)

# PENDING

## Remove Duplicate

###[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        int prev = nums[0];
        int count =0;
        for(int i=1; i< nums.length;i++){
            if(prev== nums[i]){
                count++;
            }else{
                nums[i-count] = nums[i];
                prev = nums[i];
            }
        }
        return nums.length - count;
    }
}
```

### [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/)

#### Intuition
- The solution approach involves iterating through the input array nums and maintaining two pointers, index and occurrence. The index pointer represents the length of the modified array, and the occurrence pointer tracks the number of occurrences of the current element.
- Initialize index to 1 (for the first element) and occurrence to 1.
- Iterate through the array, starting from index 1.
- If the current element is equal to the previous one, increment occurrence.
- If not, reset occurrence to 1.
- If occurrence is less than or equal to 2, update nums[index] with the current element and increment index.
- Continue until the end of the array.

```Java
class Solution {
    public int removeDuplicates(int[] nums) {

        int index = 1;
        int occurance = 1;

        for(int i=1; i < nums.length; i++){
            if (nums[i] == nums[i-1]){
                occurance++;
            }else{
                occurance = 1;
            }

            if (occurance <= 2){
                nums[index] = nums[i];
                index++;
            }
        }  

        return index;
    
    }
}
```

###[1089. Duplicate Zeros](https://leetcode.com/problems/duplicate-zeros/description/)
****Intuition
1) Count zeros: We loop through the array to count the number of zeros (zeroCount).
2) Shift elements: 
   - Start from the last element and try to place it in the correct position (i + zeroCount).
   - If the element is zero, we duplicate it by placing another zero at the next position.
3) Handle in-place modifications: Since we are shifting elements in-place, we make sure that we don’t go beyond the array’s length.
```Java
class Solution {
    public void duplicateZeros(int[] arr) {
        int zeroCount = 0;
        int length = arr.length;

        // Count the number of zeros
        for (int num : arr) {
            if (num == 0) {
                zeroCount++;
            }
        }

        // Start shifting from the end
        for (int i = length - 1; i >= 0; i--) {
            if (i + zeroCount < length) {
                arr[i + zeroCount] = arr[i];
            }

            // add one more zero
            if (arr[i] == 0) {
                zeroCount--;
                if (i + zeroCount < length) {
                    arr[i + zeroCount] = 0;
                }
            }
        }
    }
}

```

## Others (Slow & Fast Pointers)

###[1093. Statistics from a Large Sample](https://leetcode.com/problems/statistics-from-a-large-sample/description/)

# PENDING

### [763. Partition Labels](https://leetcode.com/problems/partition-labels/description/)

# PENDING

### [481. Magical String](https://leetcode.com/problems/magical-string/description/)

# PENDING

### [825. Friends Of Appropriate Ages](https://leetcode.com/problems/friends-of-appropriate-ages/description/)

# PENDING

### [845. Longest Mountain in Array](https://leetcode.com/problems/longest-mountain-in-array/description/)

# PENDING

### [1574. Shortest Subarray to be Removed to Make Array Sorted](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/description/)

# PENDING