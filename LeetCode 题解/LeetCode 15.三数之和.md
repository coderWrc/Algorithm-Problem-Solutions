# [三数之和](https://leetcode.cn/problems/3sum/description/)
先固定i，就可以转化成nums[j] + nums[k] == -nums[i]这个问题，就跟[两数之和](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/description/)这道题一样了。
```
class Solution 
{
public:
    vector<vector<int>> threeSum(vector<int>& nums) 
    {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans;
        for (int i = 0; i < n - 2; i++)
        {
            if (nums[i] + nums[i + 1] + nums[i + 2] > 0) break; // 优化
            if (nums[i] + nums[n - 1] + nums[n - 2] < 0) continue; // 优化
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int j = i + 1, k = n - 1;
            while (j < k)
            {
                int s = nums[i] + nums[j] + nums[k];
                if (s > 0) k--;
                else if (s < 0) j++;
                else 
                {
                    ans.push_back({nums[i], nums[j], nums[k]});
                    j++;
                    while (j < k && nums[j] == nums[j - 1]) j++;
                    k--;
                    while (j < k && nums[k] == nums[k + 1]) k--;
                }
            }
        }
        return ans;
    }
};
```
