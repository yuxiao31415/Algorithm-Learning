# 贪心算法 part01  
## 什么是贪心  
贪心的本质是选择每一阶段的局部最优，从而达到全局最优  
例如，有一堆钞票，你可以拿走十张，如果想达到最大的金额，你要怎么拿？  
指定每次拿最大的，最终结果就是拿走最大数额的钱。  
每次拿最大的就是局部最优，最后拿走最大数额的钱就是推出全局最优。    
## 贪心一般解题步骤  
贪心算法一般分为如下四步：  
将问题分解为若干个子问题  
找出适合的贪心策略  
求解每一个子问题的最优解  
将局部最优解堆叠成全局最优解  
**题目: 455.分发饼干**  
**位置:**  https://leetcode.cn/problems/assign-cookies/  
```java
class Solution {
    // 优先考虑饼干，小饼干先喂饱小胃口
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int start = 0;
        int count = 0;
        for (int i = 0; i < s.length && start < g.length; i++) {
            if (s[i] >= g[start]) {
                start++;
                count++;
            }
        }
        return count;
    }
}
```  
**题目: 376. 摆动序列**  
**位置:**  https://leetcode.cn/problems/wiggle-subsequence/description/  
```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if(nums.length<=1){
            return nums.length;
        }
        int preDiff =0;
        int count = 1;
        int currDiff;
        for(int i=1;i<nums.length;i++){
            currDiff = nums[i]-nums[i-1];
            if((currDiff>0&&preDiff<=0)||(currDiff<0&&preDiff>=0)){
                count++;
                preDiff=currDiff;
            }
        }
        return count;
    }
}
```  
**题目: 53. 最大子序和**   
**位置:**  https://leetcode.cn/problems/maximum-subarray/description/  
```java
// 三种解法: 前缀和 ->贪心->动态规划
//贪心
class Solution {
    public int maxSubArray(int[] nums) {
        
        int sum =Integer.MIN_VALUE;
        int count =0;
        for(int i=0;i<nums.length;i++){
            count+=nums[i];//count 表示子数组的和
            sum=Math.max(sum,count);
            if(count<=0){
                count=0; //  小于零则将子数组的和置为零,下次重新开始计数
                        //   因为否则会拖累后面的计数
            }
        }
        return sum;
    }
}
```


