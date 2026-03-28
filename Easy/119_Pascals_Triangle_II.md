## Problem 
Given an integer rowIndex, return the rowIndexth (0-indexed) row of the Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

link: https://leetcode.com/problems/pascals-triangle-ii/description/

# Intuition
Each number in Pascal’s Triangle is calculated using: 
        `value = above_left + above_right`

# Approach-1 Brute Force [by Building Entire Pascal Triangle]
Generate all rows from 0 to rowIndex, then return the last row.

**Steps**
1. Create a list to store rows.
2. Loop from 0 to rowIndex. 
3. For each row: 
    - First and last element = 1 
    - Middle elements = sum of previous row elements. 
5. Return last row.

#### Time complexity: O(N²)
#### Space complexity: O(N²)

## Java Code
```Java []
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<List<Integer>> triangle = new ArrayList<>();
        for (int i = 0; i <= rowIndex; i++) {
            List<Integer> row = new ArrayList<>();
            for (int j = 0; j <= i; j++) {
                if (j == 0 || j == i) {
                    row.add(1);
                } else {
                    row.add(triangle.get(i - 1).get(j - 1) + triangle.get(i - 1).get(j));
                }
            }
            triangle.add(row);
        }
        return triangle.get(rowIndex);
    }
}
```

# Approach-2 Better Approach [using Single Array]

**Steps:** 
1. Create list. 
2. Add 1. 
3. For each new row: 
    - Traverse backward.
    - Update values using previous values. 
    - Add 1 at the end.

#### Time complexity: O(N²)
#### Space complexity: O(N)


## Java Code
```Java []
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> row = new ArrayList<>();
        row.add(1);
        for (int i = 1; i <= rowIndex; i++) {
            for (int j = i - 1; j > 0; j--) {
                row.set(j, row.get(j) + row.get(j - 1));
            }
            row.add(1);
        }
        return row;
    }
}
```

# Approach-3 Optimal Approach [using Combination Formula]

Key Formula Each element in Pascal’s row: 

               n!
    C(n,r)= ---------
            r!(n−r)!  ​ 

But computing factorial repeatedly is slow. 
Instead use: `next = previous × ((n−r)/r+1)`
This lets us compute values sequentially.

**Steps:** 
1. Start with 1.
2. Use formula to compute next value.
3. Repeat until row ends.

#### Time complexity: O(N)
#### Space complexity: O(N)

## Java Code
```Java []
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> row = new ArrayList<>();
        long value = 1;
        row.add(1);
        for (int r = 0; r < rowIndex; r++) {
            value = value * (rowIndex - r);
            value = value / (r + 1);
            row.add((int) value);
        }
        return row;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> row;
        long long value = 1;
        row.push_back(1);
        for (int r = 0; r < rowIndex; r++) {
            value = value * (rowIndex - r);
            value = value / (r + 1);
            row.push_back(value);
        }
        return row;
    }
};
```


# JavaScript Code
```JavaScript []
var getRow = function(rowIndex) {
    let row = [];
    let value = 1;
    row.push(1);
    for (let r = 0; r < rowIndex; r++) {
        value = value * (rowIndex - r);
        value = Math.floor(value / (r + 1));
        row.push(value);
    }
    return row;
};
```
