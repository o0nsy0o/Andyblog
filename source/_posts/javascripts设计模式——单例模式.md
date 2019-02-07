---
title: 单例模式
date: 2019-02-06 12:32:34
tags: 设计模式
---
在程序中每次生成一个对象都有性能上的开销，但是往往我们需要的功能都是一样的，这样如果每次使用的时候都创建一个对象，是没有必要的。

所谓单例模式就是保证一个类只会生成一个实例。每次实例化的时候我们需要检查这个这个类上是否已经存在实例，如果已经有实例了我们就把当前实例返回回去。

以下实现的单例模式为惰性单例。(它只有在用户需要的时候才会创建对象实例。)
```
const getSingleton = (className) => {
  let singleton = null;
  return () => {
    // 检查是否存在实例
    // 如果不存在, 那么创建
    if(!singleton) singleton = new className();
    return singleton;
  }
};

/*********** 以下是测试代码 ***********/
// 为了方便展示, 这里定义一个空类
class Demo {};

// 创建指定类的单例生成函数
let getDemoSingleton = getSingleton(Demo);

let d1 = getDemoSingleton(),
  d2 = getDemoSingleton();

// 输出 true
console.log(d1 === d2);
```