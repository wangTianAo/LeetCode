# LeetCode
记录一些在LeetCode上做算法题遇到的问题和解决方案<br>
之前有些坑忘记填了，就摸了吧，从现在开始<br>

## Question11 Container With Most Water
[原题]https://leetcode.com/problems/container-with-most-water/description/<br>
>题目要求面积的最大值，一开始的思路是最简单的两次遍历vector,时间复杂度为O(n^2)，空间复杂度为O(1)(low爆<br>
>然后果然就gg了,超时...<br>
>如果这样<br>
![](https://leetcode.com/media/original_images/11_Container_Water.gif)
>>先从最左和最右选取边，得出一个面积<br>
>>然后短的一边向里移动，因为长方形的底变小了，只有高更长才有可能面积更大。<br>
>>从两头缩进的话，时间复杂度简化为了O(n),空间复杂度为O(1),快了很多呢。<br><br>
>我的解决方案<br>
```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxArea = 0;
        int left = 0;
        int right = height.size()-1;
        while(left<right){
            int length = right - left;
            int high = height.at(left)>height.at(right)?height.at(right):height.at(left);
            int area = length * high;
            if(area>maxArea)
                maxArea = area;
            height.at(left)>height.at(right)?right--:left++;
        }
        return maxArea;
    }
};
```
