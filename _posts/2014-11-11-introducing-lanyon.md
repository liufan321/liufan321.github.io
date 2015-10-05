---
layout: post
title: 使用 Jekyll 和 GitHub Pages 搭建博客
---

### 1. 注册 GitHub 账号并生成 SSH Keys

[GitHub](https://github.com)目前拥有140多万开发者用户，号称程序员的Facebook，具有极高的人气，许多重要的项目都托管在上面。

注册一个 GitHub 账号，可以和世界优秀的程序员零距离接触，相信在不远的将来，我也会成为一名优秀的程序员，:P

注册账号之后，为了方便使用，建议在本地生成一个 SSH Key，具体操作步骤可以访问 [https://help.github.com/articles/generating-ssh-keys/](https://help.github.com/articles/generating-ssh-keys/)。

### 2. 为博客项目创建代码库并 clone 到本地

* 选择 Repositories，然后点击 New，创建一个代码库，代码库的名称是：[username].github.io

>    提示：[username]，是注册的 GitHub 用户名

* 在终端中将新建的代码库 clone 到本地

```
$ git clone https://github.com/[username]/[username].github.io.git
```

### 3. 安装相关软件

本环节的步骤只需执行一次即可：

```
$ gem install jekyll
$ jekyll new [username].github.io.git
$ cd [username].github.io.git
```

### 4. 选择并安装 Jekyll 模版

在 GitHub 中搜索 jekyll theme 然后选择一款喜欢的模板，下载到本地并且解压缩到自己的博客目录中。

按照模板中的时候说明进行相应的配置，通常需要编辑一下 _config.yml 文件，设置自己博客的标题以及其他相关信息。

### 5. 编写博文 & 测试

在 _posts 目录中，新建一个文件，文件名格式如下 

```
yyyy-MM-dd-topic-name.md
```

>   提示：topic-name中不要有中文、大写字符以及空格，如果有多个单词可以使用 "-" 连接。

使用一款熟悉的文本编辑器打开这个 .md 文件，撰写博客内容即可。

文章头部的格式如下：

```
---
layout: post
title: 博文主题
---
```

当然啦，在编写博客的时候测试，测试是必不可少的。打开终端中，进入本地博客代码库的主目录，然后输入：

```
$ jekyll serve
```

接着打开浏览器，在地址栏中输入

```
http://localhost:4000
```

就可以边写便刷新，查看博客的最终效果了，:P

关于内容格式的方面，分享几个实用的技巧：

*   行首使用 # 表示标题1
*   行首使用 ## 表示标题2，依次类推……
*   行首使用 * 表示项目列表
*   行首使用 > 表示引用文字
*   如果需要插入代码
    *   三个连续的 &#96;&#96;&#96; 回车(代码段开始)
    *   粘贴代码块
    *   三个连续的 &#96;&#96;&#96; 回车(代码段结束)

怎么样？感觉还不错吧，哈哈！

### 6. 提交博文

在终端中输入：

```
$ git add .
$ git commit -a -m "新建文章"
$ git push
```

>   如果是第一次提交，GitHub 大概需要 15 分钟左右生成博客，此后就可以通过 [username].github.io 访问新的博客了，:P
