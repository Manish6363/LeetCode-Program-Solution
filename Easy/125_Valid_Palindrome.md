## Problem: 
Given a string s, determine if it is a palindrome after converting all uppercase letters to lowercase and removing all non-alphanumeric characters.
link: https://leetcode.com/problems/valid-palindrome/submissions/1927393363/


# Intuition
To determine whether a string is a palindrome, we only need to compare valid alphanumeric characters while ignoring case and special characters.

## Approach 1 — Using StringBuilder + Filtering
- Convert the string to lowercase.
- Remove all non-alphanumeric characters.
- Reverse the cleaned string.
- Compare original and reversed strings.

#### Time complexity: O(n)
#### Space complexity: O(n)

#### Java Code
``` java []
class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if ((c >= 'a' && c <= 'z') || (c >= '0' && c <= '9')) {
                sb.append(c);
            }
        }
        String str = sb.toString();
        String rev = sb.reverse().toString();
        return str.equals(rev);
    }
}
```


## Approach 2 — Using Regex + StringBuilder
- Use regex to remove non-alphanumeric characters.
- Reverse and compare.

#### Time complexity: O(n)
#### Space complexity: O(n)
**Drawback:** Regex is internally expensive → Slower than manual traversal.

#### Java Code
```java []
class Solution {
    public boolean isPalindrome(String s) {
        String str=s.replaceAll("[^a-zA-Z0-9]+", "");
        return new StringBuilder(str).reverse().toString().equalsIgnoreCase(str);
    }
}
```

## Approach 3 — Two Pointer Technique
- Use two pointers, one from start and one from end. 
- Skip non-alphanumeric characters. 
- Compare characters directly. 
- No extra memory required.


#### Time complexity: O(n)
#### Space complexity: O(1)

#### Java Code
```java []
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left)))
                left++;
            while (left < right && !Character.isLetterOrDigit(s.charAt(right)))
                right--;
            if (Character.toLowerCase(s.charAt(left)) !=
                Character.toLowerCase(s.charAt(right)))
                return false;
            left++;
            right--;
        }
        return true;
    }
}
```


## CPP / C++ Code

```Cpp []
class Solution {
public:
    bool isPalindrome(string s) {
        int left = 0, right = s.length() - 1;
        while (left < right) {
            while (left < right && !isalnum(s[left]))
                left++;
            while (left < right && !isalnum(s[right]))
                right--;
            if (tolower(s[left]) != tolower(s[right]))
                return false;
            left++;
            right--;
        }
        return true;
    }
};
```

## JavaScript Code
``` javascript []
var isPalindrome = function(s) {
    let left = 0, right = s.length - 1;
    while (left < right) {
        while (left < right && !isAlphaNumeric(s[left]))
            left++;
        while (left < right && !isAlphaNumeric(s[right]))
            right--;
        if (s[left].toLowerCase() !== s[right].toLowerCase())
            return false;
        left++;
        right--;
    }
    return true;
};

function isAlphaNumeric(ch) {
    return (
        (ch >= 'a' && ch <= 'z') ||
        (ch >= 'A' && ch <= 'Z') ||
        (ch >= '0' && ch <= '9')
    );
}
```
