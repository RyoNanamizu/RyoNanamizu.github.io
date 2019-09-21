---
title: Leetcode 2 两数相加
date: 2019-09-21 12:50:51
tags: Leetcode Javascript
---

题目要求：

> 给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。
> 
> 如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
> 
> 您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
> 
> 示例：
> 
> 输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
> 输出：7 -> 0 -> 8
> 原因：342 + 465 = 807
> 
> 来源：力扣（LeetCode）
>
> 链接：https://leetcode-cn.com/problems/add-two-numbers
>
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

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