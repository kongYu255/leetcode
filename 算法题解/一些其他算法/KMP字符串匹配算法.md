 ![在这里插入图片描述](https://img-blog.csdn.net/20181005224812581?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3OTY5NDMz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 

KMP算法本质为求当前字符前缀与整个字符串首字符重合的数，放入next数组当中，例如 

`"abcdabc"` 中，`next[] = {-1, 0, 0, 0, 0, 1, 2}` 

具体指代后三位abc中，a的前缀并没有可以与首字符`abcd 可拆分成 a, ab, abc, abcd` 重合的数

b的前缀有与首字符`abcda 可拆分成 a, ab, abc, abcd, abcda` 重合的数，即a

c的前缀有与首字符`abcdab 可拆分成 a, ab, abc, abcd, abcda, abcdab` 重合的数， 即ab

```java
private static int[] getNext(char[] p) {
    int pLen = p.length;
    int[] next = new int[pLen];
    int k = -1;
    int j = 0;
    next[0] = -1;
    while (j < pLen - 1) {
        if(k == -1 || p[j] == p[k]) {
            k++;
            j++;
            next[j] = k;
        } else {
            k = next[k];
        }
    }
    return next;
}

public static int indexOf(String source, String pattern) {
    int i = 0;
    int j = 0;
    char[] src = source.toCharArray();
    char[] pat = pattern.toCharArray();
    int sLen = src.length;
    int pLen = pat.length;
    int[] next = getNext(pat);
    while (i < sLen && j < pLen) {
        if (j == -1 || src[i] == pat[j]) {
            i++;
            j++;
        } else {
            j = next[j];
        }
    }
    if (j == pLen) {
        return i - j;
    }
    return -1;
}
```

