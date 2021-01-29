### JZ6_旋转数组的最小数字

方法一：暴力，顺序跑一遍找到可能出现的分界点（如果没有分界点则表示数列为常数数列），时间复杂度O(N)

```java
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        if (array.length == 0) return 0;
        int len = array.length;
        int ans = array[0];
        for (int i = 0; i < len-1; i++) {
            //因为只有一段被挪到最后，因此只要找到破坏单调不减的数列的那个位置就可以了
            if (array[i] > array[i+1]) {
                ans = array[i+1];
                break;
            }
        }
        //如果没有破坏单调不见的数列的位置说明整个数列是一样的
        return ans;
    }
}
```

方法二：二分法，分三种情况，关键是利用好两段单调不减的区间

```java
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        int left = 0;
        int right = array.length-1;
        while (left <= right) {
            if (left == right) break;
            //int mid = (left + right) / 2;
            //下面是二分时对int越界情况的优化
            int mid = left + (right - left) / 2;
            //中间大于右侧则最小值一定在 [mid+1, right]，因为此时left >= right
            if (array[mid] > array[right])
                left = mid + 1;
            //中间小于右侧则最小值一定在 [left, mid]，如果不是常数数列，左半区间一定是由两个单调不减序列构成，故最小值一定在左侧
            else if(array[mid] < array[right])
                right = mid;
            //中间等于右侧则最小值可能出现在mid以及mid的左右侧，如21222和22212两种情况，所以将right-1向左侧推进，而最终如果整个数组值相同，则这个算法时间复杂度将从O(log2N)退化到O(N)
            else right--;
        }
        return array[left];
    }
}
```



