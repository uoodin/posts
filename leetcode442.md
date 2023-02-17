---
title: "数组中重复的数据"
date: 2022-02-16
publishdate: 2022-02-16
lastmod: 2022-02-16
draft: false
tags: ["Algorithm"]
---
```
给你一个长度为 n 的整数数组 nums ，其中 nums 的所有整数都在范围 [1, n] 内，且每个整数出现 一次 或 两次 。请你找出所有出现 两次 的整数，并以数组形式返回。

你必须设计并实现一个时间复杂度为 O(n) 且仅使用常量额外空间的算法解决此问题。
```
```java
    public List<Integer> findDuplicates(int[] nums) {
        //时间复杂度On 空间复杂度O1
        List<Integer> res = new ArrayList<>();
        for(int i = 0; i < nums.length; i++) {
            //因为nums范围在 [1,n],所以将nums[i] 换到 i - 1位置上
            //换过来的元素,如果不在自己的位置,要继续换
            while(nums[i] != nums[nums[i] - 1]){
                swap(i,nums[i] - 1,nums);
            }
        }
        //不在自己的位置的元素,就是重复的
        for(int i = 0; i < nums.length; i++){
            if(nums[i] - 1 != i){
                res.add(nums[i]);
            }
        }
        return res;
    }

    void swap(int src,int dest,int[] nums){
        int temp = nums[src];
        nums[src] = nums[dest];
        nums[dest] = temp;
    }
```