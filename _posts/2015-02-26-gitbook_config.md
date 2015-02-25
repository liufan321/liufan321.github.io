# GitBook 配置

1. 下载并安装 npm

	* node-v0.12.0.pkg [http://nodejs.org/download/](http://nodejs.org/download/)

2. 安装 gitbook

	`$ npm install gitbook -g`

3. 进入终端 cd 到新建的电子书目录

	```
	$ touch SUMMARY.md
	$ gitbook init
	```

4. 下载并安装 gitbookEditor，gitbook 本地编辑器 [https://github.com/GitbookIO/editor/releases](https://github.com/GitbookIO/editor/releases)

	* 打开并选择刚刚 init 的目录即可编辑

5. 本地预览

	```
	gitbook serve
	```
	
6. 下载并安装 calibre，生成电子书使用

	* calibre-2.20.0 [http://calibre-ebook.com/download_osx](http://calibre-ebook.com/download_osx)
	
	* 在终端输入
	
	`$ ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin`
	
7. 生成电子书

	```
	$ gitbook epub
	$ gitbook pdf
	```
	
8. .gitignore [https://github.com/github/gitignore.git](https://github.com/github/gitignore.git)	


