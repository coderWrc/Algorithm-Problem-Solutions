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
**Golang**
>第一次遇到sort.Search
```
func minEatingSpeed(piles []int, h int) int {
    // 先算出最快速度
    max := 0
    for _, pile := range piles {
        if pile > max {
            max = pile
        }
    }
    // 速度范围是 [1, max] ，sort.Search会从[0, max - 1)中取出一个值speed
    // speed为[0, max - 1]中最小的使函数func(speed int)返回true的值，并且f(speed + 1)也为true
    // 如果无法找到该值(speed)，则返回max - 1，这也是为什么前面加了个一
    return 1 + sort.Search(max - 1, func(speed int) bool {
        speed++ // 处理 speed == 0 的情况；不是通过这里来让speed++的，而是通过sort.Search的二分查找来让speed更新的
        time := 0
        for _, pile := range piles {
            time += (pile + speed - 1) / speed
        }
        return time <= h
    }) // 这里还有半个括号
}
```
