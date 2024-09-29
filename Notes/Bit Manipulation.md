# Bit Manipulation


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

