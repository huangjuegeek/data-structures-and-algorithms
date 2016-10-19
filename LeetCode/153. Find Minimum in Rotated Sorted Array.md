## 153. Find Minimum in Rotated Sorted Array
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
#### Solution 1: binary search
> https://leetcode.com/discuss/18798/a-concise-solution-with-proof-in-the-comment <br>
> https://leetcode.com/discuss/37307/4ms-simple-c-code-with-explanation

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int low = 0, high = nums.size() - 1;
        while(nums[low] > nums[high] && low < high) {
            int mid = low + (high - low) / 2;
            if(nums[mid] < nums[high])
                high = mid;
            else // nums[mid] > nums[high], so mid element can't be the min element
                low = mid + 1;
        }
        return nums[low];
    }
};
```
