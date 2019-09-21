---
title: Leetcode 2 两数相加
date: 2019-09-21 12:50:51
categories:
- Leetcode
tags:
- Leetcode
- Javascript
---

尝试解答：

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    const result = new ListNode(0)
    let l3 = result
    let flag = true
    while(flag) {
        l3.val = l1.val + l2.val + l3.val
        if(!l1.next && !l2.next) {
            flag = false
        }
        if(l3.val > 9) {
            l3.val -= 10
            l3.next = new ListNode(1)            
        } else {
            if(flag) {
                l3.next = new ListNode(0)
            }
        }
        l1 = l1.next || new ListNode(0)
        l2 = l2.next || new ListNode(0)
        l3 = l3.next
    }
    return result
};
```

这是一个模拟竖式运算相加的题目，这里新建了一个result链表用来存储答案，同时l3作为指向result链表当前操作节点的指针。flag是判断l1和l2是否已经穷尽到末尾的标志。整体思路是将l1和l2先按位加入l3，l3当即进行进位判断。并确定是否对l3的链表进行延申。

这个例子有大量可以优化的地方，特别是在空间上存在大量浪费。