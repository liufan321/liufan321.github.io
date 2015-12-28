---
layout: post
title: 自定义 NSLog
---

## 问题

* 开发中用了大量的 `NSLog`，但是发布时想取消这些 `NSLog` 
* 开发中是否经常用过 `NSLog(@"%s", __FUNCTION__);`

## 解决问题

* 新建 `PrefixHeader.pch` 文件
* 输入以下内容：

```objc
#ifdef __OBJC__

#ifdef DEBUG
#define NSLog(fmt, ...) NSLog((@"%s [Line %d] " fmt), __PRETTY_FUNCTION__, __LINE__, ##__VA_ARGS__)
#else
#define NSLog(...)
#endif

#endif
```

* 选择 `项目`->`TARGETS`->`[ProjectName]`->`Build Settings`
* 在搜索框输入 `prefix header`
* 在 `Prefix Header`中输入 `[ProjectName]/PrefixHeader.pch`
* 如下图所示

![](/assets/20151005-01-set_prefix_header.png)

* 运行测试，如下图修改运行模式

![](/assets/20151005-02-set_scheme_mode.png)

> 搞定收工！
