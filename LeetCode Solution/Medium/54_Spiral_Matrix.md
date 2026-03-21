## Problem 
Given an m x n matrix, return all elements of the matrix in spiral order.

link: https://leetcode.com/problems/spiral-matrix/description/

# Intuition
Think of the matrix as having 4 boundaries:
- **top** → first row 
- **bottom** → last row 
- **left** → first column 
- **right** → last column

We traverse in 4 directions repeatedly:
1. Left → Right (top row)
2. Top → Bottom (right column)
3. Right → Left (bottom row)
4. Bottom → Top (left column)

After each traversal, we shrink the boundary.
We stop when: `left > right OR top > bottom`

# Approach-1 Optimal Approach [using Boundries]

![image.png](https://assets.leetcode.com/users/images/3b59a04d-0c91-420c-a506-e30c4008ff75_1774078202.5008864.png)

#### Time complexity: O(N x M)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List list=new ArrayList<>();
		int left=0, right=matrix[0].length-1;
		int top=0, bottom=matrix.length-1;
		while(left<=right && top<=bottom){
		    // Top row: Left → Right
            for (int i = left; i <= right; i++)
                list.add(matrix[top][i]);
            top++;
		    // Right column: Top → Bottom
            for (int i = top; i <= bottom; i++)
                list.add(matrix[i][right]);
            right--;
		    // Bottom row: Right → Left
            if (top <= bottom) {
                for (int i = right; i >= left; i--)
                    list.add(matrix[bottom][i]);
                bottom--;
            }
            // Left column: Bottom → Top
            if (left <= right) {
                for (int i = bottom; i >= top; i--)
                    list.add(matrix[i][left]);
                left++;
            }            
		}
        return list;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> result;
        int top = 0;
        int bottom = matrix.size() - 1;
        int left = 0;
        int right = matrix[0].size() - 1;
        while (left <= right && top <= bottom) {
            // Top row: Left → Right
            for (int i = left; i <= right; i++) {
                result.push_back(matrix[top][i]);
            }
            top++;
            // Right column: Top → Bottom
            for (int i = top; i <= bottom; i++) {
                result.push_back(matrix[i][right]);
            }
            right--;
            // Bottom row: Right → Left
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    result.push_back(matrix[bottom][i]);
                }
                bottom--;
            }
            // Left column: Bottom → Top
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    result.push_back(matrix[i][left]);
                }
                left++;
            }
        }
        return result;
    }
};
```


# JavaScript Code
```JavaScript []
var spiralOrder = function(matrix) {
    let result = [];
    let top = 0;
    let bottom = matrix.length - 1;
    let left = 0;
    let right = matrix[0].length - 1;
    while (left <= right && top <= bottom) {
        // Top row: Left → Right
        for (let i = left; i <= right; i++) {
            result.push(matrix[top][i]);
        }
        top++;
        // Right column: Top → Bottom
        for (let i = top; i <= bottom; i++) {
            result.push(matrix[i][right]);
        }
        right--;
        // Bottom row: Right → Left
        if (top <= bottom) {
            for (let i = right; i >= left; i--) {
                result.push(matrix[bottom][i]);
            }
            bottom--;
        }
        // Left column: Bottom → Top
        if (left <= right) {
            for (let i = bottom; i >= top; i--) {
                result.push(matrix[i][left]);
            }
            left++;
        }
    }
    return result;
};
```
