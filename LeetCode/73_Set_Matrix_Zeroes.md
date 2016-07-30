##73. Set Matrix Zeroes
####Solution 1:
开辟m*n的矩阵isZero来标记matrix中值为0的坐标，遍历isZero将matrix中值为0的坐标所在行列都置为0。

####Solution 2:
开辟两个一维数组空间m和n，m用来存储需要被置为0的行号，n用来存储需要被置为0的列号。

####Solution 3:
> https://discuss.leetcode.com/topic/5056/any-shortest-o-1-space-solution

```java
public class Solution {
    public static void main(String[] args) {
        int[][] a = {{0,0,0,5},{4,3,1,4},{0,1,1,4},{1,2,1,3},{0,0,1,1}};
        Solution sol = new Solution();
        sol.setZeroes(a);
    }
    public void setZeroes(int[][] matrix) {
        int col0 = 1;  //用于标记第0列是否应该置0，“0”表示应该置0，“1”表示不应该置0
        int m = matrix.length, n = matrix[0].length;

        for(int i = 0; i < m; i++) {
            if(matrix[i][0] == 0)  col0 = 0;
            for(int j = 1; j < n; j++) {
                if(matrix[i][j] == 0) {
                    matrix[i][0] = matrix[0][j] = 0;
                }
            }
        }

        //bottom-up traverse
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 1; j--)
                if (matrix[i][0] == 0 || matrix[0][j] == 0)
                    matrix[i][j] = 0;
            if (col0 == 0) matrix[i][0] = 0;
        }

//注意不能写成如下形式，因为前面置0操作有可能会覆盖掉第0行或第0列记录的状态
//        for (int i = 0; i < m; i++) {
//            for (int j = 1; j < n; j++)
//                if (matrix[i][0] == 0 || matrix[0][j] == 0)
//                    matrix[i][j] = 0;
//            if (col0 == 0) matrix[i][0] = 0;
//        }
    }
}
```
