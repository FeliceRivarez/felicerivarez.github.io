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

## 第一步：查看是否已经存在ssh-key

首先查看是否已经存在ssh-key

```bash
cd ~/.ssh
ls
```

事实上此时是有可能看不到的，比如我已经配置了ssh-key，并且.ssh文件夹下有对应rsa文件，但就是无法通过ls列出来：

![alt text](/images/2025-03-08-github-ssh-key/to-no-avail.png)

即便用sudo权限也是无法ls出来的，很奇怪。这时直接配置一个新的ssh-key即可。

## 第二步：创建新ssh-key

使用sudo创建ssh-key。注意下面的邮箱需要替换成自己的邮箱。

```bash
sudo ssh-keygen -t rsa -C "xxx@xxx.com"
```

输入完之后一路回车即可。这时新的key就生成好了，可以看到存在了/root/.ssh/id_rsa下。

![alt text](/images/2025-03-08-github-ssh-key/keygen.png)

但比较尴尬的地方在于使用ls仍然无法将这个文件列出来，所以直接cat就好了。

## 第三步：获取key内容

使用cat获取文件中存储的key值（仍然需要sudo）：

```bash
sudo cat /root/.ssh/id_rsa.pub
```

![alt text](/images/2025-03-08-github-ssh-key/getkey.png)

直接将这个文件里面的**全部内容**进行复制即可，即：`ssh-rsa [key的值，一长串] xxx@xxx.com`

## 第四步：在github中配置key

进入个人账户的settings：

![alt text](/images/2025-03-08-github-ssh-key/settings.png)

然后在`SSH and GPG keys`中选择`New SSH key`，将之前复制的内容直接粘贴进去即可。

![alt text](/images/2025-03-08-github-ssh-key/addkey.png)

## 测试配置是否成功

测试配置的key是否能直接authenticate into github：

```bash
sudo ssh -T git@github.com
```

注意这里同样是需要sudo的：

![alt text](/images/2025-03-08-github-ssh-key/testing.png)