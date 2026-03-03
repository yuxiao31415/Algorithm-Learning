# 贪心算法 part03
**题目: 134. 加油站**  
**位置:**  https://leetcode.cn/problems/gas-station/description/
```java
// 题目关键
// 结论1：如果总油量 < 总消耗 → 一定无解
// 结论2：如果总和 >= 0，一定有唯一解
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int curSum = 0;
        int totalSum = 0;
        int index = 0;
        for (int i = 0; i < gas.length; i++) {
            curSum += gas[i] - cost[i];
            totalSum += gas[i] - cost[i];
            if (curSum < 0) {
                index = (i + 1) % gas.length ; // 也可以不取余,因为到最后一个元素时i+1就表明total<0 直接返回负一
                curSum = 0;
            }
        }
        if (totalSum < 0) return -1;
        return index;
    }
}
```
**题目: 135. 分发糖果**  
**位置:** https://leetcode.cn/problems/candy/  
```java
class Solution {
    public int candy(int[] ratings) {
        int[] count = new int[ratings.length];
        count[0]=1;
        for(int i=1;i<count.length;i++){
            count[i] = ratings[i] > ratings[i-1]? count[i-1] + 1: 1;// 右侧比左侧高,右侧加1
            
        }

        for(int i=count.length-2;i>=0;i--){
            if(ratings[i]>ratings[i+1]){// 左侧大,取本身和右侧加1的最大值
                                        // 因为不能影响左->右的遍历结果
                                        // 左->右的遍历结果 保证了 当前元素(i)大于上一个元素(i-1)的情况
                                        // 所以不能覆盖,只能取最大值  
                count[i] = Math.max(count[i],count[i+1]+1);

            }
        }
        int sum=0;
        for(int i:count){
            sum+=i;
        }
        return sum;
    }
}
```
**题目: 860.柠檬水找零**  
**位置:**  https://leetcode.cn/problems/lemonade-change/description/  
```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0;
        int ten = 0;

        for (int i = 0; i < bills.length; i++) {
            if (bills[i] == 5) {
                five++;
            } else if (bills[i] == 10) {
                five--;
                ten++;
            } else if (bills[i] == 20) {
                if (ten > 0) {//  这块体现了贪心,5的用处更广,所有有10先用10
                    ten--;
                    five--;
                } else {
                    five -= 3;
                }
            }
            if (five < 0 || ten < 0) return false;
        }
        
        return true;
    }
}
```
**题目: 406.根据身高重建队列**  
**位置:**
```java
pass
```
