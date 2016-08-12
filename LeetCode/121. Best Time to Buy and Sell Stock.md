## 121. Best Time to Buy and Sell Stock
> https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

#### Solution 1:
> https://discuss.leetcode.com/topic/5863/sharing-my-simple-and-clear-c-solution
> http://bangbingsyb.blogspot.com/2014/11/leetcode-best-time-to-buy-and-sell.html

```cpp
class Solution {
public:
    int maxProfit(vector<int> &prices) {
        int maxPro = 0;
        int minPrice = INT_MAX;
        for(int i = 0; i < prices.size(); i++){
            minPrice = min(minPrice, prices[i]);
            maxPro = max(maxPro, prices[i] - minPrice);
        }
        return maxPro;
    }
};
```
```java
public class Solution {
	public int maxProfit(int[] prices) {
	    if(prices == null || prices.length < 2) return 0;      
	    int maxProfit = 0, minPrice = prices[0];
	    for(int i = 1; i < prices.length; i++) {
	        if(prices[i] > prices[i - 1]) {
	            maxProfit = Math.max(maxProfit, prices[i] - minPrice);       
	        } else {
	             minPrice = Math.min(minPrice, prices[i]);
	        }
	    }
	    return maxProfit;
	}
}
```
```java
public class Solution {
	public int maxProfit(int[] prices) {
	    if(prices == null || prices.length < 2) return 0;      
	    int maxProfit = 0, minPrice = prices[0];
	    for(int i = 1; i < prices.length; i++) {
	        if(prices[i] > minPrice) {
	            maxProfit = Math.max(maxProfit, prices[i] - minPrice);       
	        } else {
	             minPrice = prices[i];
	        }
	    }
	    return maxProfit;
	}
}
```

#### Solution 2: Kadane's Algorithm
> https://discuss.leetcode.com/topic/19853/kadane-s-algorithm-since-no-one-has-mentioned-about-this-so-far-in-case-if-interviewer-twists-the-input

```java
public class Solution {
	public int maxProfit(int[] prices) {
        int maxCur = 0, maxSoFar = 0;
        for(int i = 1; i < prices.length; i++) {
            maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
            maxSoFar = Math.max(maxCur, maxSoFar);
        }
        return maxSoFar;
    }
}
```

### Extended Problem: 需要输出最佳买入和最佳卖出日
```java
public int maxProfit(int[] prices) {
		if (prices == null || prices.length < 2)
			return 0;
		int maxProfit = 0, minPrice = prices[0];
		int buyDay = 0, sellDay = 0;

		for (int i = 1; i < prices.length; i++) {
			if (prices[i] > prices[i - 1]) {
				int curProfit = prices[i] - minPrice;
				if (maxProfit < curProfit) {
					maxProfit = curProfit;
					sellDay = i;  //只更新卖出日
				}
			} else {
				if (minPrice > prices[i]) {
					minPrice = prices[i];
					buyDay = sellDay = i;  //需要同时更新买入和卖出日
				}
			}
		}
		System.out.println(buyDay + " " + sellDay);
		return maxProfit;
	}
```
