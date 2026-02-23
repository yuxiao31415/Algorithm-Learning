# 二叉树 part05  
**题目: 654.最大二叉树**  
**位置:**  https://leetcode.cn/problems/maximum-binary-tree/  
```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return dfs(nums);
    }
    private TreeNode dfs(int[] nums){
        int len = nums.length;
        if(len==0){
            return null;
        }
        int index = maxValueIndex(nums);
        int[] leftNums = Arrays.copyOfRange(nums,0,index);
        int[] rightNums = Arrays.copyOfRange(nums,index+1,len);
        TreeNode left = dfs(leftNums);
        TreeNode right = dfs(rightNums);
        return new TreeNode(nums[index],left,right);
    } 
    private int maxValueIndex(int[] nums){
        int maxIndex =0;
        for(int i=1;i<nums.length;i++){
            if(nums[maxIndex]<nums[i]){
                maxIndex=i;
            }
        }
        return maxIndex;

    }
}
```
 
**题目:  617.合并二叉树**  
**位置:**  https://leetcode.cn/problems/merge-two-binary-trees/description/  
```java
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if (root1 == null) return root2;
        if (root2 == null) return root1;
        return new TreeNode(root1.val + root2.val,
            mergeTrees(root1.left, root2.left),    // 合并左子树
            mergeTrees(root1.right, root2.right)); // 合并右子树
    }
    }
}  
```
**题目:  700.二叉搜索树中的搜索**  
**位置:**  https://leetcode.cn/problems/search-in-a-binary-search-tree/description/    
```java
class Solution {
    private TreeNode ans = null;
    public TreeNode searchBST(TreeNode root, int val) {
        dfs(root,val);
        return ans;
    }
    private void dfs(TreeNode root,int val){
        if(root==null){
            ans=null;
            return;
        }
        if(root.val==val){
            ans= root;
        }else if(val<root.val){
            dfs(root.left,val);
        }else{
            dfs(root.right,val);
        }
    }
}  
```
**题目:  98.验证二叉搜索树**   
**位置:**  https://leetcode.cn/problems/validate-binary-search-tree/description/      
```java
class Solution {
    private long pre = Long.MIN_VALUE;
    public boolean isValidBST(TreeNode root) {
        if(root==null){
            return true;
        }
        boolean l = isValidBST(root.left);
        if(root.val<=pre){
            return false;
        }
        pre = root.val;
        boolean r = isValidBST(root.right);
        return l&&r;

    }
}
```
 
