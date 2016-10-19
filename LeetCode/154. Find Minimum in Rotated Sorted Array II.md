## 154. Find Minimum in Rotated Sorted Array II
> https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/

#### Solution 1:
> https://leetcode.com/discuss/19746/my-pretty-simple-code-to-solve-it

```cpp
// complexity: time O(logN), worst case O(N)
class Solution {
public:
    int findMin(vector<int>& nums) {
        int low = 0, high = nums.size() - 1;
        while(nums[low] >= nums[high] && low < high) {
            int mid = low + (high - low) / 2;
            if(nums[mid] < nums[high])
                high = mid;
            else if(nums[mid] > nums[high])
                low = mid + 1;
            else
                high--;
        }
        return nums[low];
    }
};
```

#### Solution 2:
> https://leetcode.com/discuss/13775/one-simple-and-clear-method-with-o-1-space-and-worst-o-n-time

