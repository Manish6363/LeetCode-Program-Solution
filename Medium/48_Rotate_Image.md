## Problem 
You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

link: https://leetcode.com/problems/rotate-image/description/

# Intuition
To rotate a matrix 90° clockwise, observe the pattern:
- First row → Last column
- Second row → Second last column
- and so on...


# Approach-1 Brute Force [using Extra Matrix]
Create a new matrix and directly place elements in their rotated positions.
**Steps**
1. Create a new matrix `res[n][n]` 
2. Traverse original matrix 
3. Place each element at correct rotated position 
4. Copy `res` back into original matrix (since in-place is required)

**Mapping Rule:** `res[j][n-i-1]=matrix[i][j];`

#### Time complexity: O(M x N)
#### Space complexity: O(M x N)


## Java Code
```Java []
class Solution {
    public void rotate(int[][] matrix) {
        int n=matrix.length;
        int[][] res=new int[n][n];
        for(int i=0; i<n; i++) {
            for(int j=0; j<n; j++) {
                res[j][n-i-1]=matrix[i][j];
            }
        }
        for(int i=0; i<n; i++) {
            for(int j=0; j<n; j++) {
                matrix[i][j]=res[i][j];
            }
        }
    }
}
```


# Approach-2 Optimal Approach [using Transpose & Reverse the Matrix]
1. Convert rows into columns
    - Swap elements across diagonal: `matrix[i][j] ↔ matrix[j][i]`
    Swap only when `j > i` to avoid double swapping.
2. Reverse Each Row using two pointers:

        start = 0, end = n-1
        swap until start < end

#### Time complexity: O(M x N)
#### Space complexity: O(1)

## Java Code
```Java []
class Solution {
    public void rotate(int[][] matrix) {
        int n=matrix.length;
        for(int i=0; i<n-1; i++) {
            for(int j=i+1; j<n; j++) {
                int temp=matrix[i][j];
				matrix[i][j]=matrix[j][i];
				matrix[j][i]=temp;
            }
        }
        for(int i=0; i<n; i++) {
		    int start=0, end=n-1;
		    while(start<=end){
		        int temp=matrix[i][start];
		        matrix[i][start]=matrix[i][end];
		        matrix[i][end]=temp;
		        start++;
		        end--;
		    }
		}
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for(int i = 0; i < n - 1; i++) {
            for(int j = i + 1; j < n; j++) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        for(int i = 0; i < n; i++) {
            int start = 0, end = n - 1;
            while(start < end) {
                swap(matrix[i][start], matrix[i][end]);
                start++;
                end--;
            }
        }
    }
};
```


# JavaScript Code
```JavaScript []
var rotate = function(matrix) {
    const n = matrix.length;
    for (let i = 0; i < n - 1; i++) {
        for (let j = i + 1; j < n; j++) {
            let temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
    for (let i = 0; i < n; i++) {
        let start = 0, end = n - 1;
        while (start < end) {
            let temp = matrix[i][start];
            matrix[i][start] = matrix[i][end];
            matrix[i][end] = temp;
            start++;
            end--;
        }
    }
};
```
