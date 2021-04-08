---
title: "前序中序重建二叉树"
date: 2021-03-15
publishdate: 2021-03-15
lastmod: 2021-03-15
draft: false
tags: ["Algorithm"]
---

```
输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof
```

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
    if len(preorder) == 0 {
        return nil
    }
    
    //前序遍历数组，第一个元素就是根节点
    head := preorder[0]
    res := TreeNode{head, nil, nil}
    middle := 0
    
    //然后在中序遍历数组里面找到这个根节点
    for i,v := range(inorder) {
        if v == head{
            middle = i
            break
        }
    }

    leftSize := middle + 1
    //左边的元素就都是左子树里面的
    res.Left = buildTree(preorder[1:leftSize],inorder[:leftSize])
    //右边的元素就都是右子树里面的。把左边和右边的子数组重复以上步骤
    res.Right = buildTree(preorder[leftSize:],inorder[leftSize:])

    return &res
}
```