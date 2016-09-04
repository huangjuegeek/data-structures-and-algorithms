## 245. Subtree
> http://www.lintcode.com/en/problem/subtree/

#### Solution 1:
```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */
class Solution {
public:
    /**
     * @param T1, T2: The roots of binary tree.
     * @return: True if T2 is a subtree of T1, or false.
     */
    bool isIdentical(TreeNode* t1, TreeNode* t2) {
        if(t1 == NULL || t2 == NULL) {
            return t1 == t2;
        }
        if(t1->val != t2->val) {
            return false;
        }
        return isIdentical(t1->left, t2->left) && isIdentical(t1->right, t2->right);
    }
    
    bool isSubtree(TreeNode *T1, TreeNode *T2) {
        if(T2 == NULL) {
            return true;
        }
        if(T1 == NULL) {
            return false;
        }
        if(isIdentical(T1, T2)) {
            return true;
        }
        if(isSubtree(T1->left, T2) || isSubtree(T1->right, T2)) {
            return true;
        }
        return false;
    }
};
```
