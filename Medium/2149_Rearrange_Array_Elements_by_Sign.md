## Problem
You are given a 0-indexed integer array nums of even length consisting of an equal number of positive and negative integers.

You should return the array of nums such that the array follows the given conditions:

Every consecutive pair of integers have opposite signs.
For all integers with the same sign, the order in which they were present in nums is preserved.
The rearranged array begins with a positive integer.
Return the modified array after rearranging the elements to satisfy the aforementioned conditions.

Example 1:
- $$Input$$: `nums = [3,1,-2,-5,2,-4]`
- $$Output$$: `[3,-2,1,-5,2,-4]`
    **Explanation:**
    - The positive integers in nums are [3,1,2]. The negative integers are [-2,-5,-4].
    - The only possible way to rearrange them such that they satisfy all conditions is [3,-2,1,-5,2,-4].
Other ways such as [1,-2,2,-5,3,-4], [3,1,2,-2,-5,-4], [-2,3,-5,1,-4,2] are incorrect because they do not satisfy one or more conditions.  


link: https://leetcode.com/problems/rearrange-array-elements-by-sign/description/

# Intuition
The array has an equal number of positive and negative elements and must start with a positive number while keeping their original order.

We iterate through the array and place:
- positives at the next available even index
- negatives at the next available odd index

# Approach-1 Better Approach
1. Instead of ArrayList, use two arrays.
    - Store positives in pos[]
    - Store negatives in neg[]
2. Fill original array alternatively.

#### Time complexity: O(N)
#### Space complexity: O(N)


## Java Code
```Java []
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int[] pos = new int[nums.length/2];
        int[] neg = new int[nums.length/2];
        for(int i = 0, p=0, n=0; i < nums.length; i++){
            if(nums[i] > 0)
                pos[p++] = nums[i];
            else
                neg[n++] = nums[i];
        }
        for(int i = 0, p=0, n=0; i < nums.length; i++){
            if(i % 2 == 0)
                nums[i] = pos[p++];
            else
                nums[i] = neg[n++];
        }
        return nums;
    }
}
```

# Approach-2 Optimal Approach
Directly place numbers in correct index positions.
- Positive → even index 0,2,4
- Negative → odd index 1,3,5

Use two pointers:
- posIndex = 0
- negIndex = 1

#### Time complexity: O(N)
#### Space complexity: O(N)


## Java Code
```Java []
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int[] res = new int[nums.length];
        int posIndex = 0;
        int negIndex = 1;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] > 0){
                res[posIndex] = nums[i];
                posIndex += 2;
            }else{
                res[negIndex] = nums[i];
                negIndex += 2;
            }
        }
        return res;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
        vector<int> res(nums.size());
        int posIndex = 0;
        int negIndex = 1;
        for(int i = 0; i < nums.size(); i++){
            if(nums[i] > 0){
                res[posIndex] = nums[i];
                posIndex += 2;
            }else{
                res[negIndex] = nums[i];
                negIndex += 2;
            }
        }
        return res;
    }
};
```


# JavaScript Code
```JavaScript []
var rearrangeArray = function(nums) {
    let res=[nums.length];
    let posIndex = 0;
    let negIndex = 1;
    for(let i = 0; i < nums.length; i++){
        if(nums[i] > 0){
            res[posIndex] = nums[i];
            posIndex += 2;
        }else{
            res[negIndex] = nums[i];
            negIndex += 2;
        }
    }
    return res;
};
```
