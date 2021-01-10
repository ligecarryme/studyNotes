### JavaScript 实现

完整的JavaScript实现包含以下几个部分：核心（ECMAScript）、文档对象模型（DOM）、浏览器对象模型（BOM）。

ECMAScript 描述了语言的语法、类型、语句、关键字、保留字、操作符、全局对象。

DOM 是一个应用编程接口（API），用于在HTML中使用扩展的XML。

BOM 用于支持访问和操作浏览器的窗口。

### HTML中的JavaScript

`<scirpt>` 元素，浏览器在解析这个资源时，会向src 属性指定的路径发送一个GET 请求，以取得相应资源。

过去，所有`<script>`元素都被放在页面的`<head>`标签内，这种做法的主要目的是把外部的CSS 和JavaScript 文件都集中放到一起。不过，把所有JavaScript文件都放在`<head>`里，也就意味着必须把所有JavaScript 代码都下载、解析和解释完成后，才能开始渲染页面（页面在浏览器解析到`<body>`的起始标签时开始渲染）。对于需要很多JavaScript 的页面，这会导致页面渲染的明显延迟，在此期间浏览器窗口完全空白。为解决这个问题，现代Web应用程序通常将所有JavaScript 引用放在`<body>`元素中的页面内容后面，这样一来，页面会在处理JavaScript 代码之前完全渲染页面。

`<noscript>` 元素对于早期浏览器不支持 JavaScript 的问题，需要一个页面优雅降级的处理方案。

`<noscript>` 元素可以包含任何可以出现在`<body>`中的HTML 元素，`<script>`除外。在下列两种情况下，浏览器将显示包含在`<noscript>`中的内容：1、浏览器不支持脚本；2、浏览器对脚本的支持被关闭。

任何一个条件被满足，包含在`<noscript>`中的内容就会被渲染。否则，浏览器不会渲染`<noscript>`中的内容。