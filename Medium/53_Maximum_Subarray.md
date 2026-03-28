## Problem
Given an integer array nums, find the subarray with the largest sum, and return its sum.

link: https://leetcode.com/problems/maximum-subarray/description/

Example 1:
- $$Input$$: `nums = [-2,1,-3,4,-1,2,1,-5,4]`
- $$Output$$: 6
- $$Explanation$$: The subarray `[4,-1,2,1]` has the largest sum 6.

# Intuition
A subarray must be continuous.
If we try every possible subarray, we can find the maximum sum, but that will take a lot of time.
**Observation:** 
- If the current running sum becomes negative, it will reduce the sum of the future elements.
- So whenever the sum becomes negative, we restart the subarray from the next element.

This idea leads to **Kadane’s Algorithm**, which solves the problem in linear time.

# Approach-1 Brute Force
Generate all possible subarrays and calculate their sum.
**Steps:**
1. Fix the starting index `i`.
2. Fix the ending index `j`.
3. Calculate the sum of elements between `i` and `j`.
4. Keep track of the maximum sum.

#### Time complexity: O(N³)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int maxSubArray(int[] nums) {
        int n=nums.length;
        int max=Integer.MIN_VALUE;
        for(int i=0; i<n; i++){
            for(int j=i; j<n; j++){
                int sum=0;
                for(int k=i; k<=j; k++)
                    sum+=nums[k];
                max=max>sum?max:sum;
            }
        }
        return max;
    }
}
```

# Approach-2 Better Approach
Instead of calculating the sum again and again, we keep adding the next element to the existing sum.
**Steps:** 
1. Fix the starting index `i` 
2. Initialize `sum = 0` 
3. Extend the subarray by increasing `j` 
4. Add `nums[j]` to sum
5. Update maximum

#### Time complexity: O(N²)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int maxSubArray(int[] nums) {
        int n=nums.length;
        int max=Integer.MIN_VALUE;
        for(int i=0; i<n; i++){
            int sum=0;
            for(int j=i; j<n; j++){
                sum+=nums[j];
                max=max>sum?max:sum; 
            }
        }
        return max;
    }
}
```

# Approach-3 Optimal Approach (using Kadane’s Algorithm)
If the current sum becomes negative, it cannot help us build a larger sum later.

So we reset the sum to 0 and start a new subarray.

**Key Observation** If `sum < 0` → discard it then start new subarray

**Steps**
1. Initialize:
        `sum = 0`
        `max = nums[0]`
2. Traverse the array
3. Add current element to sum
4. Update max
5. If sum < 0 then reset sum = 0


#### Time complexity: O(N)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int maxSubArray(int[] nums) {
        int n=nums.length;
        int sum=0, max=nums[0];
        for(int i=0; i<n; i++){
            if(sum<0)
                sum=0;
            sum+=nums[i];
            if(sum>max)
                max=sum;
        }
        return max;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n=nums.size();
        int sum=0, max=nums[0];
        for(int i=0; i<n; i++){
            if(sum<0)
                sum=0;
            sum+=nums[i];
            if(sum>max)
                max=sum;
        }
        return max;
    }
};
```


# JavaScript Code
```JavaScript []
var maxSubArray = function(nums) {
    let n=nums.length;
    int sum=0, max=nums[0];
    for(let i=0; i<n; i++){
        if(sum<0)
            sum=0;
        sum+=nums[i];
        if(sum>max)
            max=sum;
    }
    return max;
};
```
