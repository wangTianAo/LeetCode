# Question15 3Sum
[原题]https://leetcode.com/problems/3sum/description/<br>
>给一个数列，求所有三个数加起来等于0且不重复的组合。<br>
>最开始想到的是遍历三遍的方法，时间复杂度O(n^3)<br>
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> oneResult;
        for(int a = 0 ; a < nums.size(); a++){
            for(int b = a+1 ; b < nums.size(); b++){
                for(int c = b+1 ; c < nums.size(); c++){
                    if(nums[a]+nums[b]+nums[c]==0){
                        oneResult.push_back(nums[a]);
                        oneResult.push_back(nums[b]);
                        oneResult.push_back(nums[c]);
                        sort(oneResult.begin(),oneResult.end());
                        result.push_back(oneResult);
                        oneResult.clear();
                    }
                }
            }
        }
        sort(result.begin(),result.end());
        vector<vector<int>>::iterator iter = unique(result.begin(),result.end());
        result.erase(iter,result.end());
        return result;
    }
};
```
>sort方法是对数组的元素进行排序的方法，包含于头文件algorithm。需使用using namespace std<br>
>unique()函数是将重复的元素折叠缩编，使成唯一。该算法删除相邻的重复元素，然后重新排列输入范围内的元素，
并且返回一个迭代器（容器的长度没变，只是元素顺序改变了）<br>
>erase()方法，从指定容器删除指定位置的元素或某段范围内的元素。传入起始迭代器。要注意erase后野指针的问题<br><br>
>不出意外又超时了....<br><br>


>如果先排好序，以一个数为已知值，另外两个比它大的数之和等于第一个数的负数，就简化成了2Sum问题<br>
>第一个数从前往后走，后两个数可以从前和从后同时遍历，时间复杂度简化到了O(n^2)<br><br>
>代码实现并通过<br><br>
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        if(nums.size()<3){
            return result;
        }
        sort(nums.begin(),nums.end());
        for(int a = 0; a<nums.size()-2;a++){
            int left = a+1;
            int right = nums.size()-1;
            int target = 0 - nums[a];
            if(nums[a]>0)
                break;
            if(a>0&&nums[a]==nums[a-1])
                continue;
            while(left<right){
                if(nums[left]+nums[right]==target){
                    result.push_back({nums[a],nums[left],nums[right]});
                     while(left<right&&nums[left]==nums[left+1]){
                        left++;
                     }
                    while(left<right&&nums[right]==nums[right-1]){
                        right--;
                    }
                    left++;
                    right--;
                }else if(nums[left]+nums[right]<target){
                   left++;
                }else{
                    right--;
                }
               
            }
        }
        sort(result.begin(),result.end());
        vector<vector<int>>::iterator iter = unique(result.begin(),result.end());
        result.erase(iter,result.end());
        return result;
    }
};
```
