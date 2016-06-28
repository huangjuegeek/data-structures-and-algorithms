## 72. Edit Distance
> https://leetcode.com/problems/edit-distance/

#### Solution 1:
> https://leetcode.com/discuss/43398/20ms-detailed-explained-c-solutions-o-n-space

```cpp
// complexity: time O(MN), space O(MN)
class Solution { 
public:
    int minDistance(string word1, string word2) { 
        int len1 = word1.length(), len2 = word2.length();
        vector<vector<int>> dp(len1+1, vector<int>(len2+1, 0));
        for(int i = 1; i <= len1; i++) {
            dp[i][0] = i;
        }
        for(int j = 1; j <= len2; j++) {
            dp[0][j] = j;
        }
        for(int i = 1; i <= len1; i++) {
            for(int j = 1; j <= len2; j++) {
                if(word1[i-1] == word2[j-1]) {
                    dp[i][j] = dp[i-1][j-1];
                }
                else {
                    dp[i][j] = 1 + min(dp[i-1][j-1], min(dp[i-1][j], dp[i][j-1]));
                }
            }
        }
        return dp[len1][len2];
    }
};
```

#### Solution 2:
> https://leetcode.com/discuss/10426/my-o-mn-time-and-o-n-space-solution-using-dp-with-explanation
> https://leetcode.com/discuss/43398/20ms-detailed-explained-c-solutions-o-n-space

```cpp
class Solution { 
public:
    int minDistance(string word1, string word2) {
        int m = word1.length(), n = word2.length();
        vector<int> cur(m + 1, 0);
        for (int i = 1; i <= m; i++)
            cur[i] = i;
        for (int j = 1; j <= n; j++) {
            int pre = cur[0];
            cur[0] = j;
            for (int i = 1; i <= m; i++) {
                int temp = cur[i];
                if (word1[i - 1] == word2[j - 1])
                    cur[i] = pre;
                else cur[i] = min(pre + 1, min(cur[i] + 1, cur[i - 1] + 1));
                pre = temp;
            }
        }
        return cur[m]; 
    }
}; 
```
