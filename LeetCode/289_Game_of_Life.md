##289. Game of Life
> https://leetcode.com/problems/game-of-life/

####Solution 1:
> https://discuss.leetcode.com/topic/29054/easiest-java-solution-with-explanation/2

```java
public class Solution {
    public void gameOfLife(int[][] board) {
        if(board == null || board.length == 0) return;
        int m = board.length, n = board[0].length;

        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                int lives = liveNeighbors(board, m, n, i, j);

                // In the beginning, every 2nd bit is 0;
                // So we only need to care about when the 2nd bit will become 1.
                if(board[i][j] == 0B01 && lives >= 2 && lives <= 3) {
                    board[i][j] = 0B11; // Make the 2nd bit 1: 01 ---> 11
                }
                if(board[i][j] == 0B00 && lives == 3) {
                    board[i][j] = 0B10; // Make the 2nd bit 1: 00 ---> 10
                }
            }
        }

        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                board[i][j] >>= 1;  // Get the 2nd state.
            }
        }
    }

    public int liveNeighbors(int[][] board, int m, int n, int i, int j) {
        int lives = 0;
        for(int x = Math.max(i - 1, 0); x <= Math.min(i + 1, m - 1); x++) {
            for(int y = Math.max(j - 1, 0); y <= Math.min(j + 1, n - 1); y++) {
                lives += board[x][y] & 1;
            }
        }
        lives -= board[i][j] & 1;
        return lives;
    }
}
```

####Solution 2:
求活邻居个数的时候，遍历一个`方向数组`来获取各个方向邻居的坐标
> https://discuss.leetcode.com/topic/26176/c-ac-code-o-1-space-o-mn-time
> https://discuss.leetcode.com/topic/26110/clean-o-1-space-o-mn-time-java-solution/3

```cpp
// State transitions
//  0 : dead to dead
//  1 : live to live
//  2 : live to dead
//  3 : dead to live
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        int m = board.size(), n = m ? board[0].size() : 0;
        int di[8] = {-1, -1, -1,  0, 0,  1, 1, 1};
        int dj[8] = {-1,  0,  1, -1, 1, -1, 0, 1};
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int live = 0;
                for (int k = 0; k < 8; k++) {
                    int ii = i + di[k], jj = j + dj[k];
                    if (ii < 0 || ii >= m || jj < 0 || jj >= n) continue;
                    if (board[ii][jj] == 1 || board[ii][jj] == 2) live++;
                }
                if (board[i][j] == 1 && (live < 2 || live > 3)) board[i][j] = 2;
                else if (!board[i][j] && live == 3) board[i][j] = 3;
            }
        }
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++) 
                board[i][j] %= 2;
    }
};
```

####Solution 3:
另一种状态转换写法
> https://discuss.leetcode.com/topic/26112/c-o-1-space-o-mn-time
