# 二叉树part03
**题目:  110.平衡二叉树**  
**位置:** https://leetcode.cn/problems/balanced-binary-tree/     
```java
class Solution {
    boolean flag = true; 
    public boolean isBalanced(TreeNode root) {
        maxDeep(root);
        return flag;
    }
    private int maxDeep(TreeNode root){
        if(root==null){
            return 0;
        }
        int leftDeep = maxDeep(root.left);
        int rightDeep = maxDeep(root.right);
        if(Math.abs(leftDeep-rightDeep)>1){
            flag= false;
        }
        return Math.max(leftDeep,rightDeep)+1;
    }
}
```

**题目: 257. 二叉树的所有路径**  
**位置:**   https://leetcode.cn/problems/binary-tree-paths/description/  
```java
class Solution {// 使用string效率低但是不许要回溯,而使用StringBuilder需要手动回溯
    List<String> ans = new ArrayList<>();
    public List<String> binaryTreePaths(TreeNode root) {
        StringBuilder path = new StringBuilder();
        dfs(root,path);
        return ans;
    }
    private void dfs(TreeNode root,StringBuilder path){
        if(root==null) return;
        int len = path.length(); // 记录当前长度，用于回溯
        path.append(root.val);
        if(root.left==null&&root.right==null){
            ans.add(path.toString());
        }else{
             path.append("->");
            dfs(root.left,path);
            dfs(root.right,path);
        }
        //回溯
        path.setLength(len); 
    }

}
```

**题目: 404.左叶子之和**  
**位置:**   https://leetcode.cn/problems/sum-of-left-leaves/description/   
```java
class Solution {
    int ans =0;
    public int sumOfLeftLeaves(TreeNode root) {
        dfs(root);
        return ans;
    }
    private void dfs(TreeNode root){
        if(root==null){
            return;
        }
        if(isLeaf(root.left)){
            ans+=root.left.val;
        }
        dfs(root.left);
        dfs(root.right);
    }
    private boolean isLeaf(TreeNode root){
        return root!=null&&
                root.left==null&&
                root.right==null;
    }
}
```

**题目:  222.完全二叉树的节点个数**  
**位置:**  https://leetcode.cn/problems/count-complete-tree-nodes/  
```java
class Solution {
    int ans =0;
    public int countNodes(TreeNode root) {
        dfs(root);
        return ans;
    }
    private void dfs(TreeNode root){
        if(root==null){
            return;
        }
        ans++;
        dfs(root.left);
        dfs(root.right);
    }
}
``` 
