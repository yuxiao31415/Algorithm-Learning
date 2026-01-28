# 数组part01
## 数组理论知识
数组是存放在连续内存空间上的相同类型数据的集合  
二维数组? c++二维数组内存连续,java内存地址不对外暴露,不可知  
## 二分查找
**704.二分查找**  
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
```
**35.搜索插入位置**  
**位置:** https://leetcode.cn/problems/search-insert-position/description/
```java
// 左闭右开
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length;
        while(left<right){
            int mid = left+(right-left)/2;
            if(target==nums[mid]){
                return mid;
            }else if(target<nums[mid]){   
                right = mid; 
            }else{
                left = mid+1;
            }
        }
        /*
        四种情况,
        1. 答案在最左边索引0处,
        此时区间[left,right)右侧right不断左移,直到right=left->返回left;
        2.答案在mid到mid+1之间
        此时target>nums[mid],区间[mid+1,right)不断左移直到right=left=mid+1->返回left
        3.答案在mid-1到mid之间
        此时target<nums[mid],区间[left,mid)不断右移直到left=right=mid->返回left
        4.答案在最右边索引mums.length处,
        此时区间[left,right)左侧left不断左移,直到left=right->返回left
        */
        return left; 
    }
}
// 左闭右闭
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(target==nums[mid]){
                return mid;
            }else if(target<nums[mid]){   
                right = mid-1; 
            }else{
                left = mid+1;
            }
        }
        /*
        一共四种情况,
        1. 答案在最左边索引0处,
        此时区间[left,right]右侧right不断左移,直到right=left-1->返回left;
        2.答案在mid到mid+1之间
        此时target>nums[mid],区间[mid+1,right]不断左移直到right=left-1=mid->返回left
        3.答案在mid-1到mid之间
        此时target<nums[mid],区间[left,mid-1]不断右移直到left=right+1=mid->返回left
        4.答案在最右边索引mums.length处,
        此时区间[left,right]左侧left不断右移,直到left=right+1->返回left
        */
        return left;// 一般情况下带入最左端或最右端的特例即可直到是left还是right
    }
}
```
**34.在排序数组中查找元素的第一个和最后一个位置**  
**位置** https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/  
```java
// 左闭右开
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left=0;
        int right=nums.length;
        int ansleft=-1;
        int ansright=-1;
        while(left<right){
            int mid = left+(right-left)/2;
            if(target==nums[mid]){
                ansleft = mid;
                ansright= mid;
                while(ansleft>0&&nums[ansleft-1]==target){ansleft--;}
                while(ansright<nums.length-1&&nums[ansright+1]==target){ansright++;}
                break;
            }else if(target<nums[mid]){
                right=mid;
            }else{
                left=mid+1;
            }
        }
        return new int[]{ansleft,ansright};
    }
}

// 左闭右闭
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left=0;
        int right=nums.length-1;
        int ansleft=-1;
        int ansright=-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(target==nums[mid]){
                ansleft = mid;
                ansright= mid;
                while(ansleft>0&&nums[ansleft-1]==target){ansleft--;}
                while(ansright<nums.length-1&&nums[ansright+1]==target){ansright++;}
                break;
            }else if(target<nums[mid]){
                right=mid-1;
            }else{
                left=mid+1;
            }
        }
        return new int[]{ansleft,ansright};
    }
}
```









