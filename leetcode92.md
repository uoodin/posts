---
title: "反转链表2"
date: 2023-02-22
publishdate: 2023-02-22
lastmod: 2023-02-22
draft: false
tags: ["Algorithm"]
---
```java
public ListNode reverseBetween(ListNode head, int left, int right) {
        //声明一个虚拟节点,解决[1,3] 1 1 这种特殊的case,直接使用head节点无法通过
        ListNode dum = new ListNode(0,head);
        ListNode pre = dum;
        int length = 0;
        //找到左右边界
        for(int i = 0; i < left - 1; i++) {
            pre = pre.next;
        }
        ListNode end = pre;
        for(int i = 0; i < right - left + 1; i++) {
            end = end.next;
        }
        //左边界的前一个节点和右边界的下一个节点
        ListNode endNext = end.next;
        ListNode start = pre.next;
        //切割要反转的链表
        pre.next = null;
        end.next = null;
        reverse(start);
        //拼接反转后的链表
        pre.next = end;
        start.next = endNext;
        return dum.next;
    }

    void reverse(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        while(cur != null) {
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
    }
```