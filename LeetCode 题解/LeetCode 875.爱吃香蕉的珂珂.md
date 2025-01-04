# [爱吃香蕉的珂珂](https://leetcode.cn/problems/koko-eating-bananas/description/)
**C++**
```
class Solution 
{
public:
    // 这里 int 会溢出
    long long time(vector<int>& piles, int speed)
    {
        long long time = 0;
        for (int& pile : piles)
        {
            time += (pile + speed - 1) / speed;
        }
        return time;
    }

    int minEatingSpeed(vector<int>& piles, int h) 
    {
        // [0, l] 为不可能区间，[r, max(piles)] 为答案区间
        int l = 0, r = 0;
        for (int& pile : piles) r = max(r, pile); // 速度最快一个小时吃一堆，即最大那一堆的香蕉个数
        while (l + 1 < r) // 区间存在  每次让 l 变大或让 r 变小，找到最小的 r 的值
        {
            int mid = l + (r - l) / 2;  // 中间的速度
            if (time(piles, mid) <= h) r = mid; // 如果满足则更新 r
            else l = mid; // 不满足则更新 l
        }
        return r;
    }
};
```
