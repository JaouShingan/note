# Ajax/Fetch

1.  [Ajax](#ajax)
2.  [Fetch](#fetch)

## Ajax

使用XMLHttpRequest (XHR)对象可以与服务器交互。您可以从URL获取数据，而无需让整个的页面刷新。这使得Web页面可以只更新页面的局部，而不影响用户的操作。XMLHttpRequest在 Ajax 编程中被大量使用。

1、创建 XMLHttpRequest 对象

```javascript
var xhr = new XMLHttpRequest();
```

2、向服务器发送请求

使用 XMLHttpRequest 对象的 open() 和 send() 方法

| 方法                           | 描述                                                                                                                                                |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| open(method,url,async)         | 规定请求的类型、URL 以及是否异步处理请求。<br>method:请求的类型: GET 或 POST 等;<br>url:文件在服务器上的位置;<br>async:true（异步）或 false（同步） |
| send(string)                   | 将请求发送到服务器。<br>string:仅用于 POST 请求                                                                                                     |
| setRequestHeader(header,value) | 向请求添加 HTTP 头。<br>header: 规定头的名称<br>value: 规定头的值                                                                                   |

3、响应

使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性获得来自服务器的响应

| 属性         | 描述                       |
| ------------ | -------------------------- |
| responseText | 获得字符串形式的响应数据。 |
| responseXML  | 获得 XML 形式的响应数据。  |

4、onreadystatechange 事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性               | 描述                                                               |
| ------------------ | ------------------------------------------------------------------ |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         |存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。<br>0: 请求未初始化<br>1: 服务器连接已建立<br>2: 请求已接收<br>3: 请求处理中<br>4: 请求已完成，且响应已就绪<br>
status| 200: "OK"<br>404: 未找到页面


#### 引用
> [MDN XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)
> [菜鸟教程](https://www.runoob.com/ajax/ajax-tutorial.html)

## Fetch

1

1

1
1

1

1

1

1

1

1

1
1
1
1
1
1
1
1
1
1
1
1
1
1
1
1
