#### Add One To Linkedlist
```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

class Solution {
    // Utility: reverse a linked list
    private ListNode reverse(ListNode head) {
        ListNode prev = null, curr = head;
        while (curr != null) {
            ListNode nextNode = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextNode;
        }
        return prev;
    }

    public ListNode addOne(ListNode head) {
        // Step 1: reverse the list
        head = reverse(head);

        // Step 2: add 1
        ListNode curr = head;
        int carry = 1; // we have to add 1
        while (curr != null) {
            int sum = curr.val + carry;
            curr.val = sum % 10;
            carry = sum / 10;

            if (carry == 0) break; // no more carry, stop early
            if (curr.next == null && carry > 0) {
                curr.next = new ListNode(carry);
                carry = 0;
                break;
            }
            curr = curr.next;
        }

        // Step 3: reverse back
        return reverse(head);
    }
```
}

