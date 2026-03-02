# 回溯算法part03  
**题目:93.复原IP地址**  
**位置:**   https://leetcode.cn/problems/restore-ip-addresses/  
```java
class Solution {
    List<String> result = new ArrayList<>();
    List<String> path = new ArrayList<>();
    public List<String> restoreIpAddresses(String s) {
        backTracking(s,0,new StringBuilder());
        return result;
    }
    private void backTracking(String s,int start,StringBuilder sb){
        if(start==s.length()&&path.size()==4){
            StringBuilder strb = new StringBuilder();
            for(String str:path){
                strb.append(str+".");
            }
            result.add(strb.substring(0,strb.length()-1));
        }
        for(int i=start;i<s.length();i++){
            sb.append(s.charAt(i));
            if(check(sb.toString())){
                path.add(sb.toString());
                backTracking(s,i+1,new StringBuilder());
                path.removeLast();
            }else{
                break;
            }
        }
    }
    private boolean check(String s){
        Integer i = Integer.parseInt(s);
        if(i>255){
            return false;
        }
        if(s.length()>1&&s.charAt(0)=='0'){
            return false;
        }
        return true;
    }
}
```
**题目: 78.子集**  
**位置:**  https://leetcode.cn/problems/subsets/description/  
```java
class Solution {
    List<List<Integer>> result =new ArrayList<>();
    List<Integer> path= new ArrayList<>();
    public List<List<Integer>> subsets(int[] nums) {
       backTracing(nums,0);
       return result; 
    }
    private void backTracing(int[] nums,int start){
        result.add(new ArrayList<>(path));
        for(int i=start;i<nums.length;i++){
            path.add(nums[i]);
            backTracing(nums,i+1);
            path.removeLast();
        }
    }
}
```
**题目:90.子集II**  
**位置:**  https://leetcode.cn/problems/subsets-ii/description/  
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
// 去重方法类似 https://leetcode.cn/problems/combination-sum-ii/description/  
class Solution {
    List<Integer> path = new ArrayList<>();
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used;
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        used = new boolean[nums.length];
        backTracking(nums,0);
        return result;
    }
    private void backTracking(int[] nums,int start){
        result.add(new ArrayList<>(path));
        for(int i=start;i<nums.length;i++){
            if(i>0&&nums[i]==nums[i-1]&&used[i-1]==false){
                continue;
            }
            path.add(nums[i]);
            used[i]=true;
            backTracking(nums,i+1);
            path.removeLast();
            used[i]=false;
        }
    }
}
```    
