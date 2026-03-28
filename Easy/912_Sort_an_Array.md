## Problem
Given an integer array nums, sort it in ascending order.
You must **not use built-in sort functions**, achieve **O(n log n)** time complexity, and use minimum extra space.

link: https://leetcode.com/problems/sort-an-array/submissions/1929693223/

# Intuition
The goal is to sort an array efficiently without using built-in sorting functions, in:
- Time Complexity: O(n log n)
- Space Complexity: As small as possible

To achieve this, Merge Sort is one of the best choices.

# Approach-1: Merge Sort (Stable, Guaranteed O(n log n))
- Merge Sort uses divide and conquer:
    1. Divide the array into two halves.
    2. Recursively sort each half.
    3. Merge the two sorted halves.
- This guarantees O(n log n) time in all cases.

![image.png](https://assets.leetcode.com/users/images/78d4b410-0044-43a0-a6cf-0bf0be8c4cf6_1771942092.3742244.png)

### Time complexity: **O(n log n)**
### Space complexity: **O(n)**


# Java Code
```java []
class Solution {
    public int[] sortArray(int[] nums) {
        mergeSort(nums, 0, nums.length - 1);
        return nums;
    }
    private void mergeSort(int[] arr, int left, int right) {
        if (left >= right) 
            return;
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }

    private void merge(int[] arr, int left, int mid, int right) {
        int[] temp = new int[right - left + 1];
        int i = left, j = mid + 1, k = 0;
        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) 
                temp[k++] = arr[i++];
            else 
                temp[k++] = arr[j++];
        }
        while (i <= mid) 
            temp[k++] = arr[i++];
        while (j <= right) 
            temp[k++] = arr[j++];
        // Copy into original array
        for (int p = 0; p < temp.length; p++) {
            arr[left + p] = temp[p];
        }
    }
}
```


# CPP / C++
``` Cpp []
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }

private:
    void mergeSort(vector<int>& arr, int start, int end) {
        if (start >= end) return;

        int mid = start + (end - start) / 2;

        mergeSort(arr, start, mid);
        mergeSort(arr, mid + 1, end);
        merge(arr, start, mid, end);
    }

    void merge(vector<int>& arr, int start, int mid, int end) {
        int left = start, right = mid + 1;
        vector<int> temp;

        while (left <= mid && right <= end) {
            if (arr[left] < arr[right])
                temp.push_back(arr[left++]);
            else
                temp.push_back(arr[right++]);
        }

        while (left <= mid) 
	    temp.push_back(arr[left++]);
        while (right <= end) 
	    temp.push_back(arr[right++]);

        for (int i = 0; i < temp.size(); i++) {
            arr[start + i] = temp[i];
        }
    }
};
```


# JavaScript
``` JavaScript []
var sortArray = function(nums) {
    mergeSort(nums, 0, nums.length - 1);
    return nums;
};

function mergeSort(arr, start, end) {
    if (start >= end) return;

    const mid = Math.floor(start + (end - start) / 2);

    mergeSort(arr, start, mid);
    mergeSort(arr, mid + 1, end);
    merge(arr, start, mid, end);
}

function merge(arr, start, mid, end) {
    let left = start;
    let right = mid + 1;
    let res = [];

    while (left <= mid && right <= end) {
        if (arr[left] < arr[right]) {
            res.push(arr[left++]);
        } else {
            res.push(arr[right++]);
        }
    }

    while (left <= mid) 
	res.push(arr[left++]);
    while (right <= end) 
	res.push(arr[right++]);

    for (let i = 0; i < res.length; i++) {
        arr[start + i] = res[i];
    }
}
```
