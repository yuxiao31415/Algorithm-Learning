# 栈与队列 part01
## 基础理论 
**``ArrayDeque``介绍**  
队列模式
```
addLast → → → removeFirst
first → [1][2][3] ← last
```
栈模式
```
push / pop 都在 first
first(top) → [3][2][1] ← last
```  
| 功能          | 栈（Stack 用法） | 队列（Queue 用法） | 等价底层方法                     |
| ------------- | ---------------- | ------------------ | -------------------------------- |
| 入            | `push(e)`        | `offer(e)`         | `addFirst(e)` / `addLast(e)`     |
| 出            | `pop()`          | `poll()`           | `removeFirst()` / `removeLast()` |
| 查看顶部/队首 | `peek()`         | `peek()`           | `peekFirst()` / `peekLast()`     |
| 判断空        | `isEmpty()`      | `isEmpty()`        | 相同                             |

**题目: 232.用栈实现队列**   
**位置:** https://leetcode.cn/problems/implement-queue-using-stacks/description/  
```java
class MyQueue {
    private Deque<Integer> in; // 注意得用Deque这个接口而不是Queue,Queue只有队列的offer poll 方法
    private Deque<Integer> out;
    public MyQueue() {
        this.in = new ArrayDeque<>();
        this.out = new ArrayDeque<>();        
    }
    
    public void push(int x) {
        in.push(x);
    }
    
    public int pop() {
        if(out.isEmpty()){
            while(!in.isEmpty()){
                out.push(in.pop());
            }
        }
        return out.pop();
    }
    
    public int peek() {
        if(out.isEmpty()){
            while(!in.isEmpty()){
                out.push(in.pop());
            }
        }
        return out.peek();
    }
    
    public boolean empty() {
        return in.isEmpty()&&out.isEmpty();
    }
}
```
**题目: 20.有效的括号**  
**位置:** https://leetcode.cn/problems/valid-parentheses/description/  
```java
class Solution {
    public boolean isValid(String s) {
        Map<Character,Character> map = new HashMap<>();
        map.put(')','(');
        map.put(']','[');
        map.put('}','{');
        char[] chars = s.toCharArray();
        Stack<Character> st = new Stack<>();
        for(char c:chars){
            if(!st.isEmpty()&&st.peek()==map.get(c)){
                st.pop();
            }else{
                if(map.containsKey(c)) return false;
                st.push(c);
            }
        }
        return st.isEmpty();
    }
}
```
**题目:  1047.删除字符串中的所有相邻重复项**  
**位置:** https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/description/
```java
class Solution {
    public String removeDuplicates(String s) {
        char[] chars = s.toCharArray();
        StringBuilder ans = new StringBuilder();
        Deque<Character> st = new ArrayDeque<>();
        for(char c:chars){
            if(!st.isEmpty()&&st.peek()==c){
                st.pop();
            }else{
                st.push(c);
            }
        }
        while(!st.isEmpty()){
            ans.append(st.removeLast());
        }
        return ans.toString();
    }
}
```
