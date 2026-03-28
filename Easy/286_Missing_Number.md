## Problem
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

link: https://leetcode.com/problems/missing-number/description/
 

# Intuition
We are given an array `nums` containing **n** distinct numbers taken from the range **[0, n]**.
Since the range contains **n+1** numbers but the array size is **n**, exactly one number is missing.

Example: `nums = [3,0,1]`
Range should be → [0,1,2,3]
Missing number → 2

So the goal is to identify the number that does not appear in the array.
Different strategies can be used:
1. Check each number manually.
2. Use extra space to mark visited numbers.
3. Use mathematical formulas.
4. Use XOR properties.

# Approach-1: Brute Force
- Check every number from 0 → n and see whether it exists in the array.
- If any number is not found, that is the missing number.

#### Time complexity: O(n²)
#### Space complexity: O(1)

## Java Code
```java []
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        for(int i = 0; i <= n; i++){
            boolean flag = false;
            for(int j = 0; j < nums.length; j++){
                if(nums[j] == i){
                    flag = true;
                    break;
                }
            }
            if(!flag)
                return i;
        }
        return -1;
    }
}
```

# Approach-2: Better (Using Hashing / Extra Array)
- Use an auxiliary array to mark numbers that appear in the given array.
- Then check which index remains unmarked.

#### Time complexity: O(n)
#### Space complexity: O(n)

## Java Code
```java []
class Solution {
    public int missingNumber(int[] nums) {
        int res=-1;
        int temp[]=new int[nums.length+1];
        for(int i=0; i<nums.length; i++){
            temp[nums[i]]=1;
        }
         for(int i=0; i<temp.length; i++){
            if(temp[i]==0){
                res=i;
                break;
            }
        }
        return res;
    }
}
```

# Approach-3: Optimal (using Sum Formula)
- The sum of numbers from 0 → n can be calculated using the formula:
        `Sum = n(n + 1) / 2`
- If we subtract the actual array sum from the expected sum, we get the missing number.

#### Time complexity: O(n)
#### Space complexity: O(1)

## Java Code
```java []
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int expected = n*(n+1)/2;
        int actual = 0;
        for(int num : nums)
            actual += num;
        return expected - actual;
    }
}
```

# Approach-4: Optimal (using XOR)
- XOR Properties
    ``` 
    a ^ a = 0
    a ^ 0 = a
    ```

If we XOR:
- all numbers from 0 → n
- all numbers in the array
- all common numbers cancel out, leaving the missing number.

#### Time complexity: O(n)
#### Space complexity: O(1)

## Java Code
```java []
class Solution {
    public int missingNumber(int[] nums) {
        int xor1=0, xor2=0;
        for(int i=0; i<nums.length; i++){
            xor2=xor2^nums[i];
            xor1=xor1^i;
        }
        xor1=xor1^nums.length;
        return xor1^xor2;
    }
}
```


## CPP / C++ Code
```Cpp []
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int expected = n*(n+1)/2;
        int actual = 0;
        for(int num : nums)
            actual += num;
        return expected - actual;
    }
}
```

## JavaScript Code
```javascript []
var missingNumber = function(nums) {
    let n = nums.length;
    let expected = n*(n+1)/2;
    let actual = 0;
    for(let num of nums)
        actual += num;
    return expected - actual;
};
```
