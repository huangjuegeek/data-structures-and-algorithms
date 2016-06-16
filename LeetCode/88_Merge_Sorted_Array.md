## 88. Merge Sorted Array
https://leetcode.com/problems/merge-sorted-array/
#### Solution 1:
> https://leetcode.com/discuss/96148/compact-o-n-time-o-1-space-c-solution <br>
> https://leetcode.com/discuss/41926/4ms-c-solution-with-single-loop

```cpp
/*
当nums2中所有的数字已经被合并进nums1以后，nums1中剩下的那些还没有被移动过的数字已经在正确的位置上了
*/
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int k = m + n - 1, i = m - 1, j = n - 1;
        while(j >= 0) {
            nums1[k--] = (i >= 0 && nums1[i] > nums2[j]) ? nums1[i--] : nums2[j--]; 
        }
    }
};
```
