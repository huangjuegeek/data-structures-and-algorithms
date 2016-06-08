## Valid Anagram
https://leetcode.com/problems/valid-anagram/

变形词，变位词，相同字母异序词
#### Solution 1:
Use int array as hashtable
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) return false;
        const int size = 26;
        int hashtable[size] = {0};
        for (int i = 0; i < s.length(); i++) {
            hashtable[s[i] - 'a']++;
        }
        for (int i = 0; i < t.length(); i++) {
            hashtable[t[i] - 'a']--;
        }
        for (int i = 0; i < size; i++) {
            if (hashtable[i]) 
                return false;
        }
        return true;
    }
};
```
Use unordered_map https://leetcode.com/discuss/49374/2-c-solutions-with-explanations

#### Solution 2:
Use sort
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) { 
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        return s == t; 
    }
};
```
