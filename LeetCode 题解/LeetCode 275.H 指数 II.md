# [H 指数 II](https://leetcode.cn/problems/h-index-ii/description/)
```
class Solution 
{
public:
    int hIndex(vector<int>& citations)
    {
        int n = citations.size();
        // 当 l = 0 时，必定满足至少0篇论文的引用至少0次，所以直接在[1, n]中二分
        int l = 0, r = n + 1; // 开区间 (l, r)
        while (l + 1 < r) // 区间不为空
        {
            int mid = l + (r - l) / 2;
            // 每次 [n - 1, n- 2,..., n - mid] 这 mid 个数都 >= mid，就更新 l，所以最终答案就是 l(如果没更新过，答案就是0)
            if (citations[n - mid] >= mid) l = mid; // (mid, r)
            // 如果不满足，那么 r 右边的数也肯定不满足
            else r = mid; // (l, mid)
        }
        return l;
    }
};
```
