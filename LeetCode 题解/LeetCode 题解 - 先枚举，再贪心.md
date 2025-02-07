# 先枚举，再贪心
1. [行相等的最少多米诺旋转](https://leetcode.cn/problems/minimum-domino-rotations-for-equal-row/description/)



```
class Solution 
{
public:
    int minDominoRotations(vector<int>& tops, vector<int>& bottoms) 
    {
        auto min_rot = [&](int target) -> int 
        {
            int to_top = 0, to_bottom = 0;
            for (int i = 0; i < tops.size(); i++) 
            {
                int x = tops[i], y = bottoms[i];
                if (x != target && y != target) return INT_MAX;
                if (x != target) to_top++; // 把 y 旋转到 top
                if (y != target) to_bottom++; // 把 x 旋转到 bottom
            }
            return min(to_top, to_bottom);
        };
        int ans = min((min_rot(tops[0])), min_rot(bottoms[0]));
        return ans == INT_MAX ? -1 : ans;
    }
};
```
