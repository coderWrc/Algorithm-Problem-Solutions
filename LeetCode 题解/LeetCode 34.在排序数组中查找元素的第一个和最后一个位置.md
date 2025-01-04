# [在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
**C++**
  
```
class Solution 
{
public:
    int lower_bound(vector<int>& nums, int target)
    {
        int left = -1, right = nums.size(); // 开区间 (left, right)
        while (left + 1 < right) // 区间不为空
        {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target) left = mid; // (mid, right)
            else right = mid; // (left, mid)
        }
        return right;
    }
    vector<int> searchRange(vector<int>& nums, int target) 
    {
        int start = lower_bound(nums, target);
        if (start == nums.size() || nums[start] != target) return vector<int>{-1, -1};
        int end = lower_bound(nums, target + 1) - 1;
        return vector<int>{start, end};
    }
};
```
**Golang**
  
```
func searchRange(nums []int, target int) []int {
    start := sort.SearchInts(nums, target)
    if (start == len(nums) || nums[start] != target) {
        return []int{-1, -1}
    }
    end := sort.SearchInts(nums, target + 1) - 1
    return []int{start, end}
}
```
