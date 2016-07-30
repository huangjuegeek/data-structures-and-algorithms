##343. Integer Break
> https://leetcode.com/problems/integer-break/

###Solution 1: 找规律
> https://discuss.leetcode.com/topic/42991/o-log-n-time-solution-with-explanation

```java
public class Solution {
    public int integerBreak(int n) {
        if (n == 2)
            return 1;
        else if (n == 3)
            return 2;
        else if (n % 3 == 0)
            return (int) Math.pow(3, n / 3);
        else if (n % 3 == 1)
            return 2 * 2 * (int) Math.pow(3, (n - 4) / 3);
        else
            return 2 * (int) Math.pow(3, n / 3);
    }
}
```

> https://discuss.leetcode.com/topic/45341/an-simple-explanation-of-the-math-part-and-a-o-n-solution
> https://discuss.leetcode.com/topic/43042/easy-to-understand-c-with-explanation
> https://discuss.leetcode.com/topic/43055/why-factor-2-or-3-the-math-behind-this-problem

###Solution 2: DP
> https://discuss.leetcode.com/topic/42978/java-dp-solution/3
> https://discuss.leetcode.com/topic/44168/c-dynamic-programming-solution/2

```cpp
class Solution {
public:
    int integerBreak(int n) {
        
        if (n <= 2)
            return 1;

        vector<int> maxArr(n+1, 0);
                    
        /** For a number i: write i as a sum of integers, then take the product of those integers.
        maxArr[i] = maximum of all the possible products */
        
        maxArr[1] = 0;
        maxArr[2] = 1; // 2=1+1 so maxArr[2] = 1*1
        
        for (int i=3; i<=n; i++) {
            for (int j=1; j<i; j++) {
                /** Try to write i as: i = j + S where S=i-j corresponds to either one number or a sum of two or more numbers
                
                Assuming that j+S corresponds to the optimal solution for maxArr[i], we have two cases:
                (1) i is the sum of two numbers, i.e. S=i-j is one number, and so maxArr[i]=j*(i-j)
                (2) i is the sum of at least three numbers, i.e. S=i-j is a sum of at least 2 numbers,
                and so the product of the numbers in this sum for S is maxArr[i-j]
                (=maximum product after breaking up i-j into a sum of at least two integers):
                maxArr[i] = j*maxArr[i-j]
                */
                maxArr[i] = max(maxArr[i], max(j*(i-j), j*maxArr[i-j]));
            }
        }
        return maxArr[n];
    }
};
```
