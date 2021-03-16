---
title: "大数相加"
date: 2021-03-15
publishdate: 2021-03-15
lastmod: 2021-03-15
draft: false
tags: ["Algorithm"]
---

```
给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。
```

```
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {

	carry := 0
	var res *ListNode = &ListNode{}
	head := res
	for l1 != nil && l2 != nil {
		cur := l1.Val + l2.Val + carry
		if cur > 9 {
			cur = cur - 10
			carry = 1
		} else if carry > 0 {
			carry = 0
		}
		res.Val = cur
		l1 = l1.Next
		l2 = l2.Next
		if l1 != nil && l2 != nil {
			res.Next = &ListNode{}
			res = res.Next
		}
	}

	var append *ListNode = nil
	if l1 != nil {
		append = l1
	} else {
		append = l2
	}
	for append != nil {
		res.Next = &ListNode{}
		res = res.Next
		cur := append.Val + carry
		if cur > 9 {
			cur = cur - 10
			carry = 1
		} else if carry > 0 {
			carry = 0
		}
		res.Val = cur
		append = append.Next
	}

	if carry > 0 {
		res.Next = &ListNode{carry, nil}
	}

	return head
}

```