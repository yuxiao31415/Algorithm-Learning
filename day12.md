# 二叉树part02
**题目:  226.翻转二叉树**  
**位置:**  https://leetcode.cn/problems/invert-binary-tree/description/  
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root==null){
            return null;
        }
        TreeNode left = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        return new TreeNode(root.val,right,left);
    }
}
```  

**题目: 101. 对称二叉树**  
**位置:**   https://leetcode.cn/problems/symmetric-tree/  
```java
// 关键点在于看出是left和right具有这种对称关系,所以需要输入left和right而不是root
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isSymmetricTreeNode(root.left,root.right);
    }
    public boolean isSymmetricTreeNode(TreeNode left,TreeNode right){
        if(left==null||right==null){
            return left==right;
        }

        return left.val==right.val&&
                isSymmetricTreeNode(left.left,right.right)&&
                isSymmetricTreeNode(left.right,right.left);

    }
}
```  

**题目: 104.二叉树的最大深度**  
**位置:**  https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/
```java
class Solution {
    public int maxDepth(TreeNode root) {
        return dfs(root);
    }
    private int dfs(TreeNode root){
        if(root==null){
            return 0;
        }
        return Math.max(dfs(root.left),dfs(root.right))+1;
    }
}
```

**题目: 111.二叉树的最小深度**  
**位置:**  
```java
// 最小深度有所不同
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftDepth = minDepth(root.left);
        int rightDepth = minDepth(root.right);
        if (root.left == null) {
            return rightDepth + 1;
        }
        if (root.right == null) {
            return leftDepth + 1;
        }
        // 左右结点都不为null
        return Math.min(leftDepth, rightDepth) + 1;
    }
}
```
