# 前端日常总结大全
## [JavaScript运行机制](https://baijiahao.baidu.com/s?id=1615713540466951098&wfr=spider&for=pchttp:// "JavaScript运行机制")
1、JavaScript语言是单线程的，同一个时间只能做一件事；
2、遵循事件循环机制，当JS解析执行时，会被引擎分为两类任务，同步任务（synchronous） 和 异步任务（asynchronous）。对于同步任务来说，会被推到执行栈按顺序去执行这些任务。对于异步任务来说，当其可以被执行时，会被放到一个 任务队列（task queue） 里等待JS引擎去执行。当执行栈中的所有同步任务完成后，JS引擎才会去任务队列里查看是否有任务存在，并将任务放到执行栈中去执行，执行完了又会去任务队列里查看是否有已经可以执行的任务。这种循环检查的机制，就叫做事件循环(Event Loop)。对于任务队列，其实是有更细的分类。其被分为 微任务（microtask）队列 & 宏任务（macrotask）队列。

## data-name、data-age等HTML5自定义属性
1、H5自定义属性新特性。

## title的作用
## 列表循环
## script是什么
脚本执行区域块，类似于运行器。

## defer和async的区别
1、 `<script src="script.js">` 没有 defer 或 async,浏览器会立即加载并执行指定的脚本,“立即”指的是在渲染该 script 标签之下的文档元素之前,也就是说不等待后续载入的文档元素,读到就加载并执行。

2、` <script async src="script.js">` 有 async,加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步）。

3、 `<script defer src="myscript.js">` 有 defer,加载后续文档元素的过程将和 script.js 的加载并行进行（异步）,但是 script.js 的执行要在所有元素解析完成之后,DOMContentLoaded 事件触发之前完成。

从实用角度来说,首先把所有脚本都丢到 </body> 之前是最佳实践,因为对于旧浏览器来说这是唯一的优化选择,此法可保证非脚本的其他一切元素能够以最快的速度得到加载和解析。
defer 和 async 在网络读取（下载）这块儿是一样的,都是异步的（相较于 HTML 解析）
它俩的差别在于脚本下载完之后何时执行,显然 defer 是最接近我们对于应用脚本加载和执行的要求的。
关于 defer,此图未尽之处在于它是按照加载顺序执行脚本的,这一点要善加利用
async 则是一个乱序执行的主,反正对它来说脚本的加载和执行是紧紧挨着的,所以不管你声明的顺序如何,只要它加载完了就会立刻执行
仔细想想,async 对于应用脚本的用处不大,因为它完全不考虑依赖（哪怕是最低级的顺序执行）,不过它对于那些可以不依赖任何脚本或不被任何脚本依赖的脚本来说却是非常合适的

## DOMContentLoaded和window.onload的区别
何时触发这两个事件？
1、当 onload 事件触发时，页面上所有的DOM，样式表，脚本，图片，flash都已经加载完成了。
2、当 DOMContentLoaded 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash。


## 盒模型是什么
1、内容(content)、内边距(padding)、边框(border)、外边距(margin)， CSS盒子模型都具备这些属性。

## 宽度不定，如何实现三个元素按照1：1：1布局
## 介绍一下BFC
## DOM事件流的顺序
DOM事件流包括三个阶段:
事件捕获阶段
处于目标阶段
事件冒泡阶段

事件捕获阶段 => 处于目标阶段 => 事件冒泡阶段
在这个过程中可以使用event.stopPropagation();来阻止这个过程继续执行；
而addEventListener（）的第三个参数为：true则表示将事件绑定在捕获阶段，false表示将事件绑定在冒泡阶段；

捕获阶段：从window对象传导到目标节点（上层传到底层）称为“捕获阶段”（capture phase），捕获阶段不会响应任何事件；
目标阶段：在目标节点上触发，称为“目标阶段”
冒泡阶段：从目标节点传导回window对象（从底层传回上层），称为“冒泡阶段”（bubbling phase）。事件代理即是利用事件冒泡的机制把里层所需要响应的事件绑定到外层；

![](https://img-blog.csdnimg.cn/2019011111581623.jpg)


## 事件委托
1、可以大量节省内存占用，减少事件注册，比如在ul上代理所有li的click事件就非常棒
2、可以实现当新增子对象时无需再次对其绑定（动态绑定事件）

## setTimeout、Promise、Async、Await异步原理和执行顺序
## ES6的新增功能
1.Default Parameters（默认参数） in ES6
2.Template Literals（模板对象） in ES6
3.Multi-line Strings （多行字符串）in ES6
4.Destructuring Assignment （解构赋值）in ES6
5.Arrow Functions in（箭头函数） ES6
6.Promises in ES6
7.Block-Scoped Constructs Let and Const（块作用域let和const）
8.Classes （类）in ES6
9.Modules （模块）in ES6
```html
import虽然属于声明命令，但它是和export命令配合使用的。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
```

ES6为字符串扩展了几个新的API：
```html
includes()：返回布尔值，表示是否找到了参数字符串。
startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。 
```

## 从输入url到页面加载发生了什么

## 浏览器渲染过程与性能优化
https://juejin.cn/post/6844904040346681358#heading-27

## HTTP CODE 状态码

```html
100 Continue  继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
200 OK   正常返回信息
201 Created  请求成功并且服务器创建了新的资源
202 Accepted  服务器已接受请求，但尚未处理
301 Moved Permanently  请求的网页已永久移动到新位置
302 Found  临时性重定向
303 See Other  临时性重定向，且总是使用 GET 请求新的 URI
304 Not Modified  自从上次请求后，请求的网页未修改过
400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求
401 Unauthorized  请求未授权
403 Forbidden  禁止访问
404 Not Found  找不到如何与 URI 相匹配的资源
500 Internal Server Error  最常见的服务器端错误
503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）
```

## 性能分析 chrome devtool lighthouse

## 前端页面加载阻塞渲染问题，如何解决？
我认为阻塞页面渲染分为两方面：
1、JS 加载问题
2、CSS加载问题
