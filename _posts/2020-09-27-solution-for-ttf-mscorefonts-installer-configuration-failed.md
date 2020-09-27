---
layout: post
title: "修复因 ttf-mscorefonts-installer 安装 wine 应用失败的问题"
subtitle: '深度用点心吧'
author: "Y"
header-style: text
tags:
  - Linux
---

不知从哪个版本开始, 深度 `wine` 应用如企业微信/`Foxmail`等依赖包 `ttf-mscorefonts-installer`,
这个包的作用是下载安装微软核心字体. 在执行 `postinstall` 脚本时会从 `sf` 下载字体,
但不知是何原因一直无法下载成功(下载连接贴到浏览器是能够下载的). 详见 [issue](https://github.com/linuxdeepin/developer-center/issues/1904#)

解决办法:
1. 下载并安装[空包](https://ws28.cn/f/3lqatwpzrws), 该包不会执行任何操作
2. 终端执行`sudo apt-mark hold ttf-mscorefonts-installer`
3. 安装 `wine` 应用成功

