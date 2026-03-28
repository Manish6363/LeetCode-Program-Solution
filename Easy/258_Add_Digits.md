## Problem: 258. Add Digits
link: https://leetcode.com/problems/add-digits/?envType=problem-list-v2&envId=math

# Intuition
Repeatedly summing digits of a number eventually reduces it to a **single digit (digital root)**. Instead of simulating the process using loops, we can use a **mathematical property of modulo 9** to compute the result in constant time. 
But we will see different approaches to solve it.

# Approach-1 Iterative Digit Sum (Not Recommanded) 
We repeatedly sum the digits of the number until it becomes a single digit. If the sum becomes greater than 9, we repeat the process using the new sum.
    1. Extract each digit using % 10 and add it to sum. 
    2. Remove the last digit using / 10. 
    3. If num == 0 and sum > 9, restart the process using sum. 
    4. Continue until a single-digit result is obtained.
- **Time complexity:** O(log n) — number of digits processed
- **Space complexity:** O(1)

# Java Code
```java []
class Solution {
    public int addDigits(int num) {
        int sum=0;
        while(num!=0){
            sum+=num%10;
            num/=10;
            if(num==0&&sum>9){
                num=sum;
                sum=0;
            }
        }
        return sum;
    }
}
```

# Approach-2 Mathematical Digital Root (Modulo 9) *[Optimized-Recommanded]*
The repeated sum of digits of a number always converges to its digital root, which has a direct mathematical relationship with modulo 9.
    1. If num == 0, return 0. 
    2. If num % 9 == 0, return 9. 
    3. Otherwise, return num % 9.
- **Time complexity:** O(1)
- **Space complexity:** O(1)

# Java Code
```java []
class Solution {
    public int addDigits(int num) {
        if (num == 0) 
            return 0;
        return num % 9 == 0 ? 9 : num % 9;
    }
}
```

# Approach-3 Optimized Digital Root Formula (One-Liner) *[Optimized-Recommanded]*
Using the digital root formula: ``` 𝑑𝑖𝑔𝑖𝑡𝑎𝑙 𝑅𝑜𝑜𝑡 = 1 + ( 𝑛𝑢𝑚 − 1 ) % 9```
This directly gives the final digit sum without loops.
    1. If num == 0, return 0. 
    2. Otherwise, apply the formula. 
- **Time complexity:** O(1)
- **Space complexity:** O(1)

# Java Code
```java []
class Solution {
    public int addDigits(int num) {
        return num == 0 ? 0 : 1 + (num - 1) % 9;
    }
}
```

# CPP/C++ Code
```Cpp []
class Solution {
public:
    int addDigits(int num) {
        return num == 0 ? 0 : 1 + (num - 1) % 9;
    }
};
```

# JavaScript Code
```JavaScript []
var addDigits = function(num) {
    return num == 0 ? 0 : 1 + (num - 1) % 9;
};
```
