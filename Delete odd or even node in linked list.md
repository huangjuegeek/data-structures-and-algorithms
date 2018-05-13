# 删除单链表中的奇数或偶数结点
```java
public class DeleteOddOrEvenListNode {

    public ListNode constructList(int num) {
        if (num <= 0) return null;
        ListNode head = new ListNode(1);
        ListNode cur = head;
        for (int i = 2; i <= num; i++) {
            cur.next = new ListNode(i);
            cur = cur.next;
        }
        return head;
    }

    private void printList(ListNode head) {
        if (head == null) {
            System.out.println(head);
            return;
        }
        while (true) {
            if (head != null)
                System.out.print(head.val + "->");
            else {
                System.out.print(head);
                break;
            }
            head = head.next;
        }
        System.out.println();
    }

    static class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
        }
    }

    /**
     * 删除一个单链表中的奇数结点
     * @param head 单链表头结点
     * @return 删除操作完成后的单链表头结点
     */
    public ListNode deleteOddListNode(ListNode head) {
        ListNode dummy = new ListNode(Integer.MIN_VALUE);
        ListNode pre = dummy;
        ListNode odd = head;
        ListNode even = null;
        dummy.next = head;

        if (odd != null) {
            even = odd.next;
        }

        while (odd != null) {
            pre.next = even;
            if (even != null && even.next != null) {
                pre = even;
                odd = even.next;
                even = even.next.next;
            } else {
                break;
            }
        }

        return dummy.next;
    }

    /**
     * 删除一个单链表中的偶数结点
     * @param head 单链表头结点
     * @return 删除操作完成后的单链表头结点
     */
    public ListNode deleteEvenListNode(ListNode head) {
        ListNode dummy = new ListNode(Integer.MIN_VALUE);
        ListNode odd = head;
        ListNode even = null;
        dummy.next = head;

        if (odd != null) {
            even = odd.next;
        }

        while (even != null) {
            odd.next = even.next;
            odd = even.next;
            if (odd != null && odd.next != null) {
                even = odd.next;
            } else {
                break;
            }
        }
        return dummy.next;
    }

    public static void main(String[] args) {
        DeleteOddOrEvenListNode d = new DeleteOddOrEvenListNode();
        System.out.println("test for deleteOddListNode");
        for (int i = 0; i < 10; i++) {
            ListNode oldHead = d.constructList(i);
            System.out.print("删除前: ");
            d.printList(oldHead);

            ListNode newHead = d.deleteOddListNode(oldHead);

            System.out.print("删除后: ");
            d.printList(newHead);
        }

        System.out.println("test for deleteEvenListNode");
        for (int i = 0; i < 10; i++) {
            ListNode oldHead = d.constructList(i);
            System.out.print("删除前: ");
            d.printList(oldHead);

            ListNode newHead = d.deleteEvenListNode(oldHead);

            System.out.print("删除后: ");
            d.printList(newHead);
        }
    }

}

```