#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

 **示例:**

```
输入: a = 1, b = 1
输出: 2
```

**提示：**

- `a`, `b` 均可能是负数或 0
- 结果不会溢出 32 位整数



```java
public int add(int a, int b) {
    // 进位为0，直接返回a
    if(b == 0) {
        return a;
    }
    // 与运算左移来表达进位
    int c = (a & b) << 1;
    
    // 异或来代表二进制无进位的加法
    int d = a ^ b;

    return add(d, c);
}
```

