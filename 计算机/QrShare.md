---
title: QrShare
tags: 新建,模板,小书匠
grammar_cjkRuby: true
grammar_flow: true
---

```flow
st=>start: 开始
e=>end: 结束
o1=>operation: 教师将课件拖入程序
o2=>operation: 程序收到文件
o3=>operation: 程序将课件post到服务端
o4=>operation: 程序下载二维码文件并提供一个数字(三位或四位)
o5=>operation: 教师讲二维码文件手动添加到课件中
st->o1->o2->o3->o4->o5->e
```

```flow
st=>start: 开始
o1=>operation: 学生扫码或者在公众号发数字
o2=>operation: 服务端/微信服务端收到请求，提供下载地址
o3=>operation: 下载
e=>end: 结束
st->o1->o2->o3->e
```
