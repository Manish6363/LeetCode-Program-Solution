## Problem 
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.
You must write an algorithm that runs in O(n) time.

Example 1:
- $$Input$$: `nums = [100,4,200,1,3,2]`
- $$Output$$: 4
**Explanation**: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

link: https://leetcode.com/problems/longest-consecutive-sequence/description/

# Intuition
The goal is to find the **longest sequence of consecutive integers** in an unsorted array.

Example: `arr=[100,4,200,1,3,2]`
If we rearrange logically: `[1,2,3,4]` → length 4

**Key observations:**
- The numbers do not need to be adjacent in the array, only numerically consecutive.
- We only care about sequence length, not the sequence itself.
- A sequence starts only when there is no previous number (num - 1).

# Approach-1 Brute Force
For every element:
1. Assume it is the start of a sequence.
2. Keep checking if elem+1 exists in the array.
3. Continue until the next element is not found.

#### Time complexity: O(N²)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int longestConsecutive(int[] arr) {
        int longest = 0;
        for(int i=0;i<arr.length;i++){
            int count = 1;
            int elem = arr[i];
            while(isPresent(arr, elem + 1)){
                elem++;
                count++;
            }
            longest = Math.max(longest, count);
        }
        return longest;
    }
    private boolean isPresent(int[] arr, int target) {
        for (int num : arr) {
            if (num == target)
                return true;
        }
        return false;
    }
}
```

# Approach-2 Better Approach [using Sorting]
**Steps:**
1. Sort the array
2. Traverse and count consecutive numbers.

#### Time complexity: O(N log N)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int longestConsecutive(int[] arr) {
        if(arr.length==1){
            return 1;
        }
        else if (arr.length > 1) {
            Arrays.sort(arr);
            int longest = 0;
            int count = 1;
            for (int i = 1; i < arr.length; i++) {
                if (arr[i] == arr[i - 1] + 1) {
                    count++;
                } else if (arr[i] != arr[i - 1]) {
                    count = 1;
                }
                if(count>longest)
                    longest = count;
            }
            return longest;
        }
        return 0;
    }
}
```

# Approach-3 Optimal Approach [using HashSet]
**Steps:**
1. Put all numbers into a **HashSet** for **O(1) lookup**.
2. Only start counting when the number is **start of sequence**.

#### Time complexity: O(N)
- **Why O(N)?**
Each number is visited at most twice:
    - Once during iteration
    - Once during sequence expansion
#### Space complexity: O(N)


## Java Code
```Java []
class Solution {
    public int longestConsecutive(int[] arr) {
        HashSet<Integer> set = new HashSet<>();
        for(int num : arr)
            set.add(num);
        int longest = 0;
        for(int num : set){
            if(!set.contains(num - 1)){
                int current = num;
                int count = 1;
                while(set.contains(current + 1)){
                    current++;
                    count++;
                }
                longest = Math.max(longest, count);
            }
        }
        return longest;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> st(nums.begin(), nums.end());
        int longest = 0;
        for(int num : st) {
            if(st.find(num - 1) == st.end()) {
                int current = num;
                int count = 1;
                while(st.find(current + 1) != st.end()) {
                    current++;
                    count++;
                }
                longest = max(longest, count);
            }
        }
        return longest;
    }
};
```


# JavaScript Code
```JavaScript []
var longestConsecutive = function(nums) {
    let set = new Set(nums);
    let longest = 0;
    for(let num of set){
        if(!set.has(num - 1)){
            let current = num;
            let count = 1;
            while(set.has(current + 1)){
                current++;
                count++;
            }
            longest = Math.max(longest, count);
        }
    }
    return longest;
};
```
