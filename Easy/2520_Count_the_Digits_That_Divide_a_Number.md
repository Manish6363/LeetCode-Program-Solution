# 2520. Count the Digits That Divide a Number

🔗 **Problem Link:** https://leetcode.com/problems/count-the-digits-that-divide-a-number/description/

---

## 🧠 Intuition
To solve this problem, we iterate through each digit of the given number and check whether the original number is divisible by that digit. If it is, we increment a counter.

---

## 🚀 Approach
1. Store the original number in a variable for divisibility checks.
2. Use a loop to extract digits one by one using the modulo operator (`num % 10`).
3. For each extracted digit:
   - Check if the original number is divisible by that digit.
   - If true, increment the counter.
4. Remove the last digit by dividing the number by 10.
5. Repeat until all digits are processed.

---

## ⏱ Complexity
- **Time Complexity:** `O(n)` — where `n` is the number of digits in the number.
- **Space Complexity:** `O(1)` — constant extra space.

---

## 💻 Java Solution
```java
class Solution {
    public int countDigits(int num) {
        int count = 0;
        int temp = num;

        while (temp > 0) {
            int rem = temp % 10;
            if (num % rem == 0)
                count++;
            temp /= 10;
        }
        return count;
    }
}
```

## 💻 C++/CPP Solution
```java
class Solution {
public:
    int countDigits(int num) {
        int count = 0;
        int temp = num;

        while (temp > 0) {
            int rem = temp % 10;
            if (num % rem == 0)
                count++;
            temp /= 10;
        }
        return count;
    }
};

```

## 💻 JavaScript Solution
```java
var countDigits = function (num) {
    let count = 0;
    let temp = num;

    while (temp > 0) {
        let rem = temp % 10;
        if (num % rem === 0)
            count++;
        temp = Math.floor(temp / 10);
    }

    return count;
};

```

