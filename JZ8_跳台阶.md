### JZ8_跳台阶

本题可第七题类似，用动态规划或者递归的思维，对于跳上第n级台阶，显然必然是从n-1跳一下或者从n-2跳一下达到，所以dp[n] = dp[n-1] + dp[n-2]

下面的做法用了两个变量模拟动态规划的过程，将空间复杂度优化为O(N)，其余做法参考第七题

```java
public class Solution {
    public int JumpFloor(int target) {
        if (target == 1) return 1;
        if (target == 2) return 2;
        int pre1 = 1;
        int pre2 = 2;
        for (int i = 3; i <= target; i++) {
            int temp = pre1 + pre2;
            pre1 = pre2;
            pre2 = temp;
        }
        return pre2;
    }
}
```

