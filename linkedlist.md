---
title: "链表合集"
date: 2022-02-16
publishdate: 2022-02-16
lastmod: 2022-02-16
draft: false
tags: ["Algorithm"]
---

```
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
```

```java
    //空间复杂度O1 时间复杂度O1
    //声明一个假节点,两个list依次比较往里面加
    //如果用list2往list1里面插入的话,也可以
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dum = new ListNode(0);
        ListNode res = dum;
        while(list1 != null && list2 != null){
            if(list1.val > list2.val) {
                dum.next = list2;
                dum = dum.next;
                list2 = list2.next;
            }else {
                dum.next = list1;
                dum = dum.next;
                list1 = list1.next;
            }
        }

        //剩下的节点都比当前的大,直接加
        if(list1 == null) {
            dum.next = list2;
        } else {
            dum.next = list1;
        }
        return res.next;
    }
```


```
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
```

```java
    //时间复杂度On 空间复杂度O1
    //将节点依次往前指
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        while(cur != null) {
            //保留下一个
            ListNode temp = cur.next;
            //指向前一个结点
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }    
    
```

```
给你一个链表的头节点 head ，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 
为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。
注意：pos 不作为参数进行传递 。仅仅是为了标识链表的实际情况。

如果链表中存在环 ，则返回 true 。 否则，返回 false 。
```
```java
    //时间复杂度On 空间复杂度O1
   public boolean hasCycle(ListNode head) {
        //快慢指针
        //慢指针每次走一步
        //快指针每次两步
        //追及问题,如果快指针追上慢指针,有环
        ListNode cur = head;
        ListNode next = head;
        while(cur != null){
            cur = cur.next;
            next = next.next;
            if(next == null) {
                return false;
            }
            next = next.next;
            if(next == null) {
                return false;
            }
            if(next == cur) {
                return true;
            }
        }
        return false;
    }
```