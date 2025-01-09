# [搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/description/)  
>这道题跟上道题很类似，只不过上道题要找的最小值一定是在第二段，而这道题要找的 target 并不知道它在那一段上，所以我们多判断一下 target 和 mid 的相对位置，来缩小区间  

**码一**
```
class Solution 
{
public:
    int search(vector<int>& nums, int target) 
    {
        int n = nums.size();
        int left = -1, right = n - 1;
        while (left + 1 < right)
        {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] > nums[n - 1]) // mid 在第一段时
            {
                // target 也在第一段并且在 mid 左边，那么 mid 右边就不用管了
                if (target > nums[n - 1] && nums[mid] >= target) right = mid;
                // 否则，左边就不用管了
                else left = mid;
            }
            else // mid 在第二段
            {
                // target 在第一段 或者 target 在第二段并且在 mid 左边，那么 mid 右边也不用管
                if (target > nums[n - 1] || nums[mid] >= target) right = mid;
                // 否则，左边就不用管了
                else left = mid;
            }
        }
        return nums[right] == target ? right : -1;
    }
};
```
>我们再整理一下  
>什么时候右边不用管(right = mid)?
>1. nums[mid] > nums[n - 1] 时，target > nums[n - 1] && nums[mid] >= target(还有，如果后面这两个条件都成立，那么前面的第一个条件也自然成立)
>2. nums[mid] <= nums[n - 1] 时，target > nums[n - 1] || nums[mid] >= target (这两个条件最多成立一个)
>  
>其余情况左边不用管
>
>也就是说 nums[mid] > nums[n - 1]；target > nums[n - 1]； nums[mid] >= target 这三个条件要么都成立，要么就成立一个，这时候右边不用管  
>于是就可以写出下面这种代码

**码二**
```
class Solution 
{
public:
    int search(vector<int>& nums, int target) 
    {
        int n = nums.size();
        int left = -1, right = n - 1;
        while (left + 1 < right)
        {
            int mid = left + ((right - left) >> 1);
            if ((nums[mid] > nums[n - 1]) ^ (target > nums[n - 1]) ^ (nums[mid] >= target))
                right = mid;
            else
                left = mid;
        }
        return nums[right] == target ? right : -1;
    }
};
```
