## Problem
Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

- Example 1:
    - Input: nums = [1,2,3,4,5,6,7], k = 3
    - Output: [5,6,7,1,2,3,4]
        Explanation:
            - rotate 1 steps to the right: [7,1,2,3,4,5,6]
            - rotate 2 steps to the right: [6,7,1,2,3,4,5]
            - rotate 3 steps to the right: [5,6,7,1,2,3,4]

link: https://leetcode.com/problems/rotate-array/description/


# Intuition
Right rotation by k means:
- The last k elements move to the front
- The remaining elements shift right


# Approach-1: Brute Force (Using Extra Array)
- Store last k elements to a temporary array
- Shift remaining elements to right in original array
- Copy all stored elements from temporary array to front of original array
#### Time complexity: **O(n)**
#### Space complexity: **O(k)**

## Java Code
```Java []
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        int temp[] = new int[k];
        // store last k elements
        for (int i = n - k; i < n; i++) {
            temp[i - (n - k)] = nums[i];
        }
        // shift remaining elements right
        for (int i = n - k - 1; i >= 0; i--) {
            nums[i + k] = nums[i];
        }
        // copy temp back
        for (int i = 0; i < k; i++) {
            nums[i] = temp[i];
        }
    }
}
```

# Approach-2: Optimal Approach (Reversal Algorithm)
- Rotate array to the right by k steps.
    ```nums = [1,2,3,4,5,6,7], k = 3```
- Reverse the array in 3 steps.
    - **Step 1** → Reverse last **k** elements
                `Last 3 elements → [5,6,7]`
                `nums = [1,2,3,4, 7, 6, 5]`
    - **Step 2** → Reverse first **n - k **elements
                `First 4 elements → [1,2,3,4]`
                `nums = [4, 3, 2, 1, 7, 6, 5]`
    - **Step 3** → Reverse entire array
                `nums = [5, 6, 7, 1, 2, 3, 4]`


#### Time complexity: **O(n)**
#### Space complexity: **O(1)**

## Java Code
```Java []
class Solution {
    public void reverse(int[] arr, int start, int end){
        while(start<end){
            int temp=arr[start];
            arr[start]=arr[end];
            arr[end]=temp;
            start++;
            end--;
        }
    } 
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        reverse(nums, n-k, n-1);
        reverse(nums, 0, n-k-1);
        reverse(nums, 0, n-1);
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    void reverse(vector<int>& arr, int start, int end) {
        while (start < end) {
            swap(arr[start], arr[end]);
            start++;
            end--;
        }
    }
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n;
        reverse(nums, n - k, n - 1);
        reverse(nums, 0, n - k - 1);
        reverse(nums, 0, n - 1);
    }
};
```

## JavaScript Code
```JavaScript []
var reverse = function(arr, start, end) {
    while (start < end) {
        let temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
};

var rotate = function(nums, k) {
    let n = nums.length;
    k = k % n;
    reverse(nums, n - k, n - 1);
    reverse(nums, 0, n - k - 1);
    reverse(nums, 0, n - 1);
};
```
