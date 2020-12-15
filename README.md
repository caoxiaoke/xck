# 前端日常总结大全
1、JavaScript运行机制
a、JavaScript语言是单线程的，同一个时间只能做一件事；
b、遵循事件循环机制，当JS解析执行时，会被引擎分为两类任务，同步任务（synchronous） 和 异步任务（asynchronous）。对于同步任务来说，会被推到执行栈按顺序去执行这些任务。对于异步任务来说，当其可以被执行时，会被放到一个 任务队列（task queue） 里等待JS引擎去执行。当执行栈中的所有同步任务完成后，JS引擎才会去任务队列里查看是否有任务存在，并将任务放到执行栈中去执行，执行完了又会去任务队列里查看是否有已经可以执行的任务。这种循环检查的机制，就叫做事件循环(Event Loop)。对于任务队列，其实是有更细的分类。其被分为 微任务（microtask）队列 & 宏任务（macrotask）队列。

1、 data-name、data-age等HTML5自定义属性
2、title的作用
3、列表循环
4、script是什么
5、defer和async的区别
6、DOMContentLoaded和window.onload的区别
7、盒模型是什么
8、宽度不定，如何实现三个元素按照1：1：1布局
9、介绍一下BFC
10、DOM事件流的顺序
11、事件委托
12、setTimeout、Promise、Async、Await异步原理和执行顺序
13、ES6的新增功能
14、从输入url到页面加载发生了什么
