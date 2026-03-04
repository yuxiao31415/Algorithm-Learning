# 贪心算法 part05  
**题目: 56. 合并区间**  
**位置:**  https://leetcode.cn/problems/merge-intervals/description/  
```java
class Solution {
    public int[][] merge(int[][] intervals) {
       List<int[]> list = new ArrayList<>();
       Arrays.sort(intervals,(a,b)-> a[0]-b[0]);
       for(int i=0;i<intervals.length;i++){
            if(!list.isEmpty()&&intervals[i][0]<=list.getLast()[1]){
                int[] last = list.getLast();
                if(last[1]<intervals[i][1]){
                    last[1] = intervals[i][1];
                }
            }else{
                list.add(new int[]{intervals[i][0],intervals[i][1]});
            }
       }
       return list.toArray(new int[list.size()][]); 
    }
}
```
**题目: 738.单调递增的数字**  
**位置:**  https://leetcode.cn/problems/monotone-increasing-digits/description/   
```java
// 一旦出现下降,当前位置减一,后面全变成9
// 多位下降,最终把最左边的减一,后面全变成9
class Solution {
    public int monotoneIncreasingDigits(int n) {
        String s = String.valueOf(n);
        char[] chars = s.toCharArray();
        int start = s.length();
        for (int i = s.length() - 2; i >= 0; i--) {
            if (chars[i] > chars[i + 1]) {
                chars[i]--;
                start = i+1;
            }
        }
        for (int i = start; i < s.length(); i++) {
            chars[i] = '9';
        }
        return Integer.parseInt(String.valueOf(chars));
    }
}
```

