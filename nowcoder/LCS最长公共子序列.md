# LCS最长公共子序列
> http://www.nowcoder.com/courses/1/12/7

## Solution 1: DP
```java
import java.util.*;

public class LCS {
    public int findLCS(String A, int n, String B, int m) {
        char[] a = A.toCharArray();
        char[] b = B.toCharArray();
        //dp[i][j]表示A[0...i-1]和B[0...i-1]的最长公共子序列长度
        int[][] dp = new int[n + 1][m + 1];

        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(a[i - 1] == b[j - 1]){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[n][m];

    }
}
```
