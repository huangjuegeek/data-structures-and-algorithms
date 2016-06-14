## 74. Search a 2D Matrix
https://leetcode.com/problems/search-a-2d-matrix/
#### Solution 1: two binary search
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = m ? matrix[0].size() : 0;
        if(target < matrix[0][0] || target > matrix[m-1][n-1]) return false;
        int low = 0, high = m - 1, left = 0, right = n - 1, mid;
        while(low <= high){                                            
            mid = low + (high - low) / 2;
            if(matrix[mid][0] == target) return true;
            else if(matrix[mid][0] < target) low = mid + 1;
            else high = mid - 1;  // matrix[mid][0] > target
        }
        while(left <= right){
            mid = left + (right - left) / 2;
            if(matrix[high][mid] == target) return true;
            else if(matrix[high][mid] < target) left = mid + 1;
            else  right = mid - 1;  // matrix[high][mid] > target
        }
        return false;
    }
};
```
#### Solution 2: one binary search, treat the 2D matrix as an sorted list
> https://leetcode.com/discuss/80449/c-12ms-solution-using-binary-search-o-log-m-log-n <br>
> https://leetcode.com/discuss/10735/dont-treat-it-as-a-2d-matrix-just-treat-it-as-a-sorted-list

```cpp
// complexity: time O(log(M*N)) = O(log(M)+log(N))
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        if(target < matrix[0][0] || target > matrix[m-1][n-1]) return false;
        int low = 0, high = m * n - 1, mid; // m * n might cause overflow
        while(low <= high) {
            mid = low + (high - low) / 2;
            int cur = matrix[mid / n][mid % n];
            if(cur == target)    
                return true;
            else if(cur > target)    
                high = mid - 1;
            else
                low = mid + 1;
        }
        return false;
    }
};
```
#### Solution 3: idea from Search a 2D Matrix II, search from the top-right point of the matrix
> https://leetcode.com/discuss/98582/easy-c-12ms-o-n-solution-not-using-a-binary-search
