# [寻找峰值](https://leetcode.cn/problems/find-peak-element/description/)  
>虽然存在多个峰值(山顶)，但我们只要找到任意一个即可  

>因为nums[-1]= nums[n] = -∞，所以我们可以先找到一个数，如果它比旁边的数小，就说明往旁边走是上坡，就一定能找到山峰；如果它大于旁边的数，那么它自己可能就是山峰，或者还要继续爬(当然，如果往比它小的方向走，虽然是下坡，但也有可能找到新的山峰，不过也可能直接到边界了)，所以可以用二分法缩小范围  

>这里定义 <= left 均为山顶左侧元素，>= right 均为山顶或山顶右侧元素，根据这个定义：left 初始化为-1，因为第一个元素也有可能是峰值；right 初始化为最后一个元素下标，因为，因为他自己要么是山顶，要么在山顶右侧

**C++**
```
class Solution 
{
public:
    int findPeakElement(vector<int>& nums) 
    {
        int left = -1, right = nums.size() - 1; 
        while (left + 1 < right)
        {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] < nums[mid + 1]) left = mid; // 在它右边一定存在着一个山峰
            else right = mid; // 山峰可能在它左边，也可能就是他自己
        }
        return right;
    }
};
```
**Golang**
```
func findPeakElement(nums []int) int {
    left, right := -1, len(nums) - 1
    for left + 1 < right {
        mid := left + ((right - left) >> 1)
        if (nums[mid] < nums[mid + 1]) {
            left = mid
        } else {
            right = mid
        }
    }
    return right
}
```
