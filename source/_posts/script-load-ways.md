---
title: 加载JS脚本的三种方法
date: 2022-03-31 20:17:31
tags: [Front-end, Javascript, Html-event]
---

> 总结一下使用三种不同的方式加载JS脚本，对DomContentLoaded事件的影响


在本文中，我们将总结一下使用三种不同的方式加载JS脚本，对DomContentLoaded事件的影响。DomContentLoaded事件是指浏览器解析完HTML文档，构建了DOM树后触发的事件，它通常用于执行一些依赖于DOM元素的操作。加载JS脚本有三种方式：默认加载、defer和async，它们分别有不同的特点和影响。

## 默认加载
> 默认加载是最常见的一种方式，就是直接在HTML文档中使用<script src="test.js"></script>标签引入外部脚本。这种方式的特点是：

- 脚本会按照声明的顺序依次执行。
- 脚本会阻塞HTML文档的解析和DOM树的构建，直到脚本执行完毕。
- 脚本会阻塞后面的脚本和样式表的加载和渲染。
- 脚本会延迟DomContentLoaded事件的触发，直到所有的脚本执行完毕。

这种方式的优点是简单易用，保证了脚本之间的依赖关系。缺点是会影响页面的性能和用户体验，因为页面会出现白屏或者卡顿的现象。

## defer
> defer是一个HTML5新增的属性，可以用于<script>标签，表示延迟执行脚本。这种方式的特点是：

- 脚本会按照声明的顺序依次执行。
- 脚本不会阻塞HTML文档的解析和DOM树的构建，而是在后台异步下载。
- 脚本会在DomContentLoaded事件之前执行，但不会阻塞该事件的触发。
- 脚本不会阻塞后面的脚本和样式表的加载和渲染。

这种方式的优点是可以提高页面的性能和用户体验，因为页面不会出现白屏或者卡顿的现象。缺点是不支持老旧的浏览器。

## async
> async也是一个HTML5新增的属性，可以用于<script>标签，表示异步执行脚本。这种方式的特点是：

- 脚本不会按照声明的顺序执行，而是哪个脚本先下载完就先执行。
- 脚本不会阻塞HTML文档的解析和DOM树的构建，而是在后台异步下载。
- 脚本不会等待DomContentLoaded事件，而是一旦下载完就立即执行，并可能阻塞该事件的触发。
- 脚本不会阻塞后面的脚本和样式表的加载和渲染。

这种方式的优点是可以最大程度地利用网络资源，提高页面加载速度。缺点是无法保证脚本之间的依赖关系，可能导致错误或者意外结果。

## 总结
使用三种不同的方式加载JS脚本，对DomContentLoaded事件有不同程度的影响。默认加载会延迟该事件的触发，defer会在该事件之前执行，async则可能阻塞该事件的触发。根据不同场景和需求，我们可以选择合适的方式来优化页面性能和用户体验。
