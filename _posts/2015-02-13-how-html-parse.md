---
layout: post
title:  html解析
date:   2015-02-13 21:40
categories: js
---

> html解析大致流程是:

html标签 > 附加到dom tree(model) > 加上样式(css tree)reflow形成render tree(view) > paint
![](/theme/parse.png)

> 几个概念

- reflow: 定位(开销较大)
- paint: 绘画

> PS:

- 解析的过程是逐个节点处理(所以才有script阻塞渲染一说)
- head 文件必须先下载完,才会解析body的内容
- css放前面,先形成css tree,便于渲染;script放末尾,读取完整的节点信息且防止修改dom后重复渲染 