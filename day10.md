# 栈与队列 part02
**题目: 150.波兰表达式求值**     
**位置:**  https://leetcode.cn/problems/evaluate-reverse-polish-notation/description/  
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Map<String,Integer> map = new HashMap<>();
        map.put("+",1);
        map.put("-",2);
        map.put("*",3);
        map.put("/",4);
        Stack<Integer> st = new Stack<>();
        for(String s:tokens){
            if(map.containsKey(s)){
                int num1 = st.pop();
                int num2 = st.pop();
                switch(map.get(s)){ // switch的用法记一下,太久没用忘记了
                    case 1:
                        st.push(num2+num1);
                        break;
                    case 2:
                        st.push(num2-num1);
                        break;
                    case 3:
                        st.push(num2*num1);
                        break;
                    case 4:
                        st.push(num2/num1);
                        break;
                }
            }else{
                st.push(Integer.parseInt(s));
            }
        }
        return st.pop();
    }
}
```
**题目: 239.滑动窗口最大值**  
**位置:** https://leetcode.cn/problems/sliding-window-maximum/description/  
```java
// 关键点在于维护一个单调减的队列(队头最大)
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        Deque<Integer> deque = new ArrayDeque<>();
        int[] ans =new int[nums.length-k+1];
        for(int i=0;i<nums.length;i++){
            int curr = nums[i];
            while(!deque.isEmpty()&& deque.peekFirst()<i-k+1){
                deque.pollFirst();
            }
            while(!deque.isEmpty()&&curr>nums[deque.peekLast()]){//保证队头都是最大值
                deque.pollLast();
            }
            deque.offerLast(i);
            if(i-k+1>=0){
                ans[i-k+1] = nums[deque.peek()];
            }
        }
        return ans;
    }
}
```

**题目: 347.前k个高频元素**  
**位置:**  https://leetcode.cn/problems/top-k-frequent-elements/description/  
```java
class Solution {
    //解法1：基于大顶堆实现
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map = new HashMap<>(); //key为数组元素值,val为对应出现次数
        for (int num : nums) {
            map.put(num, map.getOrDefault(num,0) + 1);
        }
        //在优先队列中存储二元组(num, cnt),cnt表示元素值num在数组中的出现次数
        //出现次数按从队头到队尾的顺序是从大到小排,出现次数最多的在队头(相当于大顶堆)
        PriorityQueue<int[]> pq = new PriorityQueue<>((pair1, pair2) -> pair2[1] - pair1[1]);
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {//大顶堆需要对所有元素进行排序
            pq.add(new int[]{entry.getKey(), entry.getValue()});
        }
        int[] ans = new int[k];
        for (int i = 0; i < k; i++) { //依次从队头弹出k个,就是出现频率前k高的元素
            ans[i] = pq.poll()[0];
        }
        return ans;
    }
}
```
