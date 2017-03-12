### javascript定义
JavaScript，一种高级编程语言，通过解释执行，是一门动态类型，面向对象（基于原型）的直译语言。 它已经由ECMA（欧洲电脑制造商协会）通过ECMAScript实现语言的标准化。

//代码世界有两种方式来翻译机器语言：解释器和编译器。<br/>
//如果通过解释器，翻译是一行行的边解释边执行。<br/>
//编译器是把源代码整个编译成目标代码，执行时不再需要编译器，直接在支持目标代码的平台上运行。

所以，v8引擎是一个解释javascript的解释器。

### node定义
Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.<br/>
Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.<br/>
Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.<br/>
Node.js®是一个基于Chrome V8 引擎的 JavaScript 运行时。<br/>
Node.js 使用高效、轻量级的事件驱动、非阻塞 I/O 模型。<br/>
Node.js 之生态系统是目前最大的开源包管理系统。<br/>

以上是node的官方文档定义，其中第一段个是说，node.js是javascript的runtime平台（解释器）。<br/>
第二句是说，事件驱动，非阻塞I/O模型，之前一直迷思，model啥意思
难道不是mvvc之类的m的数据层吗？百度给出了另外一层意思在```“三层架构”中，为了面向对象编程，将各层传递的数据封装成实体类，便于数据传递和提高可读性。```这一句是从整个node的架构层面来说，也就是说javscript引擎在哪里和开始运行的呢。也就是说v8引擎它是如何被驱动的（event-driven）靠事件来驱动。no-blocking是说，在没有事件A驱动v8引擎回调事件A的回调函数时，v8引擎可以去run函数B。


### 浏览器
javascript引擎是单线程运作javascript程序。对以上没有任何的疑问，疑问是javascript中如何实现异步函数的？<br/>

>同步：在调用函数后，一直等待，直到返回有结果才能执行下面的操作。<br/>
>异步：异步就是调用函数后，并没有直接拿到结果。而是进行了其他操作（介入了其他任务），最终拿到了成果。

之前的迷思是，在js引擎运行时，那么这些异步函数的事件在哪里？<br/>
别忘记啊，浏览器是很大的，它不仅仅只有javascript引擎线程，它还有,界面渲染线程,浏览器事件触发线程,http请求线程。毕竟它不是专业去解释javascript，毕竟http， css，html也需要他们请求，渲染等...<br/>
![cmd-markdown-logo](http://p1.bqimg.com/567571/e5a6efb255e8540a.jpg)<br/>
以上可以看到，javascript是单线程运作的，在javascript中有非常多的任务列队。这些任务列队可以是javascript解释器对代码，变量，作用域，函数等的形成的任务列队。这些任务列队被javascript解释后，不一定会产生事件。但是，一旦产生事件，就会被放入到事件队列中被处理。当然不同的事件有不同的线程在处理。一旦该事件被handler了，就会被主线程event loop到（也就是主线程会不断的访问）。这个时候，就会把这个handler相应的callback函数加到javascript的任务列队中执行。所谓的事件驱动，就是将一切抽象为事件。IO操作完成是一个事件，用户点击一次鼠标是事件，Ajax完成了是一个事件，一个图片加载完成是一个事件

-----
总结：开始学习javascript，就是数据类型，表达式，面向对象开始学习。也一直以为这些代码就是在浏览器之中run。却不知道浏览器内核是有多个线程操作的，我们所写的javascript code 是js引擎的程序。但是这个引擎会和多条线程合作达到我们想要的结果。

-----
学习资料： <br/>
[朴灵对阮一峰大大的注解](http://blog.csdn.net/lin_credible/article/details/40143961)  <br/>
[输入理解javascript时间机制](http://www.laruence.com/2009/09/23/1089.html) <br/>
还有知乎的对同步异步阻塞等的回答，还有其中的node运行机制等，等以后code经验值上去了再说吧
