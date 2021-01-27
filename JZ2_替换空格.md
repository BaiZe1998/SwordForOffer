### JZ2_替换空格

双指针：Java中无法直接修改字符串类型的对象，所以用了StringBuffer类

不管是左边有空格，右边有空格，只有空格，多个空格情况，只要明确一个空格对应%20就好，StringBuffer中的字符串最终会扩展为一个新的字符串，新字符串的长度为原字符串长度 + 2*空格数，用两个指针同时从各个字符串末尾（或开头开始移动，我从后往前移动的双指针），如果原字符串中为空格新字符串就插入%20（旧指针移动1位，新串指针移动3位），否则新字符串就放入旧字符串对应位置的字符（旧串指针移动1位，新串指针也移动一位），直到遍历结束，新字符串中就是扩展后的串

```java
//测试样例也写了一下
public class Test1 {
    public static void main(String[] args) {
        Solution solution = new Solution();
        StringBuffer stringBuffer = new StringBuffer();
        stringBuffer.append("We are Happy");
        System.out.println(solution.replaceSpace(stringBuffer));
    }
}

//双指针
class Solution {
    public String replaceSpace(StringBuffer str) {
        //获取字符串长度
        int originalLength = str.length();
        int num = 0;
        for (int i = 0; i < originalLength; i++) {
            //统计空格数量
            if (str.charAt(i) == ' ')
                num++;
        }
        //为新的字符串指定长度：原来的空格占三个位置，相当于再额外加上两倍的空格数
        int nowLenght = originalLength + 2 * num;
        str.setLength(nowLenght);
        //从后往前定义双指针
        int originalPoint = originalLength - 1;
        int nowPoint = nowLenght - 1;
        System.out.println(originalLength + " " + nowLenght);

        //从后往前遍历原字符串
        while (originalPoint >= 0) {
            //遇到空格则替换为%20
            if (str.charAt(originalPoint) == ' ') {
                str.setCharAt(nowPoint, '0');
                str.setCharAt(nowPoint-1, '2');
                str.setCharAt(nowPoint-2, '%');
                originalPoint--;
                nowPoint -= 3;
            } else {//未遇到空格简单拷贝
                char c = str.charAt(originalPoint--);
                str.setCharAt(nowPoint--, c);
            }
        }
        return str.toString();
    }
}
```

