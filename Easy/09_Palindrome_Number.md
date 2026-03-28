## Problem: 9. Palindrome Number
link: https://leetcode.com/problems/palindrome-number/

# Intuition
To check whether a number is a palindrome, we need to verify if it reads the same forward and backward. There are multiple ways to achieve this:

# Approach-1:: Convert the number into a string and reverse it.
- Convert the number into a string.
- Reverse the string.
- Compare the original and reversed strings.

**Time Complexity:** O(n)
**Space Complexity:** O(n)
``` Java []
class Solution {
    public boolean isPalindrome(int x) {
        String s=x+"";
        StringBuilder sb=new StringBuilder(s);
        sb.reverse();
        return s.equals(sb.toString());
    }
}
```

# Approach-2:: Reverse the entire number mathematically and compare.
- Extract digits using % 10.
- Build the reversed number.
- Compare it with the original number.

**Time Complexity:** O(n)
**Space Complexity:** O(1)
``` Java []
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0)
            return false;
        int original = x;
        int rev = 0;
        while (x > 0) {
            rev = rev * 10 + x % 10;
            x /= 10;
        }
        return original == rev;
    }
}
```

# Approach-3:: Reverse only half of the number to optimize performance and avoid overflow.
- Reverse digits until the reversed half becomes greater than or equal to the remaining number.
- Compare the two halves. 
- This reduces operations and prevents integer overflow.

**Time Complexity:** O(n)
**Space Complexity:** O(1)
``` Java []
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0))
            return false;
        int rev = 0;
        while (x > rev) {
            rev = rev * 10 + x % 10;
            x /= 10;
        }
        return x == rev || x == rev / 10;
    }
}
```


# CPP/C++ Code

``` Cpp / C++[]
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) 
            return false;
        int original = x;
        long long rev = 0;
        while (x > 0) {
            rev = rev * 10 + x % 10;
            x /= 10;
        }
        return original == rev;
    }
};
```


# JavaScript Code

``` JavaScript []
var isPalindrome = function(x) {
    let s = x.toString();
    let rev = s.split('').reverse().join('');
    return s === rev;
};
```
