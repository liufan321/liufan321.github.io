---
layout: post
title: BLOCK写递归
---

今天又有同学面试被问到用 blcok 写递归了，写一个留在这里哈，有兴趣的同学面试前查阅一下。

首先来一个 oc 的递归：

```objc
- (int)sum:(int)num {
    if (num == 0) {
        return num;
    }
    return num + [self sum:num - 1];
}
```

写递归算法只需要记住两点即可：

1. 有一个明确的出口
2. 不满足条件出口时，自己调用自己

按照以上思路用 block 改写一下：

```objc
static int (^sumBlock)(int) = ^ (int num) {
    if (num == 0) {
        return num;
    }
    return num + sumBlock(num - 1);
}; 
```

注意，要做到自己调用自己，需要能够准确的在内存中找到 `block` 的函数入口，因此需要使用 `static` 修饰符号，其他就没啥了

另外，面试中如果被问到，一定要说下：

1. 每调用一次自己，系统都会开辟一个栈桢记录临时变量和参数
2. 递归次数过多，会出现栈溢出错误
3. 移动开发中不建议使用递归算法，现在主线程栈区只有 `512K`

上面的测试代码调用 `NSLog(@"%d", sumBlock(1024 * 128));` 就会出现栈溢出错误

提问：为啥 `1024 * 128` 会栈溢出呢？:P
