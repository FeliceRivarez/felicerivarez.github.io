---
title: Github SSH key配置
lang: zh-CN
description: 如何为github配置ssh key
date: 2025-02-14 17:20:00 +0800
categories: [Tutorial, trivial]
tags: [Technical]
pin: false
math: true
mermaid: true
---

做计算机系统设计的大作业（NJU ICS2017）时，打算用github备份一下进度，但课程要求使用的ubuntu版本实在太老，不得不配一个ssh-key。

主要参考：[原博客](https://blog.csdn.net/weixin_42310154/article/details/118340458)。此外添加了一些自己实际配置的时候碰到的问题。

## 第一步

首先查看是否已经存在ssh-key

```
cd ~/.ssh
ls
```

事实上此时是有可能看不到的，比如我已经配置了ssh-key，并且.ssh文件夹下有对应rsa文件，但就是无法通过ls列出来：

![alt text](/images/2025-03-08-github-ssh-key/to-no-avail.png)

