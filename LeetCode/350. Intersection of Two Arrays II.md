## Intersection of Two Arrays II
> https://leetcode.com/problems/intersection-of-two-arrays-ii/

> http://articles.leetcode.com/here-is-phone-screening-question-from/

### Solution 1:
hash table, using unordered_map:

> https://leetcode.com/discuss/103956/solutions-hashtable-binary-search-space-complexity-analyzed
```cpp
// complexity: time O(M + N), space O(M) or O(N), should use the smaller vector to construct hash map
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res = {};
        unordered_map<int, int> map;
        for (int i = 0; i < nums1.size(); i++) map[nums1[i]]++;
        for (int j = 0; j < nums2.size(); j++) {
            auto itr = map.find(nums2[j]); //使用find来检测元素是否存在，避免额外空间开销
            if (itr != map.end() && itr->second > 0) {
                res.push_back(nums2[j]);
                map[nums2[j]]--;
            }
        }
        return res;
    }
};
```
> https://leetcode.com/discuss/103787/table-solution-pointers-solution-with-time-space-complexity

```cpp
/*
Based on C++ map mechanism, if a key is not exist, access the key will assign a default value to the key. 
so if you simply test if map[key] is 0 or not by using "if (map[key] == 0)" without testing if the key is in the map. 
you will consume extra space....you could avoid allocate extra space either by find or count method.
*/
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res = {};
        unordered_map<int, int> map1;
        for (int i1 : nums1) map1[i1]++;
        for (int i2 : nums2) {
            if (map1[i2] > 0) {
                res.push_back(i2);
                map1[i2]--;
            }
        }
        return res;
    }
};
```
Java version:
> https://leetcode.com/discuss/103835/ac-solution-using-java-hashmap

## Solution 2:
sort, two pointers:
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        int len1 = (int)nums1.size(), len2 = (int)nums2.size();
        int i = 0, j = 0;
        vector<int> res;
        while (i < len1 && j < len2) {
            if (nums1[i] == nums2[j]) {
                res.push_back(nums1[i]);
                i++;
                j++;
            }
            else if (nums1[i] > nums2[j]) {
                j++;
            }
            else {
                i++;
            }
            /*
            注释掉去重的代码，就是本题的解法
            while (i > 0 && i < len1 && nums1[i] == nums1[i - 1]) i++;
            while (j > 0 && j < len2 && nums2[j] == nums2[j - 1]) j++;
            */
        }
        return res;
    }
};
```
C++, iterator version:
> https://leetcode.com/discuss/105464/simple-while-loop-solution-c-12ms
