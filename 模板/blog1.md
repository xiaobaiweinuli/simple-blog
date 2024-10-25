<%-*
tp.date.now("YYYY-MM-DD") %><%* const input = await tp.system.prompt("请输入文字"); await tp.file.rename(`${tp.date.now("YYYY-MM-DD-")}${input}`); 
//.获取当前文件创建时间
let createTime = tp.file.creation_date()
// 获取当前文件修改时间
let modificationDate = tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss")
-%>
---
title: 
date: <% modificationDate %> +0800
categories: [教程, 'GameMaker 8.0']
#文件夹，文件
tags: [教程, gm8, 编程语言]
pin: true
image: 
media_subpath: 
author: xingshuang
license: false
math: true
description: 
render_with_liquid: false
published: false
---