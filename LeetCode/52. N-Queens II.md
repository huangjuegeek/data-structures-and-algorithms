## 52. N-Queens II
> https://leetcode.com/problems/n-queens-ii/

#### Solution 1:
> http://bangbingsyb.blogspot.com/2014/11/leetcode-n-queens-i-ii.html

```cpp
class Solution {
public:
    int totalNQueens(int n) {
        vector<int> col;
        int count = 0;
        solveNQ(n, 0, col, count);
        return count;
    }
private:
    void solveNQ(int n, int irow, vector<int> &col, int &countSol) {
        if (irow == n) {
            countSol++;
            return;
        }

        for (int icol = 0; icol < n; icol++) {
            if (isValid(col, irow, icol)) {
                col.push_back(icol);
                solveNQ(n, irow + 1, col, countSol);
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
