---
title: 装饰者模式
date: 2019-02-07 12:32:34
tags: 设计模式
---
> 在不改变对象自身的基础上，动态地添加功能代码。

根据描述，装饰者显然比继承等方式更灵活，而且不污染原来的代码，代码逻辑松耦合。

在es6里面，添加了装饰器功能，就是使用了装饰着模式。
常用的装饰器有autobind，errorhandle等等。

装饰器修饰一个函数：
```
 @autobind()
  public checkActStatus() {
    let status: boolean = false;
    switch (this.actStatus) {
      case 0: this.showMessage('别着急，活动尚未开始'); break;
      case 1: status = true; break; // 状态正确,执行函数
      case 2: this.showMessage('你来晚了，活动已经结束'); break;
      default: console.log('状态码错误'); break;
    }
    return status;
  }

```

装饰器也可以修饰一个类：
```
@errorHandler()
class ClassName{
    
}
```

装饰器：
```
const forceLogin = function (forceFlag: boolean = true) {
  return function (target, key, decorator) {
    const fn = decorator.value;
    decorator.value = function () {
      const boundFn = fn.bind(this);
      if (forceFlag) {
        this.forceLogin((status) => {
          if (status) {
            boundFn.apply(null, arguments);
          } else {
            this.forceUpdate();
          }
        });
      } else {
        this.tryLogin(() => {
          boundFn.apply(null, arguments);
        });
      }
    };
  };
};

```