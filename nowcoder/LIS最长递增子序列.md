# LIS(最长递增子序列)问题
> http://www.nowcoder.com/courses/1/12/6

## Solution 1:
```java
import java.util.*;
/*
dp[i]表示在必须以A[i]结尾的情况下，A[0...i]中的最大递增子序列长度。

dp[i]怎么求？对于<i的所有满足A[j]<A[i](0<=j<i)的下标j，
找出dp[j]的最大值，则dp[i] = dp[j]的最大值 + 1
*/
public class LongestIncreasingSubsequence {
    public int getLIS(int[] A, int n) {
        if(A == null) return 0;
        int[] dp = new int[n]; 
        dp[0] = 1;
        int globalMax = 0;
        for(int i = 1; i < n; i++) {
            int dpjMax = 0;
            for(int j = 0; j < i; j++) { //dp[i] = max{dp[j]+1}, 其中0<=j<i, A[j]<A[i]
                if(A[j] < A[i] && dp[j] > dpjMax) {
                    dpjMax = dp[j];
                }
            }
            dp[i] = dpjMax + 1;
            if(dp[i] > globalMax) {
                globalMax = dp[i];
            }
        }
        return globalMax;
    }
}
```
