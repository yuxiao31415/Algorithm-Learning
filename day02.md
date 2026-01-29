# 数组part02
## 滑动窗口  
**题目: 209.长度最小子数组**  
**位置:** https://leetcode.cn/problems/minimum-size-subarray-sum/  
```java
// 暴力解法
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int ans=Integer.MAX_VALUE;
        int sum=0;
        for(int i=0;i<nums.length;i++){
            for(int j=i;j<nums.length;j++){// j从i开始, 不要从i+1开始,然后让外层for来处理i位置元素
                                           // 让所有元素的处理都在一个for循环内
                sum+=nums[j];
                if(sum>=target){
                    ans=Math.min(j-i+1,ans);
                    break;
                }
            }
            sum=0;
            
        }
        return ans==Integer.MAX_VALUE?0:ans;

    }
}

// 滑动窗口
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int ans=Integer.MAX_VALUE;
        int sum=0;
        int l=0;
        for(int r=0;r<nums.length;r++){// 滑动窗口只能用于单调序列,右侧不断增,通过左侧元素来调整大小
            sum+=nums[r];
            while(sum>=target){
                ans=Math.min(r-l+1,ans);
                sum-=nums[l++];
            }
        }
        return ans==Integer.MAX_VALUE?0:ans;

    }
} 
```
**题目: 59.螺旋矩阵II**  
**位置:** https://leetcode.cn/problems/spiral-matrix-ii/description/  
```java
class Solution {
    final static int[][] DIRS={{0,1},{1,0},{0,-1},{-1,0}}; // 关键点1. 分别表示 [行不变,列右移] [行下移,列不变] [行不变,列右移] [行上移,列不变]
    public int[][] generateMatrix(int n) {
        int[][] matrix=new int[n][n];
        int count = 1;
        int r=n;// 记录行和列的值     // 关键点2. 列和行的长度分开计算,因为规律是按照行列分开来看的: 第一次全列, (从此开始规律)第二次全行-1;第三次全列-1;第三次全行-2;第四次全列-2
        int c=n;
        int x=0;
        int y=-1;//关键单3. 起始点从(0,-1)开始-> 1. (0,0)不用手动加入 2.列长度可以从n开始,否则得第一次得是全列-1;
        for(int dir=0;count<=n*n;dir=(dir+1)%4){// 关键点4. 外层改变方向dir
            for(int i=0;i<c;i++){   // 关键点4. 内层遍历列或者行
                x=x+DIRS[dir][0];   // 关键点5. 这个写法得明白
                y=y+DIRS[dir][1];
                matrix[x][y]=count++;
            }
            int temp=c; // 关键点6. 每次遍历长度的规则,第一次全列已经在上面处理了,后面按照这个规则来
            c=r-1;
            r=temp;
        }
        return matrix;
    }
}
```
**题目: 54.螺旋矩阵**  
**位置:** https://leetcode.cn/problems/spiral-matrix/description/?envType=study-plan-v2&envId=top-100-liked
```java
// 与 59.螺旋矩阵II解法完全一致
class Solution {
    private final int[][] DIRS = {{0,1},{1,0},{0,-1},{-1,0}};
    public List<Integer> spiralOrder(int[][] matrix) {
        int m= matrix.length;
        int n = matrix[0].length;
        int size =m*n;
        List<Integer> ans =new ArrayList<>(size);
        int i=0;
        int j=-1;
        for(int dis =0;ans.size()<size;dis=(dis+1)%4){
            for(int k=0;k<n;k++){
                i+=DIRS[dis][0];
                j+=DIRS[dis][1];
                ans.add(matrix[i][j]);
            }
            int tmp =n;
            n=m-1;
            m = tmp; 
        }
        return ans;
    }
}
```
## 前缀和  
**题目: 58.区间和**  
**位置:** https://kamacoder.com/problempage.php?pid=1070  
```java
// 之前只写过leetcode模式
// 以及在idea的自动补全的模式下的代码
// 这是第一次实际写这种acm风格的代码,感觉还是很不一样,特别是没有自动补全,一时有点不适应
import java.util.Scanner;
class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] pre = new int[n+1];
        for(int i=1;i<=n;i++){
            pre[i]=pre[i-1]+sc.nextInt();
        }
        while(sc.hasNextInt()){
            int a=sc.nextInt();
            int b = sc.nextInt();

            int sum=pre[b+1]-pre[a];
            System.out.println(sum);
        }
        sc.close();
    }
}
```
**题目: 44.开发商购买土地**  
**位置:** https://kamacoder.com/problempage.php?pid=1044  
```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[][] matrix = new int[n][m];
        int sum=0; 
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                matrix[i][j]=sc.nextInt();
                sum+=matrix[i][j];
            }
        }
        int ans = Integer.MAX_VALUE;
        // 行分割
        int count=0;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                count+=matrix[i][j];
                if(j==m-1){
                    ans=Math.min(ans,Math.abs(sum-count-count));
                }
            }
        }

        // 列分割
        count=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                count+=matrix[j][i];
                if(j==n-1){
                    ans=Math.min(ans,Math.abs(sum-count-count));
                }
            }
        }
        System.out.println(ans);
    }
}
```
## 数组总结
### 题型: 二分法,双指针,滑动窗口,前缀和,二维数组  
#### 二分法
两种写法,1.左闭右开 2.左开右开
#### 双指针  
**1. 快慢指针**   
**1.1** 快指针在for内循环,慢指针根据条件移动  
**1.2** 链表中常用到 slow=slow.next fast=fast.next.next这种移动模式  
**2.碰撞指针**   
while循环内left右移,right左移  
#### 滑动窗口  
**主要用于单调的序列**  
**1.定长窗口**  
一般可以不定义left,直接用right-len+1等表示    
可以根据这个right-len+1是否小于零来判断此时整个窗口都进入数组了没有  
**2.变长窗口**  
得定义left,根据条件手动调整left    
#### 前缀和  
前缀和的作用主要就在于可以将计算**连续序列的和**转换为计算**任意位置的差**  
#### 二维数组  
二维数组一般都需要定义DIRS这个方向二维数组,多数情况下都能够简化代码   
还得注意外层是循环遍历方向  




