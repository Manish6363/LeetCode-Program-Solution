## Problem
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

- Example 1:
    - $$Input$$: nums = [0,1,0,3,12]
    - $$Output$$: [1,3,12,0,0]

link: https://leetcode.com/problems/move-zeroes/description/


# Intuition
We need to **move all zero elements to the end of the array while maintaining the relative order of non-zero elements**, and the operation must be done **in-place**.

A simple way is to **first collect all non-zero elements** and then place zeros at the end. We can optimize this idea by **avoiding extra space** and performing the operations **directly inside the array** using **two-pointer techniques**.

# Approach-1: Brute Force
Use a temporary array to store all non-zero elements first, then copy everything back to the original array.

#### Time complexity: **O(n)**
#### Space complexity: **O(n)**

## Java Code
```Java []
class Solution {
    public void moveZeroes(int[] nums) {
        int temp[]=new int[nums.length];
        for(int i=0, j=0; i<nums.length; i++){
            if(nums[i]!=0)
                temp[j++]=nums[i];
        }
        for(int i=0; i<nums.length; i++){
            nums[i]=temp[i];
        }
    }
}
```

# Approach-2: Better Approach [using Two in-place]
Move all non-zero elements forward.
Fill remaining positions with zero.

#### Time complexity: **O(n)**
#### Space complexity: **O(1)**

## Java Code
```Java []
class Solution {
    public void moveZeroes(int[] nums) {
        int k=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]!=0)
                nums[k++]=nums[i];
        }
        while(k<nums.length)
            nums[k++]=0;
    }
}
```

# Approach-3: Optimal Approach [using Two Pointer - Single Pass]
Let pointer **`j`** stores the index of the first zero.
Traverse with pointer **`i`**
When a non-zero appears after a zero, swap them.

#### Time complexity: **O(n)**
#### Space complexity: **O(1)**

## Java Code
```Java []
class Solution {
    public void moveZeroes(int[] nums) {
        for(int i=0, j=-1; i<nums.length; i++){
            if(nums[i]==0 && j==-1){
                j=i;
            }
            else if(nums[i]!=0 && j!=-1){
                int temp=nums[i];
                nums[i]=nums[j];
                nums[j]=temp;
                j++;
            }
        }
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int j = -1;   // index of first zero
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == 0 && j == -1) {
                j = i;
            }
            else if (nums[i] != 0 && j != -1) {
                swap(nums[i], nums[j]);
                j++;
            }
        }
    }
};
```

## JavaScript Code
```JavaScript []
var moveZeroes = function(nums) {
    let j = -1;   // index of first zero
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === 0 && j === -1) {
            j = i;
        } 
        else if (nums[i] !== 0 && j !== -1) {
            [nums[i], nums[j]] = [nums[j], nums[i]]; // Destructuring
            j++;
        }
    }
};
```
