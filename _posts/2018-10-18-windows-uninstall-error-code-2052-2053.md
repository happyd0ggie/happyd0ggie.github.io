---
layout: post
title: "Windows 卸载程序出现2052/2053错误解决方法"
subtitle: 'command line always does work'
author: "S.D.X."
header-style: text
tags:
  - windows
---

卸载程序出现以下错误`error2502/2503`时：
![](https://shengdexiang.github.io/img/uninstall_error_2052.png)
![](https://shengdexiang.github.io/img/uninstall_error_2053.png)

可以用如下方法成功卸载程序：（一下是个人根据微软社区提示安装出现类似问题时想到的，仅供参考）

1. 当选择卸载程序时，会弹出`User Account Control`对话框，此时点击“show details”，会发现程序对应的`msi installer`所在位置和名称，记下来；
2. 以管理员身份运行`Command Prompt`;
3. 按图示卸载，`2c5352.msi`即为第一步看到的文件名
![](https://shengdexiang.github.io/img/uninstall_using_msiexec.png)
4. 按照提示，成功卸载
