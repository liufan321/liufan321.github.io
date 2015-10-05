---
layout: post
title: 自定义 NSLog
---

## 问题

* 开发中用了大量的 `NSLog`，但是发布时想取消这些 `NSLog` 
* 开发中是否经常用过 `NSLog(@"%s", __FUNCTION__);`

## 解决问题

* 新建 `ExtendNSLog` 类，继承自 `NSObject`
* 在 `ExtendNSLog.h` 中删除默认代码
* 添加以下函数声明：

```objc
void ExtendNSLog(const char *file, int lineNumber, const char *functionName, NSString *format, ...);
```

* 在 `ExtendNSLog.m` 中删除默认代码
* 添加以下代码实现：

```objc
void ExtendNSLog(const char *file, int lineNumber, const char *functionName, NSString *format, ...) {
    
    va_list ap;
    
    va_start(ap, format);
    
    if (![format hasSuffix: @"\n"]) {
        format = [format stringByAppendingString: @"\n"];
    }
    
    NSString *body = [[NSString alloc] initWithFormat:format arguments:ap];
    
    va_end(ap);
    
    NSString *fileName = [[NSString stringWithUTF8String:file] lastPathComponent];
    fprintf(stderr, "(%s) (%s:%d) %s",
            functionName,
            [fileName UTF8String],
            lineNumber,
            [body UTF8String]);
}
```

* 新建 `PrefixHeader.pch` 文件
* 输入以下内容：

```objc
#ifdef __OBJC__

#import <UIKit/UIKit.h>
#import <Foundation/Foundation.h>

#import "ExtendNSLog.h"

#ifdef DEBUG
#define NSLog(args...) ExtendNSLog(__FILE__, __LINE__, __PRETTY_FUNCTION__, args);
#else
#define NSLog(x...)
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
