
## Problem
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.
You must solve this problem without using the library's sort function.

link: https://leetcode.com/problems/sort-colors/submissions/1939872479/

# Intuition
Since the array contains only 0, 1, and 2, we don't need full sorting.

# Approach-1 Brute Force [using Any Sorting Algorithm]
Use any of Sorting technique

#### Time complexity: O(n log n)
#### Space complexity: O(1)

## Java Code
```Java []
class Solution {
    public void sortColors(int[] nums) {
        Arrays.sort(nums);
    }
}
```

# Approach-2 Better Approach
Count the 0s, 1s, 2s and by traversing the array fill the value that many count time in the original array.

#### Time complexity: O(n)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public void sortColors(int[] nums) {
        int zero=0, one=0, two=0;
        for(int i=0; i<nums.length; i++){
            if(nums[i]==0)
                zero++;
            else if(nums[i]==1)
                one++;
            else
                two++;
        }
        for(int i=0; i<nums.length; i++){
            if(i<zero)
                nums[i]=0;
            else if(i<zero+one)
                nums[i]=1;
            else
                nums[i]=2;
        }
    }
}
```

# Approach-3 Optimal Approach (uing Dutch National Flag Algorithm)
Since the array contains only 0, 1, and 2, we don't need full sorting.
We maintain three regions in the array:
 - **0 → low-1** → all 0s (red)
 - **low → mid-1** → all 1s (white)
 - **high+1 → end** → all 2s (blue)

We iterate using a mid pointer and place elements in their correct region using swaps.

Pointers used:

- **low** → position where next 0 should go
- **mid** → current element being processed
- **high** → position where next 2 should go

**Rules:**

    If nums[mid] == 0
        Swap nums[mid] and nums[low]
        Move low++, mid++
    If nums[mid] == 1
        Correct position
        Move mid++
    If nums[mid] == 2
        Swap nums[mid] and nums[high]
        Move high--
        Do not increment mid (because swapped value needs checking)

#### Time complexity: O(n)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public void sortColors(int[] nums) {
        int low = 0;
        int mid = 0;
        int high = nums.length - 1;
        while(mid <= high){
            if(nums[mid] == 0){
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            }
            else if(nums[mid] == 1){
                mid++;
            }
            else{ // nums[mid] == 2
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;
                high--;
            }
        }
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int zero=0, one=0, two=0;
        for(int i=0; i<nums.size(); i++){
            if(nums[i]==0)
                zero++;
            else if(nums[i]==1)
                one++;
            else
                two++;
        }
        for(int i=0; i<nums.size(); i++){
            if(i<zero)
                nums[i]=0;
            else if(i<zero+one)
                nums[i]=1;
            else
                nums[i]=2;
        }
    }
};
```


# JavaScript Code
```JavaScript []
var sortColors = function(nums) {
    let zero=0, one=0, two=0;
    for(let i=0; i<nums.length; i++){
        if(nums[i]==0)
            zero++;
        else if(nums[i]==1)
            one++;
        else
            two++;
    }
    for(let i=0; i<nums.length; i++){
        if(i<zero)
            nums[i]=0;
        else if(i<zero+one)
            nums[i]=1;
        else
            nums[i]=2;
    }
};
```
