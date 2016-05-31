## Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/

#### Solution 1:
用栈来模拟递归调用栈
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == NULL)
            return NULL;
        stack<ListNode*> stk;
        ListNode *cur = head;
        do {
            stk.push(cur);
            cur = cur->next;
        } while(cur);
        head = stk.top();
        cur = head;
        stk.pop();
        while(!stk.empty()) {
            cur->next = stk.top();
            stk.pop();
            cur = cur->next;
        }
        cur->next = NULL;
        return head;
    }
};
```
#### Solution 2:
https://leetcode.com/course/chapters/leetcode-101/reverse-linked-list/
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *pre = NULL;
        ListNode *cur = head;
        while(cur != NULL) {
            ListNode *nextTemp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = nextTemp;
        }
        return pre;
    }
};
```
#### Solution 3:
递归求解一
```cpp
class Solution {
private:
    ListNode* newHead;
public:
    ListNode* reverseList(ListNode* head) {
        if(head == NULL)
            return NULL;
        ListNode *newTail = recursiveReverse(head);
        newTail->next = NULL;
        return newHead;
    }
    
    ListNode* recursiveReverse(ListNode* node) {
        if(node->next) {
            ListNode *ret = recursiveReverse(node->next);
            ret->next = node;
            return node;
        }
        else {
            newHead = node;
            return node;
        }
    }
};
```
递归求解二
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (head == NULL || head->next == NULL) {
            return head;
        }
        ListNode* newRoot = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return newRoot;
    }
};
```
