# [长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)  
>
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
            while (s - nums[l] >= target) 
            {
                s -= nums[l];
                l++;
            }
            if (s >= target) ans = min(ans, r - l + 1);
        }
        return ans <= nums.size() ? ans : 0;
    }
};
```
