## Intersection of Two Arrays
https://leetcode.com/problems/intersection-of-two-arrays/
#### Solution 1:
hash table
```cpp
//Using two unordered_set
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        if (!nums1.size() || !nums2.size())
            return vector<int>();
        unordered_set<int> hashset(nums1.begin(), nums1.end());
        unordered_set<int> hashres;
        for (auto i2 : nums2) {
            if (hashset.count(i2) > 0)
                hashres.insert(i2);
        }
        return vector<int>(hashres.begin(), hashres.end());
    }
};
```
```cpp
// Using one unordered_set
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> set1(nums1.begin(), nums1.end());
        vector<int> res;
        for (auto i2 : nums2)
            /*if (set1.count(i2)) {
                res.push_back(i2);
                set1.erase(i2);
            }*/
            if (set1.erase(i2)) {
                res.push_back(i2);
            }
        return res;
    }
};
```
