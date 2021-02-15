### JZ20_包含min函数的栈

这题牛客的描述太简洁了，有点难懂，瞟了眼答案~，题目的意思就是你要实现一个栈的功能（具体完全用数组或者链表手写栈还是用集合框架没指定，这里偷懒了用了Stack类~），本题的关键就是让你在模拟栈的同时，无论何时想要获得栈的中的最小元素，都能直接获得（O(1)）的复杂度，就是让你时刻准备好当前栈的min值，并且在栈变化的时候min值依旧可以随着变化为当前栈的最小值

空间换时间，除了一个栈用于模拟栈操作，在用一个辅助栈，保存当前高度的栈的最小元素，每当正常栈入栈时，如果元素小于辅助栈栈顶，则正常栈栈顶添加该元素外，辅助栈栈顶也要添加该元素，如果入栈的元素大于等于辅助栈栈顶元素，则正常栈栈顶添加该元素，但是辅助栈栈顶再添加一遍辅助栈栈顶元素~（目的就是使得辅助栈栈顶永远为同高度的正常栈的最小元素），拿支笔画一下很快就理解了，当然出栈操作两个栈都是执行一样的弹出栈顶操作，因为辅助栈即使弹出了一个元素，它的下一个栈顶元素就是高度-1的正常栈中的最小元素（辅助栈中元素很可能出现重复，但是不打紧，空间换时间嘛）

```java
import java.util.Stack;

public class Solution {
    
    Stack<Integer> normal = new Stack<>();
    Stack<Integer> minval = new Stack<>();
    public void push(int node) {
        if (minval.empty()) minval.push(node);
        else {
            if (minval.peek() > node)
                minval.push(node);
            else
                minval.push(minval.peek());
        }
        normal.push(node);
    }

    public void pop() {
        normal.pop();
        minval.pop();
    }

    public int top() {
        return normal.peek();
    }

    public int min() {
        return minval.peek();
    }
}
```

