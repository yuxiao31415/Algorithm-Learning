# 二叉树part07
**题目: 235. 二叉搜索树的最近公共祖先**  
**位置:**  https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/description/  
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left, p, q);
        if (root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);
        return root;
    }
}  
```
**题目: 701.二叉搜索树中的插入操作**  
**位置:**  https://leetcode.cn/problems/insert-into-a-binary-search-tree/description/  
```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(root==null){
            return new TreeNode(val);
        }
        dfs(root,val);
        return root;
    }
    private void dfs(TreeNode root, int val){


        if(root.val<val){
            if(root.right==null){
                root.right = new TreeNode(val);
                return;
            }
            insertIntoBST(root.right,val);
        }
        if(root.val>val){
            if(root.left==null){
                root.left = new TreeNode(val);
            }
            insertIntoBST(root.left,val);
        }
    }
}  
```
**题目:  450.删除二叉搜索树中的节点**  
**位置:**  https://leetcode.cn/problems/delete-node-in-a-bst/description/  
```java
class Solution {
  public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return root;
    if (root.val == key) {
      if (root.left == null) {
        return root.right;
      } else if (root.right == null) {
        return root.left;
      } else {
        TreeNode cur = root.right;
        while (cur.left != null) {
          cur = cur.left;
        }
        cur.left = root.left;
        root = root.right;
        return root;
      }
    }
    if (root.val > key) root.left = deleteNode(root.left, key);
    if (root.val < key) root.right = deleteNode(root.right, key);
    return root;
  }
}
```
