---
layout: post
title: NS_ENUM & NS_OPTIONS
---

`NS_ENUM` 和 `NS_OPTIONS` 是在 iOS 6 推出用于代替 enum 的更好的办法

## enum

在以前，要定义枚举类型，都是使用 `enum` 来实现的，这是在 C 语言中预设定义常量的方法

使用 `enum` 定义枚举可以有以下两种方式：

### 1. 定义枚举

```
enum {
    UITableViewCellStyleDefault,
    UITableViewCellStyleValue1,
    UITableViewCellStyleValue2,
    UITableViewCellStyleSubtitle
};
```
这种方法只定义枚举，但是不定义类型

### 2. 定义枚举 同时定义类型

```
typedef enum {
    UITableViewCellStyleDefault,
    UITableViewCellStyleValue1,
    UITableViewCellStyleValue2,
    UITableViewCellStyleSubtitle
} UITableViewCellStyle;
```

定义 `UITableViewCellStyle` 类型并且预设枚举类型

大概在 iOS 5.0 时期，苹果公司采用以下方式定义枚举类型

```
typedef enum {
    UITableViewCellStyleDefault,
    UITableViewCellStyleValue1,
    UITableViewCellStyleValue2,
    UITableViewCellStyleSubtitle
};

typedef NSInteger UITableViewCellStyle;
```

这种方式指定了 `UITableViewCellStyle` 的数据类型，但并没有告诉编译器这个类型与之前的 `enum` 有什么关系

再后来，苹果推出了 `NS_ENUM` & `NS_OPTIONS` 两个宏来定义枚举类型

## NS_ENUM

如果查看今天的 `UITableViewCell.h` 会发现，枚举类型的定义已经变为：

```
typedef NS_ENUM(NSInteger, UITableViewCellStyle) {
    UITableViewCellStyleDefault,
    UITableViewCellStyleValue1,	
    UITableViewCellStyleValue2,	
    UITableViewCellStyleSubtitle
};
```

参数说明

- 枚举的数据类型
- 枚举类型的名称

大括号里面和以前 `enum` 一样，是需要定义的预设值

这种实现方法可以在 `switch` 语句中检查类型


## NS_OPTIONS

在 C 语言开发时，也可以使用**按位掩码（bitmask）**来定义枚举类型

例如：

```
typedef enum {
    NSJSONReadingMutableContainers = (1UL << 0),
    NSJSONReadingMutableLeaves = (1UL << 1),
    NSJSONReadingAllowFragments = (1UL << 2)
} NSJSONReadingOptions;
```

使用**按位掩码**枚举的最大的好处在于：**只使用一个参数便可以传递各种选项的组合**

- 使用**按位或(|)**为枚举类型赋值
- 使用**按位与(&)**判断是否设置了某个选项
- 传入**0**表示什么附加选线都没有

在 OC 中，要定义按位掩码的枚举类型，可以使用 ```NS_OPTIONS``` 宏，示例如下：

```
typedef NS_OPTIONS(NSUInteger, NSJSONReadingOptions) {
    NSJSONReadingMutableContainers = (1UL << 0),
    NSJSONReadingMutableLeaves = (1UL << 1),
    NSJSONReadingAllowFragments = (1UL << 2)
};
```

又如：

```
typedef NS_OPTIONS(NSUInteger, NSKeyValueObservingOptions) {
    NSKeyValueObservingOptionNew = 0x01,
    NSKeyValueObservingOptionOld = 0x02,
    NSKeyValueObservingOptionInitial = 0x04,
    NSKeyValueObservingOptionPrior = 0x08
};

```

今后大家看到凡是用 `NS_OPTIONS` 定义的枚举，就可以：

- 使用**按位或(|)**指定多个选项的组合
- 如果不需要任何附加选项，直接传入 0，这样效率最高，:D

