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

![](https://img2018.cnblogs.com/blog/1659314/201908/1659314-20190822111456778-550471352.jpg)

**一、解析DOM树和CSSOM
**

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

## 前端技术专家

![](https://static001.geekbang.org/resource/image/e0/92/e0c654fa7cf5f63cdcca1b6c51008992.jpeg)

对标阿里 P7 级别。到了这个级别，我们从图上可以看到，要求又不一样了，比如组件变成了组件体系，工具变成了工具链和持续集成体系，性能优化变成了性能体系。这些东西变得不仅仅是称呼，还有工作的内容，这个级别跟资深工程师的主要区别是，从解决单点问题变成系统性方法，从服务自己变成服务团队，从一次性发挥变成持续性输出。比如，资深工程师可能做一些组件，然后在项目里面用，自己的代码可维护性提升了，复用也做得更好了。但是前端专家要考虑制定组件规范推广到团队，还要做培训，考虑组件如何开发、管理和下线。资深工程师做性能，把自己的页面优化好了就可以了，但是前端专家就需要考虑采集数据、做报表和监控、总结 checklist、跟工具结合、定性能指标等等。由于这个级别对架构能力、工程和软技能要求很高，所以算是比较难以跨越的。
