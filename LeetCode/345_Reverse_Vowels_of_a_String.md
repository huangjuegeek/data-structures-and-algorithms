## 345. Reverse Vowels of a String
> https://leetcode.com/problems/reverse-vowels-of-a-string/

```
用一个哈希表存储所有的元音字母，注意大小写字母都要包括。
定义两个指针，
循环的每次迭代，第一个指针从前往后扫描，遇到元音字母就停下，第二个指针从后往前扫描，遇到元音字母就停下。
交换两个指针所指的字符。
注意循环过程中，要保证第一个指针小于等于第二个指针。
```
```cpp
class Solution {
public:
    string reverseVowels(string s) {
        const int size = 256;
        int hashtable[size];
        for(int i = 0; i < size; i++) {
            hashtable[i] = 0;
        }
        string vowels = "aeiouAEIOU";
        for(char vowel : vowels) {
            hashtable[vowel] = 1;
        }
        int len = s.length();
        int i = 0, j = len - 1;
        while(i <= j) {
            while(!hashtable[s[i]] && i < j)  i++;
            while(!hashtable[s[j]] && i < j)  j--;
            
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
