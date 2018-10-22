---
layout: post
title: "从进程内存空间寻找下载链接"
subtitle: 'process hacker is a good tool'
author: "S.D.X."
header-style: text
tags:
  - Vim
---

时刻保持软件是最新发布版本。无奈在线升级很慢，需要从升级对话框找出升级包现在链接。
!()[https://shengdexiang.github.io/img/update-notepad++.png]

速度实在是慢
!()[https://shengdexiang.github.io/img/update-notepad-progress.png]

打开任务管理器，找到进程
!()[https://shengdexiang.github.io/img/find-process-name.png]

右键转到详细信息，找到进程ID
!()[https://shengdexiang.github.io/img/find-process-pid.png]

打开Process Hacker找到进程
!()[https://shengdexiang.github.io/img/find-process-using-process-hacker.png]

右键打开属性，选择memory，strings查找字符串
!()[https://shengdexiang.github.io/img/process-hacker-search-string.png]

选择Filter&rarr;Contains(case-insensitive...)
!()[https://shengdexiang.github.io/img/process-hacker-filter-string.png]

保存查找结果
!()[https://shengdexiang.github.io/img/process-hacker-save-filter-result.png]

找到下载链接
!()[https://shengdexiang.github.io/img/find-download-uri-from-search-result.png]
