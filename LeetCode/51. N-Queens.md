## 51. N-Queens
> https://leetcode.com/problems/n-queens/

#### Solution 1: Backtracing
> http://bangbingsyb.blogspot.com/2014/11/leetcode-n-queens-i-ii.html

```cpp
class Solution {
public:
    vector<vector<string> > solveNQueens(int n) {
        vector<vector<string>> allSol;
        vector<string> sol;
        vector<int> col;
        solveNQ(n, 0, col, sol, allSol);
        return allSol;
    }

    void solveNQ(int n, int irow, vector<int> &col, vector<string> &sol, vector<vector<string>> &allSol) {
        if (irow == n) {
            allSol.push_back(sol);
            return;
        }

        for (int icol = 0; icol < n; icol++) {
            if (isValid(col, irow, icol)) {
                string s(n, '.');
                s[icol] = 'Q';
                sol.push_back(s);
                col.push_back(icol);
                solveNQ(n, irow + 1, col, sol, allSol);
                sol.pop_back();
                col.pop_back();
            }
        }
    }

    bool isValid(vector<int> &col, int irow, int icol) {
        int colSize = col.size();
        for (int i = 0; i < colSize; i++) {
            if (icol == col[i] || abs(irow - i) == abs(icol - col[i]))
                return false;
        }
        return true;
    }
};
```

#### Solution 2:
