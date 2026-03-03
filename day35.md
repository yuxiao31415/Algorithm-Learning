# 贪心算法 part04  
**题目: 452. 用最少数量的箭引爆气球**  
**位置:**  https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/description/   
```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        // 二维数组排序 对于右端点排序
        // Arrays.sort(points, (a, b) -> a[1] - b[1]);// 容易出现整数溢出
        Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));// 经典区间贪心策略是：按右端点升序排序
        long currArrow = Long.MIN_VALUE;
        int count =0;
        for(int i=0;i<points.length;i++){
            if(currArrow<points[i][0]){
                currArrow = (long) points[i][1];
                count++;    
            }
        }
        return count;
    }
}
```  
```
右端点
__
____
   ___
左端点
__________
 __
   _______
很明显右端点可以封住上限,只需要判断当前上限跟下一个下限的关系即可
而左端点需要判断当前上限跟下一个的上下限的关系,更为复杂
```
**题目: 435. 无重叠区间**  
**位置:**  https://leetcode.cn/problems/non-overlapping-intervals/description/  
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        if (intervals.length == 0) return 0;

        Arrays.sort(intervals, (a, b) -> 
            Integer.compare(a[1], b[1])// 右端点升序排序
        );

        int count = 1;
        int end = intervals[0][1];

        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] >= end) {
                count++;
                end = intervals[i][1];
            }
        }

        return intervals.length - count;
    }
}
```
**题目:  763.划分字母区间**  
**位置:**  https://leetcode.cn/problems/partition-labels/description/  
```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        char[] s = S.toCharArray();
        int n = s.length;
        int[] last = new int[26];
        for (int i = 0; i < n; i++) {
            last[s[i] - 'a'] = i; // 每个字母最后出现的下标
        }

        List<Integer> ans = new ArrayList<>();
        int start = 0, end = 0;
        for (int i = 0; i < n; i++) {
            end = Math.max(end, last[s[i] - 'a']); // 更新当前区间右端点的最大值
            if (end == i) { // 当前区间合并完毕
                ans.add(end - start + 1); // 区间长度加入答案
                start = i + 1; // 下一个区间的左端点
            }
        }
        return ans;
    }
}
```
