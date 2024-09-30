# Bit Manipulation

# Table of Contents

1. [Bit Manipulation](#bit-manipulation)
    - [Operators](#operators)
        - AND (&)
        - OR (|)
        - XOR (^)
        - NOT (~)
        - Left Shift (<<)
        - Right Shift (>>)
        - Unsigned Right Shift (>>>)
2. [Important Bit Manipulation Operations](#important-bit-manipulation-operations)
    - [Check if the i-th bit is set](#1-check-if-the-i-th-bit-is-set)
    - [Set the i-th bit of a number](#2-set-the-i-th-bit-of-a-number)
    - [Clear the i-th bit of a number](#3-clear-the-i-th-bit-of-a-number)
    - [Remove the last set bit of a number](#4-remove-the-last-set-bit-of-a-number)
    - [Find the position of the rightmost set bit](#5-find-the-position-of-the-rightmost-set-bit)
    - [Toggle the i-th bit of a number](#6-toggle-the-i-th-bit-of-a-number)
3. [Problems](#problems)
    - [Check if number is power of 4](#2-check-if-number-is-power-of-4)
    - [Check if number is power of 8](#3-check-if-number-is-power-of-8)
    - [Check if number is power of 16](#4-check-if-number-is-power-of-16)
    - [Check if number is power of 32](#5-check-if-number-is-power-of-32)
    - [Count Number of set bits in a number](#6-count-number-of-set-bits-in-a-number)
    - [Single Number](#7-single-number)
    - [Single Number II](#8-single-number-ii)
    - [Single Number III](#9-single-number-iii)
    - [Convert uppercase to lowercase](#10-convert-uppercase-to-lowercase)
    - [Convert lowercase to uppercase](#11-convert-lowercase-to-uppercase)
    - [Invert alphabets case](#12-invert-alphabets-case)
    - [Find letter position in alphabet](#13-find-letter-position-in-alphabet)
    - [Swap two numbers without temp variable](#14-swap-two-numbers-without-temp-variable)
    - [Calculate XOR from 1 to n](#15-calculate-xor-from-1-to-n)
    - [Find XOR from the range L-R](#15b-find-xor-from-the-range-lr)
    - [Find XOR of all subset of array](#16-find-xor-of-all-subset-of-array)
    - [Count number of bits to be flipped to convert A to B](#17-count-number-of-bits-to-be-flipped-to-convert-a-to-b)
    - [Finding missing number in array](#18-finding-missing-number-in-array)
    - [Print the binary representation of decimal number](#19-print-the-binary-representation-of-decimal-number)
    - [Reverse the bits of a number](#20-reverse-the-bits-of-a-number)
    - [Swap the ith and jth bit](#21-swap-the-ith-and-jth-bit)
    - [Swap all even and odd bits](#22-swap-all-even-and-odd-bits)
    - [Copy set bits in a range (Toggle set bits in a range)](#23-copy-set-bits-in-a-range-toggle-set-bits-in-a-range)
    - [Divide two integers without using multiplication, division and mod operator](#24-divide-two-integers-without-using-multiplication-division-and-mod-operator)
    - [Reduce a number to 1](#25-reduce-a-number-to-1)
    - [Detect if two integers have opposite sign](#26-detect-if-two-integers-have-opposite-sign)
    - [Add 1 to an integer](#27-add-1-to-an-integer)
    - [Find XOR of a number without using XOR operator](#28-find-xor-of-a-number-without-using-xor-operator)
    - [Determine if two integers are equal without using comparison and arithmetic operators](#29-determine-if-two-integers-are-equal-without-using-comparison-and-arithmetic-operators)
    - [Find minimum or maximum of two integers without using branching](#30-find-minimum-or-maximum-of-two-integers-without-using-branching)
4. [Leetcode Problems](#leetcode-problems)
    - [Find Missing and Repeating Number / Set Mismatch](#1-find-missing-and-repeating-number--set-mismatch)
    - [Maximum Product of Word Lengths (Amazon, Google)](#2-maximum-product-of-word-lengths-amazon-google)
    - [Concatenation of Consecutive Binary Numbers](#3-concatenation-of-consecutive-binary-numbers)
    - [Check If a String Contains All Binary Codes of Size K](#4-check-if-a-string-contains-all-binary-codes-of-size-k)
    - [Find the Duplicate Number](#5-find-the-duplicate-number)

### Operators

1. **AND (`&`)**: Compares each bit of two numbers; results in `1` if both bits are `1`, otherwise `0`.
2. **OR (`|`)**: Compares each bit of two numbers; results in `1` if at least one bit is `1`, otherwise `0`.
3. **XOR (`^`)**: Compares each bit of two numbers; results in `1` if the bits are different, otherwise `0`.
4. **NOT (`~`)**:
   - The `NOT` operator flips (inverts) each bit of a number. It changes every `1` to `0` and every `0` to `1`.
   - This process is also referred to as **1's complement**.

    **1's Complement**:
   - 1's complement is the process of inverting all the bits of a number.
   - In binary, `1` becomes `0`, and `0` becomes `1`.

    ```
    Example:  
    Let’s take the number `5` as an example:
    - `5` in binary (32 bits): `0000 0000 0000 0000 0000 0000 0000 0101`
    - Applying `~5` (1's complement of `5`):  
      Flip all bits → `1111 1111 1111 1111 1111 1111 1111 1010`
    - In a signed 32-bit integer system, 
      this binary representation equals `-6`.
    
    So, `~5 = -6` in 1's complement form when considering signed integers.
    ```


2's Complement:
  - **2's complement** is the standard method used by computers to represent negative numbers.
  - To get the 2's complement of a number, take its 1's complement (invert all bits), then add `1` to the result.

```
Example (2's complement):  
For the number `5`:
- Step 1: Start with `5` in binary: `0000 0000 0000 0000 0000 0000 0000 0101`
- Step 2: Invert the bits (1's complement): `1111 1111 1111 1111 1111 1111 1111 1010`
- Step 3: Add `1`:  
  `1111 1111 1111 1111 1111 1111 1111 1010` + `1` → `1111 1111 1111 1111 1111 1111 1111 1011`
- Result: This represents `-5` in 2's complement form.

Negative number example:  
For `-5`, computers store it as its 2's complement:
- `-5` in binary (2's complement): `1111 1111 1111 1111 1111 1111 1111 1011`
- To verify, invert the bits to get `1's complement` (`0000 0000 0000 0000 0000 0000 0000 0100`) and add `1` → `0000 0000 0000 0000 0000 0000 0000 0101`, which equals `5`.
```

**Integer Range in 32-bit Systems**:
- In a **32-bit signed integer** system, numbers are represented using 32 bits. The range is:
    - Minimum: `-2^31 = -2147483648`
    - Maximum: `2^31 - 1 = 2147483647`

- The most significant bit (leftmost) is the sign bit:
    - `0` indicates a positive number.
    - `1` indicates a negative number.

For example:
- `5` in binary: `0000 0000 0000 0000 0000 0000 0000 0101`
- `-5` in 2's complement binary: `1111 1111 1111 1111 1111 1111 1111 1011`

**Unsigned Integers**:
- In an **unsigned integer** system, all bits represent the magnitude of the number, so there is no sign bit, and the range is different.
- In a **32-bit unsigned integer** system, the range is:
    - Minimum: `0`
    - Maximum: `2^32 - 1 = 4294967295`

When you apply the `NOT (~)` operator to an unsigned integer, it still inverts all the bits, but the result will always be interpreted as a positive number within the unsigned range.

```
Example (unsigned):  
For `x = 5`:
- `5` in binary: `0000 0000 0000 0000 0000 0000 0000 0101`
- `~5` (NOT 5):  
  Flip all bits → `1111 1111 1111 1111 1111 1111 1111 1010`
- In an **unsigned 32-bit integer** system, `1111 1111 1111 1111 1111 1111 1111 1010` equals `4294967290`.

Thus, for unsigned integers:
- `~5` becomes `4294967290`, which is still a valid positive number in the unsigned integer range.
```

5. **Left Shift (`<<`)**:
   - The **left shift** operator shifts the bits of the number to the left by a specified number of positions. Zeros are added to the right.
   - Effectively, a left shift **multiplies the number by `2` for each shift.**
    
    ```
    Example:  
    If `x = 3` (binary: `0000 0011`), 
   then `x << 2 = 12` (binary: `0000 1100`), because `3 * 2^2 = 12`.
    ```

6. **Right Shift (`>>`)**:
   - The **right shift** operator shifts the bits of the number to the right by a specified number of positions. The sign bit (most significant bit) is used to fill the leftmost positions (for negative numbers, this ensures the sign is preserved).
   - This is an **arithmetic shift** and divides the number by `2` for each shift.
    ```
    Example:  
    If `x = 8` (binary: `0000 1000`), 
   then `x >> 2 = 2` (binary: `0000 0010`), because `8 / 2^2 = 2`.

    For negative numbers:  
    If `x = -8` (binary: `1111 1000` in two's complement), 
   then `x >> 2 = -2` (binary: `1111 1110`).
    ```
   
7. **Unsigned Right Shift (`>>>`)**:
   - The **unsigned right shift** operator shifts bits to the right, and zeros are added to the left, **ignoring the sign** of the number.
   - It is a **logical shift** and works differently for negative numbers because it doesn't preserve the sign bit.

    ```
    Example:  
    If `x = 8` (binary: `0000 1000`), 
   then `x >>> 2 = 2` (binary: `0000 0010`), 
   which is the same as the arithmetic shift for positive numbers.
    
    For negative numbers:  
    If `x = -8` (binary: `1111 1000`), 
   then `x >>> 2 = 1073741822` (binary: `0011 1111 1111 1111 1111 1111 1111 1110`), 
   because zeros are filled on the left, resulting in a large positive number.
    ```

## Important Bit Manipulation Operations

### 1. **Check if the i-th bit is set**:
- To check if the i-th bit is set (i.e., if it is `1`), we use a **bitwise AND** operation.

**Intuition**: 
  - Create a mask by left-shifting `1` by `i` positions and then perform an AND operation with the number. If the result is not `0`, then the i-th bit is set.

**Formula**:  
(number & (1 << i)) != 0

**Example**:  
For `number = 5` (binary: `0101`) and `i = 2`:
- Create the mask by shifting `1`: `1 << 2` → `0100`
- Perform AND: `0101 & 0100 = 0100`, which is not `0`. So, the 2nd bit is set.


```Java
public class BitManipulation {
  public static boolean isBitSet(int number, int i) {
      return (number & (1 << i)) != 0;
  }

  public static void main(String[] args) {
      int number = 5;  // binary: 0101
      int i = 2;
      System.out.println(isBitSet(number, i));  // Output: true
  }
}
```

### 2. **Set the i-th bit of a number:**
- To set the i-th bit to 1, we use the **bitwise OR** operation.

**Intuition**:
- Create a mask by left-shifting `1` by `i` positions and then perform an OR operation with the number. This guarantees that the i-th bit becomes `1`.

**Formula**:  
number | (1 << i)

**Example**:  
For `number = 5` (binary: `0101`) and `i = 1`:
- Create the mask by shifting `1`: `1 << 1` → `0010`
- Perform OR: `0101 | 0010 = 0111` (now the 1st bit is set).

```Java
public class BitManipulation {
    public static int setBit(int number, int i) {
        return number | (1 << i);
    }

    public static void main(String[] args) {
        int number = 5;  // binary: 0101
        int i = 1;
        System.out.println(setBit(number, i));  // Output: 7 (binary: 0111)
    }
}

```

### 3. **Clear the i-th bit of a number**:
- To clear (turn to `0`) the i-th bit of a number, we use a **bitwise AND** operation with the **negation** of a mask.

**Intuition**:
- Create a mask by left-shifting `1` by `i` positions, invert the mask, and then perform an AND operation. This ensures the i-th bit is cleared, while other bits remain unchanged.

**Formula**:  
number & ~(1 << i)

**Example**:  
For `number = 5` (binary: `0101`) and `i = 2`:
- Create the mask: `1 << 2` → `0100`
- Invert the mask: `~0100` → `1011`
- Perform AND: `0101 & 1011 = 0001` (the 2nd bit is cleared).

```Java
public class BitManipulation {
    public static int clearBit(int number, int i) {
        return number & ~(1 << i);
    }

    public static void main(String[] args) {
        int number = 5;  // binary: 0101
        int i = 2;
        System.out.println(clearBit(number, i));  // Output: 1 (binary: 0001)
    }
}

```

### 4. **Remove the last set bit of a number**:
-  To remove the last set bit (i.e., the rightmost `1`), we use the expression `number & (number - 1)`.

**Intuition**:
- Subtracting `1` from the number flips all bits after the rightmost `1`. Performing an AND operation with the original number clears the rightmost set bit.

**Formula**:  
number & (number - 1)

For `number = 12` (binary: `1100`):
- `number - 1 = 11` → `1011`
- Perform AND: `1100 & 1011 = 1000` (the last set bit is removed, leaving only the 4th bit).

```Java
public class BitManipulation {
    public static int removeLastSetBit(int number) {
        return number & (number - 1);
    }

    public static void main(String[] args) {
        int number = 12;  // binary: 1100
        System.out.println(removeLastSetBit(number));  // Output: 8 (binary: 1000)
    }
}

```

### 5. **Find the position of the rightmost set bit**:
- To find the position of the rightmost set bit (i.e., the least significant `1`)

**Formula**:  
(number & ~(number - 1))


**Example**:  
```
For n = 6:
Binary representation: 0110
n - 1: 0101
~(n - 1): 1010
n & ~(n - 1): 0110 & 1010 = 0010 (which is 2, position of right most set bit)
```

```Java
public class BitManipulation {
    public static int findRightmostSetBit(int number) {
        return number & ~(number -1);
    }

    public static void main(String[] args) {
        int number = 10;  // binary: 1010
        System.out.println(findRightmostSetBit(number));  // Output: 2 (binary: 0010)
    }
}

```


### 6. **Toggle the i-th bit of a number**:
- To toggle the i-th bit (i.e., flip it from 0 to 1 or from 1 to 0), we use the expression number ^ (1 << i).

**Intuition**:
- By left-shifting 1 by i positions, we create a mask that has only the i-th bit set to 1 and all other bits set to 0.
- The XOR operation will flip the i-th bit of the number. If the i-th bit is 1, it will become 0, and if it is 0, it will become 1.

**Formula**:  
number ^ (1 << i)

**Example:**
Example:
For number = 12 (binary: 1100) and i = 2:
- Create the mask: 1 << 2 → 0000 0100 (binary representation of 4).
- Perform XOR: 1100 ^ 0100 = 1000 (binary), which equals 8 in decimal.

```Java
public class BitManipulation {
    public static int toggleIthBit(int number, int i) {
        return number ^ (1 << i);
    }

    public static void main(String[] args) {
        int number = 12;  // binary: 1100
        int i = 2;
        System.out.println(toggleIthBit(number, i));  // Output: 8 (binary: 1000)

        // Additional example: toggling the same bit again
        System.out.println(toggleIthBit(toggleIthBit(number, i), i));  // Output: 12 (original number)
    }
}

```

### Problems:
#### 1) Find whether number is even or odd

**Intuition:**
- If first bit is set then number is odd otherwise even
- Use check ith(1st) set bit formula 

```Java
public class EvenOddCheck {
    public static boolean isEven(int number) {
        return (number & 1) == 0; // If LSB is 0, the number is even
    }

    public static void main(String[] args) {
        int number1 = 4;  // Even
        int number2 = 7;  // Odd

        System.out.println(number1 + " is even: " + isEven(number1)); // Output: true
        System.out.println(number2 + " is even: " + isEven(number2)); // Output: false
    }
}

```

**Another approach:**

**Intuition:**
- If we shift right first and then shift left then number remain same then even, otherwise odd

```Java
public class EvenOddCheck {
    public static boolean isEven(int number) {
        int shiftedRight = number >> 1;  // Shift right by 1 bit
        int shiftedLeft = shiftedRight << 1;  // Shift back left by 1 bit
        return shiftedLeft == number;  // If the number remains the same, it's even
    }

    public static void main(String[] args) {
        int number1 = 4;  // Even
        int number2 = 7;  // Odd

        System.out.println(number1 + " is even: " + isEven(number1)); // Output: true
        System.out.println(number2 + " is even: " + isEven(number2)); // Output: false
    }
}

```

#### 2) Check if number is power of 2

**Intuition:**
- In power of 2 only one element will be set (ex: 10 or 100 or 1000)
- If we remove that element then number should be 0
- Can we aply remove last set bit of number algo here?
- N & (N-1) == 0

```Java
public class PowerOfTwoCheck {
    public static boolean isPowerOfTwo(int number) {
        return number > 0 && (number & (number - 1)) == 0;
    }

    public static void main(String[] args) {
        int number1 = 8;  // Power of 2
        int number2 = 10; // Not a power of 2

        System.out.println(number1 + " is power of 2: " + isPowerOfTwo(number1)); // Output: true
        System.out.println(number2 + " is power of 2: " + isPowerOfTwo(number2)); // Output: false
    }
}
```

#### 2) Check if number is power of 4

**Intuition:**
- In power of 4 only one element will be set (ex: 100 or 10000)
- It it is power of 4 then it should be power of 2 first!!
- This thought is slightly tricky: another thing we can do number % 3 == 1 [We can leverage the fact that powers of 4 have the binary representation of a single 1 bit in even positions (0-indexed). Additionally, another way to check if a number is a power of 4 is to see if 𝑛 % 3 == 1]
- let's combine together: power of 2 && (number % 3 == 1)

```Java
public class PowerOfFourCheck {
    public static boolean isPowerOfFour(int number) {
        // Check if the number is a power of 2 and if number % 3 == 1
        return number > 0 && (number & (number - 1)) == 0 && (number % 3 == 1);
    }

    public static void main(String[] args) {
        int number1 = 16;  // Power of 4 (4^2)
        int number2 = 8;   // Not a power of 4
        int number3 = 64;  // Power of 4 (4^3)

        System.out.println(number1 + " is power of 4: " + isPowerOfFour(number1)); // Output: true
        System.out.println(number2 + " is power of 4: " + isPowerOfFour(number2)); // Output: false
        System.out.println(number3 + " is power of 4: " + isPowerOfFour(number3)); // Output: true
    }
}

```

**Similarly we can do power of 8, 16, 32 with slight change**

#### 3) Check if number is power of 8
number > 0 && (number & (number - 1)) == 0 && (number % 7 == 1);

#### 4) Check if number is power of 16
number > 0 && (number & (number - 1)) == 0 && (number % 15 == 1);

#### 5) Check if number is power of 32
number > 0 && (number & (number - 1)) == 0 && (number % 31 == 1);

#### 6) Count Number of set bits in a number

**Approach: 1**
- iterate until n!=0 and shift right number AND
- check last bit is set or not

```Java
public class BitManipulation {
    public static int countSetBits(int number) {
        int count = 0;
        while (number != 0) {
            count += (number & 1); // Increment if last bit is set
            number >>= 1; // Right shift to check the next bit
        }
        return count;
    }

    public static void main(String[] args) {
        int number = 12;  // binary: 1100
        System.out.println(countSetBits(number));  // Output: 2
    }
}
```

#### Brian Kernighan's Algorithm
**Approach: 2**
- clear right most set bit until number is 0
- For each iteration, increment the count of set bits.

```Java
public class BitManipulation {
    public static int countSetBits(int number) {
        int count = 0;
        while (number != 0) {
            number &= (number - 1); // Clear the rightmost set bit
            count++; // Increment the count
        }
        return count;
    }

    public static void main(String[] args) {
        int number = 12;  // binary: 1100
        System.out.println(countSetBits(number));  // Output: 2
    }
}

```

#### 7) Single Number

**Problem:**

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

**Intuition:**
- How can I find elements in O(n) time complexity?
- **every element appears twice except for one**
- Can we use xor operation to remove duplicate?

```Java
class Solution {
    public int singleNumber(int[] nums) {
        int xor =0;
        for(int n: nums){
            xor^= n;
        }
        return xor;
    }
}
```

#### 8) Single Number II

**Problem:**

Given an integer array nums where every element appears three times except for one, which appears exactly once. Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.

**Intuition:**
- Can we use bit manipulation?
- Can we do bit count? if you look at each bit position individually, you know that if the number appears three times, then the total sum of bits at that position should be divisible by 3.
- If a bit appears in the single number but not in others, the total count of bits at that position will not be divisible by 3.
- By counting the occurrences of each bit and applying modulo 3, we can figure out the bits that belong to the single number that doesn't follow the "appearing three times" rule.

**Example:**

2 = 0010

2 = 0010

3 = 0011

2 = 0010
    
    
Bit count:
0th position: 1 count
1st position: 4 count
2nd position: 0 count
3rd position: 0 count


on 0th and 1st position we have additional ones, so answer is 0011

**Steps:**
- iterate 0 to 31 bit
- extract ith bit and add into sum
- once we iterate all the number then we will find modulo by 3 and if we have additional one then we will set in answer

```Java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;

        // Iterate over every bit position (0 to 31)
        for (int i = 0; i < 32; i++) {
            int bitSum = 0;

            // Count how many numbers have the i-th bit set
            for (int num : nums) {
                bitSum += (num >> i) & 1;  // Extract the i-th bit
            }

            // If the sum of bits at this position is not divisible by 3,
            // then the single number has a '1' at this bit position.
            if (bitSum % 3 != 0) {
                result |= (1 << i);  // Set the i-th bit in the result
            }
        }

        return result;
    }
}
```


#### 9) Single Number III

**Problem:**

Given an integer array nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in any order.

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.

 **Intuition:**
- Exactly two elements appear only once, and all the other elements appear exactly twice — how should we approach this?
- Can we use xor operation?
- If we do, we will get the result of num1 ^ num2, which is the XOR of the two unique numbers.
- What does this number suggest? This result has set bits wherever the two numbers differ.
- If we know, for example, that the 2nd bit is different, can we split the numbers into two groups — one where the 2nd bit is set, and one where it is unset?
- In each group, the duplicate elements will cancel each other out (due to XOR), leaving only one element in each group.

```Java
class Solution {
    public int[] singleNumber(int[] nums) {
        // Step 1: XOR all numbers. This will give us num1 ^ num2
        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }

        // Step 2: Find the rightmost set bit in the XOR result
        int rightmostSetBit = xor & -xor;  // This isolates the rightmost set bit

        // Step 3: Split numbers into two groups and XOR within each group
        int num1 = 0, num2 = 0;
        for (int num : nums) {
            if ((num & rightmostSetBit) == 0) {
                num1 ^= num;  // Group with bit not set
            } else {
                num2 ^= num;  // Group with bit set
            }
        }

        // Step 4: Return the two unique numbers
        return new int[]{num1, num2};
    }
}
```

#### 10) Convert Uppercase to Lowercase
- The ASCII value of 'A' is 65, and the ASCII value of 'a' is 97.
- Is this 32 bit diffrence?
- If we turn on the 2^5 (or 32) bit of an uppercase letter, it will convert it to lowercase. The difference between uppercase and lowercase letters in ASCII is exactly 32.

```Java
public class UpperToLower {
    public static char toLowerCase(char ch) {
        return (char) (ch | (1 << 5));  // Turn on the 6th bit (add 32)
    }

    public static void main(String[] args) {
        char uppercase = 'A';
        char lowercase = toLowerCase(uppercase);
        System.out.println("Lowercase of '" + uppercase + "' is: " + lowercase);  // Output: 'a'
    }
}

```

#### 11) Convert Lowercase to Uppercase
- The difference between lowercase and uppercase letters is exactly 32 in ASCII.
- Is this 32 bit diffrence?
- To convert a lowercase letter to uppercase, we turn off the 6th bit (2^5 or 32), which can be done using the bitwise AND operation with ~32 (~ is the NOT operator).
```Java
public class LowerToUpper {
    public static char toUpperCase(char ch) {
        return (char) (ch & ~(1 << 5));  // Turn off the 6th bit (subtract 32)
    }

    public static void main(String[] args) {
        char lowercase = 'a';
        char uppercase = toUpperCase(lowercase);
        System.out.println("Uppercase of '" + lowercase + "' is: " + uppercase);  // Output: 'A'
    }
}


```

#### 12) Invert Alphabet's case
- Is this toggle 2^5 bit problem?

```Java
public class ToggleCase {
    public static char invertCase(char ch) {
        return (char) (ch ^ (1 << 5));  // Toggle the 6th bit (XOR with 32)
    }

    public static void main(String[] args) {
        char uppercase = 'A';
        char lowercase = 'a';
        
        // Toggle case
        System.out.println("Inverted case of '" + uppercase + "' is: " + invertCase(uppercase));  // Output: 'a'
        System.out.println("Inverted case of '" + lowercase + "' is: " + invertCase(lowercase));  // Output: 'A'
    }
}

```

#### 13) Find Letter position in alphabet
- A has 64 ASCII value
- If we remove 64 value bit then we can easily find letter position

```Java
public class AlphabetPosition {
    public static int getPosition(char ch) {
        return (ch | (1 << 6));  // Turn on the 7th bit (add 64)
    }

    public static void main(String[] args) {
        char letter = 'A'; // Change this to test with different letters
        int position = getPosition(letter);
        System.out.println("Position of '" + letter + "' in the alphabet is: " + position); // Output: 1
    }
}

```

#### 14) Swap Two numbers without temp variable

```Java
public class SwapNumbers {
    public static void swapUsingXOR(int a, int b) {
        a = a ^ b;  // XOR a and b
        b = a ^ b;  // XOR the new a with b gives original a
        a = a ^ b;  // XOR the new a with new b gives original b

        System.out.println("After swapping: a = " + a + ", b = " + b);
    }

    public static void main(String[] args) {
        int a = 5;
        int b = 10;
        System.out.println("Before swapping: a = " + a + ", b = " + b);
        swapUsingXOR(a, b);
    }
}

```

#### 15) Calculate xor from 1 to n
**Intuition:**
- One way is to iterate from 1 to n and find the answer
-  If it were that easy, it wouldn’t be a question!
- Is there any operator that can provide the answer quickly? Not really!
- Can we find pattern?

1 -> 1

1 ^ 2 -> 3

1 ^ 2 ^ 3 -> 3 ^ 3 -> 0

1 ^ 2 ^ 3 ^ 4 -> 0 ^ 4 -> 4

(1-4) ^ 5 -> 4 ^ 5 -> 100 ^ 1001 -> 1

(1-5) ^ 6 -> 1 ^ 6 -> 1 ^ 110 -> 7

(1-6) ^ 7 -> 7 ^ 7 -> 0

(1-7) ^ 8 -> 0 ^ 8 -> 8

Let's find pattern:

we observed repeatation after 4th elements

**if(n%4 == 0) => n**

**if(n%4== 1) => 1**

**if(n%4 == 2) => n+1;**

**if(n%4 == 3) => 0**

```Java
public class XORFrom1ToN {
    public static int calculateXOR(int n) {
        switch (n % 4) {
            case 0:
                return n;
            case 1:
                return 1;
            case 2:
                return n + 1;
            case 3:
                return 0;
            default:
                return -1; // This case should never occur
        }
    }

    public static void main(String[] args) {
        int n = 5; // Example input
        System.out.println("XOR from 1 to " + n + " is: " + calculateXOR(n)); // Output: 1
    }
}

```

#### 15.b) Find xor from the range [L,R]
**Intuition:**
- Can we find x or of 1 to R and 1 to L-1
- [1, R] ^ [1, L-1]
- 1 to L-1 will be repeated and removed through xor operation

#### 16) Find xor of all subset of array

**Example:**

[1,2,3]

Subsets: [[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]

1^2^(1^2)^3^(1^3)^(2^3)^(1^2^3)

Answer = 0

**Intuition:**
- If we have size of array greater than 1 then we will have even number of elements and answer would be 0

```Java
public class XOROfSubsets {
    public static int findXOROfSubsets(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }
       
        return 0;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        int result = findXOROfSubsets(nums);
        System.out.println("XOR of all subsets: " + result);  // Output: 0
    }
}

```

#### 17) Count number of bits to be flipped to convert A to B
**Intuition:**
- we need to find bits which is different
- xor can handle that easily; find xor of 2 numbers and count number of set bits in (num1 ^ num2)

```Java
public class BitFlipCounter {
    // Function to count the number of set bits
    public static int countSetBits(int number) {
        int count = 0;
        while (number > 0) {
            count += (number & 1); // Increment count if the last bit is set
            number >>= 1;          // Right shift the number by 1
        }
        return count;
    }

    // Function to count the number of bits to be flipped to convert A to B
    public static int countBitsToFlip(int A, int B) {
        int xor = A ^ B; // XOR A and B
        return countSetBits(xor); // Count the number of set bits in the XOR result
    }

    public static void main(String[] args) {
        int A = 29; // Example number A (binary: 11101)
        int B = 15; // Example number B (binary: 01111)
        int bitsToFlip = countBitsToFlip(A, B);
        System.out.println("Number of bits to be flipped to convert A to B: " + bitsToFlip);  // Output: 2
    }
}

```
#### 18) Finding missing number in array

**Problem:**
Given an array nums containing n distinct numbers in the range [0,n], return the only number in the range that is missing from the array.

**Intuition:**
- Can we do xor of given aray with range [0,n]
- Duplicate elements will be discarded only missing number will be present

```Java
public class MissingNumberFinder {
    // Function to find the missing number in the array
    public static int findMissingNumber(int[] nums) {
        int n = nums.length; // Length of the array
        int xorAll = 0; // XOR of all numbers from 0 to n
        int xorArray = 0; // XOR of all elements in the array

        // XOR all numbers from 0 to n
        for (int i = 0; i <= n; i++) {
            xorAll ^= i;
        }

        // XOR all elements in the given array
        for (int num : nums) {
            xorArray ^= num;
        }

        // The missing number will be the XOR of xorAll and xorArray
        return xorAll ^ xorArray;
    }

    public static void main(String[] args) {
        int[] nums = {3, 0, 1}; // Example array with missing number 2
        int missingNumber = findMissingNumber(nums);
        System.out.println("The missing number is: " + missingNumber); // Output: 2
    }
}

```

#### 19) Print the binary representation of decimal number

**Inuition:**
- To convert a decimal number to binary, repeatedly divide the number by 2.
- For each division, record the remainder (either 0 or 1).
- Insert each remainder at the starting position of the binary representation, as the last remainder obtained represents the least significant bit (LSB) while the first remainder represents the most significant bit (MSB).

```Java
public class BinaryRepresentation {
    // Function to print the binary representation of a decimal number
    public static void printBinary(int number) {
        StringBuilder binaryString = new StringBuilder();
     
        while (number > 0) {
            binaryString.insert(0, number % 2); // Insert the remainder at the beginning
            number /= 2; // Divide number by 2
        }
        
        System.out.println("The binary representation is: " + binaryString.toString());
    }

    public static void main(String[] args) {
        int number = 10; // Example decimal number
        printBinary(number); // Output: 1010
    }
}

```

#### 20) Reverse the bits of a number

**Inuition:**
- Start with an answer initialized to 0.
  - While the given number is not 0, do the following:
    - Extract the least significant bit (LSB) of the number using bitwise AND with 1.
    - If the extracted bit is 1, set the corresponding bit in the answer.
    - Right-shift the given number to process the next bit.
    - Left-shift the answer to make space for the next bit.
- Repeat this until all bits of the number have been processed.

```Java
public class BitManipulation {
    public static int reverseBits(int number) {
        int reversed = 0;
        while (number != 0) {
            // Extract the least significant bit
            int lsb = number & 1; 
            // Left shift the reversed number to make space for the next bit
            reversed = (reversed << 1) | lsb; 
            // Right shift the original number to process the next bit
            number >>= 1; 
        }
        return reversed;
    }

    public static void main(String[] args) {
        int number = 13; // binary: 1101
        System.out.println("Reversed bits of " + number + " is: " + reverseBits(number)); // Output: 11 (binary: 1011)
    }
}

```

#### 21) Swap the ith and Jth bit.


**Example:**
- `num = 43`, `i = 2`, `j = 5`.
- Binary representation of `43`: `00101011`.

**Output:**
- After swapping the bits at positions `2` and `5`, the output should be `57` (binary: `00111001`).

**Step-by-step Process:**

1) Initial Binary Representation:


    num = 43
    
    Binary of 43 = 00101011

3) Identify the ith and jth bits:


    Position i = 2: Look at the second bit from the right, which is 1.
    
    Position j = 5: Look at the fifth bit from the right, which is 0.
    
    So, we have:
    
    ith bit = 1
    
    jth bit = 0

3) Check if the bits are different:


    Since the ith and jth bits are different (1 and 0), we need to swap them.

4) Swap the bits:


    We toggle the ith and jth bits using XOR (^) operation.
    
    Toggle the 2nd bit: 00101011 ^ (1 << 1) → 00101011 ^ 00000010 → 00101001.
    
    Toggle the 5th bit: 00101001 ^ (1 << 4) → 00101001 ^ 00010000 → 00111001.

**Final result:**

After the swap, the binary representation becomes 00111001, which is 57 in decimal.

**Intuition:**
- Check ith bit is set or not [ A =  (n >> i-1) & 1 ]
- Check jth bit is set or not [ B = (n >> j-1) & 1 ]
- now we have 2 possibility; both bits are same or opposite [ temp = (A ^ B) ]
- For same bit, we don't need to do anything
- For opposite, we can apply toggle bit approach

  Number = temp << (i-1) ^ Number

  Number = temp << (j-1) ^ Number


```Java
public class BitManipulation {
    public static int swapBits(int n, int i, int j) {
        // Check if ith bit is set
        int A = (n >> (i - 1)) & 1;
        
        // Check if jth bit is set
        int B = (n >> (j - 1)) & 1;
        
        // XOR of A and B
        int temp = A ^ B;
        
        // If bits are different, swap them
        if (temp != 0) {
            // Toggle ith bit
            n ^= (1 << (i - 1));
            
            // Toggle jth bit
            n ^= (1 << (j - 1));
        }
        
        return n;
    }

    public static void main(String[] args) {
        int number = 10;  // Binary: 1010
        int i = 2;
        int j = 4;
        
        System.out.println("Original number: " + number);
        int result = swapBits(number, i, j);
        System.out.println("After swapping " + i + "th and " + j + "th bits: " + result);
    }
}
```

#### 22) Swap all even and odd bits
**Intuition:**
- Can we use above approach?
- Instead of odd even, can we assume 1st and 2nd bit and swap them
- If we do same process for all the position, would it be our answer?

**Above approach is not optimized, can we optimize that?**
- What if we know all the even positions where bits are set?
- Similarly, can we determine all the odd positions where bits are set?
- If we shift them and combine the results, would that give us the answer?

**Example:**

Let's take the integer `23`, which has the binary representation:

    23 in binary: 0000 0000 0000 0000 0000 0000 0001 0111
    (binary: ...10101010) to extract even bits
    (binary: ...01010101) to extract odd bits
    number & mask will have set bits
    swap and combine even amd odd bits

```Java
public class SwapEvenOddBits {
    public static int swapEvenOddBits(int num) {
        // Define masks for even and odd bits using binary literals
        final int EVEN_MASK = 0b10101010101010101010101010101010; // 0xAAAAAAAA
        final int ODD_MASK = 0b01010101010101010101010101010101;  // 0x55555555

        // Isolate even and odd bits
        int evenBits = num & EVEN_MASK;
        int oddBits = num & ODD_MASK;

        // Shift even bits right and odd bits left
        int evenBitsShifted = evenBits >> 1;
        int oddBitsShifted = oddBits << 1;

        // Combine the shifted bits
        return evenBitsShifted | oddBitsShifted;
    }

    public static void main(String[] args) {
        int number = 23; // Binary: 10111
        int swappedNumber = swapEvenOddBits(number);
        System.out.println(Integer.toBinaryString(swappedNumber)); // Output will be the binary representation after swapping
    }
}

```


#### 23) Copy set bits in a range, toggle set bits in a range:
**Problem:**
Copy set bit-we have two numbers A and B, and  we want to copy the bits of B to A for a given range [to R from LSB to MSB.

**Intuition:**
- We want to create mask for L to R (1111) where L=3 and R = 7
- extract set bits from both numbers
- swap them

??
- How can we create mask?
- Can we create 1111 of size R-L? [ (1 << (R - L + 1 ) - 1]
- Shift that to L position [ mask << (L - 1)]
- Toogle bit (N ^ mask)

#### 24) Divide two integers without using Multiplication, Division and mod operator
**Approach:1**
- Keep subtracting the divisor from dividend untill divident less than divisor

**Example:**
Dividend = 10
Divisor = 3
Quotient = 3

10 - 3 = 7

7 - 3 = 4

4 - 3 = 1 < 3

**Approach:2**

**Handle Edge Cases:** 
- If the divisor is 0, return an error or infinity (undefined).
- If the dividend is Integer.MIN_VALUE and the divisor is -1, return Integer.MAX_VALUE (to avoid overflow).

**Convert to Positive:** 
- Work with positive numbers by using the absolute values of the dividend and divisor. Keep track of whether the result should be negative or positive by checking if the signs of dividend and divisor are different.

**Bit Manipulation:**
- Use bit shifts to perform the division operation.
- Left shift the divisor until it's greater than or equal to the dividend, then subtract the shifted divisor from the dividend and count how many times you shifted. The total count gives you the quotient.
- Essentially, we're trying to subtract multiples of the divisor as much as possible without exceeding the dividend.

**Final Result:**
- Restore the sign of the result and check for overflow (return Integer.MAX_VALUE if overflow occurs).

```Java
public class DivideWithoutOperators {

    public static int divide(int dividend, int divisor) {
        // Handle edge case: overflow
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;  // Overflow case
        }

        // Determine the sign of the result
        boolean negative = (dividend < 0) ^ (divisor < 0);

        // Convert dividend and divisor to positive long values
        long absDividend = Math.abs((long) dividend);
        long absDivisor = Math.abs((long) divisor);

        int result = 0;

        // Perform division using bit manipulation
        while (absDividend >= absDivisor) {
            long tempDivisor = absDivisor, multiple = 1;
            
            // Shift left the divisor until it's less than or equal to the dividend
            while (absDividend >= (tempDivisor << 1)) {
                tempDivisor <<= 1;
                multiple <<= 1;
            }

            // Subtract the largest shifted divisor from the dividend
            absDividend -= tempDivisor;
            result += multiple;
        }

        // Apply the correct sign to the result
        return negative ? -result : result;
    }

    public static void main(String[] args) {
        int dividend = 43;
        int divisor = 5;
        System.out.println("Quotient: " + divide(dividend, divisor));  // Output: 8
    }
}

```
#### 25) Reduce a Number to 1:
# PENDNG

#### 26) Detect if two integers have opposite sign

**Intuition:**
- signed integers in computer are store in 2's complement form: where MSB fit represent the sign of the number

     1 -> Negative integer

     0 -> positive integer

- So, if we do ^(xor) of two numbers then it will be negative because MSB (1^0) = 1 which shows negative number

```Java
public class OppositeSigns {

    public static boolean hasOppositeSigns(int a, int b) {
        // XOR the two numbers and check if the result is negative
        return (a ^ b) < 0;
    }

    public static void main(String[] args) {
        int a = 5;    // Positive
        int b = -10;  // Negative

        if (hasOppositeSigns(a, b)) {
            System.out.println(a + " and " + b + " have opposite signs.");
        } else {
            System.out.println(a + " and " + b + " do not have opposite signs.");
        }
    }
}

```
#### 27) Add 1 to an integer
# PENDNG

#### 28) Find Xor of a number without using XOR operator

**Property of XOR:**
a^b = (a∧¬b)∨(¬a∧b)

- This equation means that XOR can be rewritten in terms of AND (&), OR (|), and NOT (~) operations:

```Java
public class XorWithoutOperator {

    // Function to compute XOR without using the ^ operator
    public static int xor(int a, int b) {
        return (a & ~b) | (~a & b);
    }

    public static void main(String[] args) {
        int a = 5;   // binary: 0101
        int b = 3;   // binary: 0011
        int result = xor(a, b);

        System.out.println("XOR of " + a + " and " + b + " is: " + result);  // Output: 6
    }
}

```

#### 29) Determine if two integers are equal without using comparison and arithmetic operators
- We can achieve by xor
```Java
public class EqualIntegers {
    public static boolean areEqual(int a, int b) {
        return (a ^ b) == 0;
    }

    public static void main(String[] args) {
        int num1 = 5;
        int num2 = 5;
        if (areEqual(num1, num2)) {
            System.out.println("Numbers are equal.");
        } else {
            System.out.println("Numbers are not equal.");
        }
    }
}
 
```
#### 30) Find minimum or maximum of two integers without using branching
# PENDNG

### Leetcode Problems:

#### 1) Find missing and repeating number / Set mismatch
# PENDNG

#### 2) Maximum Product of Word Lengths (Amazon, google)
# PENDNG

#### 3) Concatenation of Consecutive Binary Numbers
# PENDNG

#### 4) Check if a String Contains all binary codes of size k
# PENDNG

#### 5) Find the Duplicate Number
# PENDNG
