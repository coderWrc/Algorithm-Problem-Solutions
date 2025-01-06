# [礼盒的最大甜蜜度](https://leetcode.cn/problems/maximum-tastiness-of-candy-basket/description/)
**C++**
```
class Solution 
{
public:
    int maximumTastiness(vector<int>& price, int k) 
    {
        sort(price.begin(), price.end());
        int left = 0, right = (price.back() - price.front()) / (k - 1) + 1;
        while (left + 1 < right) 
        {
            int mid = left + (right - left) / 2;
            int pre = price[0], cnt = 1;
            for (int& p : price)
            {
                if (p >= pre + mid)
                {
                    cnt++;
                    pre = p;
                }
            }
            if (cnt >= k) left = mid;
            else right = mid;
        }
        return left;
    }
};
```
