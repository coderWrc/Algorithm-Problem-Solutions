# 动态规划

#### 三、背包
   1. 01 背包
      * [和为目标值的最长子序列的长度](#和为目标值的最长子序列的长度)



   2. 完全背包
   3. 多重背包
   4. 分组背包



# [和为目标值的最长子序列的长度](https://leetcode.cn/problems/length-of-the-longest-subsequence-that-sums-to-target/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    int lengthOfLongestSubsequence(vector<int>& nums, int target) 
    {
        vector<int> f(target + 1, INT_MIN);
        f[0] = 0;
        int s = 0;
        for (int x : nums)
        {
            s = min(s + x, target);
            for (int j = s; j >= x; j--)
            {
                f[j] = max(f[j], f[j - x] + 1);
            }
        }

        return f[target] > 0 ? f[target] : -1;
    }
};
```
JAVA:
```
class Solution {
    public int lengthOfLongestSubsequence(List<Integer> nums, int target) {
        int[] f = new int[target + 1];
        Arrays.fill(f, Integer.MIN_VALUE);
        f[0] = 0;
        int s = 0;
        for (int x : nums) {
            s = Math.min(s + x, target);
            for (int j = s; j >= x; j--) {
                f[j] = Math.max(f[j], f[j - x] + 1);
            }
        }
        return f[target] > 0 ? f[target] : -1;
    }
}
```
