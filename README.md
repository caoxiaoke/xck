# 前端日常总结大全
## [JavaScript运行机制](https://baijiahao.baidu.com/s?id=1615713540466951098&wfr=spider&for=pchttp:// "JavaScript运行机制")
1、JavaScript语言是单线程的，同一个时间只能做一件事；
2、遵循事件循环机制，当JS解析执行时，会被引擎分为两类任务，同步任务（synchronous） 和 异步任务（asynchronous）。对于同步任务来说，会被推到执行栈按顺序去执行这些任务。对于异步任务来说，当其可以被执行时，会被放到一个 任务队列（task queue） 里等待JS引擎去执行。当执行栈中的所有同步任务完成后，JS引擎才会去任务队列里查看是否有任务存在，并将任务放到执行栈中去执行，执行完了又会去任务队列里查看是否有已经可以执行的任务。这种循环检查的机制，就叫做事件循环(Event Loop)。对于任务队列，其实是有更细的分类。其被分为 微任务（microtask）队列 & 宏任务（macrotask）队列。

## data-name、data-age等HTML5自定义属性
1、H5自定义属性新特性。

## title的作用
网站标题信息
有利于SEO引擎搜索
更友好、语义化

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
父元素：display: flex;
子集：flex:1;

## 介绍一下BFC
一、常见定位方案
在讲 BFC 之前，我们先来了解一下常见的定位方案，定位方案是控制元素的布局，有三种常见方案:

普通流 (normal flow)
在普通流中，元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。
浮动 (float)
在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，其效果与印刷排版中的文本环绕相似。
绝对定位 (absolute positioning)
在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。

二、BFC 概念
Formatting context(格式化上下文) 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。


那么 BFC 是什么呢？

BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于上述定位方案的普通流。

具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。

通俗一点来讲，可以把 BFC 理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

三、触发 BFC
只要元素满足下面任一条件即可触发 BFC 特性：

body 根元素
浮动元素：float 除 none 以外的值
绝对定位元素：position (absolute、fixed)
display 为 inline-block、table-cells、flex
overflow 除了 visible 以外的值 (hidden、auto、scroll)

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

这是一道经典的面试题，这道题没有一个标准的答案，它涉及很多的知识点，面试官会通过这道题了解你对哪一方面的知识比较擅长，然后继续追问看看你的掌握程度。当然我写的这些也只是我的一些简单的理解，从前端的角度出发，我觉得首先回答必须包括几个基本的点，然后在根据你的理解深入回答。

　　1、浏览器的地址栏输入URL并按下回车。

　　2、浏览器查找当前URL是否存在缓存，并比较缓存是否过期。

　　3、DNS解析URL对应的IP。

　　4、根据IP建立TCP连接（三次握手）。

　　5、HTTP发起请求。

　　6、服务器处理请求，浏览器接收HTTP响应。

　　7、渲染页面，构建DOM树。

　　8、关闭TCP连接（四次挥手）。

　　说完整个过程的几个关键点后我们再来展开的说一下。

　　一、URL

　　我们常见的RUL是这样的:http://www.baidu.com,这个域名由三部分组成：协议名、域名、端口号，这里端口是默认所以隐藏。除此之外URL还会包含一些路径、查询和其他片段，例如：http://www.tuicool.com/search?kw=%E4%。我们最常见的的协议是HTTP协议，除此之外还有加密的HTTPS协议、FTP协议、FILe协议等等。URL的中间部分为域名或者是IP，之后就是端口号了。通常端口号不常见是因为大部分的都是使用默认端口，如HTTP默认端口80，HTTPS默认端口443。说到这里可能有的面试官会问你同源策略，以及更深层次的跨域的问题，我今天就不在这里展开了。

　　二、缓存

　　说完URL我们说说浏览器缓存,HTTP缓存有多种规则，根据是否需要重新向服务器发起请求来分类，我将其分为强制缓存，对比缓存。

　　强制缓存判断HTTP首部字段：cache-control，Expires。

　　Expires是一个绝对时间，即服务器时间。浏览器检查当前时间，如果还没到失效时间就直接使用缓存文件。但是该方法存在一个问题：服务器时间与客户端时间可能不一致。因此该字段已经很少使用。

　　cache-control中的max-age保存一个相对时间。例如Cache-Control: max-age = 484200，表示浏览器收到文件后，缓存在484200s内均有效。 如果同时存在cache-control和Expires，浏览器总是优先使用cache-control。

　　对比缓存通过HTTP的last-modified，Etag字段进行判断。

　　last-modified是第一次请求资源时，服务器返回的字段，表示最后一次更新的时间。下一次浏览器请求资源时就发送if-modified-since字段。服务器用本地Last-modified时间与if-modified-since时间比较，如果不一致则认为缓存已过期并返回新资源给浏览器；如果时间一致则发送304状态码，让浏览器继续使用缓存。

　　Etag：资源的实体标识（哈希字符串），当资源内容更新时，Etag会改变。服务器会判断Etag是否发生变化，如果变化则返回新资源，否则返回304。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329142757404-377860259.png)

　　三、DNS域名解析

　　我们知道在地址栏输入的域名并不是最后资源所在的真实位置，域名只是与IP地址的一个映射。网络服务器的IP地址那么多，我们不可能去记一串串的数字，因此域名就产生了，域名解析的过程实际是将域名还原为IP地址的过程。

　　首先浏览器先检查本地hosts文件是否有这个网址映射关系，如果有就调用这个IP地址映射，完成域名解析。

　　如果没找到则会查找本地DNS解析器缓存，如果查找到则返回。

　　如果还是没有找到则会查找本地DNS服务器，如果查找到则返回。

　　最后迭代查询，按根域服务器 ->顶级域,.cn->第二层域，hb.cn ->子域，www.hb.cn的顺序找到IP地址。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329144552311-345405404.jpg)

　　递归查询，按上一级DNS服务器->上上级->....逐级向上查询找到IP地址。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329144611358-1044454178.jpg)

　　四、TCP连接

　　在通过第一步的DNS域名解析后，获取到了服务器的IP地址，在获取到IP地址后，便会开始建立一次连接，这是由TCP协议完成的，主要通过三次握手进行连接。

　　第一次握手： 建立连接时，客户端发送syn包（syn=j）到服务器，并进入SYN_SENT状态，等待服务器确认； 

　　第二次握手： 服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；

　　第三次握手： 客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK(ack=k+1），此包发送完毕，客户端和服务器进入ESTABLISHED（TCP连接成功）状态，完成三次握手。

 

　　完成三次握手，客户端与服务器开始传送数据。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329145607592-1103856922.png)

**五、浏览器向服务器发送HTTP请求**

　　完整的HTTP请求包含请求起始行、请求头部、请求主体三部分。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329150734545-432760222.jpg)

　　**六、浏览器接收响应**

　　服务器在收到浏览器发送的HTTP请求之后，会将收到的HTTP报文封装成HTTP的Request对象，并通过不同的Web服务器进行处理，处理完的结果以HTTP的Response对象返回，主要包括状态码，响应头，响应报文三个部分。

　　状态码主要包括以下部分

　　1xx：指示信息–表示请求已接收，继续处理。

　　2xx：成功–表示请求已被成功接收、理解、接受。

　　3xx：重定向–要完成请求必须进行更进一步的操作。

　　4xx：客户端错误–请求有语法错误或请求无法实现。

　　5xx：服务器端错误–服务器未能实现合法的请求。

　　响应头主要由Cache-Control、 Connection、Date、Pragma等组成。

　　响应体为服务器返回给浏览器的信息，主要由HTML，css，js，图片文件组成。

　　七、页面渲染

　　如果说响应的内容是HTML文档的话，就需要浏览器进行解析渲染呈现给用户。整个过程涉及两个方面：解析和渲染。在渲染页面之前，需要构建DOM树和CSSOM树。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329153247436-670728382.png)

　　在浏览器还没接收到完整的 HTML 文件时，它就开始渲染页面了，在遇到外部链入的脚本标签或样式标签或图片时，会再次发送 HTTP 请求重复上述的步骤。在收到 CSS 文件后会对已经渲染的页面重新渲染，加入它们应有的样式，图片文件加载完立刻显示在相应位置。在这一过程中可能会触发页面的重绘或重排。这里就涉及了两个重要概念：Reflow和Repaint。

　　Reflow，也称作Layout，中文叫回流，一般意味着元素的内容、结构、位置或尺寸发生了变化，需要重新计算样式和渲染树，这个过程称为Reflow。

　　Repaint，中文重绘，意味着元素发生的改变只是影响了元素的一些外观之类的时候（例如，背景色，边框颜色，文字颜色等），此时只需要应用新样式绘制这个元素就OK了，这个过程称为Repaint。

　　所以说Reflow的成本比Repaint的成本高得多的多。DOM树里的每个结点都会有reflow方法，一个结点的reflow很有可能导致子结点，甚至父点以及同级结点的reflow。

下面这些动作有很大可能会是成本比较高的：

增加、删除、修改DOM结点时，会导致Reflow或Repaint

移动DOM的位置，或是搞个动画的时候

内容发生变化

修改CSS样式的时候

Resize窗口的时候（移动端没有这个问题），或是滚动的时候

修改网页的默认字体时

　　基本上来说，reflow有如下的几个原因：

Initial，网页初始化的时候

Incremental，一些js在操作DOM树时

Resize，其些元件的尺寸变了

StyleChange，如果CSS的属性发生变化了

Dirty，几个Incremental的reflow发生在同一个frame的子树上

**八、关闭TCP连接或继续保持连接**
　　
  通过四次挥手关闭连接(FIN ACK, ACK, FIN ACK, ACK)。

　　![](https://images2015.cnblogs.com/blog/1034346/201703/1034346-20170329153945389-2019926409.png)

　　第一次挥手是浏览器发完数据后，发送FIN请求断开连接。

　　第二次挥手是服务器发送ACK表示同意，如果在这一次服务器也发送FIN请求断开连接似乎也没有不妥，但考虑到服务器可能还有数据要发送，所以服务器发送FIN应该放在第三次挥手中。

　　这样浏览器需要返回ACK表示同意，也就是第四次挥手。


　　至此从浏览器地址栏输入URL到页面呈现到你面前的整个过程就分析完了。



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

一、解析DOM树和CSSOM

1.HTML标签进行Dom树解析 
解析遇到link、script、img标签时，浏览器会向服务器发送请求资源。
script的加载或者执行都会阻塞html解析、其他下载线程以及渲染线程。
link加载完css后会解析为CSSOM(层叠样式表对象模型,一棵仅含有样式信息的树)。css的加载和解析不会阻塞html的解析，但会阻塞渲染。
img的加载不会阻塞html的解析，但img加载后并不渲染，它需要等待Render Tree生成完后才和Render Tree一起渲染出来。未下载完的图片需等下载完后才渲染。

2.CSS语法进行CSS树解析 
	CSS解释器将CSS进行解释然后解析
	划重点！！！Dom树和CSSOM两者不是解析完再渲染的，而是边解析边进行渲染的！
	DOM树和CSSOM渲染完成后合并生成Render树
	布局（reflow重排发生在这个阶段）
	布局（reflow重排发生在这个阶段）

这个阶段是通过递归调用进行布局的，引擎计算各元素的尺寸大小，进行布局树绘制

触发重排：

页面首次渲染
浏览器窗口大小变化
元素尺寸、位置、内容、字体大小发生变化
添加或删除可见的元素
激活伪类时
 
绘制（repainting重绘发生在这个阶段）
触发重绘：改变元素颜色、背景、visibility、outline等属性

重排一定会触发重绘，重绘不一定会触发重排 。

阻塞问题总结
阻塞发生的情况：
遇到script标签加载js的时候会加载js并且执行完毕才开始渲染
遇到alert会阻塞
css也会阻塞
css是由单独的下载线程异步下载的。

总结：
1.css加载不会阻塞DOM树的解析
2.css加载会阻塞DOM树（render树）的渲染
3.css加载会阻塞后面js语句的执行

为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以下几种方法:

使用CDN(因为CDN会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)
对css进行压缩(可以用很多打包工具，比如webpack,gulp等，也可以通过开启gzip压缩)
合理的使用缓存(设置cache-control,expires,以及E-tag都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决防范是在文件名字后面加一个版本号)
减少http请求数，将多个css文件合并，或者是干脆直接写成内联样式(内联样式的一个缺点就是不能缓存)

![](https://img2018.cnblogs.com/blog/1659314/201908/1659314-20190822111456778-550471352.jpg)

## JS更新DOM后页面及时渲染问题

深入研究浏览器内核可以发现，浏览器内核是多线程的，其中一个常驻线程叫javascript引擎线程，负责执行js代码，还有一个常驻线程叫GUI渲染线程，负责页面渲染，dom重画等操作。javascript引擎是基于事件驱动单线程执行的，js线程一直在等待着任务列表中的任务到来，而js线程与gui渲染线程是互斥的，当js线程执行时，渲染线程呈挂起状态，只有当js线程空闲时渲染线程才会执行。所以，我们可以理解为什么dom更新总是不能被立刻执行。就我们的代码来说，显示提示和隐藏提示的dom操作都被浏览器记下来了并放在gui渲染线程的任务队列中，但都没有立刻进行渲染，而是在当前函数完成后（js线程已处于空闲状态），进行最终的dom渲染，而我们的用户则基本感受不到这个过程，因为经过show和hide两个相反的操作，相当于dom完全没变。

![](https://img-blog.csdn.net/20131116163500734)

浏览器的行为虽然是合理的，但却给我们带来了麻烦，怎么才能强制浏览器执行dom更新的操作以满足我们的业务需要，给用户友好的提示呢，有两种方法：

采用alert语句进行提示，alert语句会block住js线程，将执行权让给gui渲染线程，执行alert之后浏览器会把这个语句之前的所有对dom的操作都进行体现。这个方法虽然简单有效，但不具有可操作性，首先alert是简单粗暴的一种提示方式，反倒降低了用户体验，其次不能适用在各种场景中，不可能在系统中无缘无故地弹出个alert框只是为了强制重画更新的dom。所以，该方法不值得推广。

采用setTimeout方法，这是普遍的解决方案。把计算逻辑和隐藏提示的方法放在setTimeout里可以解决这个问题，因为setTimeout启用了一个定时器，指定在经过一段时间后执行某段逻辑，从而使这段逻辑跳离了当前函数体，使当前函数可以快速地执行完，之后如果js引擎线程中没有排队的任务，则gui渲染线程得到执行，showTip相关的dom更新得到体现。当定时器到时后，js线程又得到了新的任务，从而使计算逻辑和隐藏提示的操作得到执行。

## HTTP 1.0 和 HTTP2.0 的区别

HTTP/2没有改变HTTP的基本语义和操作，各种操作方法（如GET/POST/HEAD等）、请求头和请求体机制都没有改变，不同的只是传输的方式改变了。HTTP/1.x 协议以换行符作为纯文本的分隔符，而 HTTP/2 将所有传输的信息分割为更小的消息和帧，并采用二进制格式对它们编码。

**HTTP/2的主要功能特性**

将HTTP协议中的纯文本传输修改成了二进制帧传输，分为头部帧和数据帧。
使用HPCAK对头部数据压缩，添加头部索引减少重复头部数据传输。
添加数据优先级，针对不同的数据源建立不同的优先级树，确保优先级高的数据不会被阻塞。
请求响应的复用，同一个数据流中可以同时以不同的顺序发送多个不同的帧，每个数据源只产生一个连接。
流控制，阻止发送方向接收方发送的大量数据，通过请求窗口限制请求速率。
服务端推送，打破严格的请求-响应机制，服务端也可以主动推送数据到客户端。

**HTTP/2数据传输的基本元素**

新的HTTP/2协议通过二进制帧来传输数据，改变了客户端与服务器之间交换数据的方式，主要涉及了三个概念：

帧：HTTP/2数据传输的基本单位，通过把原始的文本数据处理成二进制帧来发送。
消息：逻辑请求和响应构成的统一整体就是消息。
数据流：建立的TCP连接，承载发送一条和多条消息。
帧和消息

和HTTP/1一样，HTTP/2依旧还是保留了请求头、请求体以及响应体的部分。只不过在传输的时候被处理成了二进制的内容格式，同时把请求帧和响应帧区分开来了，两者可以单独发送。


## 手撕 简版 Promise 

```javascript
let myPromise = function (executor) {
    let self = this;//缓存一下this

    self.status = 'pending';// 状态管理 状态的变化只能由pending变为resolved或者rejected。一件事情不能既成功又失败。所以resolved和rejected不能相互转化。
    self.value = undefined;// 成功后的值 传给resolve
    self.reason = undefined;//失败原因 传给reject

    self.onResolvedCallbacks = [];// 存放then中成功的回调
    self.onRejectedCallbacks = []; // 存放then中失败的回调 
    // 这里说明一下，第三步使用定时器。执行完 new Promise 之后，会执行then方法，此时会把then中的方法缓存起来，并不执行：此时状态还是pending。等到定时器2秒之后，执行
    // resolve|reject 时，而是依次执行存放在数组中的方法。 参考发布订阅模式

    function resolve(value) {
        // pending => resolved
        if (self.status === 'pending') {
            self.value = value;
            self.status = 'resolved';
            // 依次执行缓存的成功的回调
            self.onResolvedCallbacks.forEach(fn => fn(self.value));
        }
    }

    function reject(reason) {
        // pending => rejected
        if (self.status === 'pending') {
            self.value = value;
            self.status = 'rejected';
            // 依次执行缓存的失败的回调
            self.onRejectedCallbacks.forEach(fn => fn(self.reason));
        }
    }

    try {
        //new Promise 时 executor执行
        executor(resolve, reject);
    } catch (error) {
        reject(error);// 当executor中执行有异常时，直接执行reject
    }
}

// 每个Promise实例上都有then方法
Promise.prototype.then = function (onFulfilled, onRejected) {
    let self = this;

    // 执行了 resolve
    if (self.status === 'resolved') {
        // 执行成功的回调
        onFulfilled(self.value);
    }

    // 执行了 reject
    if (self.status === 'rejected') {
        // 执行失败的回调
        onRejected(self.reason);
    }

    // new Promise中可以支持异步行为 当既不执行resolve又不执行reject时 状态是默认的等待态pending
    if (self.status === 'pending') {
        // 缓存成功的回调
        self.onResolvedCallbacks.push(onFulfilled);
        // 缓存失败的回调
        self.onRejectedCallbacks.push(onRejected);
    }
};

```
## 前端技术专家

![](https://static001.geekbang.org/resource/image/e0/92/e0c654fa7cf5f63cdcca1b6c51008992.jpeg)

对标阿里 P7 级别。到了这个级别，我们从图上可以看到，要求又不一样了，比如组件变成了组件体系，工具变成了工具链和持续集成体系，性能优化变成了性能体系。这些东西变得不仅仅是称呼，还有工作的内容，这个级别跟资深工程师的主要区别是，从解决单点问题变成系统性方法，从服务自己变成服务团队，从一次性发挥变成持续性输出。比如，资深工程师可能做一些组件，然后在项目里面用，自己的代码可维护性提升了，复用也做得更好了。但是前端专家要考虑制定组件规范推广到团队，还要做培训，考虑组件如何开发、管理和下线。资深工程师做性能，把自己的页面优化好了就可以了，但是前端专家就需要考虑采集数据、做报表和监控、总结 checklist、跟工具结合、定性能指标等等。由于这个级别对架构能力、工程和软技能要求很高，所以算是比较难以跨越的。
