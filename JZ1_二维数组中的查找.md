### JZ1_二维数组中的查找

暴力的写法：

因为每行每列从左往右依次递增，假设从左上点开始，对二维矩阵用bfs搜索下面的和右边的元素，并标记搜索过的元素，每次判断：如果该元素大于目标元素则停止该方向的搜索（因为再往右往下都会更大，不可能搜到），如果扫描到的元素小于等于目标元素则将其坐标加入集合（队列），while循环每次取出集合中一个坐标判断该点的值是否为目标的值，相等则return返回true，直到集合为空返回false

```java
import java.util.LinkedList;

public class Solution {
    public boolean Find(int target, int [][] array) {
        //对于int[][] = {{}}，array.length == 1
        if (array[0].length == 0) return false;
        
        //访问标记数组，对于出现过的元素则下次不再访问
        int[][] vis = new int[array.length][array[0].length];
        //只要是个集合都可以，或自己写个数组也可以，但要注意空间
        LinkedList<Item> list = new LinkedList<Item>();
        boolean ans = false;
        list.add(new Item(0, 0));
        //每次加入集合的坐标就标记1表示访问过了
        vis[0][0] = 1;
        
        while (list.size() > 0) {
            Item item = list.remove();
            int x = item.getX();
            int y = item.getY();
            if (array[x][y] == target) return true;
            else {
                //x表示纵坐标，处理下标越界的情况
                if (x+1 < array.length && vis[x+1][y] == 0 && array[x+1][y] <= target) {
                    vis[x+1][y] = 1;
                    list.add(new Item(x+1, y));
                }
                //y表示横坐标，处理下标越界情况
                if (y+1 < array[0].length && vis[x][y+1] == 0 && array[x][y+1] <= target) {
                    vis[x][y+1] = 1;
                    list.add(new Item(x, y+1));
                }
            }
        }
        return ans;
    }
}

//用于存放坐标(x, y)
class Item {
    private int x;
    private int y;

    public Item(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public void setX(int x) {
        this.x = x;
    }

    public int getY() {
        return y;
    }

    public void setY(int y) {
        this.y = y;
    }
}
```

