# [P3405 [USACO16DEC] Cities and States S](https://www.luogu.com.cn/problem/P3405)
#### 解题思路
>由题意知:每行输入的第一个字符串只有前两个字母有用,所以我们可以用substr来截取第一个字符串的前两个字母,并将它与第二个字符串拼接,然后再定义一个**unordered_map<strint, int> <城市名称+所在的州, 出现次数>**  
>这里简单介绍下[substr()](https://legacy.cplusplus.com/reference/string/string/substr/)  
>substr() 函数用于截取字符串中指定位置指定长度的子串。函数原型如下：
```
1 string.substr (size_t pos = 0, size_t len = npos) const;  
2 //pos 的默认值是0，也就是从下标为0的位置开始截取    
3 //len 的默认值是npos，意思是⼀直截取到字符串的末尾  
```
```substr()``` :如果函数不传参数，就是从下标为0的位置开始截取，直到结尾，得到的是整个字符串； 
```substr(pos)``` :从指定下标 pos 位置开始截取子串，直到结尾； 
```substr(pos, len)``` ：从指定下标 pos 位置开始截取长度为 len 的子串。 
返回值类型：```string``` ，返回的是截取到的字符串，可以使用 ```string``` 类型的字符串接收。
>
>
#### 参考代码
```
#include <iostream>
#include <unordered_map>

using namespace std;

int main()
{
    int n; cin >> n;
    unordered_map<string, int> mp;
    int ans = 0;
    while (n--)
    {
        string s1, s2; cin >> s1 >> s2;
        s1 = s1.substr(0, 2);
        if (s1 == s2) continue; //如果来自相同的洲,就跳过
        ans += mp[s2 + s1]; //加上与其配对城市的数量
        mp[s1 + s2]++; //当前这种城市的数量+1
    }
    cout << ans << endl;

    return 0;
}
```
