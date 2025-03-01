# 动态规划

#### 三、背包
   1. 01 背包
      * [和为目标值的最长子序列的长度](#和为目标值的最长子序列的长度)
      * [分割等和子集](#分割等和子集)


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
# [分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    bool canPartition(vector<int>& nums) 
    {
        int sum = 0;
        for (int x : nums) sum += x;
        if (sum % 2) return false;
        sum >>= 1;
        vector<int> f(sum + 1);
        f[0] = true;
        int s = 0;
        for (int x : nums) 
        {
            s = min(s + x, sum);
            for (int j = s; j >= x; j--)
            {
                f[j] |= f[j - x];
            }
            if (f[sum]) return true;
        }
        return false;
    }
};
```
JAVA:
```
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int x : nums) {
            sum += x;
        }
        if (sum % 2 != 0) {
            return false;
        }
        sum >>= 1;
        boolean[] f = new boolean[sum + 1];
        f[0] = true;
        int s = 0;
        for (int x : nums) {
            s = Math.min(s + x, sum);
            for (int j = s; j >= x; j--) {
                f[j] |= f[j - x]; 
            }
            if (f[sum]) {
                return true;
            } 
        }
        return false;
    }
}
```
