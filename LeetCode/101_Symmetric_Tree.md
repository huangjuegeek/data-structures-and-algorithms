## 101. Symmetric Tree
> https://leetcode.com/problems/symmetric-tree/

#### Solution 1: Recursive
> http://bangbingsyb.blogspot.com/2014/11/leetcode-symmetric-tree.html

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode *root) {
        return isSym(root, root);
    }

    bool isSym(TreeNode *lr, TreeNode *rr) {
        if(!lr && !rr) return true;
        if((!lr || !rr)) return false;
        if(lr == rr) return isSym(lr->left, lr->right); // lr and rr both point to root
        if(lr->val != rr->val) return false;
        return isSym(lr->left, rr->right) && isSym(lr->right, rr->left);
    }
};
```
#### Solution 2: Iterative
```cpp
class Solution {
public:
    bool isSymmetric(TreeNode *root) {
        if(!root) return true;
        queue<TreeNode*> ql, qr;
        ql.push(root->left);
        qr.push(root->right);
        
        while(!ql.empty() && !qr.empty()) {
            TreeNode *lnode = ql.front();
            TreeNode *rnode = qr.front();
            ql.pop();
            qr.pop();
            
            if(!lnode && !rnode) continue;
            if((!lnode && rnode) || (lnode && !rnode)) return false;
            if(lnode->val != rnode->val) return false;
            ql.push(lnode->left);
            qr.push(rnode->right);
            ql.push(lnode->right);
            qr.push(rnode->left);
        }
        
        if(!ql.empty() || !qr.empty()) return false;
        return true;
    }
};
```
