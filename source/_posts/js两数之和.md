---
title: LeetCode两数之和
categories:
  - 前端
  - 算法
tags:
  - JavaScript
  - leetcode
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210601203830.png'
abbrlink: 9d66cb49
date: 2021-06-01 19:14:40
---



## LeetCode两数之和

### 题目

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

示例:

```javascript
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

[leetcode链接](https://leetcode-cn.com/problems/two-sum)

### 求解

#### 方法一：暴力枚举

时间复杂度：O(N^2)

空间复杂度：O(1)

思路及算法

最容易想到的方法是枚举数组中的每一个数 x，寻找数组中是否存在 target - x。

当我们使用遍历整个数组的方式寻找 target - x 时，需要注意到每一个位于 x 之前的元素都已经和 x 匹配过，因此不需要再进行匹配。而每一个元素不能被使用两次，所以我们只需要在 x 后面的元素中寻找 target - x。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
const twoSum = function(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target){
            	return [i,j];
            }
        }
    }
}
```

#### 方法二：哈希表

思路及算法

时间复杂度：O(n)

空间复杂度：O(n)

- 这里我们可以增加一个 Map 记录已经遍历过的数字及其对应的索引值。这样当遍历一个新数字的时候就去 Map 里查询 **target 与该数的差值是否已经在前面的数字中出现过**。如果出现过，就找到了答案，就不必再往下继续执行了。
- 利用数组存储差值的索引位来减少一次遍历，降低时间复杂度为O(n);
- 用 `hashMap` 存储遍历过的元素和对应的索引。
- 每遍历一个元素，看看 hashMap 中是否存在满足要求的目标数字。
- 所有事情在一次遍历中完成（用了空间换取时间）。

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
const twoSum = function (nums, target) {
  const map = new Map();
  for (let i = 0; i < nums.length; i++) {
    const diff = target - nums[i];
    if (map.has(diff)) {
      return [map.get(diff), i];
    }
    map.set(nums[i], i);
  }
};
```

