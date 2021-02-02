### JZ9_变态跳台阶

有了第八题的铺垫，很容易就发现了规律，对于n级台阶的种数为dp[n] = dp[n-1] + dp[n-2] + ... + dp[0]，然后如果这题用两个for循环维护一个数组是可以的，但是可以进一步优化空间与时间，因为归根结底是求n级台阶的情况，所以只要用两个变量去代替实现数组求和的功能即可

通过推理得知：第 i 级台阶的跳法等于前 i - 1 级所有种数求和 + 1，用pre表示前 i - 1的种数和，用ans表示当前层结果

时间复杂度：O(N)

空间复杂度：O(1)

```java
public class Solution {
    public int JumpFloorII(int target) {
        if (target == 1) return 1;
        if (target == 2) return 2;
        //pre表示前i-1位的和
        int pre = 3;
        //ans表示i级台阶共有ans种方法
        int ans = 0;
        for (int i = 3; i <= target; i++) {
            ans = pre+1;
            pre += ans;
        }
        return ans;
    }
}
```

