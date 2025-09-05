#### Add Two Numbers ||

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> st1 = new Stack<>();
        Stack<Integer> st2 = new Stack<>();
        ListNode list = new ListNode(0);
        while(l1!=null){
             st1.push(l1.val);
             l1 = l1.next;

        }
        while(l2!=null){
            st2.push(l2.val);
            l2 = l2.next;
        }
        int  sum = 0;
        int carry = 0;
        while(!st1.isEmpty() || !st2.isEmpty()){
            if(!st1.isEmpty()){
                sum += st1.pop();
            }
            if(!st2.isEmpty()){
                sum += st2.pop();
            }

            list.val = sum%10;
            carry = sum/10;
            ListNode newNode = new ListNode(carry);
            newNode.next = list;
            list = newNode;
            sum = carry;
        }
        if(carry!=0) return list;
        return list.next;
   }
}
```
