---
title: 工厂模式
date: 2019-02-05 16:37:57
tags: 设计模式
---

* 什么是工厂模式？

工厂的作用或者说特点是可以快速重复的生产一种产品，其效率和成本是我们追求的目标。

* 工厂模式能解决什么问题，应用在什么样的场景？

23种COF设计模式中，光是工厂模式就有三种：

简单工厂模式：
> 一个可以生成对象的类，传入一个参数，得到我们相应的想要的对象。

```
class Factory{
    constructor(production){
        switch(production){
            case 'car':
                this.production = 'car';
                break;
            case 'train':
                this.production = 'train';
                break;
            default:
                break;
        }
    }
    
    public getProductionName(){
        return this.production;
    }
}

const car =  new Factory('car'); // 我们想让工厂生产一个对象车，于是我们传入车这个参数，得到我们想要的参数

car.getProductionName() // 'car'
```

工厂模式

> 在简单的工厂模式上增加一个继承子类，将生产对象的任务交给子类。父类则只需要集中和抽象一个些公共的方法和属性。

在我们的项目中很普遍的使用了这种模式，service.js就使用了这种模式。
```
class Factory{

    public production = 'no production';

    public getProductionName(){
        return this.production;
    }
}

class Car extends Factory{
    public production = 'car';
}

class Train extends Factory{
    public production = 'train';
}

const car = new Car();
car.getProductionName(); // car

const train = new Train();
train.getProductionName(); // train
```

抽象工厂模式

> 抽象工厂模式就是在工厂模式的基础上使用抽象类，抽象类不能参与实例生成。抽象类更多的是定义，打个比方，在抽象类中定义一个方法或者属性，但是子类继承之后，生成实例的时候并不会存在这个属性或者方法，如果不再子类中重写这个方法，实例上就无法存在。所以抽象类更多的作用是定义。更加通俗的理解就是，把所有工厂类的共有属性名放在一个抽象类中，所有的工厂类都继承这个抽象类。抽象类指定的是工厂类的机构。

javascript中暂时不存在抽象类的概念，但是我们可以模拟出抽象类。