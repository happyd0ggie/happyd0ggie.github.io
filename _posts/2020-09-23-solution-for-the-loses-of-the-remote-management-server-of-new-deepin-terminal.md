---
layout: post
title: "修复新版深度终端远程管理服务器丢失的问题"
subtitle: '深度用点心吧'
author: "Y"
header-style: text
tags:
  - Linux
---

前提是原服务器配置文件还在, 配置文件默认位置为: `~/.config/deepin/deepin-terminal/server-config.conf`.
将配置文件中的 `[<username>%40<ip>%40<port>]` 改为 `[<username>%40<ip>%40<port>%40<name>]` 即可.

问题原因: 新版深度终端新特性, 支持添加多个相同地址的远程服务器, 唯一标识远程服务器
的 `key` 变成了 `用户名+ip+端口+名称`. 即可以添加多个相同的服务器, 通过名称区分.

据深度社区[论坛](https://bbs.deepin.org/)反映, 该问题影响还不小, 难怪[老王](https://manateelazycat.github.io/)说终端越做越烂了. >^.^<
