##236. Lowest Common Ancestor of a Binary Tree
> https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

###Solution 1: Recursively
> https://discuss.leetcode.com/topic/18561/4-lines-c-java-python-ruby/2
> https://discuss.leetcode.com/topic/18566/my-java-solution-which-is-easy-to-understand

```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q)  return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        return left == null ? right : right == null ? left : root;
    }
}
```

###Solution 2: Iteratively bottom-up
> https://discuss.leetcode.com/topic/27479/java-python-iterative-solution/2

先找出所有节点到父节点的映射，记录在parent里，<br>
问题转化为求 p到root路径 与 q到root路径 的交点

```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Map<TreeNode, TreeNode> parent = new HashMap<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        parent.put(root, null);
        stack.push(root);

        while (!parent.containsKey(p) || !parent.containsKey(q)) {
            TreeNode node = stack.pop();
            if (node.left != null) {
                parent.put(node.left, node);
                stack.push(node.left);
            }
            if (node.right != null) {
                parent.put(node.right, node);
                stack.push(node.right);
            }
        }
        Set<TreeNode> ancestors = new HashSet<>();
        while (p != null) {
            ancestors.add(p);
            p = parent.get(p);
        }
        while (!ancestors.contains(q))
            q = parent.get(q);
        return q;
    }
}
```

###Solution 3: Iteratively top-down
找从`root到p`和`root到q`的路径，从root出发遍历这两条路径，最后一个相同的节点即为p和q的LCA
```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        List<TreeNode> pathP = null; //保存root到p的路径
        List<TreeNode> pathQ = null; //保存root到q的路径
        Deque<TreeNode> path = new LinkedList<>(); //path 记录root到当前遍历节点的路径
        TreeNode cur = null, pre = null;
        path.offerLast(root);

        while (pathP == null || pathQ == null) {
            cur = path.peekLast();
            if (cur == p) pathP = new ArrayList<>(path);
            if (cur == q) pathQ = new ArrayList<>(path);
            //当前遍历的节点出栈的条件
            if(cur.left == null && cur.right == null
                    || cur.right == null && pre == cur.left
                    || cur.right != null && pre == cur.right) {
                path.pollLast();
                pre = cur;
            } else { //当前遍历的节点入栈的条件
                if(cur.left == null || pre == cur.left) path.offerLast(cur.right);
                else path.offerLast(cur.left);
            }
        }
        int minLen = Math.min(pathP.size(), pathQ.size());
        for (int i = 1; i < minLen; i++) { //遍历pathP和pathQ，寻找从root出发，最后一个相同的节点，即为LCA
            if (pathP.get(i) != pathQ.get(i))
                return pathP.get(i - 1);
        }
        return pathP.get(minLen - 1);
    }
}
```
