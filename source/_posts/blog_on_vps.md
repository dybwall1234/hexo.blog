---
title: 购买VPS搭建hexo博客
date: 2016-03-10
tags: [随笔]
---

## 配置VPS
我使用的是linode，注册选择最低配置的服务器。最好选择东京的服务器。然后进入管理界面，
![](https://github.com/dybwall1234/files/raw/master/linode.png)
1. 选择Ubuntu，设置root密码，Rebuild。
2. 然后进入Dashboard界面，BOOT启动机器。
3. 在Remote Access界面查看登录ip。
至此，服务器部分完成。
## 搭建博客
通过ssh连接服务器后，需要首先装git，gem，jekyll等工具。
1. `apt install build-essential git vim gcc make ruby_dev gem -y`
2. `gem install bundler`
3. 添加新用户 `adduser user`，把此用户加入sudoers，如何设置请百度，进入此用户环境 `su - user`，clone github博客到本地。jekyll搭建博客部分请参照http://jekyllbootstrap.com/usage/jekyll-quick-start.html
5. `cd blogdir`, 然后`bundle install`
6. `jekyll serve --host 0.0.0.0` 启动博客。就可通过ip访问了
## 配置域名
我使用的是goaddy，购买过程请自己研究，然后在管理域名里，设置转址，稍等几分钟后，就可以用域名访问博客了。



