# 哈希表part01  
## 哈希表  
哈希表就是通过hash函数来定位索引的数组  
## hash函数  
hash函数就是通过hashcode将由属性值转化为数值,然后映射到到某个索引处  
但是因为是由大范围映射到小范围(数组长度),所以会有hash冲突  
## hash冲突  
<img width="965" height="702" alt="image" src="https://github.com/user-attachments/assets/895a044d-3950-4c3e-b178-4512be93d9c7" />  
解决hash冲突的方法有 
1. 拉链法　　
索引后跟链表　　
２. 线性探测法
当前位置已经存在元素就向下移动直到找到空位置;

