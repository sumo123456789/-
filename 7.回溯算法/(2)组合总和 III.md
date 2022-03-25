# 题目
[力扣题目链接](https://leetcode-cn.com/problems/combination-sum-iii/)
## 总结：
```
    该题和 77. 组合 的思路差不多，在明确题目需求后，
直接套用递归回溯模板，修改下参数和条件即可。
```
## 我的题解：
```
//216. 组合总和 III
        vector<vector<int>> result_216;//返回的结果
        vector<int> element_216;//result的元素
        void backtrackingCombinationSum3(int k, int n, int curSum, int curElement) {//curSum为当前和，curElement为当前element_216长度
            if (curSum == n && element_216.size() == k) {
                result_216.push_back(element_216);
                return;
            }
            else if (element_216.size() >= k) return;         
            for (; curElement <= 9;++curElement) {
                element_216.push_back(curElement);
                backtrackingCombinationSum3(k, n, curSum + curElement, curElement + 1);
                element_216.pop_back();//回溯操作
            }
        }
        vector<vector<int>> combinationSum3(int k, int n) {
            //result_216.clear();
            //element_216.clear();         
            backtrackingCombinationSum3(k, n, 0, 1);
            return result_216;
        }

```
## 代码随想录的题解:
```
    vector<vector<int>> result; // 存放结果集
    vector<int> path; // 符合条件的结果
    void backtracking(int targetSum, int k, int sum, int startIndex) {
        if (sum > targetSum) { // 剪枝操作
            return; // 如果path.size() == k 但sum != targetSum 直接返回
        }
        if (path.size() == k) {
            if (sum == targetSum) result.push_back(path);
            return;
        }
        for (int i = startIndex; i <= 9 - (k - path.size()) + 1; i++) { // 剪枝
            sum += i; // 处理
            path.push_back(i); // 处理
            backtracking(targetSum, k, sum, i + 1); // 注意i+1调整startIndex
            sum -= i; // 回溯
            path.pop_back(); // 回溯
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        result.clear(); // 可以不加
        path.clear();   // 可以不加
        backtracking(n, k, 0, 1);
        return result;
    }
```
