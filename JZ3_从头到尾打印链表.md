### JZ3_从头到尾打印链表

简单题：遍历一遍链表，用一个栈存放遍历结果，然后后进先出就是输出结果，第一次用Java写链表题，突然想到Java没有c/c++繁琐的指针，而对象实例本身就是在栈内存存放的堆内存的地址，所以对象之间用==比较就可以理解为c/c++中指针去比较地址~

```java
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> arrayList1 = new ArrayList<Integer>();
        //这个数组列表被用作栈的作用，由于不知道有多少个元素，无法提前设置大小
        while (listNode != null) {
            arrayList1.add(listNode.val);
            listNode = listNode.next;
        }
        int len = arrayList1.size();
        //逆序一下
        for (int i = 0; i < len/2; i++) {
            Integer temp = arrayList1.get(i);
            arrayList1.set(i, arrayList1.get(len-1-i));
            arrayList1.set(len-1-i, temp);
        }
        return arrayList1;
    }
}
```

