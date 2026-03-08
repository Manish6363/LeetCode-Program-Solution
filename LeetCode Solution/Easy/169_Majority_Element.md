## Problem
Given an array nums of size n, return the majority element.
The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

link: https://leetcode.com/problems/majority-element/description/

# Intuition
If an element appears more than n/2 times, it dominates the array.
This means that even if all other elements are paired against it, it will still remain.

# Approach-1 Brute Force
For every element, count how many times it appears in the array.

If count > n/2 → return that element.

**Steps**
- Iterate through the array.
- For each element `nums[i]`, count its frequency by scanning the entire array.
- If `frequency > n/2`, return the element.

#### Time complexity: O(n²)
#### Space complexity: O(1)

## Java Code
```Java []
class Solution {
    public int majorityElement(int[] nums) {
        int n = nums.length;
        for(int i = 0; i < n; i++){
            int count = 0;
            for(int j = 0; j < n; j++){
                if(nums[i] == nums[j])
                    count++;
            }
            if(count > n/2)
                return nums[i];
        }
        return -1;
    }
}
```

# Approach-2 Better Approach [using Hashing]
Use a **HashMap** to **store frequency of each element**.
**Steps**
- Create a `HashMap<element, frequency>`.
- Traverse the array and update frequency.
- Check if any element `frequency > n/2`.
- Return that element.

#### Time complexity: O(n)
#### Space complexity: O(n) `But O(1) in average`

## Java Code
```Java []
import java.util.*;

class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() > nums.length/2)
                return entry.getKey();
        }
        return -1;
    }
}
```

# Approach-3 More Better Approach [using Sorting]
If an **element occurs more than n/2 times**, after sorting it must occupy the **middle index**.

**Steps**
- Sort the array.
- Return element at index n/2.

#### Time complexity: O(n log n) `depends on sorting algorithm`
#### Space complexity: O(log n)


## Java Code
```Java []
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```


# Approach-4 Optimal Approach [using Moore’s Voting Algorithm]

#### Time complexity: O()
#### Space complexity: O()
This is the most important interview solution.

**Idea:**
- Majority element dominates the array.
- Every time we see a different element, we cancel one vote.

**Steps**

1. Initialize:
        `candidate = 0`
        `count = 0`

2. Traverse array 
    - `if count == 0` choose current element as candidate.
    - `if element == candidate` then `count++`
    - otherwise `count--`

3. After traversal candidate is the majority element.

Optional: verify by counting again.

## Java Code
```Java []
class Solution {
    public int majorityElement(int[] nums) {
        int candidateElem = 0;
        int count = 0;
        for(int num : nums){
            if(count == 0)
                candidateElem = num;
            if(num == candidateElem)
                count++;
            else
                count--;
        }
        return candidateElem;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidateElem = 0;
        int count = 0;
        for(int num : nums){
            if(count == 0)
                candidateElem = num;
            if(num == candidateElem)
                count++;
            else
                count--;
        }
        return candidateElem;
    }
};
```


# JavaScript Code
```JavaScript []
var majorityElement = function(nums) {
    let candidateElem = 0;
    let count = 0;
    for(let num of nums){
        if(count == 0)
            candidateElem = num;
        if(num == candidateElem)
            count++;
        else
            count--;
    }
    return candidateElem;
};
```
