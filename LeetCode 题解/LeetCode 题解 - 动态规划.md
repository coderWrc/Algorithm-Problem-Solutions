# 动态规划

#### 三、背包
   1. 01 背包
      * [和为目标值的最长子序列的长度](#和为目标值的最长子序列的长度)
      * [分割等和子集](#分割等和子集)
      * [目标和](#目标和)
      * [将一个数字表示成幂的和的方案数](#将一个数字表示成幂的和的方案数)
      * [执行操作可获得的最大总奖励 |](#执行操作可获得的最大总奖励-)
      * [执行操作可获得的最大总奖励 ||](#执行操作可获得的最大总奖励--1)
      * [一和零](#一和零)
      * [最后一块石头的重量 ||](#最后一块石头的重量-)
      * [最接近目标价格的甜点成本](#最接近目标价格的甜点成本)

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
# [执行操作可获得的最大总奖励 ||](https://leetcode.cn/problems/maximum-total-reward-using-operations-ii/description/)
[top](#三背包)  
C++:
```
class Solution 
{
public:
    int maxTotalReward(vector<int>& rewardValues) 
    {
        // 设 m = max(rewardValues)，如果数组中包含 m − 1 或 有两个不同元素之和等于 m − 1，则答案为 2 * m − 1，无需计算 DP。
        int m = ranges::max(rewardValues);
        unordered_set<int> s;
        for (int v : rewardValues)
        {
            if (s.contains(v)) continue;
            if (v == m - 1 || s.contains(m - 1 - v)) return m * 2 - 1;
            s.insert(v);
        }

        ranges::sort(rewardValues); // 排序
        rewardValues.erase(unique(rewardValues.begin(), rewardValues.end()), rewardValues.end()); // 去重
        // 用二进制数 f 代替数组，第 j 位为 1 表示 f[j] = true
        bitset<100000> f{1}; // 初始化，f[0] = 1，即总奖励为零是可以满足的（就是啥都不选）
        for (int v : rewardValues) 
        {
            int shift = f.size() - v;
            // 左移 shift 再右移 shift，把所有 >= v 的比特位置为 0，保留 v 位(0 ~ v - 1) 
            // f |= f << shift >> shift << v
            f |= f << shift >> (shift - v);
        }
        int ans = rewardValues.back() * 2 - 1;
        while (!f.test(ans)) ans--;
        return ans;
    }
};
```
# [一和零](https://leetcode.cn/problems/ones-and-zeroes/description/)
[top](#三背包)
```
class Solution 
{
public:
    int findMaxForm(vector<string>& strs, int m, int n) 
    {
        vector f(m + 1, vector<int>(n + 1));
        for (string& s : strs)
        {
            int cnt0 = ranges::count(s, '0');
            int cnt1 = s.size() - cnt0;
            for (int j = m; j >= cnt0; j--)
            {
                for (int k = n; k >= cnt1; k--)
                {
                    f[j][k] = max(f[j][k], f[j - cnt0][k - cnt1] + 1);
                }
            }
        }
        return f[m][n];
    }
};
```
优化：
```
class Solution 
{
public:
    int findMaxForm(vector<string>& strs, int m, int n) 
    {
        vector f(m + 1, vector<int>(n + 1));
        int sum0 = 0, sum1 = 0;
        for (string& s : strs)
        {
            int cnt0 = ranges::count(s, '0');
            int cnt1 = s.size() - cnt0;
            sum0 = min(sum0 + cnt0, m);
            sum1 = min(sum1 + cnt1, n);
            for (int j = sum0; j >= cnt0; j--)
            {
                for (int k = sum1; k >= cnt1; k--)
                {
                    f[j][k] = max(f[j][k], f[j - cnt0][k - cnt1] + 1);
                }
            }
        }
        int ans = 0;
        for (auto& row : f) 
        {
            ans = max(ans, ranges::max(row));
        }
        return ans;
    }
};
```
# [最后一块石头的重量 ||](https://leetcode.cn/problems/last-stone-weight-ii/description/)
[top](#三背包)
```
class Solution 
{
public:
    int lastStoneWeightII(vector<int>& stones) 
    {
        int sum = accumulate(stones.begin(), stones.end(), 0);
        int target = sum >> 1;
        vector<int> f(target + 1);
        for (int stone : stones)
        {
            for (int j = target; j >= stone; j--)
            {
                f[j] = max(f[j], f[j - stone] + stone);
            }
        }
        return sum - 2 * f[target];
    }
};
```
# [最接近目标价格的甜点成本](https://leetcode.cn/problems/closest-dessert-cost/description/)
[top](#三背包)
```
class Solution 
{
public:
    int closestCost(vector<int>& baseCosts, vector<int>& toppingCosts, int target) 
    {
        int x = *min_element(baseCosts.begin(), baseCosts.end()); // 找到最小的基料开销
        if (x >= target) return x; // 若 x >= target，添加配料没法缩小开销与 target 的距离，直接返回

        vector<bool> f(target + 1, false); // f[i] 表示是否能制作开销为 i 的甜品
        // 最小的基料开销与 target 的距离为 target - x，所以答案一定在 [x, target * 2 - x] 中
        // 对于超过 target 的基料，只需保存 (target, target * 2 - x] 范围内的
        int res = target * 2 - x; // 大于 target 的最小开销
        for (auto& b : baseCosts) 
        {
            if (b <= target) f[b] = true;
            else res = min(res, b);
        }
        for (auto& t : toppingCosts) 
        {
            for (int cnt = 1; cnt <= 2; cnt++)
            {
                for (int i = target; i >= 1; i--) 
                {
                    if (f[i] && i + t > target) res = min(res, i + t); // 这个必须在前，即在加辅料之前，否则相当于多加了
                    if (i > t) f[i] = f[i] | f[i - t]; // 这个必须在后，执行一次这个，相当于加一次辅料
                }
            }
        }

        for (int i = target; target - i <= res - target; i--)
        {
            if (f[i]) return i;
        }
        return res;
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
