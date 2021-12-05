# 合并k个生序链表
    把自己第一时间写的贴了上来，如果面试官看到这种代码是不是很减分

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode head = new ListNode(0);
        int n = lists.length;
        
        int count = n;
        ListNode curr = head;
        while (count > 0) {
            int min = 10001;
            int minI = -1;
            for (int i = 0; i < n; i++) {
                if (lists[i] == null) continue;
                if (lists[i].val < min) {
                    min = lists[i].val;
                    minI = i;
                }
            }
            if (minI == -1) break;
            curr.next = lists[minI];
            curr = curr.next;
            lists[minI] = lists[minI].next;
            if (lists[minI] == null) count--;
        }
        return head.next;
    }
}
```