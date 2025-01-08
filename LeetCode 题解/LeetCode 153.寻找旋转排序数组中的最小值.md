# [寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/description/)  
>因为每次旋转都是把数组中的最后一个数放到最前面，假设 nums = [4, 5, 6, 7, 0, 1, 2]，就可以把数组分为两个：[4, 5, 6, 7] [0, 1, 2]，易知，**比旋转后数组的最后一个数大的，在第一段；比旋转后数组的最后一个数小的，在第二段。**
>
> 所以，数组中的最小元素一定在第二段。依此我们可以定义 left 以及它左边的数都在第一段，right 及它右边的都在第二段，让 right 尽可能的往左走，到达第二段的最左侧，那么 nums[right] 就是答案
  
**C++**
```
class Solution 
{
public:
    int findMin(vector<int>& nums) 
    {
        int left = -1, right = nums.size() - 1;
        while (left + 1 < right) 
        {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] < nums[nums.size() - 1]) right = mid; // mid 在第二段，让right往左走
            else left = mid; // mid 在第一段，让left往右走
        }
        return nums[right];
    }
};
```
**Golang**
```
func findMin(nums []int) int {
    left, right := -1, len(nums) - 1
    for left + 1 < right {
        mid := left + ((right - left) >> 1)
        if (nums[mid] > nums[len(nums) - 1]) {
            left = mid
        } else {
            right = mid
        }
    }
    return nums[right]
}
```
