## Problem
A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for `arr = [1,2,3]`, the following are all the permutations of arr: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.

link: https://leetcode.com/problems/next-permutation/description/

# Intuition
To find the next permutation, we need to generate the next lexicographically greater arrangement of the numbers.

If we observe permutations carefully, we notice that:
- The rightmost part of the array is usually in decreasing order when we reach the last permutations.
- To get the next permutation, we must modify the array from the right side, because changing elements on the left would produce a much larger permutation instead of the immediate next one.

# Approach-1 Brute Force
**Steps:**
1. Generate all permutations of the array. 
2. Sort them lexicographically. 
3. Find the current permutation. 
4. Return the next permutation in the list. 
5. If it is the last permutation then return the first permutation.


Example: `nums = [1,2,3]`

    All permutations: [1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]
    If input = [1,2,3] then Next → [1,3,2]
    If input = [3,2,1] then Next → [1,2,3]

#### Time complexity: O(N! log N!)

    Permutation generation = O(N!)
    Sorting permutations = O(N! log N!)
    Searching = O(N!)
    Total ≈ O(N! log N!)

#### Space complexity: O(N!)



# Approach-2 Optimal Approach
**Steps:**
1. Find first decreasing element (pivot) index from right side of an Array
2. Find the immediate next greater element from right.
3. Reverse right part from the pivot element.

Example: `nums = [1, 3, 5, 4, 2, 0]`
- The First decreasing element (pivot) is 3 at 1st index.
- Immediate Greater element is 4 at 3rd index.
- Swap the 1st index with 3rd index element. `nums = [1, 4, 5, 3, 2, 0]`
- Finally swap the right side of pivot array element: `nums = [1, 4, 0, 2, 3, 5]` which is the next Permutation.

#### Time complexity: O(N)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public void swap(int[] nums, int start, int end){
        while(start<end){
            int temp=nums[start];
            nums[start]=nums[end];
            nums[end]=temp;
            start++;
            end--;
        }
    }
    public void nextPermutation(int[] nums) {
        int searchIndex=-1;
        for(int i=nums.length-1; i>0; i--){
            if(nums[i-1]<nums[i]){
                searchIndex=i-1;
                break;
            }
        }
        if(searchIndex==-1){
            swap(nums, 0, nums.length-1);
        }else{
            int immediateGreatestIndex=searchIndex;
            for(int i=nums.length-1; i>=0; i--){
                if(nums[i]>nums[searchIndex]){
                    immediateGreatestIndex=i;
                    break;
                }
            }
            int temp=nums[searchIndex];
            nums[searchIndex]=nums[immediateGreatestIndex];
            nums[immediateGreatestIndex]=temp;
            swap(nums, searchIndex+1, nums.length-1);
        }
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    void swap(vector<int>& nums, int start, int end){
        while(start < end){
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
    void nextPermutation(vector<int>& nums) {
        int searchIndex = -1;
        for(int i = nums.size()-1; i > 0; i--){
            if(nums[i-1] < nums[i]){
                searchIndex = i-1;
                break;
            }
        }
        if(searchIndex == -1){
            swap(nums, 0, nums.size()-1);
        } 
        else{
            int immediateGreatestIndex = searchIndex;
            for(int i = nums.size()-1; i >= 0; i--){
                if(nums[i] > nums[searchIndex]){
                    immediateGreatestIndex = i;
                    break;
                }
            }
            int temp = nums[searchIndex];
            nums[searchIndex] = nums[immediateGreatestIndex];
            nums[immediateGreatestIndex] = temp;
            swap(nums, searchIndex+1, nums.size()-1);
        }
    }
};
```


# JavaScript Code
```JavaScript []
var nextPermutation = function(nums) {
    function swap(nums, start, end){
        while(start < end){
            let temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
    let searchIndex = -1;
    for(let i = nums.length-1; i > 0; i--){
        if(nums[i-1] < nums[i]){
            searchIndex = i-1;
            break;
        }
    }
    if(searchIndex === -1){
        swap(nums, 0, nums.length-1);
    }
    else{
        let immediateGreatestIndex = searchIndex;
        for(let i = nums.length-1; i >= 0; i--){
            if(nums[i] > nums[searchIndex]){
                immediateGreatestIndex = i;
                break;
            }
        }
        let temp = nums[searchIndex];
        nums[searchIndex] = nums[immediateGreatestIndex];
        nums[immediateGreatestIndex] = temp;

        swap(nums, searchIndex+1, nums.length-1);
    }
};
```
