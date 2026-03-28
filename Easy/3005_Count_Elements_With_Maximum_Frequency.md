## Problem: 
You are given an array nums consisting of positive integers. Return the total frequencies of elements in nums such that those elements all have the maximum frequency. 
The frequency of an element is the number of occurrences of that element in the array.

link: https://leetcode.com/problems/count-elements-with-maximum-frequency/


# Intuition
Count how many times each number appears → find the highest frequency → add all frequencies equal to that highest frequency.
The problem does NOT ask for the element(s) — it asks for the total count of elements that appear maximum times.

**So logically:**
1. Every element appears some number of times.
2. Among these counts, one count will be the maximum frequency.
3. There might be multiple elements having this same maximum frequency.
4. We must add up all those frequencies.

# Approach-1: Using Frequency Array
Since nums[i] is between 1 and 100, we use an array of size 101 to store frequency.

#### Time complexity: **O(n)**
#### Space complexity: **O(1)**


## Java Code
```java []
class Solution {
    public int maxFrequencyElements(int[] nums) {
        int[] freq = new int[101];
        for (int num : nums) {
            freq[num]++;
        }
        int max = 0;
        for (int f : freq) {
            max = Math.max(max, f);
        }
        int result = 0;
        for (int f : freq) {
            if (f == max) {
                result += f;
            }
        }
        return result;
    }
}
```

# Approach-2: Using HashMap
Use HashMap to store element → frequency.

#### Time complexity: **O(n)**
#### Space complexity: **O(n)**


## Java Code
```java []
import java.util.*;
class Solution {
    public int maxFrequencyElements(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        int max = 0;
        for (int freq : map.values()) {
            max = Math.max(max, freq);
        }
        int sum = 0;
        for (int freq : map.values()) {
            if (freq == max) {
                sum += freq;
            }
        }
        return sum;
    }
}
```


## Cpp / C++ Code
```Cpp []
class Solution {
public:
    int maxFrequencyElements(vector<int>& nums) {
        int freq[101] = {0};
        for (int num : nums) {
            freq[num]++;
        }
        int maxFreq = 0;
        for (int i = 0; i <= 100; i++) {
            maxFreq = max(maxFreq, freq[i]);
        }
        int result = 0;
        for (int i = 0; i <= 100; i++) {
            if (freq[i] == maxFreq) {
                result += freq[i];
            }
        }
        return result;
    }
};
```

## JavaScript Code
```javascript []
var maxFrequencyElements = function(nums) {
    let freq = new Array(101).fill(0);
    for (let num of nums) {
        freq[num]++;
    }
    let maxFreq = 0;
    for (let f of freq) {
        maxFreq = Math.max(maxFreq, f);
    }
    let result = 0;
    for (let f of freq) {
        if (f === maxFreq) {
            result += f;
        }
    }
    return result;
};
```






