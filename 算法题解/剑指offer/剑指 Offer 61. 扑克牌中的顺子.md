#### [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

**示例 1:**

```
输入: [1,2,3,4,5]
输出: True
```

**示例 2:**

```
输入: [0,0,1,2,5]
输出: True
```



```java
/**
	该问题最后比较的是任意牌（0）是否能填满非顺子的所有间距。
*/
public boolean isStraight(int[] nums) {
    int zero = 0;
    int interval = 0;
    Arrays.sort(nums);
    for(int i = 0; i < nums.length - 1; i++) {
        if(nums[i] == 0) {
            zero++;
        } else {
            // 如果有两个相同，就不可能是顺子
            if(nums[i] == nums[i+1]) {
                return false;
            }
            // 算出两个牌之间的间距。
            else if(nums[i] + 1 != nums[i+1]) {
                interval += (nums[i+1] - nums[i] - 1); 
            }
        }
    }
    return zero >= interval;
}
```

