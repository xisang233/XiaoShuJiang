---
title: New Idownload
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---

[toc]

# Todo List

## 服务端

1. 使用ROR(或Django)重写
2. 主页美化(使用Bootstrap等工具)
3. 制作一些静态网页，上面主要放各种ranking(常用软件、电子书、电影TOPXXX)
静态网页可以使用md制作。gitblog是只需要上传.md文件就能实现的博客程序，不需要数据库支持，适合这一任务。
4. 既然都有blog了，那就顺便把FAQ也重写一些吧。

## 管理员

1. 使用Python制作客户端，实现批量上传

## 公众号

静态页面可以做一个链接，放到公众号底部(制作一个按钮)
公众号搜索(需要先把storage.bfsu.edu.cn的硬伤改了)
日常推送制作...(大坑)

## 其他功能

比如一键分享小文件，建议限制文件尺寸、限制分享时效(例如72小时)，分享时不需要输入账号密码登录。
此功能最好放在idownload之外。

# 现在Idownload的迷之bug

1. 上传文件总是上传到/Public/xiaoshu/xxxx.xxx，原因暂时不明
2. 手机不能使用北外网盘
