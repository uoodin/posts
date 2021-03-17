---
title: "数组全部排列组合DFS"
date: 2021-03-16
publishdate: 2021-03-16
lastmod: 2021-03-16
draft: false
tags: ["Algorithm"]
---

```
给定一个 没有重复 数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```
var res [][]int

func permute(nums []int) [][]int {
	res = make([][]int, 0)
	has := make([]bool, len(nums))
	cur := make([]int, 0)
	traversal(has, cur, 0, nums)
	return res
}

func combine(src []int, num int) []int {
	var dest = make([]int, len(src))
	copy(dest, src)
	return append(dest, num)
}

func traversal(has []bool, cur []int, depth int, nums []int) {
	if depth == len(nums) {
		res = append(res, cur)
		return
	}
	for i := 0; i < len(nums); i++ {
		v := nums[i]
		if !has[i] {
			has[i] = true
			cur = combine(cur, v)
			//这里不能用append
			//append在扩容的时候会返回一个新的slice，和旧的slice不再是同一个引用
			//cur = append(cur, v)
			traversal(has, cur, depth+1, nums)
			has[i] = false
			cur = cur[:len(cur)-1]
		}
	}
}


```

```
//解法2,传slice指针,解决append问题
func permute(nums []int) [][]int {
	res := make([][]int, 0)
	has := make([]bool, len(nums))
	cur := make([]int, 0)
	traversal(has, &cur, 0, nums, &res)
	return res
}


func traversal(has []bool, cur *[]int, depth int, nums []int, res *[][]int) {
	if depth == len(nums) {
		size := len(*cur)
		var dest = make([]int, size)
		copy(dest, *cur)
		*res = append(*res, dest)
		return
	}
	for i := 0; i < len(nums); i++ {
		v := nums[i]
		if !has[i] {
			has[i] = true
			*cur = append(*cur, v)
			traversal(has, cur, depth+1, nums, res)
			has[i] = false
			*cur = (*cur)[:len(*cur)-1]
		}
	}
}
```