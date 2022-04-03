# 题目
[力扣题目链接](https://leetcode-cn.com/problems/reverse-linked-list/)
## 思路图
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/%E9%93%BE%E8%A1%A8/image/ListImage.png)
## 总结：
```
    该题相对于 46. 全排列 而言，多了个树层查重的步骤。
在之前的练习中，我已经遇过多次树层查重的情况，一般而言
树层查重需要定义一个局部变量，且需要对数据进行排序。而
树枝查重，则需要定义一个全局变量。在下面的代码中，我定
义的哈希表是一个二维数组，但这种哈希表不利于拓展，应该
定义一个 nums长度的vector记录nums中元素是否被选用较好。
```
## 我的题解：
```
        //47. 全排列 II
        vector<vector<int>> result_47;//返回的结果
        vector<int> element_47;//result的元素
        int hash_47[21][8];//哈希表，树枝去重
        void backtrackintPermuteUnique(vector<int>& nums) {
            if (element_47.size() == nums.size()) {
                result_47.push_back(element_47);
                return;
            }
            int lastVal = -100;//树层去重
            for (int i = 0; i < nums.size(); ++i) {
                //前一条件用于树枝去重，后一条件用于树层查重
                if (hash_47[nums[i] + 10][i] == 1 || nums[i] == lastVal) {
                    continue;
                }
                lastVal = nums[i];
                element_47.push_back(nums[i]);
                ++hash_47[nums[i] + 10][i];
                backtrackintPermuteUnique(nums);
                element_47.pop_back();
                --hash_47[nums[i] + 10][i];
            }
        }
        vector<vector<int>> permuteUnique(vector<int>& nums) {
            sort(nums.begin(), nums.end());
            backtrackintPermuteUnique(nums);
            return result_47;
        }
```
## 代码随想录的题解:
```
    vector<vector<int>> result;
    vector<int> path;
    void backtracking (vector<int>& nums, vector<bool>& used) {
        // 此时说明找到了一组
        if (path.size() == nums.size()) {
            result.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            // used[i - 1] == true，说明同一树枝nums[i - 1]使用过
            // used[i - 1] == false，说明同一树层nums[i - 1]使用过
            // 如果同一树层nums[i - 1]使用过则直接跳过
            if (i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false) {
                continue;
            }
            if (used[i] == false) {
                used[i] = true;
                path.push_back(nums[i]);
                backtracking(nums, used);
                path.pop_back();
                used[i] = false;
            }
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        result.clear();
        path.clear();
        sort(nums.begin(), nums.end()); // 排序
        vector<bool> used(nums.size(), false);
        backtracking(nums, used);
        return result;
    }
```
