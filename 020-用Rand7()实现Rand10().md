### Leetcode470，用Rand7()实现Rand10()

​		已有方法 rand7 可生成 1 到 7 范围内的均匀随机整数，试写一个方法 rand10 生成 1 到 10 范围内的均匀随机整数。

​		不要使用系统的 Math.random() 方法。

思路：

（1）保证得到1~10的数字是等概率的。

（2）主要问题：小的随机数生成大的随机数如何保证等概率

```
采用公式：（randN-1）*N + randN

【0，7，14，21，28，35，42】+【1，2，3，4，5，6，7】=【1~49的正整数，等概率】，最后保留小于11的数

因为1~40模10得到1~10的数，可以过滤掉一些数提高效率。
```



```java
/**
 * The rand7() API is already defined in the parent class SolBase.
 * public int rand7();
 * @return a random integer in the range 1 to 7
 */
class Solution extends SolBase {
    public int rand10() {
        int num = (rand7()-1)*7 + rand7();
        while(num>40){
            num = (rand7()-1)*7 + rand7();
        }
        return 1+num%10;
    }
}
```







**要求1：从Rand10()到Rand7()**

思路：

（1）由大的随机数生成小的随机数是比较方便的，本身就是等概率的。

```
因为rand10()在1~10生成的数是等概率的，只要判断生成的随机数是否小于8，返回结果即可
```



