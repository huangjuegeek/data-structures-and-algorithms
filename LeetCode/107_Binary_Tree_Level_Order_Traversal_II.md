## 107. Binary Tree Level Order Traversal II
> https://leetcode.com/problems/binary-tree-level-order-traversal-ii/

#### Solution 1:
```cpp
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> res;
        if(!root)    return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            vector<int> levelRes;
            int size = q.size();
            for(int i = 0; i < size; i++) {
                TreeNode* cur = q.front();
                q.pop();
                if(cur->left)  q.push(cur->left);
                if(cur->right)  q.push(cur->right);
                levelRes.push_back(cur->val);
            }
            res.push_back(levelRes);
        }
        reverse(res.begin(), res.end());  // add this line to reverse the result set
        return res;
    }
};
```
