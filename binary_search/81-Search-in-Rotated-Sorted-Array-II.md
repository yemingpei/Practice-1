### 81. 搜索旋转排序数组 II

> 题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,0,1,2,2,5,6] 可能变为 [2,5,6,0,0,1,2] )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。

示例 1:
```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true
```

示例 2:
```
输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```

进阶:

这是 搜索旋转排序数组 的延伸题目，本题中的 nums  可能包含重复元素。
这会影响到程序的时间复杂度吗？会有怎样的影响，为什么？

> 思路

这是典型的在排序数组里找特定项，但是和普通的查找不太一样。我们先看下例子。
```
nums = [2,5,6,0,0,1,2]， target = 0，取中位数，刚好在中间

nums = [2,5,6,0,0,1,2]， target = 5，取中位数0，发现 0 < 5 && 2 < 5，则在左边寻找

nums = [2,5,6,7,0,1,2]， target = 1，取中位数7，发现 2  > 1 && 7 > 2，则在右边寻找

nums = [1,1,2,1]， 这种判断不出排序关系，只能从低到高开始遍历
```
所以是先判断是否有顺序，有顺序则可以用二分法。否则只能遍历。

> 代码

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {boolean}
 */
var search = function (nums, target) {
    const len = nums.length;

    let low = 0;
    let height = len - 1;

    while (low <= height) {
        const pos = Math.floor((low + height) / 2);
        const val = nums[pos];
        const lowVal = nums[low];
        const heightVal = nums[height];

        if (val === target || lowVal === target || heightVal === target) {
            return true;
        } else if (val < heightVal) {
            if (target > val && target < heightVal) {
                low = pos + 1;
            } else {
                height = pos - 1;
            }
        } else if (lowVal < val) {
            if (target > lowVal && target < val) {
                height = pos - 1;
            } else {
                low = pos + 1;
            }
        } else {
            low++;
        }
    }

    return false;
};
```

> 复杂度分析

当数组顺序二分法刚好适用，时间复杂度为O(logn)。极端情况下为O(n)。

空间复杂度为O(1)。

> 执行

执行用时：100 ms, 在所有 JavaScript 提交中击败了8.89%的用户。

内存消耗：38 MB, 在所有 JavaScript 提交中击败了100.00%的用户。

> 算法

二分法