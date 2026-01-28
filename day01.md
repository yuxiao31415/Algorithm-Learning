# 数组part01
## 数组理论知识
数组是存放在连续内存空间上的相同类型数据的集合  
二维数组? c++二维数组内存连续,java内存地址不对外暴露,不可知  
## 二分查找
**位置**: https://leetcode.cn/problems/binary-search/description/  
**目标**: 掌握二分的两种写法,1.左闭右开2.左闭右闭
```java
// 左闭右开
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length;// 关键点1. 右开区间,时刻保证取不到这个值
        while(left<right){      // 关键点2. 左闭右开,left等于right就说明结束了 例如[1,1) 取不到1
            int mid = left+(right-left)/2;
            if(nums[mid]==target){ // 关键点3. 把==情况单独拿出来
                return mid;
            }else if(nums[mid]<target){ // 关键点4. left可以取到mid但是nums[mid]!=target,所以left不能为mid,可以为mid+1;
                left = mid +1;
            }else{
                right= mid; // 关键点5. right取不到mid,答案区间在[left,mid),如果mid-1,那么就会变成[left,mid-1)导致缺少mid-1时的值
            }
        }
        return -1;
    }
}
// 左闭右闭
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(nums[mid]==target){
                return mid;
            }else if(nums[mid]<target){
                left = mid +1;
            }else{
                right= mid-1;
            }
        }
        return -1;
    }
}

