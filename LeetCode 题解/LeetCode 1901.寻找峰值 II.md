# [寻找峰值 II](https://leetcode.cn/problems/find-a-peak-element-ii/description/)  
> 峰值肯定是当前这一行的最大值，那么找到当前这一行最大值再跟上下的值比较即可，一直往大的值那边缩小行范围,就能找到其中一个
  
**C++**
```
class Solution 
{
    int indexOfMax(vector<int>& a) // 寻找当前行最大值的下标
    {
        int ret = 0;
        for (int i = 1; i < a.size(); i++)
        {
            if (a[i]> a[ret]) ret = i;
        }
        return ret;
    }
public:
    vector<int> findPeakGrid(vector<vector<int>>& mat) 
    {
        int left = -1, right = mat.size() - 1;
        while (left + 1 < right)
        {
            int i = left + ((right - left) >> 1);
            int j = indexOfMax(mat[i]);
            (mat[i][j] < mat[i + 1][j] ? left : right) = i; // 往大的那边缩小范围
        }
        return {right, indexOfMax(mat[right])};
    }
};
```
**Golang**
```
func findPeakGrid(mat [][]int) []int {
    left, right := -1, len(mat) - 1
    for left + 1 < right {
        i := left + ((right - left) >> 1)
        j := indexOfMax(mat[i])
        if mat[i][j] < mat[i + 1][j] {
            left = i
        } else {
            right = i
        }
    }
    return []int{right, indexOfMax(mat[right])}
}

func indexOfMax(a []int) (ret int) {
    for i, val := range a {
        if val > a[ret] {
            ret = i
        }
    }
    return
}
```
