---
title: "二叉树的最近公共祖先"
date: 2021-03-17
publishdate: 2021-03-17
lastmod: 2021-03-17
draft: false
tags: ["Algorithm"]
---
```
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q，最近公共祖先表示为一个节点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”
```
```
func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
	if root == nil || p == nil || q == nil {
		return nil
	}
	if root == p || root == q {
		return root
	}
	//从当前节点开始找
	left := lowestCommonAncestor(root.Left, p, q)
	right := lowestCommonAncestor(root.Right, p, q)
	//如果在两边，那当前节点就是
	if left != nil && right != nil {
		return root
	}
	//如果都在某一边,那这边的这个节点就是
	if left == nil && right != nil {
		return right
	}
	if right == nil && left != nil {
		return left
	}

	return nil
}
```