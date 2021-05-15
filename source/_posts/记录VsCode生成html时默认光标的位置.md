---
title: 修改VsCode生成html时默认光标的位置
date: 2021-05-15 12:05:47
cover:
tags:
  - 经验
---
#####   记录在VsCode生成默认html时，修改其光标的默认位置

<!--more-->

### 首先打开code的安装路径

然后在路径的文件夹搜索：expand-full.js
如果没有可以找这个：emmetNodeMain.js

找到之后用code 打开

### 打开之后搜索 device ，会发现下面这句代码
"meta[name=viewport content='width={1:device-width}, initial-scale={2:1.0}']" 

 将其修改为 以下这句代码

"meta[name=viewport content='width=device-width, initial-scale=1.0']"

### 修改完之后目前的光标应该在title标签里，如果想修改到body里，往下看
搜索vp+title 

找到这句代码 meta:vp+title{${1:Document}})+body 

修改为 meta:vp+title{${Document}})+body

 (Document是默认生成标题，可以修改为自定义的)

### 重启Vs code
再次tab+！就会发现光标在body标签中

