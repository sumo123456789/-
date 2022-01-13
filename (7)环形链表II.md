# 题目
[力扣题目链接](https://leetcode-cn.com/problems/linked-list-cycle-ii/)
## 思路图
### 方法一：暴力解法
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/%E9%93%BE%E8%A1%A8/image/ListImage5.1.png)
### 方法二：双指针解法
![image](https://github.com/sumo123456789/DataStructureAndAlgorithm/blob/main/%E9%93%BE%E8%A1%A8/image/ListImage5.2.png)
## 总结：
```
    我做题时虽然有想到双指针的方式去解题，但是该题的：
“在首元结点和相遇结点各放置一个指针，两指针正常向后移
动，相遇之处就是循环开始点”的这个特征确实难以发现，无
奈之下只好用暴力解法去解决该题。通过这题，我也知道了在
看不出题目中隐藏的数据关系时，可以用数学公式，尝试求出
内在的数据关系。
```
## 我的题解：
//暴力解法
```
 ListNode* detectCycle(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {//1. 判断传入的 head 节点及其 next 是否为空
            return nullptr;
        }
        ListNode* Orange = head; //2. 橙色、绿色指针指向 head 节点
        ListNode* Green = head;
        while (true) {//重复3、4、5、6 
            Green = Green->next;//3. 绿色指针向后移动一个节点
            while (Orange != Green) {//重复4、5 直到橙色指针等于绿色指针
                if (Green->next == nullptr) {
                    return nullptr;
                }
                if (Green->next == Orange) {
                    return Orange;
                }
                Orange = Orange->next;
            }
            Orange = head;
        }
    }

```
//双指针解法
```
 ListNode* detectCycle(ListNode* head) {
        ListNode* Fast = head;
        ListNode* Slow = head;
        while (Fast != nullptr && Fast->next != nullptr) {  
            Fast = Fast->next->next;
            Slow = Slow->next;
            if (Fast == Slow) {
                ListNode* Index_1 = head;
                ListNode* Index_2 = Fast;
                while (Index_1 != Index_2) {
                    Index_1 = Index_1->next;
                    Index_2 = Index_2->next;                
                }
                return  Index_1;
            }
        }
        return nullptr;
    }
```
## 代码随想录的题解:
```
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            // 快慢指针相遇，此时从head 和 相遇点，同时查找直至相遇
            if (slow == fast) {
                ListNode* index1 = fast;
                ListNode* index2 = head;
                while (index1 != index2) {
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index2; // 返回环的入口
            }
        }
        return NULL;
    }
```                                    
