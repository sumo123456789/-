# 题目
[力扣题目链接](https://leetcode-cn.com/problems/spiral-matrix-ii/)

## 我的题解：
```
class Solution {
public:
vector<vector<int>> generateMatrix(int n) {
        vector< vector<int> > arr(n, vector<int>(n, 0));
        int Row = 0;// 二维数组中的行
        int List = 0;// 二维数组中的列
        for (int i = 1; i <= n * n;) {
            // 向右填装数据
             while (List + 1 < n && i <= n * n) {// 检测是否到达边界
                 arr[Row][List] = i++;              
                 if (arr[Row][List + 1] == 0) {// 检测右边是否已有数据
                     List++;// 若无数据，则向右移动一个单位                  
                 }
                 else {
                     if (arr[Row + 1][List] == 0) {//若下边没有数据
                         Row++;//向下移动一个单位
                     }
                     break;
                 }               
             } 
             // 向下填装数据
             while (Row + 1 < n && i <= n * n) {
                 arr[Row][List] = i++;
                 if (arr[Row + 1][List] == 0) {
                     Row++;                    
                 }
                 else {
                     if (arr[Row][List - 1] == 0) {
                         List--;
                     }
                     break;
                 }            
             } 
             // 向左填装数据
             while (List - 1 >= 0 && i <= n * n){
                 arr[Row][List] = i++;
                 if (arr[Row][List - 1] == 0) {
                     List--;
                 }
                 else {
                     if (arr[Row - 1][List] == 0) {
                         Row--;
                     }
                     break;
                 }               
             }
             // 向上填装数据
             while (Row - 1 >= 0 && i <= n * n){
                 arr[Row][List] = i++;
                 if (arr[Row - 1][List] == 0) {
                     Row--;
                 }
                 else {
                     if (arr[Row][List + 1] == 0) {
                         List++;
                     }
                     break;
                 }             
             }      
        }
        return arr;
    }
}
```
## 代码随想录的题解:
```
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, 0)); // 使用vector定义一个二维数组
        int startx = 0, starty = 0; // 定义每循环一个圈的起始位置
        int loop = n / 2; // 每个圈循环几次，例如n为奇数3，那么loop = 1 只是循环一圈，矩阵中间的值需要单独处理
        int mid = n / 2; // 矩阵中间的位置，例如：n为3， 中间的位置就是(1，1)，n为5，中间位置为(2, 2)
        int count = 1; // 用来给矩阵中每一个空格赋值
        int offset = 1; // 每一圈循环，需要控制每一条边遍历的长度
        int i,j;
        while (loop --) {
            i = startx;
            j = starty;

            // 下面开始的四个for就是模拟转了一圈
            // 模拟填充上行从左到右(左闭右开)
            for (j = starty; j < starty + n - offset; j++) {
                res[startx][j] = count++;
            }
            // 模拟填充右列从上到下(左闭右开)
            for (i = startx; i < startx + n - offset; i++) {
                res[i][j] = count++;
            }
            // 模拟填充下行从右到左(左闭右开)
            for (; j > starty; j--) {
                res[i][j] = count++;
            }
            // 模拟填充左列从下到上(左闭右开)
            for (; i > startx; i--) {
                res[i][j] = count++;
            }

            // 第二圈开始的时候，起始位置要各自加1， 例如：第一圈起始位置是(0, 0)，第二圈起始位置是(1, 1)
            startx++;
            starty++;

            // offset 控制每一圈里每一条边遍历的长度
            offset += 2;
        }

        // 如果n为奇数的话，需要单独给矩阵最中间的位置赋值
        if (n % 2) {
            res[mid][mid] = count;
        }
        return res;
    }
};

```                                     
## 总结：
```
    这道题主要考察对代码的掌握能力，题目的难点主要集中在编写限制条件。
我的做题思路不够系统、清晰，总是从题目中总结出少许规律，在对题目理解不
够深刻时就开始打代码，导致打出来的代码很多漏洞，常常发现自己漏掉了一些
隐含的规律然后就要耗费大量时间在调试、对代码进行修补中。应该在打代码前
就用流程图从代码角度做足够仔细的推演。
```
