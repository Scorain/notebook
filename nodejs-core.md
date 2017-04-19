# nodejs核心基础

> &copy; suny 2017-04-19 10:30


### Events 模块

1）理解

　　javascript的核心特性之一是异步，对于jser而言，异步编程有如下几种不同的方式： 回调函数、事件监听、观察者模式、Promise。其中事件监听和观察者模式的使用其实是一样的，触发器触发事件、监听器执行操作。两者的不同之处在于实现，事件监听中的事件是由运行环境（run-time）提供的，何时触发由运行环境决定；观察者模式中的事件类型及其触发时机都是由开发者自定义的。

　　nodejs中的Events模块可以理解为一个实现了观察者模式的库，要在自己的模块中使用，需要显示的引入此模块。此外，Events模块默认实现了一个 `error` 事件来处理模块实例出现异常的情况。

2）API

    EventEmitter类
    监听事件： EventEmitter#on(eventName, listener), EventEmitter#addListener(eventName, listener)
    移除事件监听：EventEmitter#removeListener(eventName, listener)
    触发事件：EventEmitter#emit(eventName, args)

3) 原理

![观察者模式数据结构图解](./images/pubsub-data-structure.png)


### Buffer 模块

　　Buffer类是用于处理二进制数据的，其实例代表一个大小固定、在V8堆外分配的物理内存。

### Stream 模块

### File System 模块

### HTTP 模块

### Errors 模块

### Timers 模块