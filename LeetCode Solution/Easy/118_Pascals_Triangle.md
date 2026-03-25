## Problem 
Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

link: https://leetcode.com/problems/pascals-triangle/description/


# Intuition
Each number in Pascal’s Triangle follows the rule: 

            n!
    nCr =----------
          r!(n−r)!
​here, `n` represents row and `r` represents the column

**Key Pattern Rule:**
- First element of every row = 1
- Last element of every row = 1
- Middle element: `value=previousRow[j−1]+previousRow[j]`

Examples: `n=5`

    Row 0:        1
    Row 1:       1 1
    Row 2:      1 2 1
    Row 3:     1 3 3 1
    Row 4:    1 4 6 4 1

# Approach-1 Brute Force [using nCr Formula]
For each row `i` and each column `j` Compute: $$value=nCr(i,j)$$  
So every element is calculated independently.

**Algorithm**
1. Create result list 
2. Loop rows from 0 to numRows-1 
3. For each row: 
    - Create new list 
    - Loop columns from 0 to row 
    - Calculate nCr(row, col) 
    - Add to row list 
4. Add row list to result 
4. Return result

#### Time complexity: O(N³)
    Outer loop -> N
    Inner loop -> N
    nCr calculation loop -> N
    so, N x N x N = N³
#### Space complexity: O(N²)

## Java Code
```Java []
class Solution {
    private static int nCr(int n, int r) {
        long res=1;
        for(int i=0; i<r; i++) {
            res*=(n-i);
            res/=(i+1);
        }
        return (int)res;
    }
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res=new ArrayList<>();
	    for(int i=0; i<numRows; i++) {
	        ArrayList<Integer> temp=new ArrayList<>();
	        for(int j=0; j<=i; j++) {
	           temp.add(nCr(i, j));
	        }
	       res.add(temp);
	    }
        return res;
    }
}
```

# Approach-2 Optimal Approach [using Mathematical Row Generation]
Instead of factorial:
Use recurrence relation: `next = previous × ((row−col​)/col+1)`

This is Optimal Because:
- No factorial 
- No extra loops 
- No previous row needed 
- Constant calculation per element

**Algorithm:**
For each row: 
1. Start with: res = 1 
2. Add first element: 1 
3. For each column:
    `res = res * (row - i) `
    `res = res / (i + 1) `
4. Add result to list

#### Time complexity: O(N²)
#### Space complexity: O(N²)

## Java Code
```Java []
class Solution {
    private static ArrayList<Integer> nCRow(int row) {
        ArrayList<Integer> list=new ArrayList<>();
        int res=1;
        list.add(res);
        for(int i=0; i<row; i++) {
            res*=(row-i);
            res/=(i+1);
            list.add(res);
        }
        return list;
    }
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res=new ArrayList<>();
	    for(int i=0; i<numRows; i++) {
	        res.add(nCRow(i));
	    }
        return res;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    static vector<int> nCRow(int row) {
        vector<int> list;
        int res = 1;
        list.push_back(res);
        for (int i = 0; i < row; i++) {
            res = res * (row - i);
            res = res / (i + 1);
            list.push_back(res);
        }
        return list;
    }
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> res;
        for (int i = 0; i < numRows; i++) {
            res.push_back(nCRow(i));
        }
        return res;
    }
};
```


# JavaScript Code
```JavaScript []
var generate = function(numRows) { 
    function nCRow(row) {
        let list = [];
        let res = 1;
        list.push(res);
        for (let i = 0; i < row; i++) {
            res = res * (row - i);
            res = Math.floor(res / (i + 1));
            list.push(res);
        }
        return list;
    }
    let result = [];
    for (let i = 0; i < numRows; i++) {
        result.push(nCRow(i));
    }
    return result;
};
```
