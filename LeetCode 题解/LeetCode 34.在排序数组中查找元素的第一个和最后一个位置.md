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
>直接用库函数也行，不过有一点需要注意：
>start 和 end 是迭代器，它们指向 nums 容器中的某个位置。为了得到这些位置的索引（即从容器开始到该位置的距离），你需要计算迭代器与容器起始位置之间的距离。这可以通过减去 nums.begin() 来实现，但结果是一个 std::vector<int>::difference_type 类型的值，通常是一个有符号整数类型（如 ptrdiff_t）。**为了确保返回的是 int 类型，需要使用static_cast<int> 进行显式转换**。
```
class Solution 
{
public:
    vector<int> searchRange(vector<int>& nums, int target) 
    {
        auto start = lower_bound(nums.begin(), nums.end(), target);
        if (start == nums.end() || *start != target) return vector<int>{-1, -1};
        auto end = lower_bound(nums.begin(), nums.end(), target + 1) - 1;
        return vector<int>{static_cast<int>(start - nums.begin()), static_cast<int>(end - nums.begin())};
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
