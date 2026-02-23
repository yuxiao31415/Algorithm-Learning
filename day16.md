##  二叉树part07 
**题目:  530.二叉搜索树的最小绝对差**  
**位置:**  https://leetcode.cn/problems/minimum-absolute-difference-in-bst/description/   
```java
class Solution { // 跟day15的 98.验证二叉搜索树  思路类似
    TreeNode pre;
    int ans =  Integer.MAX_VALUE;
    public int getMinimumDifference(TreeNode root) {
        dfs(root);
        return ans;
        
    }
    private void  dfs(TreeNode root){
        if(root==null){
            return;
        }
        dfs(root.left);
        if(pre!=null){
            ans = Math.min(ans,Math.abs(root.val-pre.val));
        }
        pre = root;
        dfs(root.right);
    }
}
```
**题目: 501.二叉搜索树中的众数**  
**位置:**  https://leetcode.cn/problems/find-mode-in-binary-search-tree/description/   
```java
class Solution {
    ArrayList<Integer> resList;
    int maxCount;
    int count;
    TreeNode pre;

    public int[] findMode(TreeNode root) {
        resList = new ArrayList<>();
        maxCount = 0;
        count = 0;
        pre = null;
        findMode1(root);
        int[] res = new int[resList.size()];
        for (int i = 0; i < resList.size(); i++) {
            res[i] = resList.get(i);
        }
        return res;
    }

    public void findMode1(TreeNode root) { 
        if (root == null) {
            return;
        }
        findMode1(root.left);

        int rootValue = root.val;
        // 计数
        if (pre == null || rootValue != pre.val) {
            count = 1;
        } else {
            count++;
        }
        // 更新结果以及maxCount
        if (count > maxCount) {
            resList.clear();
            resList.add(rootValue);
            maxCount = count;
        } else if (count == maxCount) {
            resList.add(rootValue);
        }
        pre = root;

        findMode1(root.right);
    }
}
```
**题目: 236. 二叉树的最近公共祖先**  
**位置:**  https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/description/  
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null||root==p||root==q){
            return root;
        }
        TreeNode left =lowestCommonAncestor(root.left,p,q);
        TreeNode right =lowestCommonAncestor(root.right,p,q);
        if(left!=null&&right!=null){
            return root;
        }
        return left != null ? left : right;
    }
}
```

