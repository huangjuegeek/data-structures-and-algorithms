## Reverse String
https://leetcode.com/problems/reverse-string/
#### Solution 1:
O(N) space complexity
```cpp
class Solution {
public:
    string reverseString(string s) {
        int len = s.length();
        char* space = new char[len + 1];
        int p = len - 1, q = 0;
        while(p >= 0) {
            space[q++] = s[p--];
        }
        space[q] = '\0';
        string res(space);
        delete[] space;
        return res;
    }
};
```
#### Solution 2:
双指针，一个指针从头往后走，另一个指针从尾往前走，每次循环交换两个指针所指的字符。
```cpp
class Solution {
public:
    string reverseString(string s) {
        int len = s.length();
        int i = 0, j = len - 1;
        while(i <= j) {
            char temp = s[i];
            s[i] = s[j];
            s[j] = temp;
            i++;
            j--;
        }
        return s;
    }
};
```
