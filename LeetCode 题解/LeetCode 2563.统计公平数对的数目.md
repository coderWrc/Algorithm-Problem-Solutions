# [统计公平数对的数目](https://leetcode.cn/problems/count-the-number-of-fair-pairs/description/)  
  
**解题思路**
>1. 这道题只是要我们求数对的数目，所以排序并不影响答案   
>2. 此题只看一边，可以想到类似的题[《三数之和》](LeetCode%2015.三数之和.md)，即枚举其中一个数，求满足条件的另一个数，所以我们可以枚举 j ， 每次加上满足 lower - nums[j] <= nums[i] <= upper - nums[j] && i < j 的元素个数  
>3. 因为数组我们已经排好序了，所以要满足 i < j 很容易，只要我们在 [0, j) 中找满足条件的 i 的个数  
>4. 那么怎么求 i 的个数呢，我们可以把区间划成 [nums[0], lower - nums[j]) , [lower - nums[j], upper - nums[j]] , (upper - nums[j], nums[j]] ，我们只需要用[nums[0], upper - nums[j]] 的nums[i] 的个数减去[nums[0], lower - nums[j]) 的nums[i] 的个数
>5. 那么这个个数怎么得到呢，<= upper-nums[j] 的 nums[i] 的个数，就是>upper-nums[j]的第一个数的下标；同理< lower-nums[j] 的 nums[i] 的个数，就是>=lower-nums[j]的第一个数的下标

**参考代码**
```
class Solution 
{
public:
    long long countFairPairs(vector<int>& nums, int lower, int upper) 
    {
        sort(nums.begin(), nums.end());
        long long ans = 0;
        for (int j = 0; j < nums.size(); j++) 
        {
            auto r = upper_bound(nums.begin(), nums.begin() + j, upper - nums[j]); // <= upper-nums[j] 的 nums[i] 的个数
            auto l = lower_bound(nums.begin(), nums.begin() + j, lower - nums[j]); // < lower-nums[j] 的 nums[i] 的个数
            ans += r - l;
        }
        return ans;
    }
};
```
