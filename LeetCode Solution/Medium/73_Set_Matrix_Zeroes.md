## Problem
Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.
You must do it in place.

link: https://leetcode.com/problems/set-matrix-zeroes/description/


# Intuition
If we immediately convert the whole row and column to 0 when we encounter a 0, newly created zeros may affect other rows and columns incorrectly.

**So the idea is:**
1. **Mark cells that should become zero** using a temporary marker ('*') for all type of array but for positive array use marker -1.
2. After scanning the matrix, convert all markers to 0.

Another better idea is to **store rows and columns containing zero** and then update the matrix.

# Approach-1 Brute Force
Step: 
1. Traverse the matrix.
2. Whenever 0 is found:
    - Mark the entire row and column with a temporary value (**'*'**).
3. In the second pass convert **'*'** → 0.

#### Time complexity: O(N³)
Traversing the matrix → O(M × N) 
For every 0 we traverse: entire row → O(N) entire column → O(M) 
So worst case: **O(M × N × (M + N))**

#### Space complexity: O(1)

## Java Code
```Java []
class Solution {
    
    private void markRow(int[][] matrix, int i){
        for(int j=0; j<matrix[0].length; j++){
            if(matrix[i][j] != 0)
                matrix[i][j] = '*';
        }
    }
    
    private void markColumn(int[][] matrix, int j){
        for(int i=0; i<matrix.length; i++){
            if(matrix[i][j] != 0)
                matrix[i][j] = '*';
        }
    }
    
    public void setZeroes(int[][] matrix) {
        int rows=matrix.length;
        int cols=matrix[0].length;

        for(int i=0; i<rows; i++) {
            for(int j=0; j<cols; j++) {
                if(matrix[i][j]==0){
                    markColumn(matrix, j);
                    markRow(matrix, i);
                }
            }
        }
        
        for(int i=0; i<rows; i++) {
            for(int j=0; j<cols; j++) {
                if(matrix[i][j]=='*'){
                    matrix[i][j]=0;
                }
            }
        }
    }
}
```


# Approach-2 Optimal Approach 
**Step:**
Instead of modifying the matrix during traversal:
1. Store rows containing 0
2. Store columns containing 0
3. In the second pass set them to zero.

#### Time complexity: O(M × N)
#### Space complexity: O(M+N)


## Java Code
```Java []
class Solution {
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;

        int[] row = new int[rows];
        int[] col = new int[cols];

        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(matrix[i][j] == 0){
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        for(int i = 0; i < rows; i++){
            for(int j = 0; j < cols; j++){
                if(row[i] == 1 || col[j] == 1){
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {

        int rows = matrix.size();
        int cols = matrix[0].size();

        vector<int> row(rows,0);
        vector<int> col(cols,0);

        for(int i=0;i<rows;i++){
            for(int j=0;j<cols;j++){
                if(matrix[i][j]==0){
                    row[i]=1;
                    col[j]=1;
                }
            }
        }

        for(int i=0;i<rows;i++){
            for(int j=0;j<cols;j++){
                if(row[i]==1 || col[j]==1){
                    matrix[i][j]=0;
                }
            }
        }
    }
};
```


# JavaScript Code
```JavaScript []
var setZeroes = function(matrix) {

    let rows = matrix.length;
    let cols = matrix[0].length;

    let row = new Array(rows).fill(0);
    let col = new Array(cols).fill(0);

    for(let i=0;i<rows;i++){
        for(let j=0;j<cols;j++){
            if(matrix[i][j] === 0){
                row[i] = 1;
                col[j] = 1;
            }
        }
    }

    for(let i=0;i<rows;i++){
        for(let j=0;j<cols;j++){
            if(row[i] === 1 || col[j] === 1){
                matrix[i][j] = 0;
            }
        }
    }
};
```
