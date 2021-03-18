---
title: "无重复字符的最长子串"
date: 2021-03-17
publishdate: 2021-03-17
lastmod: 2021-03-17
draft: false
tags: ["Algorithm"]
---
```
/*
 * @lc app=leetcode.cn id=3 lang=golang
 *
 * [3] 无重复字符的最长子串
 */

// @lc code=start
func lengthOfLongestSubstring(s string) int {
	//卡住的几个test case
	//dvdf
	//tmmzuxt
	//pwwkew
	size := len(s)
	//已出现字符的index,比map快4ms
	var dic [256]int = [256]int{}
	for i, _ := range dic {
		dic[i] = -1
	}
	start := 0
	cur := start
	res := 0
	for cur < size {
		letter := s[cur]
		v := dic[letter]
		if v != -1 {
			//主要是这里,如果出现过存了index
			//和左边界比较,小于左边界的话,说明已经有新的重复字符,把左边切掉了
			//这个index在切掉的部分,就用不上了,直接从左边开始
			//比如 [ab][ba],不切掉的话,从第一个a的index开始,是a[bba]
			start = Max(v+1, start)
		}
		currentSize := cur - start + 1
		res = Max(currentSize, res)
		dic[letter] = cur
		cur = cur + 1
	}

	return res
}

func Max(src int, dest int) int {
	if src > dest {
		return src
	}
	return dest
}
```