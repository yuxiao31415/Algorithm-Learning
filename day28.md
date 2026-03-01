# 回溯算法part02
**题目:  39. 组合总和**    
**位置:**  https://leetcode.cn/problems/combination-sum/description/  
```java
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> reslut = new ArrayList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        int sum=0;
        backTracking(candidates,target,sum,0);
        return reslut;
    }
    private void backTracking(int[] candidates,int target,int sum,int start){
        if(sum==target){
            reslut.add(new ArrayList<>(path));
            return;
        }
        if(sum>target){
            return;
        }
        
        for(int i=start;i<candidates.length;i++){
            path.add(candidates[i]);
            sum+=candidates[i];
            backTracking(candidates,target,sum,i);
            path.remove(path.size()-1);
            sum-=candidates[i];
        }
        
    }
}
```
**题目:  40.组合总和II**    
**位置:**  https://leetcode.cn/problems/combination-sum-ii/description/  
**方法一**   
```java
// 这个方法比较好理解 如果当前元素跟上一个元素相等时,只有上个元素已经存在于path中当前元素才可以用 否则不能用;
class Solution {
  LinkedList<Integer> path = new LinkedList<>();
  List<List<Integer>> ans = new ArrayList<>();
  boolean[] used;
  int sum = 0;

  public List<List<Integer>> combinationSum2(int[] candidates, int target) {
    used = new boolean[candidates.length];
    // 加标志数组，用来辅助判断同层节点是否已经遍历
    Arrays.fill(used, false);
    // 为了将重复的数字都放到一起，所以先进行排序
    Arrays.sort(candidates);
    backTracking(candidates, target, 0);
    return ans;
  }

  private void backTracking(int[] candidates, int target, int startIndex) {
    if (sum == target) {
      ans.add(new ArrayList(path));
    }
    for (int i = startIndex; i < candidates.length; i++) {
      if (sum + candidates[i] > target) {
        break;
      }
      // 出现重复节点，同层的第一个节点已经被访问过，所以直接跳过
      if (i > 0 && candidates[i] == candidates[i - 1] && !used[i - 1]) {
        continue;
      }
      used[i] = true;
      sum += candidates[i];
      path.add(candidates[i]);
      // 每个节点仅能选择一次，所以从下一位开始
      backTracking(candidates, target, i + 1);
      used[i] = false;
      sum -= candidates[i];
      path.removeLast();
    }
  }
}  
```
**方法二**    
```java
class Solution {
  List<List<Integer>> res = new ArrayList<>();
  LinkedList<Integer> path = new LinkedList<>();
  int sum = 0;
  
  public List<List<Integer>> combinationSum2( int[] candidates, int target ) {
    //为了将重复的数字都放到一起，所以先进行排序
    Arrays.sort( candidates );
    backTracking( candidates, target, 0 );
    return res;
  }
  
  private void backTracking( int[] candidates, int target, int start ) {
    if ( sum == target ) {
      res.add( new ArrayList<>( path ) );
      return;
    }
    for ( int i = start; i < candidates.length && sum + candidates[i] <= target; i++ ) {
      //正确剔除重复解的办法
      //跳过同一树层使用过的元素
      if ( i > start && candidates[i] == candidates[i - 1] ) {
        continue;
      }

      sum += candidates[i];
      path.add( candidates[i] );
      // i+1 代表当前组内元素只选取一次
      backTracking( candidates, target, i + 1 );

      int temp = path.getLast();
      sum -= temp;
      path.removeLast();
    }
  }
}
```  
**题目:  131.分割回文串**     
**位置:**   https://leetcode.cn/problems/palindrome-partitioning/description/  
```java
class Solution {
    List<List<String>>  reslut = new ArrayList<>();
    List<String> path = new ArrayList<>();

    public List<List<String>> partition(String s) {
        backTracking(s,0,new StringBuilder());
        return reslut;
    }
    private void backTracking(String s,int start,StringBuilder sb){
        if(start == s.length()){
            reslut.add(new ArrayList<>(path));
            return;
        }
        for(int i=start;i<s.length();i++){
            sb.append(s.charAt(i));
            if(check(sb.toString())){
                path.add(sb.toString());
                backTracking(s,i+1,new StringBuilder());
                path.removeLast();
            }
        }
    }
    private boolean check(String s){
        int left=0;
        int right = s.length()-1;
        while(left<right){
            if(s.charAt(left++)!=s.charAt(right--)){
                return false;
            }
        }
        return true;
    }
}
```
