### JZ4_重建二叉树

递归建树

非常常见的二叉树题目，核心思想是理解中序中的任意元素，其左侧元素都是在左子树上，右侧元素都是在右子树上 **左 中 右**。而先序遍历遵循：**中 左 右** 的顺序，对于其中的任意元素，先访问自己，再访问这个元素的左子树所有的元素，后访问右子树所有的元素

 ```java
//因为这个Solution的方法不是静态方法，所以猜测：在测试机器跑的时候是实例化这个类的对象调用方法的形式，因此我完全可以自己在这个方法内再调用一个递归
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        TreeNode treeNode = null;
        treeNode = createTree(pre, 0, pre.length-1, in, 0, in.length-1);
        return treeNode;
    }

    public TreeNode createTree(int[] pre, int pre_left, int pre_right, int[] in, int in_left, int in_right) {
        //如果对应区间内没有元素直接返回null，这种情况存在于如对一个有2个元素的子区间再调用递归后会分割为含有1 0个元素的两个区间
        if (pre_left > pre_right ) return null;
        
        //如果区间内只剩下一个元素则直接返回该元素（表示只有一个根，左右子树为null），直接新建对象调用构造方法即可，其左右对象的引用会自动赋予默认值null
        if (pre_left == pre_right) return new TreeNode(pre[pre_left]);

        //index用于表示先序左侧第一个元素在中序遍历中的位置
        int index = 0;
        for (int i = in_left; i <= in_right; i++) {
            if (in[i] == pre[pre_left]) {
                index = i;
                break;
            }
        }
        //以index为根，（以中序为基准）其左侧的元素均为index的左子树上元素，index右侧均为index右子树上的元素
        TreeNode treeNode = new TreeNode(in[index]);
        //每个根找到后，递归找左右子树的根(关键)
        treeNode.left = createTree(pre, pre_left + 1, pre_left + index - in_left, in, in_left, index - 1);
        treeNode.right = createTree(pre, pre_left + index - in_left + 1, pre_right, in, index+1, in_right);
        return treeNode;
    }
}
 ```

