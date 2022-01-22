# 题目
[反转字符串题目链接](https://leetcode-cn.com/problems/reverse-string/)

[反转字符串II题目链接](https://leetcode-cn.com/problems/reverse-string-ii/)
## 思路图
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/4.%E5%AD%97%E7%AC%A6%E4%B8%B2/image/string1.png)
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/4.%E5%AD%97%E7%AC%A6%E4%B8%B2/image/string2.png)
## 总结：
```
    反转字符串一道热身题，就不多叙述，
反转字符串II则是一道中规中矩的题，值得
注意的点在 reverse 函数本身是左闭右开
的，这要求打代码时很要清楚指针的指向。

```
## 我的题解：
```
void reverseString(vector<char>& s) {//反转字符串
            char temp;
            int begin = 0, end = s.size() - 1;
            while (begin < end) {
                temp = s[begin];
                s[begin] = s[end];
                s[end] = temp;
                begin++;
                end--;
            }            
        }

        string reverseStr(string s, int k) {//反转字符串II
            for (int begin = 0, end = k - 1;; begin += 2*k ,end += 2*k ) {
                if (begin > s.size() - 1 && end > s.size()-1) {
                    return  s;
                }
                else if (begin <= s.size() - 1 && end > s.size() - 1) {
                    end = s.size() - 1;
                    reverse(s.begin() + begin, s.begin() + end+1);
                    return  s;
                }
                reverse(s.begin() + begin, s.begin() + end + 1);
            }
            return  s;
        }

```
## 代码随想录的题解:
```
//反转字符串
void reverseString(vector<char>& s) {
    for (int i = 0, j = s.size() - 1; i < s.size()/2; i++, j--) {
        swap(s[i],s[j]);
    }
}
//反转字符串II
string reverseStr(string s, int k) {
        for (int i = 0; i < s.size(); i += (2 * k)) {
            // 1. 每隔 2k 个字符的前 k 个字符进行反转
            // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
            if (i + k <= s.size()) {
                reverse(s.begin() + i, s.begin() + i + k );
                continue;
            }
            // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
            reverse(s.begin() + i, s.begin() + s.size());
        }
        return s;
    }
```
                                     
