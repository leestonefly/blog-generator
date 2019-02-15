---
title: git简单用法
date: 2018-12-17 14:56:34
tags: 学习笔记
categories: IT
---
简单介绍几个常用git命令
<!-- more -->
# 1. git init
    在本目录下创建git仓库
{% asset_img gitinit.jpg [创建仓库] %}

---

# 2. git add
    新建一个test.txt文件添加文件到缓存
{% asset_img gitadd.jpg [添加到缓存] %}

---

# 3. git commit -v
*   提交更改文件，此时会打开vim，若不输入文本提交的话会出错
{% asset_img commit.jpg [提交文件] %}
*   在test.txt文件输入 11111111，再次执行git add test.txt --> git commit -v 
{% asset_img add111.jpg [添加更改后提交] %}
*   确认无误后用i输入文本，按ESC退出，输入:wq保存更改并提交
{% asset_img addsuccess.jpg [提交过程] %}
*   最终效果
{% asset_img end.jpg [提交成功] %}
---