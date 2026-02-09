# 二叉树part01  
## 理论基础
### 二叉树的种类
在我们解题过程中二叉树有两种主要的形式：满二叉树和完全二叉树.  
### 满二叉树  
满二叉树：如果一棵二叉树只有度为0的结点和度为2的结点，并且度为0的结点在同一层上，则这棵二叉树为满二叉树  
### 完全二叉树  
完全二叉树的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置  
### 二叉搜索树  
前面介绍的树，都没有数值的，而二叉搜索树是有数值的了，二叉搜索树是一个有序树。
1. 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值；  
2. 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；  
3. 它的左、右子树也分别为二叉排序树
### 平衡二叉搜索树  
又被称为AVL（Adelson-Velsky and Landis）树，  
且具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。  
###  二叉树的存储方式  
二叉树可以链式存储，也可以顺序存储。  
那么链式存储方式就用指针， 顺序存储的方式就是用数组。  
### 二叉树的遍历方式  
二叉树主要有两种遍历方式：  
1. 深度优先遍历：先往深走，遇到叶子节点再往回走。  
2. 广度优先遍历：一层一层的去遍历。

这两种遍历是图论中最基本的两种遍历方式  
那么从深度优先遍历和广度优先遍历进一步拓展，才有如下遍历方式：  
1. 深度优先遍历
前序遍历（递归法，迭代法）  
中序遍历（递归法，迭代法）  
后序遍历（递归法，迭代法）  
3. 广度优先遍历   
层次遍历（迭代法）
### 二叉树的定义   
```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```
### 二叉树递归遍历  
```java
// 前序遍历·递归·LC144_二叉树的前序遍历
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        preorder(root, result);
        return result;
    }

    public void preorder(TreeNode root, List<Integer> result) {
        if (root == null) {
            return;
        }
        result.add(root.val);
        preorder(root.left, result);
        preorder(root.right, result);
    }
}
// 中序遍历·递归·LC94_二叉树的中序遍历
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        return res;
    }

    void inorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        inorder(root.left, list);
        list.add(root.val);             // 注意这一句
        inorder(root.right, list);
    }
}
// 后序遍历·递归·LC145_二叉树的后序遍历
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorder(root, res);
        return res;
    }

    void postorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        postorder(root.left, list);
        postorder(root.right, list);
        list.add(root.val);             // 注意这一句
    }
}
```
### 二叉树的层序遍历  
```java
// 102.二叉树的层序遍历
class Solution {
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();

    public List<List<Integer>> levelOrder(TreeNode root) {
        //checkFun01(root,0);
        checkFun02(root);

        return resList;
    }

    //BFS--递归方式
    public void checkFun01(TreeNode node, Integer deep) {
        if (node == null) return;
        deep++;

        if (resList.size() < deep) {
            //当层级增加时，list的Item也增加，利用list的索引值进行层级界定
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);

        checkFun01(node.left, deep);
        checkFun01(node.right, deep);
    }
}
```
