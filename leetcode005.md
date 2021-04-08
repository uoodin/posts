---
title: "最长回文子串"
date: 2021-03-14
publishdate: 2021-03-14
lastmod: 2021-03-14
draft: false
tags: ["Algorithm"]
---

```
给你一个字符串 s，找到 s 中最长的回文子串。

 

示例 1：

输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
示例 2：

输入：s = "cbbd"
输出："bb"
示例 3：

输入：s = "a"
输出："a"
示例 4：

输入：s = "ac"
输出："a"
 

提示：

1 <= s.length <= 1000
s 仅由数字和英文字母（大写和/或小写）组成
```

```go
package main

import "fmt"

func longestPalindrome(s string) string {
	var str string
	if len(s) == 1 {
		return s
	}
	for i := 0; i < len(s)-1; i++ {
		res := search(i, i, s)
		if len(res) > len(str) {
			str = res
		}
		if i != len(s)-1 {
			res1 := search(i, i+1, s)
			if len(res1) > len(str) {
				str = res1
			}
		}
	}
	return str
}

func search(left, right int, s string) string {
	for left >= 0 && right < len(s) && s[left] == s[right] {
		left--
		right++
	}
	return s[left+1 : right]
}

func main() {
	fmt.Println(longestPalindrome("babad"))
}
```