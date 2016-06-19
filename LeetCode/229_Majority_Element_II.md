## 229. Majority Element II
> https://leetcode.com/problems/majority-element-ii/

#### Solution 1: Boyer-Moore Majority Vote algorithm
> https://leetcode.com/discuss/43248/boyer-moore-majority-vote-algorithm-and-my-elaboration
> https://leetcode.com/discuss/42806/boyer-moore-majority-vote-algorithm-generalization

```
长度为n的数组中，至多有两个不同元素的出现次数大于n/3次
长度为n的数组中，至多有k-1个不同元素的出现次数大于n/k次
```
```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int candidate1 = 0, candidate2 = 0, count1 = 0, count2 = 0;
        for(int i : nums) {
            if(i == candidate1)  count1++;
            else if(i == candidate2)  count2++;
            else if(count1 == 0) { candidate1 = i; count1 = 1; }
            else if(count2 == 0) { candidate2 = i; count2 = 1; }
            else { count1--; count2--; }
        }
        count1 = count2 = 0;
        for(int i : nums) {
            if(i == candidate1)  count1++;
            else if(i == candidate2)  count2++;
        }
        vector<int> res;
        if(count1 > nums.size() / 3)  res.push_back(candidate1);
        if(count2 > nums.size() / 3)  res.push_back(candidate2);
        return res;
    }
};
```

#### Solution 2: general solution for searching elements that appear more n/k times
> https://leetcode.com/discuss/57953/general-solution-searching-elements-that-appear-more-times

