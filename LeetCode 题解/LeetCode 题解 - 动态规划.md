# 动态规划

#### 三、背包
   1. 01 背包
      * [和为目标值的最长子序列的长度](#和为目标值的最长子序列的长度)
      * [分割等和子集](#分割等和子集)
      * [目标和](#目标和)
      * [将一个数字表示成幂的和的方案数](#将一个数字表示成幂的和的方案数)
      * [执行操作可获得的最大总奖励 |](#执行操作可获得的最大总奖励-)

   2. 完全背包
      * [零钱兑换](#零钱兑换)



   3. 多重背包
   4. 分组背包
  
  
01 背包
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
# [目标和](https://leetcode.cn/problems/target-sum/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    int findTargetSumWays(vector<int>& nums, int target) 
    {
        int m = reduce(nums.begin(), nums.end()) - abs(target);
        if (m < 0 || m % 2) return 0;
        m >>= 1;
        int n = nums.size();
        vector<int> f(m + 1);
        f[0] = 1;
        for (int x : nums)
        {
            for (int c = m; c >= x; c--)
            {
                f[c] = f[c] + f[c - x];
            }
        }
        return f[m];
    }
};
```
JAVA:
```
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int m = 0;
        for (int x : nums) {
            m += x;
        }
        m -= Math.abs(target);
        if (m < 0 || m % 2 == 1) {
            return 0;
        } 
        m >>= 1;
        int[] f = new int[m + 1];
        f[0] = 1;
        for (int x : nums) {
            for (int c = m; c >= x; c--) {
                f[c] = f[c] + f[c - x];
            }
        }
        return f[m];
    }
}
```
# [将一个数字表示成幂的和的方案数](https://leetcode.cn/problems/ways-to-express-an-integer-as-sum-of-powers/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    int numberOfWays(int n, int x) 
    {
        vector<long long> f(n + 1);
        f[0] = 1;
        for (int i = 1; pow(i, x) <= n; i++)
        {
            int v = pow(i, x);
            for (int j = n; j >= v; j--)
            {
                f[j] += f[j  - v];
            }
        }
        const int MOD = 1e9 + 7;
        return f[n] % MOD;
    }
};
```
JAVA:
```
class Solution {
    public int numberOfWays(int n, int x) {
        long[] f = new long[n + 1];
        f[0] = 1;
        for (int i = 1; Math.pow(i, x) <= n; i++)
        {
            int v = (int)Math.pow(i, x);
            for (int j = n; j >= v; j--)
            {
                f[j] += f[j - v];
            }
        }
        return (int)(f[n] % 1_000_000_007);
    }
}
```
# [执行操作可获得的最大总奖励 |](https://leetcode.cn/problems/maximum-total-reward-using-operations-i/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    int maxTotalReward(vector<int>& rewardValues)
    {
        sort(rewardValues.begin(), rewardValues.end());
        int n = rewardValues.size();
        const int m = rewardValues.back() << 1;
        bool f[m]; // f[j] 表示能否得到总奖励 j
        memset(f, false, sizeof f);
        f[0] = true;
        for (int v : rewardValues)
        {
            for (int j = 2 * v - 1; j >= v; j--) 
            {
                f[j] |= f[j - v]; 
            }
        }
        int ans = m - 1;
        while (!f[ans]) ans--;
        return ans;
    }
};
```
完全背包
# [零钱兑换](https://leetcode.cn/problems/coin-change/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    int coinChange(vector<int>& coins, int amount) 
    {
        vector<int> f(amount + 1, amount + 1);
        f[0] = 0;
        for (int x : coins)
        {
            for (int c = x; c <= amount; c++)
            {
                f[c] = min(f[c], f[c - x] + 1);
            }
        }
        return f[amount] < amount + 1 ? f[amount] : -1 ;
    }
};
```
JAVA:
```
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] f = new int[amount + 1];
        Arrays.fill(f, amount + 1);
        f[0] = 0;
        for (int x : coins) 
        {
            for (int c = x; c <= amount; c++)
            {
                f[c] = Math.min(f[c], f[c - x] + 1);
            }
        }
        return f[amount] < amount + 1 ? f[amount] : -1; 
    }
}
```
