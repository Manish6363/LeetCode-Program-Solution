## Problem
Given a binary array nums, return the maximum number of consecutive 1's in the array.

link: https://leetcode.com/problems/max-consecutive-ones/description/

Example 1:
- $$Input$$: `nums = [1,1,0,1,1,1]`
- $$Output$$: 3

# Intuition
The array contains only **0**s and **1**s, and we need to find the **maximum number of consecutive 1**s.

# Approach-1 
The idea is simple:
- Traverse the array from left to right.
- Maintain a variable count to store the current consecutive 1s.
- When we encounter a 1, increase count.
- When we encounter a 0, reset count to 0 because the sequence of consecutive 1s breaks.
- During traversal, keep updating the maximum value of count.

This ensures we track the longest sequence of consecutive 1s in a single pass.

#### Time complexity: O(n)
#### Space complexity: O(1)

## Java Code
```java []
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max=0, count=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]==1){
                count++;
                max=count>max?count:max;
            }else{
                count=0;
            }
        }
        return max;
    }
}
```

# Approach-2 Shorter Implementation 


#### Time complexity: O(n)
#### Space complexity: O(1)

## Java Code
```java []
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0, count = 0;
        for(int num : nums){
            count = (num == 1) ? count + 1 : 0;
            max = Math.max(max, count);
        }
        return max;
    }
}
```


## CPP / C++ Code
```Cpp []
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int max=0, count=0;
        for(int i=0; i<nums.size(); i++){
            if(nums[i]==1){
                count++;
                max=count>max?count:max;
            }else{
                count=0;
            }
        }
        return max;
    }
};
```

## JavaScript Code
```JavaScript []
var findMaxConsecutiveOnes = function(nums) {
    let max=0, count=0;
    for(let i=0; i<nums.length; i++){
        if(nums[i]==1){
            count++;
            max=count>max?count:max;
        }else{
            count=0;
        }
    }
    return max;
};
```

