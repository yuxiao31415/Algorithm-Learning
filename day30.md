# 回溯算法 part04
**题目:491.递增子序列**  
**位置:**  https://leetcode.cn/problems/non-decreasing-subsequences/description/  
```
            []
        /    |    \
       1     2     2
     /  \    | 
    2    2   2
同层 树层去重
path 树枝去重
```
```java
// 本题难点在于同层去重
class Solution {
    List<List<Integer>>  result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> findSubsequences(int[] nums) {
            backTracking(nums,0);
            return result;
    }
    private void backTracking(int[] nums,int start){
        if(path.size()>=2){
            result.add(new ArrayList<>(path));
        }
        Set<Integer> set = new HashSet<>();
        for(int i=start;i<nums.length;i++){
            if(!path.isEmpty()&&path.getLast()>nums[i]||set.contains(nums[i])){
                continue;
            }
            set.add(nums[i]);
            path.add(nums[i]);
            backTracking(nums,i+1);
            path.removeLast();
        }
    }
}
```
**题目: 46.全排列**    
**位置:**  https://leetcode.cn/problems/permutations/description/  
```java
// 同枝去重 used
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    boolean[] used ;
    public List<List<Integer>> permute(int[] nums) {
        used = new boolean[nums.length];
        backTracking(nums);
        return result;
        
    }
    private void backTracking(int[] nums){
        if(path.size()==nums.length){
            result.add(new ArrayList<>(path));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if(used[i]==true){
                continue;
            }
            path.add(nums[i]);
            used[i]=true;
            backTracking(nums);
            path.removeLast();
            used[i]=false;
        }
    }
}
```
**题目:47.全排列 II**  
**位置:**  https://leetcode.cn/problems/permutations-ii/description/   
```java
// 同层去重+同枝去重
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    boolean[] pathused;
    public List<List<Integer>> permuteUnique(int[] nums) {
        pathused = new boolean[nums.length];
        backTracking(nums);
        return result;
    }
    private void backTracking(int[] nums){
        if(path.size()==nums.length){
            result.add(new ArrayList<>(path));
            return;
        }
        Set<Integer> set = new HashSet<>();
        for(int i=0;i<nums.length;i++){
            if(pathused[i]==true||set.contains(nums[i])){
                continue;
            }
            set.add(nums[i]);

            pathused[i]=true;
            path.add(nums[i]);
            backTracking(nums);
            path.removeLast();
            pathused[i]=false;
        }
    }
}  
```

**题目: 51.N皇后**  
**位置:**  https://leetcode.cn/problems/n-queens/description/  
```java
// 方法2：使用boolean数组表示已经占用的直(斜)线
class Solution {
    List<List<String>> res = new ArrayList<>();
    boolean[] usedCol, usedDiag45, usedDiag135;    // boolean数组中的每个元素代表一条直(斜)线
    public List<List<String>> solveNQueens(int n) {
        usedCol = new boolean[n];                  // 列方向的直线条数为 n
        usedDiag45 = new boolean[2 * n - 1];       // 45°方向的斜线条数为 2 * n - 1
        usedDiag135 = new boolean[2 * n - 1];      // 135°方向的斜线条数为 2 * n - 1
		//用于收集结果, 元素的index表示棋盘的row，元素的value代表棋盘的column
        int[] board = new int[n];
        backTracking(board, n, 0);
        return res;
    }
    private void backTracking(int[] board, int n, int row) {
        if (row == n) {
            //收集结果
            List<String> temp = new ArrayList<>();
            for (int i : board) {
                char[] str = new char[n];
                Arrays.fill(str, '.');
                str[i] = 'Q';
                temp.add(new String(str));
            }
            res.add(temp);
            return;
        }

        for (int col = 0; col < n; col++) {
            if (usedCol[col] | usedDiag45[row + col] | usedDiag135[row - col + n - 1]) {
                continue;
            }
            board[row] = col;
			// 标记该列出现过
            usedCol[col] = true;
			// 同一45°斜线上元素的row + col为定值, 且各不相同
            usedDiag45[row + col] = true;
			// 同一135°斜线上元素row - col为定值, 且各不相同
			// row - col 值有正有负, 加 n - 1 是为了对齐零点
            usedDiag135[row - col + n - 1] = true;
            // 递归
            backTracking(board, n, row + 1);
            usedCol[col] = false;
            usedDiag45[row + col] = false;
            usedDiag135[row - col + n - 1] = false;
        }
    }
}
```

