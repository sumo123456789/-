# 题目
[力扣题目链接](https://leetcode-cn.com/problems/4sum-ii/)
## 思路图
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/3.%E5%93%88%E5%B8%8C%E8%A1%A8/image/HashImage4.png)
## 总结：
```
    该题的突破点在于意识到把4个数组简化成两个，
再利用map的特性设计数据。最后检测是否符合条件。
    该题我一开始其实并没有思路，在看了题解后才
知道这种解题思路。也从侧面反映了我对map并不熟悉
，以及解题思路的匮乏。
```
## 我的题解：
```
int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
            int count = 0;
            unordered_map<int, int> Sum;
            for (int a : nums1) {
                for (int b : nums2) {
                    Sum[a + b]++;//其中的key为 和 ，value为 该和的出现次数。
                }
            }
            for (int c : nums3) {
                for (int d : nums4) {
                    if (Sum.find(0 - (c + d)) != Sum.end()) {//检测 0 -（ 和 ）的值是否存在于map中，
                        count += Sum[0 - (c + d)];//若存在，则将用于记录的count+value；
                    }
                }
            }
            return count;
        }
```
## 代码随想录的题解:
```
int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        unordered_map<int, int> umap; //key:a+b的数值，value:a+b数值出现的次数
        // 遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中
        for (int a : A) {
            for (int b : B) {
                umap[a + b]++;
            }
        }
        int count = 0; // 统计a+b+c+d = 0 出现的次数
        // 在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就把map中key对应的value也就是出现次数统计出来。
        for (int c : C) {
            for (int d : D) {
                if (umap.find(0 - (c + d)) != umap.end()) {
                    count += umap[0 - (c + d)];
                }
            }
        }
        return count;
    }
```                                     
