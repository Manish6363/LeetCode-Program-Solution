## Problem
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

link: https://leetcode.com/problems/two-sum/

# Intuition
We need to find **two numbers whose sum equals target**.

# Approach-1 Brute Force
Check every pair of elements and see if their sum equals the target.

#### Time complexity: O(n²)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0; i<nums.length; i++){
            for(int j=i+1; j<nums.length; j++){
                if(nums[i]+nums[j]==target){
                    return new int[] {i, j};
                }
            }
        }
        return new int[] {-1, -2};;
    }
}
```

# Approach-2 Better Approach [using Map]
Instead of checking all pairs, store elements in a HashMap.
For each element:
- Calculate the needed value
- Check if it already exists in the map.

**Optimal for Unsorted Array**

#### Time complexity: O(n)
#### Space complexity: O(n)


## Java Code
```Java []
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            int need = target - nums[i];
            if(map.containsKey(need)){
                return new int[]{map.get(need), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{-1,-1};
    }
}
```

# Approach-3 Optimal Approach [using Two Pointer (Array must be sorted)]
Use two pointers but array should be sorted.

#### Time complexity: O(n)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right){
            int sum = nums[left] + nums[right];
            if(sum == target){
                return new int[]{left, right};
            }
            else if(sum < target){
                left++;
            }
            else{
                right--;
            }
        }
        return new int[]{-1,-1};
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) { 
        unordered_map<int,int> map;
        for(int i = 0; i < nums.size(); i++){
            int need = target - nums[i];
            if(map.find(need) != map.end()){
                return {map[need], i};
            }
            map[nums[i]] = i;
        }
        return {-1,-1};
    }
};
```


# JavaScript Code
```JavaScript []
var twoSum = function (nums, target) {
    let map = new Map();
    for (let i = 0; i < nums.length; i++) {
        let need = target - nums[i];
        if (map.has(need)) {
            return [map.get(need), i];
        }
        map.set(nums[i], i);
    }
    return [-1, -1];
};
```
