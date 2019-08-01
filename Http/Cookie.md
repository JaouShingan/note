# Cookie

HTTP Cookie（也叫 Web Cookie 或浏览器 Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。

Cookie 主要用于以下三个方面：

1、会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
2、个性化设置（如用户自定义设置、主题等）
3、浏览器行为跟踪（如跟踪分析用户行为等）

### 会话期 Cookie

会话期 Cookie 是最简单的 Cookie：浏览器关闭之后它会被自动删除，也就是说它仅在会话期内有效。会话期 Cookie 不需要指定过期时间（Expires）或者有效期（Max-Age）。需要注意的是，有些浏览器提供了会话恢复功能，这种情况下即使关闭了浏览器，会话期 Cookie 也会被保留下来，就好像浏览器从来没有关闭一样。

### 持久性 Cookie

和关闭浏览器便失效的会话期 Cookie 不同，持久性 Cookie 可以指定一个特定的过期时间（Expires）或有效期（Max-Age）。

```
    // eg:
    Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

### JavaScript 通过 Document.cookies 访问 Cookie

通过 Document.cookie 属性可创建新的 Cookie，也可通过该属性访问非 HttpOnly 标记的 Cookie。

```javascript
document.cookie = 'yummy_cookie=choco';
document.cookie = 'tasty_cookie=strawberry';
console.log(document.cookie);
// logs "yummy_cookie=choco; tasty_cookie=strawberry"
```
