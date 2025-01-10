# [寻找旋转排序数组中的最小值 II](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array-ii/description/)  
**C++**
>这道题跟之前的题目很类似，只不过会有重复的，那么重复会对我们解这道题有什么影响呢？我们先来看看之前的代码
```
 if (nums[mid] < nums[nums.size() - 1]) right = mid;
 else left = mid;
```
>之前那道题，判断的时候不会出现等于的情况，而这道题出现等于时，如果还这样写，可能会跳过最小值，要解决这个问题，就要特殊处理 nums[mid] == nums[nums.size() - 1] (因为相等时 mid 既可能在第一段，也可能在第二段)我们只需要改变 mid 的值即可，与此同时缩小范围
```
class Solution 
{
public:
    int findMin(vector<int>& nums) 
    {
        int n = nums.size();
        int left = -1, right = n - 1;
        while (left + 1 < right)
        {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] > nums[n - 1]) left = mid;
            else if (nums[mid] < nums[n - 1]) right = mid;
            else right--; 
        }
        return nums[right];
    }
};
```
>进一步想，其实只有开头的数与最后一个数重复时，才会影响最终结果，因为大于最后一个数的一定在第一段，小于最后一个数的在第二段，这些数重复都不会影响我们判断，所以我们也可以先处理开头与末尾相等的数
```
class Solution 
{
public:
    int findMin(vector<int>& nums) 
    {
        int n = nums.size();
        int left = -1, right = n - 1;
        while (left + 1 < right && nums[left + 1] == nums[n - 1]) left++;
        while (left + 1 < right) 
        {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] > nums[n - 1]) left = mid;
            else right = mid;
        }
        return nums[right];
    }
};
```
