### JZ7_斐波那契数列

方法一：数组存储顺序暴力

时间复杂度：O(N)

空间复杂度：O(N)

```java
public class Solution {
    public int Fibonacci(int n) {
        int[] fib = new int[40];
        fib[0] = 0;
        fib[1] = 1;
        for (int i = 2; i <= n; i++) {
            fib[i] = fib[i-1] + fib[i-2];
        }
        return fib[n];
    }
}
```

方法二：在一的基础上不用数组而是用三个变量不断传递斐波那契数列

时间复杂度：O(N)

空间复杂度：O(1)

```java
public class Solution {
    public int Fibonacci(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
 
        int pre0 = 0;
        int pre1 = 1;
 
        while (n > 1) {
            int temp = pre0 + pre1;
            pre0 = pre1;
            pre1 = temp;
            n--;
        }
        return pre1;
    }
}
```

方法三：递归

时间复杂度：O(2^N)

空间复杂度：系统栈空间消耗

```java
public class Solution {
    public int Fibonacci(int n) {
        if (n == 0) return 0;
        if (n == 1 || n == 2) return 1;
        else return Fibonacci(n-1) + Fibonacci(n-2);
    }
}
```

方法四：记忆化搜索

由于在递归的时候发现，其实有很多fib[i]的值是重复计算了，所以可以利用记忆话搜索进一步优化递归的情况，但是这种方法要传递一个公共的数组去维护，Java只给了一个n为参数~，下面是记忆化搜索的一个方法

时间复杂度：O(N)，没有重复计算

空间复杂度：递归系统栈空间消耗

```java
public class Test {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int[] fib = new int[n+1];
        System.out.println(new Solution().Fibonacci(fib, n));
    }
}

class Solution {
    public int Fibonacci(int[] fib, int n) {
        if (n == 0 || n == 1) return n;
        if (fib[n] != 0) return fib[n];
        return fib[n] = Fibonacci(fib, n-1) + Fibonacci(fib, n-2);
    }
}
```

