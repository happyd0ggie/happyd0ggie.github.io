---
layout: post
title: "让 Linux Deepin 企业微信支持选择加密盘作为文件保存位置"
subtitle: 'let linux deepin WXWork support truecrypt volumn to storage data'
author: "S.D.X."
header-style: text
tags:
  - truecrypt, deepin, WXWork
---


不知从哪个版本开始, 深度系统 wine 的企业微信无法在设置中选择文件的保存位置为
truecrypt 加密盘目录了, 会提示`目录不可访问, 请重新选择`.

由于信息保密要求, 企业微信所有数据必须保存在加密盘中, 开始折腾了好久, 无意中在
网上看到了 `deepinwine-mgr` 这个包, 提供了非常简洁的配置界面, 可以设置容器的驱
动器映射, 还可以手动增加映射, 于是我手动添加了到加密盘的映射(其实就是建立了一个
到加密盘的软链), 结果发现可以修改企微的文件保存位置了.

后来 v20 版本发布(现在武汉深之度已经成为统信软件全资子公司了, 以前的深度系统变成
了现在统信的UOS桌面社区版), 重启系统打开企微后发现文件的保存位置又变为默认的了.

为了满足公司的合规要求, 又开始折腾了. 特意去研究了下企微的启动过程, 如下:
1. 点击启动器的企微图标, 解析文件 `/opt/apps/com.qq.weixin.work.deepin/entries/applications/com.qq.weixin.work.deepin.desktop`
2. Exec="/opt/apps/com.qq.weixin.work.deepin/files/run.sh" -u %u
3. 2 实际调用 `/opt/deepinwine/tools/run_v3.sh`
4. RunApp
5. CallApp
6. FixLink
7. CallWXWork
8. CallProcess
9. wine
在追踪到第 6 步时发现了有价值的东西: 删除目录下的 c: z: y: 然后重建软链.

到此发现了问题, 只要重启系统/企微, 以上软链就会重建. 这些软件分别指向:
- c: -> ../drive_c
- z: -> /
- y: -> $HOME
并没有指向加密盘的软链, 那么加上即可解决.
```
...

rm c: z: y: x:
ln -s -f ../drive_c c:
ln -s -f / z:
ln -s -f $HOME y:
ln -s -f /media/veracrypt1/docs x:
...

```

这个问题详见 [issue](https://github.com/linuxdeepin/developer-center/issues/1889)
