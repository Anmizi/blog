---
title: 剑指Offer 22 链表中倒数第k个节点
categories:
  - 前端
  - 算法
tags:
  - JavaScript
  - leetcode
  - 链表
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210601203830.png'
abbrlink: 72c33327
date: 2021-06-03 22:55:56
---

## [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

### 题目

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

**示例 1：**

```
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

### 题解

#### 方法一 双指针法

解题思路可参考 [点击此处](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/jian-zhi-offer-22-lian-biao-zhong-dao-sh-7u6x/)

```javascript
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var getKthFromEnd = function(head, k) {
    let latter = head;
    let former = head;
    while(k--){
        former = former.next;
    }
    while(former){
        latter = latter.next;
        former = former.next;
    }
    return latter;
};
```

#### 

###　参考链接

[链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/jian-zhi-offer-22-lian-biao-zhong-dao-sh-7u6x/)

[面试题22. 链表中倒数第 k 个节点（双指针，清晰图解）](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/mian-shi-ti-22-lian-biao-zhong-dao-shu-di-kge-j-11/)