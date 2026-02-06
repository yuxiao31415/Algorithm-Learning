# 栈与队列 part01
## 基础理论 
**``ArrayDeque``介绍**  
对比  
| 功能          | 栈（Stack 用法） | 队列（Queue 用法） | 等价底层方法                     |
| ------------- | ---------------- | ------------------ | -------------------------------- |
| 入            | `push(e)`        | `offer(e)`         | `addFirst(e)` / `addLast(e)`     |
| 出            | `pop()`          | `poll()`           | `removeFirst()` / `removeLast()` |
| 查看顶部/队首 | `peek()`         | `peek()`           | `peekFirst()` / `peekLast()`     |
| 判断空        | `isEmpty()`      | `isEmpty()`        | 相同                             |

