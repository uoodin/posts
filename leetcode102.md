---
title: "二叉树层序遍历和锯齿层序遍历"
date: 2021-03-16
publishdate: 2021-03-16
lastmod: 2021-03-16
draft: false
tags: ["Algorithm"]
---

### 二叉树层序遍历
```go {linenos=table}
func levelOrder(root *TreeNode) [][]int {
	if root == nil {
		return nil
	}
	res := make([][]int, 0)
	traver(root, 0, &res)
	return res

}

func traver(root *TreeNode, depth int, res *[][]int) {
	if root == nil {
		return
	}
	if depth == len(*res) {
		*res = append(*res, []int{})
	}
	(*res)[depth] = append((*res)[depth], root.Val)
	traver(root.Left, depth+1, res)
	traver(root.Right, depth+1, res)
}

```
### 二叉树锯齿层序遍历(Z字型)
```go {linenos=table}
unc zigzagLevelOrder(root *TreeNode) [][]int {
	if root == nil {
		return nil
	}
	res := make([][]int, 0)
	traver(root, 0, &res)
	return res
}

func reverseInts(input []int) []int {
	if len(input) == 0 {
		return input
	}
	return append(reverseInts(input[1:]), input[0])
}

func traver(root *TreeNode, depth int, res *[][]int) {
	if root == nil {
		return
	}
	if depth == len(*res) {
		*res = append(*res, []int{})
	}

	if depth%2 == 1 {
		var local []int = make([]int, 0)
		local = append(local, root.Val)
		(*res)[depth] = append(local, (*res)[depth]...)
	} else {
		(*res)[depth] = append((*res)[depth], root.Val)
	}

	traver(root.Left, depth+1, res)
	traver(root.Right, depth+1, res)
}
```