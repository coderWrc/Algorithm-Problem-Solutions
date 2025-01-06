# [最小化数组中的最大值](https://leetcode.cn/problems/minimize-maximum-of-array/description/)
>
**C++**
解法一：
>易知答案位于区间 [min_nums, max_nums] ,所以我们每次尝试一个答案(mid)，且该答案越大越容易满足条件(因为题目要求最小化)，越小越不能满足，就可以用二分法一直缩小范围，找到最小的满足条件的值  
>  
>可以从后往前遍历数组，将每一次超出答案(mid)的值(extra)，全部给到前面一个数，直到第一个数，那么后面的数就都满足条件了(nums[i] <= mid),最后只需要判断第一个数加上后面多出来的数是否满足条件(nums[i] + extra <= mid)就行了，依此缩小范围
```
class Solution 
{
public:
    int minimizeArrayValue(vector<int>& nums) 
    {
        int left = -1, right = 1e9; // 开区间 (left, right),这里right也可以是数组中最大的那个数
        while (left + 1 < right) // 开区间存在
        {
            int mid = left + (right - left) / 2;
            long long extra = 0;
            for (int i = nums.size() - 1; i > 0; i--)
            {
                extra = max(nums[i] + extra - mid, 0LL);
            }
            if (nums[0] + extra <= mid) right = mid;
            else left = mid;
        }
        return right;
    }
};
```
解法二：
>我们发现，有些情况下后面多出一个数是不会影响答案的，只有多出来的数足够大才会影响最终答案(因为只有后面的数能影响前面，而前面的数不能影响后面，且如果太小也不会把他的大小加到前面的数)，那么什么情况下才会影响答案呢？就是**加上后面的值后的平均值 > 之前的答案**
```
class Solution 
{
public:
    int minimizeArrayValue(vector<int>& nums) 
    {
        long long ans = 0, sum = 0;
        for (int i = 0; i < nums.size(); i++)
        {
            sum += nums[i];
            ans = max(ans, (sum + i) / (i + 1));
        }
        return ans;
    }
};
```
