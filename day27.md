# 回溯算法part01  
## 理论基础  
回溯 = 试探 + 递归 + 撤销选择    
```
它的本质是一种：  
构造“决策树”
深度优先遍历
不满足条件就“剪枝”
返回上一层继续尝试
```
## 回溯法解决的问题
回溯法，一般可以解决如下几种问题： 
1. 组合问题：N个数里面按一定规则找出k个数的集合   
2. 切割问题：一个字符串按一定规则有几种切割方式   
3. 子集问题：一个N个数的集合里有多少符合条件的子集    
4. 排列问题：N个数按一定规则全排列，有几种排列方式   
5. 棋盘问题：N皇后，解数独等等

## 算法题  
**题目: 77. 组合**  
**位置:**  https://leetcode.cn/problems/combinations/description/  
```java
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans  = new ArrayList<>();
    public List<List<Integer>> combine(int n, int k) {
        backTracking(n,k,1);
        return ans;

    }
    private void backTracking(int n, int k,int start) {
        if(path.size()==k){
            ans.add(new ArrayList<>(path));
            return ;
        }
        for(int i=start;i<=n;i++){
            path.add(i);
            backTracking(n,k,i+1);
            path.remove(path.size()-1);
        }
    }
}  
```
**题目: 216.组合总和III**  
**位置:**   https://leetcode.cn/problems/combination-sum-iii/description/  
```java
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> ans = new ArrayList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        backTracking(k,n,1,0);
        return ans;
    }
    private void backTracking(int k,int target,int start,int sum){
        if(path.size()==k){
            if(target==sum){
                ans.add(new ArrayList<>(path));
            }
            return;
        }
        if(sum>target){// 剪枝
            return;
        }

        for(int i=start;9-i+1>=k-path.size();i++){
                                // 剪枝 ( k-path.size() ) 表示还要选几个
                                 //  9 - i + 1 表示 从i到9 还有几个数字
                                 // 所以得保证 9-i+1>=k-path.size()
            path.add(i);
            sum+=i;
            backTracking(k,target,i+1,sum);
            path.remove(path.size()-1);
            sum-=i;
        }

    }
}  
```
**题目: 17.电话号码的字母组合**  
**位置:**  https://leetcode.cn/problems/letter-combinations-of-a-phone-number/description/    
```java
class Solution {
    private static final String[] MAPPING = new String[]{"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"}; 
    StringBuilder path = new StringBuilder();
    List<String> ans= new ArrayList<>();
    public List<String> letterCombinations(String digits) {
        backTracking(digits,0);
        return ans;
    }
    private void backTracking(String digits,int index){
        if(path.length()==digits.length()){
            ans.add(path.toString());
            return;
        }
        String str = MAPPING[digits.charAt(index)-'0'];// abc
        for(int i=0;i<str.length();i++){
            path.append(str.charAt(i));
            backTracking(digits,index+1);
            path.deleteCharAt(path.length() - 1);
        }
    }
}
```
