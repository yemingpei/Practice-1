### 136. 只出现一次的数字

> 题目

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,1]
输出: 1
```

示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```

> 思路

要有线性的时间复杂度，又不能使用额外的空间，所以先排序，然后分别判断前后两个元素是否一致。这样的时间复杂度就是O(NlogN + N)。

但是看了题解才知道，最优解时间复杂度可以去到O(N)，使用异或运算。因为异或运算有以下特点

* 任何数和 0 做异或运算，结果仍然是原来的数，即 a ^ 0=a。
* 任何数和其自身做异或运算，结果是 0，即 a ^ a=0。
* 异或运算满足交换律和结合律，即 a ^ b ^ a=b ^ a ^ a=b ^ (a ^ a)=b ^0=b。

> 代码

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function (nums) {
  let single = 0;
  for (let num of nums) {
    single ^= num;
  }

  return single;
};
```

> 复杂度分析

时间复杂度：O(N)。

空间复杂度：O(1)。

> 执行

执行用时：84 ms, 在所有 JavaScript 提交中击败了46.13%的用户。

内存消耗：40.3 MB, 在所有 JavaScript 提交中击败了27.20%的用户。


