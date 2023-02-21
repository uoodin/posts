---
title: "常用命令"
date: 2022-02-21
publishdate: 2022-02-21
lastmod: 2022-02-21
draft: false
tags: ["backup"]
---

### Debug Root手机进程

``` shell
adb shell
su
magisk resetprop ro.debuggable 1
stop;start;
```