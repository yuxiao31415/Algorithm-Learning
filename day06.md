# 哈希表part02
**题目: 454.四数相加II**  
**位置:** https://leetcode.cn/problems/4sum-ii/description/  
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) { // 关键点是四个数组分开的,而不是一个数组任意四个位置的和
                                                                                  // 一个数组应该考虑三数之和的做法
                                                                                  // 四个数组先考虑到用四层for循环,但是内部循环也还是去找另外三组的之和是不是0-当前元素值
                                                                                  // 进而想到用map记录
        int ans =0;
        Map<Integer,Integer> map = new HashMap<>();
        for(int i:nums1){
            for(int j: nums2){
                map.merge(i+j,1,Integer::sum);
            }
        }
        for(int i:nums3){
            for(int j: nums4){
                if(map.containsKey(-i-j)){// 还可以优化使用getOrDefault()
                    ans+=map.get(-i-j);
                }
            }
        }
        return ans;
    }

```  
**题目: 393.赎金信**  
**位置:** https://leetcode.cn/problems/ransom-note/description/   
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        // 题目要求很简单，即看magazine中的字母能否包含ransomNote中的字母
        int[] cnt1 = new int[28];
        int[] cnt2=new int[28];
        for(char c :ransomNote.toCharArray()){
            cnt1[c-'a']++;
        }
        for(char c :magazine.toCharArray()){
            cnt2[c-'a']++;
        }
        // 开始判断
        for(int i=0;i<cnt1.length;i++){
            if(cnt1[i]>cnt2[i]){
                return false;
            }
        }
        return true;
    }
}
```  
**题目: 15.三数之和**  
**位置:**  https://leetcode.cn/problems/3sum/description/  
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        for(int i=0;i<nums.length-2;i++){
            if(i!=0&&nums[i]==nums[i-1]) continue; // 111 222 这种情况,只有第一次遇到1或者2才会执行,再遇到如果处理就会造成结果元素重复，所以得跳过
            if(nums[i]>0) break;
            int l = i+1;
            int r = nums.length-1;
            while(l<r){
                int sum=nums[i]+nums[l]+nums[r];
                if(sum==0){
                    ans.add(new ArrayList<>(Arrays.asList(nums[i],nums[l],nums[r])));
                    while(l<r&&nums[r--]==nums[r]);
                    while(l<r&&nums[l++]==nums[l]);
                }else if(sum<0){
                    l++;
                }else if(sum>0){
                    r--;
                }
            }
        }
        return ans;
    }
}
```  
**题目: 18.四数之和**  
**位置:** https://leetcode.cn/problems/4sum/description/  
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        // 按照三数之和的思路
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<>();
        for(int i=0;i<nums.length-3;i++){
            if(i>0&&nums[i]==nums[i-1]){
                continue;
            }
            for(int j=i+1;j<nums.length-2;j++){
                if(j!=i+1&&nums[j]==nums[j-1]){// 关键点1. 比如这种情况 1 1 1 1 2 3 4 5 此时i等于1 j也得等于1,且下次j就得跨过全部1
                                                // 以及11 22 3456 这种情况，所以仅仅当j=i+1时放行，其余时候都得判断是否等于上一个元素
                    continue;
                }
                int l = j+1;
                int r = nums.length-1;
                while(l<r){
                    long sum = (long)nums[i]+nums[j]+nums[l]+nums[r]; //关键点2. 注意取值范围用long来记录
                    if(sum==target){
                        ans.add(new ArrayList<>(Arrays.asList(nums[i],nums[j],nums[l],nums[r])));
                        while(l<r&&nums[l]==nums[l+1]) l++;
                        while(l<r&&nums[r]==nums[r-1]) r--;
                        l++;
                        r--;
                    }else if(sum<target){
                        l++;
                    }else if(sum>target){
                        r--;
                    }
                }
            }
        } 
        return ans;
    }
}
```
