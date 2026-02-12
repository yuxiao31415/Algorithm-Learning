## 二叉树 part04  
**题目: 513.找树左下角的值**   
**位置:**  https://leetcode.cn/problems/find-bottom-left-tree-value/  
```java
// 自己用层序遍历写的版本 有点low
class Solution {
    List<List<Integer>> list = new ArrayList<>();
    public int findBottomLeftValue(TreeNode root) {
        dfs(root,1);
        List<Integer> list2 =  list.get(list.size()-1);
        for(Integer i:list2){
            if(i!=null){
                return i;
            }
        }
        return -1;
    }
    private void dfs(TreeNode root,int deep){
        if(root==null){
            return;
        }
        if(list.size()<deep){
            list.add(new ArrayList<Integer>() );
        }
        list.get(deep-1).add(root.val);
        dfs(root.left,deep+1);
        dfs(root.right,deep+1);

    }
}
// 升级版,关键点在于维护一个Deep来比较深度,先左递归保证先要左边值
class Solution {
    int ans =0;
    int Deep = -1;
    public int findBottomLeftValue(TreeNode root) {
        ans = root.val;
        dfs(root,1);
        return ans;
        
    }
    private void dfs(TreeNode root,int deep){
        if(root==null){
            return;
        }
        if(root.left==null&&root.right==null){
            if(deep>Deep){
                ans = root.val;
                Deep = deep;
            }
        }
        dfs(root.left,deep+1);
        dfs(root.right,deep+1);
    }
}
```

**题目: 112.路径总和**   
**位置:**  https://leetcode.cn/problems/path-sum/description/   
```java
// 叶子节点 root.left==null&&root.right==null
class Solution { 
    boolean flag = false;
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root==null){
            return false;
        }
        dfs(root,0,targetSum);
        return flag;
    }
    private void dfs(TreeNode root,int sum,int targetSum){
        if(root==null) {
            return;
        }
        sum+=root.val; 
        if(root.left==null&&root.right==null&&sum==targetSum){// 是叶子节点并且此时 sum=targetSum
            flag = true;
        }
           
        dfs(root.left,sum,targetSum);
        dfs(root.right,sum,targetSum);
        sum-=root.val;
    }
}
```

**题目: 113. 路径总和II**   
**位置:**  https://leetcode.cn/problems/path-sum-ii/     
```java
class Solution {
    List<List<Integer>> ans = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        dfs(root,new ArrayList<Integer>(),0,targetSum);
        return ans;
    }
    private void dfs(TreeNode root,List<Integer> path,int sum,int targetSum){
        if(root==null){
            return;
        }
        sum+=root.val;
        path.add(root.val);
        if(root.left==null&&root.right==null&&sum==targetSum){
            //ans.add(path);  注意这个点 加的是地址,所以ans中的全部path都会跟着变化
            ans.add(new ArrayList<>(path));
        }
        dfs(root.left,path,sum,targetSum);
        dfs(root.right,path,sum,targetSum);
        sum-=root.val;
        path.remove(path.size()-1);

    }
}
```
**题目: 106. 从中序与后序遍历序列构造二叉树**   
**位置:**  https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/    
```java

```
