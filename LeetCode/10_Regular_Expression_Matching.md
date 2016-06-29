## 10. Regular Expression Matching
> https://leetcode.com/problems/regular-expression-matching/

#### Solution 1: Java built-in
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Solution {
    public boolean isMatch(String s, String p) {
        Pattern r = Pattern.compile(p);
        Matcher m = r.matcher(s);
        return m.matches();
    }
}
```

#### Solution 2: Recursive
> https://leetcode.com/discuss/18970/concise-recursive-and-dp-solutions-with-full-explanation-in

```c
bool matchCore(char* s, char* p) {
    if(*p == '\0')    return *s == '\0';
    if ('*' == *(p + 1)) {
        return (matchCore(s, p + 2) || (*s != '\0') && (*s == *p || '.' == *p) && matchCore(s + 1, p));
    } 
    else {
        if (*s == '\0')    return false;
        return (*s == *p || '.' == *p) ? matchCore(s + 1, p + 1) : false;
    }
}
bool isMatch(char* s, char* p) {
    if(s == NULL || p == NULL)    return false;
    return matchCore(s, p);
}
```
> https://leetcode.com/discuss/9405/the-shortest-ac-code


#### Solution 3: DP with 2D space
> https://leetcode.com/discuss/18970/concise-recursive-and-dp-solutions-with-full-explanation-in

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int len1 = s.size(), len2 = p.size();
        vector<vector<bool>> f(len1 + 1, vector<bool>(len2 + 1, false));

        f[0][0] = true;
        for (int i = 1; i <= len1; i++)
            f[i][0] = false;
        // p[0.., j - 3, j - 2, j - 1] matches empty iff p[j - 1] is '*' and p[0..j - 3] matches empty
        for (int j = 1; j <= len2; j++)
            f[0][j] = j > 1 && '*' == p[j - 1] && f[0][j - 2];

        for (int i = 1; i <= len1; i++)
            for (int j = 1; j <= len2; j++)
                if (p[j - 1] != '*')
                    f[i][j] = f[i - 1][j - 1] && (s[i - 1] == p[j - 1] || '.' == p[j - 1]);
                else
                    // p[0] cannot be '*' so no need to check "j > 1" here
                    f[i][j] = f[i][j - 2] || (s[i - 1] == p[j - 2] || '.' == p[j - 2]) && f[i - 1][j];

        return f[len1][len2];
    }
};
```
> https://leetcode.com/discuss/43860/9-lines-16ms-c-dp-solutions-with-explanations

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.length(), n = p.length(); 
        vector<vector<bool> > dp(m + 1, vector<bool> (n + 1, false));
        dp[0][0] = true;
        for (int i = 0; i <= m; i++)
            for (int j = 1; j <= n; j++)
                if (p[j - 1] == '*')
                    dp[i][j] = dp[i][j - 2] || (i > 0 && (s[i - 1] == p[j - 2] || p[j - 2] == '.') && dp[i - 1][j]);
                else dp[i][j] = i > 0 && dp[i - 1][j - 1] && (s[i - 1] == p[j - 1] || p[j - 1] == '.');
        return dp[m][n];
    }
};
```
#### Solution 4: DP with 1D space
> https://leetcode.com/discuss/26809/dp-java-solution-detail-explanation-from-2d-space-to-1d-space
