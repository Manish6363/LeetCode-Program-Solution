## Problem: Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-2^31, 2^31 - 1], then return 0.
Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

link: https://leetcode.com/problems/reverse-integer/description/

# Intuition
The main idea is to extract digits one by one from the number and build the reversed number mathematically instead of converting the number into a string. This allows us to solve the problem efficiently using only integer operations.

However, reversing the digits may cause integer overflow because the reversed number might exceed the signed 32-bit integer range [-2³¹, 2³¹ − 1]. Since we are not allowed to use 64-bit integers, we must detect overflow before it happens.

So, the challenge is
- Reverse the digits.
- Ensure the result always stays within 32-bit integer limits.

# Approach
1. Initialize a variable rev = 0 to store the reversed number.
2. While x is not zero:
   - Extract the last digit using: ```rem = x % 10 ```
   - Remove the last digit from x: ```x /= 10 ```
   - Before adding rem to rev, check for possible overflow:
        - If rev > Integer.MAX_VALUE / 10, then multiplying by 10 will overflow.
        - If rev == Integer.MAX_VALUE / 10 and rem > 7, it will exceed 2147483647.
        - Similarly, check for underflow using Integer.MIN_VALUE.
3. If any overflow condition is detected, return 0.
4. Otherwise, safely update: ```rev = rev * 10 + rem;```
5. After the loop ends, return rev.

**Why Overflow Check Works** 
  - For a 32-bit signed integer:

        MAX =  2147483647
        MIN = -2147483648

- Before doing: ```rev = rev * 10 + rem```
- We check:

        rev <= MAX / 10
        rev >= MIN / 10

This guarantees that multiplying by 10 and adding the next digit won’t exceed limits.

# Complexity
**- Time complexity:** O(log10​(n))
Because we process each digit once. A 32-bit integer has at most 10 digits, so the loop runs at most 10 times.

**- Space complexity:** O(1)
Only a few integer variables are used → constant space.

# Java Code
```java []
class Solution {
    public static int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int rem = x % 10;
            x /= 10;
            if (rev > Integer.MAX_VALUE / 10 ||
                    (rev == Integer.MAX_VALUE / 10 && rem > 7))
                return 0;
            if (rev < Integer.MIN_VALUE / 10 ||
                    (rev == Integer.MIN_VALUE / 10 && rem < -8))
                return 0;
            rev = rev * 10 + rem;
        }
        return rev;
    }
}
```

# CPP/C++ Code
``` Cpp / C++ []
class Solution {
public:
    int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int rem = x % 10;
            x /= 10;
            if (rev > INT_MAX / 10 || (rev == INT_MAX / 10 && rem > 7))
                return 0;
            if (rev < INT_MIN / 10 || (rev == INT_MIN / 10 && rem < -8))
                return 0;
            rev = rev * 10 + rem;
        }
        return rev;
    }
};

```

# JavaScript Code
```JavaScript []
var reverse = function(x) {
    let rev = 0;
    while (x !== 0) {
        let rem = x % 10;
        x = (x / 10) | 0; 
        if (rev > 214748364 || (rev === 214748364 && rem > 7))
            return 0;
        if (rev < -214748364 || (rev === -214748364 && rem < -8))
            return 0;
        rev = rev * 10 + rem;
    }
    return rev;
};
```
