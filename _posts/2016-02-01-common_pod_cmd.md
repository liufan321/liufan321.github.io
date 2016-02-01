---
layout: post
title: 常用 CocoaPod 终端命令
---

## 简介

* CocoaPods 是 iOS 非常常用的类库管理工具
* 作为 iOS 程序员，掌握 CocoaPods 的常用终端命令，是必不可少的基本技能

### 集成框架命令

```bash
# 创建默认的 Podfile
$ pod init

# 第一次使用安装框架
$ pod install

# 安装框架，不更新本地索引，速度快，但是不会升级本地代码库
$ pod install --no-repo-update 

# 今后升级、添加、删除框架
$ pod update

# 更新框架，不更新本地索引，速度快
# 可以安装新框架或者删除不用的框架，但是不会升级项目已经安装的框架
$ pod update --no-repo-update 

# 查看哪些框架有更新版本，如果习惯使用 `--no-repo-update` 参数，这个命令就显得格外重要了 
$ pod outdated

# 搜索框架
# - 空格 下一页
# - q 退出
# - / 搜索
$ pod search AFNetworking

# 只搜索复合名字的框架，这个对于搜索结果非常多时，尤其有用
$ pod search AFNetworking --simple

# 帮助
$ pod --help
```

### Podfile 格式说明

```bash
# 最低支持的 iOS 版本
platform :ios, '8.0'


# Swift 项目需要使用 `frameworks`
# OC 和 Swift 混编项目也需要使用 `frameworks`
# 如果使用 `framework`，OC 文件在导入头文件时需要使用 `@import xxx;` 格式
use_frameworks!


# DemoProject 安装的框架列表，cocoapod 1.0 版本以上一定要有 target
target 'DemoProject' do

# ~> 后面的数字是 3.0.4 版本，如果省略，则安装或升级最新版本
pod 'AFNetworking', '~> 3.0.4'

end


# DemoProjectTests 安装的框架列表
target 'DemoProjectTests' do

end

# DemoProjectUITests 安装的框架列表
target 'DemoProjectUITests' do

end
```