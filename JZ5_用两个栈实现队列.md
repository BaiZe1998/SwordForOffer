### JZ5_用两个栈实现队列

简单题

注意这题让我们做什么：封装一个类，让它能实现队列的功能，用两个栈实现，就是倒来倒去，push就是往第一个栈压入元素，pop就是从第二个栈弹出元素，如果第二个栈空了，就将第一个栈的所有元素弹出，压入第二个栈后弹出，重复上述操作即可，题目没有讲如果两个栈都为空，此时再弹出元素会有什么反应

（提示中给出了Stack类，平时我们也可以根据元素个数用数组手写栈功能，我两种方法都会给出）

Stack类实现：

```java
import java.util.Stack;

//就是说：它让我写一个类（封装），可以实现队列的功能，要求用两个栈实现队列的push和pop方法，并且这里是用的Java的Stack类，完全可以用数组手写栈
public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();

    public void push(int node) {
        stack1.push(node);
    }

    //如果两个栈都空会遇到这种情况吗？
    public int pop() {
        if (stack2.isEmpty()) {
            //将第一个栈中元素全部弹出压入第二个栈
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
            //如果栈2依旧为空（此时表示两个栈都已经空了，则返回-1，意思意思，题目没要求~）
            if (stack2.isEmpty()) return -1;
            else return stack2.pop();
        } else {
            return stack2.pop();
        }
    }
}
```

手写栈：

```java
//就是说：它让我写一个类（封装），可以实现队列的功能，要求用两个栈实现队列的push和pop方法，并且这里是用的Java的Stack类，完全可以用数组手写栈(但空间大小要根据实际情况而定)
public class Solution {
    private int[] stack1 = new int[100005];
    private int[] stack2 = new int[100005];
    private int s1_top = -1;
    private int s2_top = -1;

    public void push(int node) {
        stack1[++s1_top] = node;
    }

    //如果两个栈都空会遇到这种情况吗？
    public int pop() {
        if (s2_top >= 0) {
            return stack2[s2_top--];
        } else {
            while (s1_top >= 0) {
                stack2[++s2_top] = stack1[s1_top--];
            }
            if (s2_top >= 0) return stack2[s2_top--];
            else return -1;
        }
    }
}
```

