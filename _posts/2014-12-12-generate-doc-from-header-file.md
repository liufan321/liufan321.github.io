---
layout: post
title: 从.H文件中提取文档
---

# headerdoc2html

* 作用：处理头文件，并基于特殊格式的注释生成HTML文档

* 示例：

`
$ find . -name \*.h | xargs headerdoc2html -o ~/Desktop/docs -j
`

* 说明：
	1. 遍历当前文件夹及子文件夹
	2. 查找所有 .h 文件
	3. 使用`headerdoc2html`生成 .h 的文档并输出至 ~/Desktop/docs 目录中
	4. 允许 .h 文件中使用`javadoc`的注释格式 
	5. `xargs`命令可以将`find`的结果分块传递给`headerdoc2html`

# 从.h中提取文档

* 作用：处理`headerdoc2html`的输出目录，创建一个链接到每个标题文档的索引页面
* 示例：

`
$ gatherheaderdoc ~/Desktop/docs
`

