## 152. Maximum Product Subarray
#### Solution 1:
> https://leetcode.com/discuss/14235/possibly-simplest-solution-with-o-n-time-complexity

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int len = nums.size();
        if(!len)    return 0;
        int res = nums[0], imax = nums[0], imin = nums[0];
        for(int i = 1; i < len; i++) {
            if(nums[i] < 0)  //如果遇到负数，最大值和最小值发生调换
                swap(imax,imin);
            imax = max(nums[i], imax * nums[i]);
            imin = min(nums[i], imin * nums[i]);
            res = max(res, imax);
        }
        return res;
    }
};
```
DP with O(N) space
> https://leetcode.com/discuss/11839/share-my-dp-code-that-got-ac

#### Solution 2:
```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if(nums.size() == 0) return 0;
        int curmax = nums[0], curmin = nums[0], res = nums[0];
        for(int i = 1; i < nums.size(); i++){
            int premax = curmax;
            curmax = max(curmax*nums[i], max(curmin*nums[i], nums[i]));
            curmin = min(premax*nums[i], min(curmin*nums[i], nums[i]));
            res = max(res, curmax);
        }
        return res;
    }
};
```

#### Solution 3:
> https://leetcode.com/discuss/14733/solution-though-not-as-great-as-answer-provided-by-leetcode
> https://leetcode.com/discuss/15134/simpler-solution-with-6-lines-code-o-n-complexity
> https://leetcode.com/discuss/19795/share-my-c-solution-maybe-is-the-simplest-solution
