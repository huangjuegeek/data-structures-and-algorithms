## Intersection of Two Arrays
https://leetcode.com/problems/intersection-of-two-arrays/
#### Solution 1:
hash set
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
#### Solution 2:
sort, two pointers

https://leetcode.com/discuss/103224/my-c-solution-with-sort
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        std::sort(nums1.begin(), nums1.end());
        std::sort(nums2.begin(), nums2.end());
        vector<int> ans;
        int i = 0, j = 0;
        while (i < nums1.size() && j < nums2.size()) {
            if (nums1[i] < nums2[j])
                i++;
            else if (nums1[i] > nums2[j])
                j++;
            else {
                if (!ans.size() || ans.back() != nums1[i])
                    ans.push_back(nums1[i]);
                i++;
                j++;
            }
        }
        return ans;
    }
};
```

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
            while (i > 0 && i < len1 && nums1[i] == nums1[i - 1]) i++;
            while (j > 0 && j < len2 && nums2[j] == nums2[j - 1]) j++;
        }
        return res;
    }
};
```
