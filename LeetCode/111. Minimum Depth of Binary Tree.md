## 111. Minimum Depth of Binary Tree
> https://leetcode.com/problems/minimum-depth-of-binary-tree/

#### Solution 1: Recursive
```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (!root)
            return 0;
        if (root->left == NULL)
            return minDepth(root->right) + 1;
        if (root->right == NULL)
            return minDepth(root->left) + 1;
        return min(minDepth(root->left), minDepth(root->right)) + 1;
    }
};
```
#### Solution 2: Iterative
```
 迭代解法同样采用层序遍历(相当于图的BFS），只是在检测到第一个叶子的时候就可以返回了
```
```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        queue<pair<TreeNode*, int>> q;
        if(root == NULL)  return 0;
        q.push(make_pair(root, 1));
        while (!q.empty()) {
            pair<TreeNode*, int> cur = q.front();
            q.pop();
            if (!cur.first->left && !cur.first->right) return cur.second;
            if (cur.first->left)
                q.push(make_pair(cur.first->left, cur.second + 1));
            if (cur.first->right)
                q.push(make_pair(cur.first->right, cur.second + 1));
        }
    }
};
```
