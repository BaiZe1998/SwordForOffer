### JZ14_链表中倒数第k个节点

方法一：求倒数第k个节点可以算求正数第num-k个节点，前提是要先遍历一遍链表得到链表中元素的总个数，整体要遍历两边链表

```java
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        int num = 0;
        ListNode p = head;
        while (p != null) {
            num++;
            p = p.next;
        }
        //对于返回null的情况要提前判断，相比双指针处理会方便一些
        if (k < 1 || k > num) return null;
        num -= k;
        p = head;
        while (num > 0) {
            p = p.next;
            num--;
        }
        return p;
    }
}
```

方法二：双指针（快慢指针）

注意快指针先走k个位置，然后快慢指针同时向右移动，（慢指针初始位null，第一次右移后指向head头指针）在有解情况下，等快指针指向null（末尾的指针的next就是null），此时慢指针就指向链表中倒数第k个节点

由于题目没有给出k的限定范围，以及无解情况也可能出现，所以要注意边界条件的判断

```java
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        //对于倒数第k个可能是0也可能是负数
        if (k <= 0) return null;
        ListNode p1 = head;
        ListNode p2 = null;
        //先将快指针移动k位
        int move = k-1;
        while (move > 0) {
            //如果链表中元素个数小于k则表示没有倒数k的说法，直接返回空
            if (p1 == null) return null;
            p1 = p1.next;
            //快指针先右移k次
            move--;
        }
        //在慢指针开始移动前要将其指向head
        if (p1 != null) {
            p2 = head;
            p1 = p1.next;
        }
        while (p1 != null) {
            p1 = p1.next;
            p2 = p2.next;
        }
        return p2;
    }
}
```

