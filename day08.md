# 字符串part01
**题目: 344.反转字符串**  
**位置:** https://leetcode.cn/problems/reverse-string/  
```java
class Solution {// 跟翻转数组一个思路
    public void reverseString(char[] s) {
        int l=0;
        int r = s.length-1;
        while(l<r){
            char tmp = s[l];
            s[l] = s[r];
            s[r] = tmp;
            l++;
            r--;
        }
    }
}
```

**题目: 541. 反转字符串II**  
**位置:** https://leetcode.cn/problems/reverse-string-ii/description/ 
```java
class Solution {
    public String reverseStr(String s, int k) {
        int len = s.length();//记录剩余要处理的长度；
        char[] chars = s.toCharArray();

        for(int i=2*k;i<=s.length();i+=2*k){// 从2k作为起点,表示只有满足2k时才处理,然后剩下的要是不满足2k就交给后续处理
                                           // 否则从0开始必定会进行一次处理,但是如果原始的string不满足2k长度那就会出问题
            int start = i-2*k;
            int end = i-k-1;//特例法,k=2,  0 1 2 3 4
            len-=2*k;// 记录剩下还未处理的长度
            reverse(chars,start,end);
        }
        if(len<=k){
            reverse(chars,s.length()-len,s.length()-1); // 特例法  只剩下 2 3 (s.length)
        }else if(len>k){ // 特例法: 1 2 3 剩下三个k=2
            reverse(chars,s.length()-len,s.length()-len+k-1);
        }
        return new String(chars);
    }
    private void reverse(char[] s,int start,int end){//[,]
        int r= end;
        int l = start;
        while(l<r){
            char tmp = s[l];
            s[l] =  s[r];
            s[r] = tmp;
            l++;
            r--;
        }
    }
}
```

**题目: 54.替换数字**  
**位置:** https://kamacoder.com/problempage.php?pid=1064  
```java
import java.util.Scanner;// 这块可以写import java.util.* 这样就不用再认为记忆了,每次acm之前都贴上即可
class Main{
    public static void  main(String[] args){
        Scanner sc = new  Scanner(System.in);
        String str = sc.nextLine();
        StringBuilder sb = new StringBuilder();
        char[] chars = str.toCharArray();
        for(char c:chars){
            if('0'<=c&&c<='9'){
                sb.append("number");
            }else{
                sb.append(c);
            }
        }
        System.out.println(sb.toString());

    }
}
```


