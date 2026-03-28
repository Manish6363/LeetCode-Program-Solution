## Problem
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. 
link: https://leetcode.com/problems/fibonacci-number/description/

# Intuition
The Fibonacci sequence is built by **adding the previous two numbers**.

# Approach-1: Recursive Approach (Brute Force)
- Directly follow the recursive definition.
``` 
fib(5)
→ fib(4) + fib(3)
→ (fib(3) + fib(2)) + (fib(2) + fib(1))
→ ...
```
#### Time complexity: **O(2ⁿ)**
#### Space complexity: **O(n)**

#### Java Code
``` java []
class Solution {
    public int fib(int n) {
        if (n <= 1)
            return n;
        return fib(n - 1) + fib(n - 2);
    }
}
```

# Approach-2: Iterative Optimized (BEST PRACTICAL SOLUTION)
- We only need last two value.
#### Time complexity: **O(n)**
#### Space complexity: **O(1)**

#### Java Code
``` java []
class Solution {
    public int fib(int n) {
        if (n <= 1)
            return n;
        int a = 0, b = 1;
        for (int i = 2; i <= n; i++) {
            int sum = a + b;
            a = b;
            b = sum;
        }
        return b;
    }
}
```


## CPP / C++ Code
``` cpp []
class Solution {
public:
    int fib(int n) {
        if (n <= 1)
            return n;
        int a = 0, b = 1;
        for (int i = 2; i <= n; i++) {
            int sum = a + b;
            a = b;
            b = sum;
        }
        return b;
    }
};
```

## JavaScript Code
```javascript []
var fib = function(n) {
    if (n <= 1)
        return n;
    let a = 0, b = 1;
    for (let i = 2; i <= n; i++) {
        let sum = a + b;
        a = b;
        b = sum;
    }
    return b;
};
```
