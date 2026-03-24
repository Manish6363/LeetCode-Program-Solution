## Problem 
Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.

- Example 1:
    - $$Input:$$ `nums = [1,1,1], k = 2`
    - $$Output:$$ 2

- Example 2:
    - $$Input:$$ `nums = [9,4,20,3,10,5], k = 33`
    - $$Output:$$ 2

link: https://leetcode.com/problems/subarray-sum-equals-k/description/

https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1

# Intuition
We need to return the total number of subarrays whose `sum` is equal to the given `K`.

# Approach-1 Brute Force
This uses three loops.
**Steps:**
1. Generate all possible subarrays 
2. Calculate the sum of each subarray 
3. If `sum` equals `k`, increment `count` 

#### Time complexity: O(N³)
#### Space complexity: O(1)

## Java Code
```Java []
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        int count = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int sum = 0;
                for (int k = i; k <= j; k++) {
                    sum += nums[k];
                }
                if (sum == k) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

# Approach-2 Better Approach
Instead of recalculating the sum every time:
**Steps:**
1. Fix starting index `i`
2. Keep adding elements to running `sum`, if `sum` equals `k`, increment `count`


#### Time complexity: O(N²)
#### Space complexity: O(1)

## Java Code
```Java []
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        int count = 0;
        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                if (sum == k) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

# Approach-3 Optimal Approach [using Prefix Sum + HashMap]
Instead of checking every subarray:
- We store prefix sums in a HashMap.
- We use the formula: `previousSum = currentSum - k`
- If that previous `sum` exists → we found a subarray.

**$$Use$$ HashMap<sum, frequency>**

**Algorithm**
1. Initialize: `map.put(0, 1)`
2. Traverse array and add number to `sum`
3. Check `if (map contains (sum - k))` then `count += frequency`
4. Store current `sum` in map

#### Time complexity: O(N)
#### Space complexity: O(N)

## Java Code
```Java []
class Solution {
    public int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int sum = 0, count = 0;
        map.put(0, 1);
        for (int num : nums) {
            sum += num;
            if (map.containsKey(sum - k)) {
                count += map.get(sum - k);
            }
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        int count = 0;
        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                if (sum == k) {
                    count++;
                }
            }
        }
        return count;
    }
};
```


# JavaScript Code
```JavaScript []
var subarraySum = function(nums, k) {
    let n = nums.length;
    let count = 0;
    for (let i = 0; i < n; i++) {
        let sum = 0;
        for (let j = i; j < n; j++) {
            sum += nums[j];
            if (sum == k) {
                count++;
            }
        }
    }
    return count;
};
```
