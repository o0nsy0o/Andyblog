---
title: 发布订阅模式
date: 2019-02-06 12:32:32
tags: 设计模式
---

订阅-发布模式定义了对象之间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖它的对象都可以得到通知。

订阅-发布模式和观察者模式概念相似，但在订阅-发布模式中，订阅者和发布者之间多了一层中间件：一个被抽象出来的信息调度中心。但其实没有必要太深究2者区别，因为《Head First 设计模式》这本经典书都写了：发布+订阅=观察者模式。其核心思想是状态改变和发布通知。在此基础上，根据语言特性，进行实现即可。

signal.js是一个典型的发布订阅的js工具库

我们看一下常用的用法：
```
import signal from 'signal-js';
 
signal.on('basic', arg => console.log(arg);
 
signal.emit('basic', 1);

signal.on('multiple', () => console.log(1));
signal.on('multiple', () => console.log(2));
signal.on('multiple', () => console.log(3));
 
signal.trigger('multiple');
```

我们可以发现不管在这个事件上绑定多少监听器，只要触发这个事件，这些监听器都能触发相应的事件。


传入多个参数
```
import signal from 'signal-js';
 
signal.on('params', (one, two, three) => console.log(one, two, three));
 
signal.emit('params', 1, 2, 3);
```

取消注册
```
import signal from 'signal-js';
 
signal.on('test', () => console.log('hi'))
signal.off('test') // removes all `test` events
signal.emit('test'); // nothing happens
```


使用once可以只触发一次
```
import signal from 'signal-js';
 
signal.once('bam', function() {
  console.log('Boom!');
});
 
signal.emit('bam')
// > "Boom!"
 
signal.emit('bam');
// nothing is logged
```

你可以创建不同的监听池
```
import signal from 'signal-js';
 
signal.on('foo', () => console.log('global'));
 
const local = signal();
local.on('foo', () => console.log('local'));
 
const local2 = local();
local2.on('foo', () => console.log('local2'));
 
signal.emit('foo');
// > "global"
 
local.emit('foo');
// > "local"
 
local2.emit('foo');
// > "local2"
```