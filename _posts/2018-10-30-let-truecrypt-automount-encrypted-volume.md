---
layout: post
title: "让TrueCrypt开机自动挂载加密卷"
subtitle: '命令行真是好玩意儿'
author: "Y"
header-style: text
tags:
  - windows
---

处于安全考虑，我们经常把重要文档和聊天记录加密保存，让心怀不轨的人即使拿到了数据也是加密的。
`TrueCrypt`这个工具支持`AES`加密，使用方便，但每次开机都需要手动打开，选择文件，加载，输入密码这些步骤，很是厌烦。
并且在执行完这些步骤之前，还不能打开微信、企业微信、TIM、邮箱等常用软件，因为这些软件的文档和记录保存位置为`TrueCrypt`创建的加密卷中，在加密卷未加载之前这些软件是无法正常启动的。

幸运的是`TrueCrypt`提供了<strong>命令行接口</strong>，我们可以在批处理脚本中调用。
因此可采用如下解决方案，让这些操作自动完成。

<strong>参考代码</strong>

```
@ECHO OFF

REM start truecrypt
START "" "C:\\Program Files\\TrueCrypt\\TrueCrypt.exe" /v "<path-to-encrypted-volume" /lg /a /p "<password>" /b /q

TIMEOUT /T 2 /nobreak
REM start wxwork
START "" "C:\\Program Files (x86)\\WXWork\\WXWork.exe" -min -autorun

TIMEOUT /T 1 /nobreak
REM start tim
START "" "C:\\Program Files (x86)\\Tencent\\TIM\\Bin\\TIM.exe" /background

TIMEOUT /T 1 /nobreak
REM start wechat
START "" "C:\\Program Files (x86)\\Tencent\\WeChat\\WeChat.exe"
```

注：代码首先使用 `TrueCrypt` 的命令行接口自动加载加密卷，其中`<path-to-encrypted-volume>`是指向加密卷文件的路径，`<password>`是创建加密卷是设置的密码；然后暂停2秒钟依次启动并自动登陆企业微信、TIM和微信。
