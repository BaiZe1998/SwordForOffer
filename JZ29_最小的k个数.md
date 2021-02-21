### JZ29_最小的k个数

这题刻意回顾了一下推排序，IDEA的调试真方便~，但是堆排序具体怎么写还是看自己，可能每次写出来都有点不一样

```java
public class Test {
    public static void main(String[] args) {
        int[] a = {4,5,1,6,2,7,3,8};
        Solution solution = new Solution();
        ArrayList<Integer> list = solution.GetLeastNumbers_Solution(a, 4);
        System.out.println(list);
    }
}

class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        int len = input.length;
        //诡异的边界条件
        if (len < k) return new ArrayList<Integer>();
        //注意下标从0开始
        for (int i = len/2-1; i >= 0; i--)
            adjust(input, i, len);
        //此时小顶堆已经建立
        ArrayList<Integer> ans = new ArrayList<>();
        for (int i = 0; i < k; i++) {
            //将最小的放入结果数组，然后交换到无序末尾
            int temp = input[0];
            ans.add(input[0]);
            input[0] = input[len-i-1];
            input[len-i-1] = temp;
            adjust(input, 0, len-i-1);
        }
        return ans;
    }

    //以root为根，len为下标的边界
    public void adjust(int[] a, int root, int len) {
        while (root < len) {
            int left = root*2+1;
            int right = root*2+2;
            int temp = root;
            if (left < len && a[root] > a[left])
                temp = left;
            //这里比较巧妙，如果left比root小，则temp表示left，否则依旧表示root
            if (right < len && a[right] < a[temp])
                temp = right;
            //交换
            if (temp != root) {
                int p = a[temp];
                a[temp] = a[root];
                a[root] = p;
                root = temp;
            } else
                break;
        }
    }
}
```

