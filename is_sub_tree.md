---
title: "判断树的子结构"
date: 2021-03-16
publishdate: 2021-03-16
lastmod: 2021-03-16
draft: false
tags: ["Algorithm"]
---

```
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：

输入：A = [1,2,3], B = [3,1]
输出：false
示例 2：

输入：A = [3,4,5,1,2], B = [4,1]
输出：true


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSubStructure(A *TreeNode, B *TreeNode) bool {
    //定义一个匿名函数用来递归
    type fp func(*TreeNode,*TreeNode) bool
    var sub fp
    //以subA当前node为root，开始判断是不是同一棵树
    sub = func (subA *TreeNode, subB *TreeNode) bool{
        if subB == nil{
            return true
        }
        if subA == nil || subA.Val != subB.Val{
            return false
        }
        return sub(subA.Left,subB.Left) && sub(subA.Right,subB.Right)
    }
    isEnd := A != nil && B != nil 
    //树的第一层
    fromRoot := sub(A,B)
    //如果树的第一层不是，继续往下找
    return  isEnd && (fromRoot || isSubStructure(A.Left,B) || isSubStructure(A.Right,B))
}
```