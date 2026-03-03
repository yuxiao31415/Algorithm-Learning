# 贪心算法 part02
**题目: 122.买卖股票的最佳时机II**  
**位置:**  https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/description/    
```java
class Solution {
    public int maxProfit(int[] prices) {
        int pre = prices[0];
        int sum =0;
        for(int i=1;i<prices.length;i++){
            if(prices[i]>pre){
                sum+=(prices[i]-pre);
            }
            pre = prices[i];
        }
        return sum;
    }
}
```
**题目: 55. 跳跃游戏**  
**位置:**  https://leetcode.cn/problems/jump-game/description/    
```java
class Solution {
    public boolean canJump(int[] nums) {
        int maxSize = 0;//上一步的最大距离
        for(int i=0;i<nums.length;i++){
            if(i>maxSize){
                return false;
            }
            maxSize = Math.max(maxSize,i+nums[i]);
        }
        return true;
    }
}
```
**题目: 45.跳跃游戏II**   
**位置:**  https://leetcode.cn/problems/jump-game-ii/description/     
```java
class Solution {
    public int jump(int[] nums) {
        int ans = 0;
        int curRight = 0; 
        int nextRight = 0; 
        for (int i = 0; i < nums.length - 1; i++) {// 注意nums.length -1
            
            nextRight = Math.max(nextRight, i + nums[i]);
            if (i == curRight) { 
                curRight = nextRight; 
                ans++;
            }
        }
        return ans;
    }
}

```
**题目: 1005.K次取反后最大化的数组和**  
**位置:**  https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/  
```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        if (nums.length == 1) return nums[0];

        // 排序：先把负数处理了
        Arrays.sort(nums); 

        for (int i = 0; i < nums.length && k > 0; i++) { // 贪心点, 通过负转正, 消耗尽可能多的k
            if (nums[i] < 0) {
                nums[i] = -nums[i];
                k--;
            }
        }

        // 退出循环, k > 0 || k < 0 (k消耗完了不用讨论)
        if (k % 2 == 1) { // k > 0 && k is odd：对于负数：负-正-负-正
            Arrays.sort(nums); // 再次排序得到剩余的负数，或者最小的正数
            nums[0] = -nums[0];
        }
        // k > 0 && k is even，flip数字不会产生影响: 对于负数: 负-正-负；对于正数：正-负-正 

        int sum = 0;
        for (int num : nums) { // 计算最大和
            sum += num;
        }
        return sum;
    }
}
```

