## 二叉树part08  
**题目:  669. 修剪二叉搜索树**  
**位置:**  https://leetcode.cn/problems/trim-a-binary-search-tree/description/  
```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) {
            return null;
        }
        if (root.val < low) {
            return trimBST(root.right, low, high);
        }
        if (root.val > high) {
            return trimBST(root.left, low, high);
        }
        // root在[low,high]范围内
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

**题目: 108.将有序数组转换为二叉搜索树**   
**位置:**  https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/description/  
```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return dfs(nums,0,nums.length-1);
    }
    private TreeNode  dfs(int[] nums,int start,int end){//[]
        if(start>end){
            return null;
        }
        int mid = (start+end)/2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = dfs(nums,start,mid-1);
        root.right = dfs(nums,mid+1,end);
        return root;
    }
}
```

**题目:  538.把二叉搜索树转换为累加树**    
**位置:**  https://leetcode.cn/problems/convert-bst-to-greater-tree/description/  
```java
class Solution {
    int sum=0;
    public TreeNode convertBST(TreeNode root) {
        dfs(root);
        return root;
    }
    private void dfs(TreeNode root){
        if(root==null){
            return;
        }
        dfs(root.right);
        sum +=root.val;
        root.val = sum;
        dfs(root.left);
    }
}
```
