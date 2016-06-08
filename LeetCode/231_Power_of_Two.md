## Power of Two
#### Solution 1:
若n为负数，直接返回false。经典位运算操作，计算输入整数n的二进制表示中"1"的个数，若个数为1，则n是2的N次幂。
```cpp
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n < 0)    return false;
        int numOfOne = 0;
        while(n) {
            n = n & (n-1);
            numOfOne++;
        }
        return numOfOne == 1;
    }
};
```
