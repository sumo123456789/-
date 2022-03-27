# 题目
[力扣题目链接](https://leetcode-cn.com/problems/combination-sum-ii/)
## 思路图
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/7.%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95/image/backtracking4.png)
## 总结：
```
    我的题解执行用时【0 ms】，内存消耗【10.5 MB】，
题目的要求意味着答案的组合中可以出现相同的数字，次数
取决于candidates，但是解集的组合不能相同。
    该题的要求落实到操作时，就是递归时可以使用相同的
元素，但在for循环时，不能使用相同的元素，也就是递归时
不用查重，for循环时需要查重。
    该题的查重方法我选用先排序，达到相同的元素都紧靠
的效果，再比较当前的candidates与上一个是否相同，若相
同，则判断为重复，跳过当前candidates。
    最后再用target - candidates[startIndex] >= 0
进行剪枝，并用target取代curSum（当前和）即可优化完成。
    随想录的查重方法是i > 0 && candidates[i] == 
candidates[i - 1] ，相比之下，可以每次都节省4个字节。
```
## 我的题解：
```
      //40. 组合总和 II
        void quickSortVector(vector<int>& candidates, int low, int high) {//快速排序
            int temp = candidates[low];
            int begin = low;
            int end = high;
            while (begin < end) {
                while (begin < end && candidates[end] >= temp) {
                    --end;
                }
                candidates[begin] = candidates[end];
                while (begin < end && candidates[begin] <= temp) {
                    ++begin;
                }
                candidates[end] = candidates[begin];
            }
            candidates[begin] = temp;
            if(low < begin - 1) quickSortVector(candidates, low, begin - 1);
            if(begin + 1 < high)  quickSortVector(candidates, begin + 1, high);
        }
        vector<vector<int>> result_40;//返回的结果
        vector<int > element_40;//result的元素
        void backtrackingCombinationSum2(vector<int>& candidates, int target, int startIndex) {//求组合
            if (target == 0) {
                result_40.push_back(element_40);
                return;
            }
            else if (target < 0) return;
            int preVal_40 = 0;//上一个candidates的值，因为candidates在1 - 50，所以初始值设置为0
            //剪枝条件为target - candidates[startIndex] >= 0
            for (; startIndex < candidates.size() && target - candidates[startIndex] >= 0; ++startIndex) {
                //若上一个candidates的值与当前candidates相同，则continue，这行代码是查重的核心步骤。
                if (preVal_40 == candidates[startIndex]) continue;
                preVal_40 = candidates[startIndex];
                element_40.push_back(candidates[startIndex]);
                backtrackingCombinationSum2(candidates, target - candidates[startIndex], startIndex + 1);
                element_40.pop_back();//回溯
            }
        }
        vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
            //result_40.clear();
            //element_40.clear();
            if (candidates.empty()) return result_40;//判断空
            quickSortVector(candidates, 0, candidates.size() - 1);//排序
            backtrackingCombinationSum2(candidates, target, 0);//求组合
            return result_40;
        }
```
## 代码随想录的题解:
```
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(vector<int>& candidates, int target, int sum, int startIndex, vector<bool>& used) {
        if (sum == target) {
            result.push_back(path);
            return;
        }
        for (int i = startIndex; i < candidates.size() && sum + candidates[i] <= target; i++) {
            // used[i - 1] == true，说明同一树枝candidates[i - 1]使用过
            // used[i - 1] == false，说明同一树层candidates[i - 1]使用过
            // 要对同一树层使用过的元素进行跳过
            if (i > 0 && candidates[i] == candidates[i - 1] && used[i - 1] == false) {
                continue;
            }
            sum += candidates[i];
            path.push_back(candidates[i]);
            used[i] = true;
            backtracking(candidates, target, sum, i + 1, used); // 和39.组合总和的区别1，这里是i+1，每个数字在每个组合中只能使用一次
            used[i] = false;
            sum -= candidates[i];
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<bool> used(candidates.size(), false);
        path.clear();
        result.clear();
        // 首先把给candidates排序，让其相同的元素都挨在一起。
        sort(candidates.begin(), candidates.end());
        backtracking(candidates, target, 0, 0, used);
        return result;
    }
```
