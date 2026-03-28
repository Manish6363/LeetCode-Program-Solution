## Problem
You are given an array prices where `prices[i]` is the price of a given stock on the `i`th day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.


Example 1:
- $$Input$$: `prices = [7,1,5,3,6,4]`
- $$Output$$: 5
    - **Explanation**: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
    - Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.


link: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

# Intuition
To make a profit, we must **buy at a lower price and sell later at a higher price**.

A simple idea is to check every possible pair of buy and sell days, but this is inefficient.
Instead, we can track the **minimum price encountered so far** while iterating through the array.

For every day:
- Assume we sell on that day.
- Calculate the profit using the lowest price seen before it.
- Keep updating the maximum profit.

This ensures we always buy before we sell and get the best possible profit.

# Approach-1 Brute Force
Check every pair of days (buy day i, sell day j) where j > i and compute the profit.

**Steps**
1. Buy on day `i`
2. Sell on day `j`
3. Calculate `profit = prices[j] - prices[i]`
4. Track maximum profit.

#### Time complexity: O(n²)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for(int i = 0; i < prices.length; i++){
            for(int j = i + 1; j < prices.length; j++){
                int profit = prices[j] - prices[i];
                if(profit > maxProfit){
                    maxProfit = profit;
                }
            }
        }
        return maxProfit;
    }
}
```

# Approach-2 Better Approach
Keep track of the minimum price so far and compute profit for each day.
But instead of updating min every iteration directly, we separate logic clearly.

**Steps**
1. Track minPrice 
2. Calculate profit with current price
3. Update maxProfit

#### Time complexity: O(N)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;
        for(int i = 0; i < prices.length; i++){
            if(prices[i] < minPrice){
                minPrice = prices[i];
            }
            int profit = prices[i] - minPrice;
            if(profit > maxProfit){
                maxProfit = profit;
            }
        }
        return maxProfit;
    }
}
```

# Approach-3 Optimal Approach
**Step**
1. Track minimum price seen so far
2. Calculate profit for each day.
3. Update maximum profit.

#### Time complexity: O(N)
#### Space complexity: O(1)


## Java Code
```Java []
class Solution {
    public int maxProfit(int[] prices) {
        int buy = prices[0];
        int profit = 0;
        for(int i = 1; i < prices.length; i++) {
            int cost = prices[i] - buy;
            profit = cost > profit ? cost : profit;
            buy = buy < prices[i] ? buy : prices[i];
        }
        return profit;
    }
}
```

## CPP / C++ Code
```Cpp []
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int min=prices[0], profit=0;	
		for(int i=1; i<prices.size(); i++) {
			int cost=prices[i]-min;
			profit=cost>profit?cost:profit;
			min=min<prices[i]?min:prices[i];
		}
        return profit;
    }
};
```


# JavaScript Code
```JavaScript []
var maxProfit = function(prices) {
    let min=prices[0], profit=0;
    for(let i=1; i<prices.length; i++) {
        let cost=prices[i]-min;
        profit=cost>profit?cost:profit;
        min=min<prices[i]?min:prices[i];
    }
    return profit;
};
```
