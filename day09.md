# 字符串 part02
**题目: 151.翻转字符串里的单词**  
**位置:**  https://leetcode.cn/problems/reverse-words-in-a-string/description/   
```java
class Solution {
    public String reverseWords(String s) {
        s = s.trim();                                    // 删除首尾空格
        int j = s.length() - 1, i = j;
        StringBuilder res = new StringBuilder();
        while (i >= 0) {
            while (i >= 0 && s.charAt(i) != ' ') i--;     // 搜索首个空格
            res.append(s.substring(i + 1, j + 1) + " "); // 添加单词
            while (i >= 0 && s.charAt(i) == ' ') i--;     // 跳过单词间空格
            j = i;                                       // j 指向下个单词的尾字符
        }
        return res.toString().trim();                    // 转化为字符串并返回
    }
}
```  
**题目: 55.右旋转字符串**  
**位置:**   https://kamacoder.com/problempage.php?pid=1065 
```java
import java.util.*;
class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int k = Integer.parseInt(sc.nextLine());
        String s = sc.nextLine();
        char[] ans = new char[s.length()];
        int rightIndex = s.length()-k;
        int leftIndex = 0;
        for(int i=0;i<ans.length;i++){
            if(rightIndex<ans.length){
                ans[i]=s.charAt(rightIndex++);

            }else{
                ans[i]=s.charAt(leftIndex++);
            }
        }
        System.out.println(new String(ans));
    }
}
//该方法更为简单
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int k = sc.nextInt();
        String s = sc.next();
        StringBuilder sb = new StringBuilder();
        sb.append(s.substring(s.length() - k, s.length()));
        sb.append(s.substring(0, s.length() - k));
        System.out.println(sb.toString());
    }
}
```  
**题目: 28. 实现 strStr()**   
**位置:**  https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/description/   
```java
/*
1、next数组初始化不用想，next[0] =0,因为首字符没有前后缀这一说(知道什么叫做前缀以及后缀)，
下面就是定义双指针了，i表示后缀的末尾位置，j表示前缀的末尾位置，也表示最长公共前后缀的长度，
j = 0，后序遍历i从1开始，注意：i与j都表示的是next数组下标的位置。
2、前后缀位置所指的字符相等的情况(i,j)
3、前后缀位置所指的元素不相等的情况
4、更新next数组；
*/
// aabaabaafa aabaaf这个例子最契合
class Solution {
    // KMP 算法
    // ss: 原串(string)  pp: 匹配串(pattern)
    // next[i] 表示什么？ 匹配串前 i 个字符中，最长的相等前后缀长度
    // j表示最长的相等前后缀长度,所以必须从零开始
    public int strStr(String ss, String pp) {
        if (pp.isEmpty()) return 0;
        
        // 分别读取原串和匹配串的长度
        int n = ss.length(), m = pp.length();
        // 原串和匹配串前面都加空格，使其下标从 1 开始
        ss = " " + ss;
        pp = " " + pp;

        char[] s = ss.toCharArray();
        char[] p = pp.toCharArray();

        // 构建 next 数组，数组长度为匹配串的长度（next 数组是和匹配串相关的）
        int[] next = new int[m + 1];
        // 构造过程 i = 2，j = 0 开始，i 小于等于匹配串长度 【构造 i 从 2 开始】
        for (int i = 2, j = 0; i <= m; i++) {
            // 匹配不成功的话，j = next(j)
            while (j > 0 && p[i] != p[j + 1]) j = next[j];
            // 匹配成功的话，先让 j++
            if (p[i] == p[j + 1]) j++;
            // 更新 next[i]，结束本次循环，i++
            next[i] = j;
        }

        // 匹配过程，i = 1，j = 0 开始，i 小于等于原串长度 【匹配 i 从 1 开始】
        for (int i = 1, j = 0; i <= n; i++) {
            // 匹配不成功 j = next(j)
            while (j > 0 && s[i] != p[j + 1]) j = next[j];
            // 匹配成功的话，先让 j++，结束本次循环后 i++
            if (s[i] == p[j + 1]) j++;
            // 整一段匹配成功，直接返回下标
            if (j == m) return i - m;
        }

        return -1;
    }
}
```  
**题目:  459.重复的子字符串**   
**位置:** https://leetcode.cn/problems/repeated-substring-pattern/description/   
```java
lass Solution {
    public boolean repeatedSubstringPattern(String s) {
        if (s.equals("")) return false;

        int len = s.length();
        // 原串加个空格(哨兵)，使下标从1开始，这样j从0开始，也不用初始化了
        s = " " + s;
        char[] chars = s.toCharArray();
        int[] next = new int[len + 1];

        // 构造 next 数组过程，j从0开始(空格)，i从2开始
        for (int i = 2, j = 0; i <= len; i++) {
            // 匹配不成功，j回到前一位置 next 数组所对应的值
            while (j > 0 && chars[i] != chars[j + 1]) j = next[j];
            // 匹配成功，j往后移
            if (chars[i] == chars[j + 1]) j++;
            // 更新 next 数组的值
            next[i] = j;
        }

        // 最后判断是否是重复的子字符串，这里 next[len] 即代表next数组末尾的值
        if (next[len] > 0 && len % (len - next[len]) == 0) {
            return true;
        }
        return false;
    }
}
```  
