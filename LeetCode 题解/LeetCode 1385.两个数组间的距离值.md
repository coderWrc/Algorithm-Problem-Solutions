# [两个数组间的距离值](https://leetcode.cn/problems/find-the-distance-value-between-two-arrays/description/)  
**C++**
法一：模拟
```
class Solution 
{
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) 
    {
        int cnt = 0;
        for (auto& x : arr1)
        {
            bool ok = true;
            for (auto& y : arr2)      //      这一行也可以换成：
            {                         //      if (abs(x - y) <= d)
                ok &= abs(x - y) > d; // -->  {
            }                         //          ok = false;
            cnt += ok;                //          break;
        }                             //      } // 并且这样子更快
        return cnt;
    }
};
```
法二：排序 + 二分查找
>其实不需要像上一个方法列举那么多y，只需要看离x最近的两个y(一个大于x，一个小于x)就可以了，看他们是否满足| x - y | > d
```
class Solution 
{
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) 
    {
        sort(arr2.begin(), arr2.end());
        int ans = 0;
        for (int& x : arr1)
        {
            // 先找到 >= x - d 的
            auto it = lower_bound(arr2.begin(), arr2.end(), x - d);
            {   // 看它是否存在，存在的话再看它是否满足 <= x + d
                if (it == arr2.end() || *it > x + d) ans++;
            }
        }
        return ans;
    }
};
```
法三：
```
class Solution 
{
public:
    int findTheDistanceValue(vector<int>& arr1, vector<int>& arr2, int d) 
    {
        ranges::sort(arr1);
        ranges::sort(arr2);
        int ans = 0, j = 0;
        for (int x : arr1)
        {
            while (j < arr2.size() && arr2[j] <x - d) j++; // 最小的满足 arr[j] >= x - d 的数的下标 j
            if (j == arr2.size() || arr2[j] > x + d) ans++; // 如果不存在或者不满足 arr[j] <= x + d
        }
        return ans;
    }
};
```
