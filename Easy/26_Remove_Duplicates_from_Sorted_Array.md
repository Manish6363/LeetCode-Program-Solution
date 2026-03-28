## Problem
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Consider the number of unique elements in nums to be k​​​​​​​​​​​​​​. After removing duplicates, return the number of unique elements k.

The first k elements of nums should contain the unique numbers in sorted order. The remaining elements beyond index k - 1 can be ignored.

link: https://leetcode.com/problems/remove-duplicates-from-sorted-array/

# Intuition
Since the array is already sorted, all duplicate elements appear next to each other.  
So, we can iterate through the array and keep only the first occurrence of each number by overwriting duplicates in-place using two pointers. But we will see all way of solving it.

# Approach-1 Brute Force Approach
- Create a temporary array / list.
- Traverse the array and store only unique values. 
- Copy the result back into the original array. 

This is not in-place, but easiest to understand. This approach is not allowed as per problem constraints because it uses extra space.

#### Time complexity: **O(n)**
#### Space complexity: **O(n)**
## Java Code
```java []
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int[] temp = new int[nums.length];
        int k = 0;
        temp[k++] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[i - 1]) {
                temp[k++] = nums[i];
            }
        }
        for (int i = 0; i < k; i++) {
            nums[i] = temp[i];
        }
        return k;
    }
}
```

# Approach-2 Better Approach (Shifting Elements In-place)
Traverse array.
When a new unique element appears, shift it left.
Since array is sorted, we don't really need nested loop — which leads directly to Approach-3.

#### Time complexity: **O(n²)**
#### Space complexity: **O(1)**
## Java Code
```java []
class Solution {
    public int removeDuplicates(int[] nums) {
        int k = 0;
        for (int i = 0; i < nums.length; i++) {
            boolean isDuplicate = false;
            for (int j = 0; j < k; j++) {
                if (nums[i] == nums[j]) {
                    isDuplicate = true;
                    break;
                }
            }
            if (!isDuplicate) {
                nums[k++] = nums[i];
            }
        }
        return k;
    }
}
```

# Approach-3 Optimal Approach (using Two Pointer)
**Why two pointers?**
Since array is sorted, all duplicates are adjacent. Two pointers allow us to overwrite duplicates in-place while maintaining order and using O(1) extra space.
Already array is sorted, duplicates are adjacent.
- i → last unique index
- j → scan pointer

Whenever a new element is found, move it forward.

#### Time complexity: **O(n)**
#### Space complexity: **O(1)**
## Java Code
```java []
class Solution {
    public int removeDuplicates(int[] nums) {
        int i=0;
        for(int j=1; j<nums.length; j++){
            if(nums[i]!=nums[j]){
                i++;
                nums[i]=nums[j];
            }
        }
        return i+1;
    }
}
```

## CPP / C++ Code
```cpp []
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int i = 0;
        for (int j = 1; j < nums.size(); j++) {
            if (nums[i] != nums[j]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
};
```

## JavaScript Code
```javascript []
var removeDuplicates = function(nums) {
    let i = 0;
    for (let j = 1; j < nums.length; j++) {
        if (nums[i] !== nums[j]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
};
```
