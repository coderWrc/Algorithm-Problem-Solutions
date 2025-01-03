# [无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/)
**C++**
```
class Solution 
{
public:
    int lengthOfLongestSubstring(string s) 
    {
        unordered_map<char, int> mp;
        int l = 0;
        int ans = 0;
        for (int r = 0; r < s.size(); r++)
        {
            mp[s[r]]++;
            while (mp[s[r]] > 1) mp[s[l++]]--; // 这里不能用mp.erase(s[l++])
            ans = max(ans, r - l + 1);
        }
        return ans;
    }
};
```
**Golang**
```
func lengthOfLongestSubstring(s string) int {
    mp := map[byte]int{}
    ans := 0
    l := 0
    for r := 0; r < len(s); r++ {
        mp[s[r]]++
        for mp[s[r]] > 1 {
            mp[s[l]]--
            l++
        }
        ans = max(ans, r - l + 1)
    }
    return ans
}
```
