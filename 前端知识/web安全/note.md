
XSS 和 CSRF
https://juejin.im/post/5cef3a3bf265da1b8d160052

XSS （跨站脚本攻击）
    攻击者通过修改客户端注入恶意脚本 获取一些用户的cookie session 隐私数据发送给攻击者
    xss攻击可分为三类 反射型 存储型 基于DOM型
    XSS 主要是通过输入框等形式提交 js 脚本，最终在页面上被执行。
防范
    XSS 攻击的防范
现在主流的浏览器内置了防范 XSS 的措施，例如 CSP。但对于开发者来说，也应该寻找可靠的解决方案来防止 XSS 攻击。
HttpOnly 防止劫取 Cookie
HttpOnly 最早由微软提出，至今已经成为一个标准。浏览器将禁止页面的 Javascript 访问带有 HttpOnly 属性的 Cookie。
上文有说到，攻击者可以通过注入恶意脚本获取用户的 Cookie 信息。通常 Cookie 中都包含了用户的登录凭证信息，攻击者在获取到 Cookie 之后，则可以发起 Cookie 劫持攻击。所以，严格来说，HttpOnly 并非阻止 XSS 攻击，而是能阻止 XSS 攻击后的 Cookie 劫持攻击。
输入检查
不要相信用户的任何输入。  对于用户的任何输入要进行检查、过滤和转义。建立可信任的字符和 HTML 标签白名单，对于不在白名单之列的字符或者标签进行过滤或编码。
在 XSS 防御中，输入检查一般是检查用户输入的数据中是否包含 <，> 等特殊字符，如果存在，则对特殊字符进行过滤或编码，这种方式也称为 XSS Filter。
而在一些前端框架中，都会有一份 decodingMap， 用于对用户输入所包含的特殊字符或标签进行编码或过滤，如 <，>，script，防止 XSS 攻击：


CSRF (跨站请求伪造)Cross Site Request Forgery
   是一种劫持受信任用户向服务器发送非预期请求的攻击方式。