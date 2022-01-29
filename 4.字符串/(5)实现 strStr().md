# 题目
[力扣题目链接](https://leetcode-cn.com/problems/implement-strstr/)
## 思路图
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/4.%E5%AD%97%E7%AC%A6%E4%B8%B2/image/string6.png)
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/4.%E5%AD%97%E7%AC%A6%E4%B8%B2/image/string7.png)
## 总结：
```
    使用了KMP算法去解决该题，
在我学习的过程中，KMP算法的
学习难点在构建Next数组。Next
数组中i、j指针的所代指的意思，
以及指针的动向都是需要掌握的
关键点。
```
## 我的题解：
```
 int GetNext(vector<int> Next, int P_needle) {
            if (P_needle == 0) {
                return -1;
            }
            return  Next[P_needle - 1];
        }
        int strStr(string haystack, string needle) {
            //当其中一个字符串为空时
            if ((haystack.size() == 0 && needle.size() == 0) || (needle.size() == 0)) {
                return 0;
            }
            //初始化Next
            vector<int> Next(needle.size());
            Next[0] = 0;
            for (int i = 1, j = 0; i < needle.size(); i++) {
                if (needle[i] == needle[j]) {
                    Next[i] = ++j;
                }
                else {
                    if (j == 0) {
                        Next[i] = 0;
                        continue;
                    }
                    j = Next[j - 1];
                    i--;
                }
            }
            //对比两个字符串
            int P_haystack = 0, P_needle = 0;//设置指向h、n数组下标的指针
            for (; P_haystack < haystack.size() && P_needle < needle.size(); P_haystack++) {
                if (haystack[P_haystack] == needle[P_needle]) {
                    P_needle++;
                }
                else {          
                    P_needle = GetNext(Next, P_needle);
                    while (P_needle != -1) {
                        if (haystack[P_haystack] == needle[P_needle]) {
                            P_needle++;
                            break;
                        }
                        P_needle = GetNext(Next, P_needle);
                    }
                    if (P_needle == -1) {
                        P_needle = 0;
                    }                 
                }
            }
            if (P_needle == needle.size()) {
                return  P_haystack - needle.size() ;
            }          
            return -1;        
        }
```
## 代码随想录的题解:
```
 void getNext(int* next, const string& s) {
        int j = 0;
        next[0] = 0;
        for(int i = 1; i < s.size(); i++) {
            while (j > 0 && s[i] != s[j]) {
                j = next[j - 1];
            }
            if (s[i] == s[j]) {
                j++;
            }
            next[i] = j;
        }
    }
    int strStr(string haystack, string needle) {
        if (needle.size() == 0) {
            return 0;
        }
        int next[needle.size()];
        getNext(next, needle);
        int j = 0;
        for (int i = 0; i < haystack.size(); i++) {
            while(j > 0 && haystack[i] != needle[j]) {
                j = next[j - 1];
            }
            if (haystack[i] == needle[j]) {
                j++;
            }
            if (j == needle.size() ) {
                return (i - needle.size() + 1);
            }
        }
        return -1;
    }
```                                   
