## Problem
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.
You must implement a solution with a linear runtime complexity and use only constant extra space.

link: https://leetcode.com/problems/single-number/description/ 

# Intuition
In the given array, every element appears twice except one element that appears only once.
Our goal is to find that unique element.

# Approach-1: Brute Force
Compare every element with all others and count occurrences.
**Steps:**
1. Traverse the array using index **i**. 
2. For each element, count how many times it appears in the array. 
3. Use another loop to compare **nums[i]** with every element. 
4. If the count is **1**, return that element.

#### Time complexity: O(n²)
#### Space complexity: O(1)

# Java Code
```Java []
class Solution {
    public int singleNumber(int[] nums) {
        for(int i = 0; i < nums.length; i++){
            int count = 0;
            for(int j = 0; j < nums.length; j++){
                if(nums[i] == nums[j]){
                    count++;
                }
            }
            if(count == 1){
                return nums[i];
            }
        }
        return -1;
    }
}
```

# Approach-2: Better Approach (using HashMap)
Use a HashMap to store frequency of each number.
**Step**
1. Create a HashMap to store number frequency. 
2. Traverse the array and update frequency. 
3. Traverse the array again and check which element has frequency 1. 
4. Return that element.

#### Time complexity: O(n)
#### Space complexity: O(n)


# Java Code
```Java []
import java.util.*;
class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(int num : nums){
            if(map.get(num) == 1){
                return num;
            }
        }
        return -1;
    }
}
```

# Approach-3: Optimal Approach (Using XOR)
Use the properties of the Bitwise XOR operator.
Important XOR properties:
        `a ^ a = 0`
        `a ^ 0 = a`
XOR is commutative and associative
So when we XOR all elements, duplicate numbers cancel out and only the unique number remains.

Example: `nums = [4,1,2,1,2]`

    4 ^ 1 ^ 2 ^ 1 ^ 2
    = 4 ^ (1 ^ 1) ^ (2 ^ 2)
    = 4 ^ 0 ^ 0
    = 4


#### Time complexity: O(n)
#### Space complexity: O(1)

# Java Code
```Java []
class Solution {
    public int singleNumber(int[] nums) {
        int xor=0;
        for(int i=0; i<nums.length; i++){
            xor^=nums[i];
        }
        return xor;
    }
}
```


# CPP / C++ Code
```Cpp []
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int xors=0;
        for(int i=0; i<nums.size(); i++){
            xors^=nums[i];
        }
        return xors;
    }
};
```


# JavaScript Code
```JavaScript []
var singleNumber = function(nums) {
    let xor=0;
    for(let i=0; i<nums.length; i++){
        xor^=nums[i];
    }
    return xor;
};
```
