# [长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)  
>
```
class Solution 
{
public:
    int minSubArrayLen(int target, vector<int>& nums) 
    {
        if (nums.size() == 0) return 0; 
        int ans = nums.size() + 1; // 定义成一个取不到的值，INF也是可以的
        int l = 0;
        int s = 0;
        for (int r = 0; r < nums.size(); r++) //遍历右边界
        {
            s += nums[r];
            while (s - nums[l] >= target) // 看是否左边界能缩小
            {
                s -= nums[l];
                l++;
            }
            if (s >= target) ans = min(ans, r - l + 1);  // 更新最小长度
        }
        return ans <= nums.size() ? ans : 0;
    }
};
```
**下面这样也行**
```
class Solution 
{
public:
    int minSubArrayLen(int target, vector<int>& nums) 
    {
        if (nums.size() == 0) return 0;
        int ans = nums.size() + 1;
        int l = 0;
        int s = 0;
        for (int r = 0; r < nums.size(); r++)
        {
            s += nums[r];
            while (s >= target)
            {
                ans = min(ans, r - l + 1);
                s -= nums[l];
                l++;
            }
        }
        return ans <= nums.size() ? ans : 0;
    }
};
```
