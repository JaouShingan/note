# Event

事件的三个阶段: 捕获阶段（Capture Phase）、目标阶段（Target Phase）、冒泡阶段（Bubbling Phase）
[阶段图](https://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture)
[Dom 事件](https://www.cnblogs.com/LIUYANZUO/p/5332583.html)
[MDN Event](https://developer.mozilla.org/zh-CN/docs/Web/API/Event)

currentTarget: 当前注册事件的对象的引用（注册事件的对象）
target：对事件起源目标的引用（触发事件的对象）

事件注册方式：
1、addEventListener 方式
2、HTML 属性方式(eg: click="a()")
3、dom 元素属性方式(eg: xx.onclick)

停止事件冒泡
event.stopPropagation

取消事件
event.preventDefault
