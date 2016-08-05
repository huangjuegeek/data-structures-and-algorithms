##238. Product of Array Except Self
> https://leetcode.com/problems/product-of-array-except-self/

###Solution 1:
> https://discuss.leetcode.com/topic/18864/simple-java-solution-in-o-n-without-extra-space/6
> https://discuss.leetcode.com/topic/28792/super-easy-java-solution-in-o-n-time-and-o-1-space/2
> https://discuss.leetcode.com/topic/19033/my-simple-java-solution

```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] res = new int[len];
        for(int i = 0; i < len; i++) {
            res[i] = 1;
        }
        for(int i = 0, j = len-1, left = 1, right = 1; i < len; i++, j--) {
            res[i] *= left;  left *= nums[i];
            res[j] *= right;  right *= nums[j];
        }
        return res;
    }
}
```
