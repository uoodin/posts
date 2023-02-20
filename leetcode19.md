---
title: "删除链表的倒数第N个结点"
date: 2023=3-02-20
publishdate: 2023-02-20
lastmod: 2023-02-20
draft: false
tags: ["Algorithm"]
---

```java
    //时间复杂度On 空间复杂度O1
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dum = new ListNode(head.val,head.next);
        //计算长度
        int length = 0;
        while(dum != null){
            length = length + 1;
            dum = dum.next;
        }
        //获取倒数第 n+1 个节点
        int countDown = length - n + 1;
        // 因为有arr = [1] n = 1 这种情况,所以造一个假的pre节点 
        dum = new ListNode(0,head);
        ListNode res = dum;
        while(countDown > 1) {
            dum = dum.next;
            countDown = countDown - 1;
        }
        //倒数第n+1节点,删除它的next
        dum.next = dum.next.next;
        return res.next;
    }
