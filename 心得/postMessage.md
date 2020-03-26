# [postMessage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage)

window.postMessage() 方法可以安全地实现跨源通信。

1、页面内嵌套情况：子窗口发送消息给父窗口。
2、一个页面打开另一个页面情况：被打开页面发送消息给上一个页面。

## window.parent与window.opener区别

window.parent 是嵌套页面的父页面
window.opener引用的是window.open打开的页面的父页面。

## 使用postMessage

在情况2中，当需要传递消息给父页面时，使用

    window.opener.postMessage(message, [targetOrigin]);

父页面监听

    window.addEventListener("message", receiveMessage, false);

receiveMessage是一个方法，接收一个参数e，其中e.data是子页面传过来的数据。更多属性点击[详情](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage#The_dispatched_event)