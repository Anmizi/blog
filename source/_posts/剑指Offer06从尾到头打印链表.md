---
title: 剑指 Offer 06. 从尾到头打印链表
categories:
  - 前端
  - 算法
tags:
  - JavaScript
  - leetcode
  - 链表
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210601203830.png'
abbrlink: 8c70c103
date: 2021-06-01 20:51:40
---

## [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

### 题目

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1：

```
输入：head = [1,3,2]
输出：[2,3,1]
```

限制：

```
0 <= 链表长度 <= 10000
```

### 求解

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var reversePrint = function(head) {
    let arr = [];
    let cur = head;
    while(cur){
        arr.push(cur.val);
        cur = cur.next;
    }
    return arr.reverse();
};
```

*tips*:

**使用push+reverse而不是unshift理由：**

例如 `var arr = [1,2,3]`
由于数组这种数据结构是有序的
那么我们按常理通常说当使用unshift插入到数组第一项时，后续的每一项都要向后移动一位，复杂度较高
而使用push追加至数组末尾，则只用改变一项，最终只使用reverse反转一次数组就OK

**但是在JS中是没有这个问题的，JS中使用push和unshift都可以，没有时间上的问题，主要是因为JS数组的内部实现同其他语言有区别**，而我们这里依然强调使用push+reverse而不是unshift，目的是为了让大家统一思路，因为其他语言中类似于unshift的方法确实存在这个问题