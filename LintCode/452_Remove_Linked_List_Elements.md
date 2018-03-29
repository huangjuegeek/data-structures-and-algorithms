## 452. Remove Linked List Elements
> http://www.lintcode.com/problem/remove-linked-list-elements

### Solution 1:
```cpp
// C++
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
    /**
     * @param head a ListNode
     * @param val an integer
     * @return a ListNode
     */
    ListNode *removeElements(ListNode *head, int val) {
        ListNode* dummy = new ListNode(0);
        ListNode* pre = dummy;
        ListNode* cur = head;
        dummy->next = head;
        while(cur) {
            if(cur->val == val) {
                pre->next = cur->next;
                delete cur;
                cur = pre->next;
            }
            else {
                cur = cur->next;
                pre = pre->next;
            }
        }
        head = dummy->next;
        delete dummy;
        return head;
    }
};
```
```java
// Java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param head: a ListNode
     * @param val: An integer
     * @return: a ListNode
     */
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        ListNode pre = dummy;
        ListNode cur = head;
        dummy.next = head;
        while(cur != null) {
            if (cur.val == val) {
                pre.next = cur.next;
                cur = pre.next;
            } else {
                pre = pre.next;
                cur = cur.next;
            }
        }
        head = dummy.next;
        return head;
    }
}
```
