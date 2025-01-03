# [接雨水](https://leetcode.cn/problems/trapping-rain-water/description/)

```
class Solution 
{
public:
    int trap(vector<int>& height) 
    {
        int ans = 0;
        int l = 0, r = height.size() - 1;
        int pre_max = 0, suf_max = 0;
        while (l < r) //这里不需要 '=' ，因为他们会在顶峰相遇
        {
            pre_max = max(pre_max, height[l]);
            suf_max = max(suf_max, height[r]);
            if (pre_max <= suf_max) 
            {
                ans += pre_max - height[l];
                l++;
            }
            else
            {
                ans += suf_max - height[r];
                r--;
            }
        }
        return ans;
    }
};
```
