## Subsets
https://leetcode.com/problems/subsets/
#### Solution 1:
http://www.cnblogs.com/TenosDoIt/p/3451902.html
```cpp
class Solution {
public:
    vector<vector<int> > subsets(vector<int> &nums) {
        //先排序，然后dfs每个元素选或者不选，最后叶子节点就是所有解
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        vector<int>tmpres;
        dfs(nums, 0, tmpres, res);
        return res;
    }
    void dfs(vector<int> &nums, int depth, vector<int> &tmpres, vector<vector<int>> &res) {
        if (depth == nums.size()) {
            res.push_back(tmpres);
            return;
        }
        //选择S[iend]
        tmpres.push_back(nums[depth]);
        dfs(nums, depth + 1, tmpres, res);
        tmpres.pop_back();
        //不选择S[iend]
        dfs(nums, depth + 1, tmpres, res);
    }
};
```
#### Solution 2:
http://www.cnblogs.com/TenosDoIt/p/3451902.html
```cpp
class Solution {
public:
    vector<vector<int> > subsets(vector<int> &nums) {
        int len = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int> > res(1);//开始加入一个空集
        for (int i = 0; i < len; ++i) {
            int resSize = res.size();
            for (int j = 0; j < resSize; j++) {
                res.push_back(res[j]);
                res.back().push_back(nums[i]);
            }
        }
        return res;
    }
};
```
#### Solution 3:
http://www.cnblogs.com/TenosDoIt/p/3461555.html
```cpp
class Solution {
public:
    vector<vector<int> > subsets(vector<int> &nums) {
        int len = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int> > res(1);//开始加入一个空集

        unsigned long long bit = 1, bitmax = (1 << len);
        vector<int> tmpres;
        while (bit < bitmax) {
            tmpres.clear();
            unsigned long long curBit = bit;
            for (int i = 0; i < len; i++) { //依次检测前len个二进制位
                if (curBit & 1)
                    tmpres.push_back(nums[i]);
                curBit >>= 1;
            }
            res.push_back(tmpres);
            bit++;
        }
        return res;
    }
};
```
