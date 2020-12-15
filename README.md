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
## 事件委托
## setTimeout、Promise、Async、Await异步原理和执行顺序
## ES6的新增功能
## 从输入url到页面加载发生了什么

## 浏览器渲染过程与性能优化
https://juejin.cn/post/6844904040346681358#heading-27
