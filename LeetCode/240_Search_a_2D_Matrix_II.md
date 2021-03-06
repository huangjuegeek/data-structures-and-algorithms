## Search a 2D Matrix II
https://leetcode.com/problems/search-a-2d-matrix-ii/
#### Solution 1:
https://leetcode.com/discuss/48025/6-9-lines-c-python-solutions-with-explanations
```cpp
/*
complexity: time O(M+N)
把矩阵想象成一棵BST，右上角和左下角都可算是一个root.
从矩阵右上角开始, 比较target和matrix[i][j]的值. 
如果target大于matrix[i][j], 则该行不可能有target, 所以i++; 
如果target小于matrix[i][j], 则该列不可能有target, 所以j--. 
如果target等于matrix[i][j]，则找到target.
遇到边界则表明该矩阵不含target.
*/
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m, n;
        if ((m = matrix.size()) == 0 || (n = matrix[0].size()) == 0) return false;
        int i = 0, j = n - 1;
        while (i < m && j >= 0) {
            int x = matrix[i][j];
            if (target > x) i++;
            else if (target < x) j--;
            else return true;  //把target==x的情况放最后，可以减少所需判断次数
        }
        return false;
    }
};
```
#### Solution 2:
quad partition search, divide and conquer

https://leetcode.com/discuss/77842/java-an-easy-to-understand-divide-and-conquer-method
```
First, we divide the matrix into four quarters as shown below:
  zone 1      zone 2
*  *  *  * | *  *  *  *
*  *  *  * | *  *  *  *
*  *  *  * | *  *  *  *
*  *  *  * | *  *  *  *
-----------------------
*  *  *  * | *  *  *  *
*  *  *  * | *  *  *  *
*  *  *  * | *  *  *  *
*  *  *  * | *  *  *  *
  zone 3      zone 4
We then compare the element in the center of the matrix with the target. There are three possibilities:
center < target. In this case, we discard zone 1 because all elements in zone 1 are less than target.
center > target. In this case, we discard zone 4.
center == target. return true.
```

C++ version: https://leetcode.com/discuss/83239/clean-c-implementation-with-detailed-complexity-analysis

complexity analysis: <br>
> https://leetcode.com/discuss/47528/c-with-o-m-n-complexity <br>
> http://articles.leetcode.com/searching-2d-sorted-matrix-part-ii
