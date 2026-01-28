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
        int right = nums.length;
        while(left<right){
            int mid = left+(right-left)/2;
            if(nums[mid]==target){
                return mid;
            }else if(nums[mid]<target){
                left = mid +1;
            }else{
                right= mid;
            }
        }
        return -1;
    }
}

