# cookie

## cookie 的生成

通常是通过服务端生成

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class SetCookieServlet extends HttpServlet {
  public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException {
    // 创建一个Cookie对象
    Cookie cookie = new Cookie("username", "john");

    // 设置Cookie属性
    cookie.setPath("/"); //path
    cookie.setDomain("example.com"); //domain
    cookie.setMaxAge(60*60*24); // 有效期为1天
    cookie.setSecure(true); // 仅在HTTPS连接时发送
    cookie.setHttpOnly(true); // 仅在HTTP请求中发送，防止JavaScript等脚本访问
    cookie.setSameSite("Strict"); // SameSite策略设置为Strict

    // 发送Cookie到Web浏览器
    response.addCookie(cookie);

    // 输出响应结果
    response.setContentType("text/html");
    PrintWriter out = response.getWriter();
    out.println("<html><body>");
    out.println("<h1>Cookie设置成功</h1>");
    out.println("</body></html>");
  }
}

```

请求的 response 头就会包含 Set-Cookie 字段

## 作用

session manage、 个性化、 追踪

## 各属性的简单作用

### httpOnly

仅在请求时携带 cookie，可以防止 cookie 被 js 获取

```js
//js获取cookie

let cookieList = document.cookie.split("; ");
for (let i = 0; i < cookieList.length; i++) {
  let cookieItem = cookieList[i].split("=");
  if (cookieItem[0] === "myCookie") {
    console.log(cookieItem[0]); // 输出"myCookie"
    break;
  }
}

//覆盖cookie

document.cookie = "myCookie=myNewValue; path=/";
```

### Secure

仅在使用时 HTTPS 安全协议时，发送 cookie
是否对 cookie 进行加密

Secure 和 Http-Only 并无依赖关系，可以单独开启或关闭

### domian

设置 cookie 在哪个域，当该域发送请求时，携带 cookie

第一方 cookie: cookie 设置的域名与当前网页的域名相同, 否则是第三方的

是否是第一方是相对的，取决于用户所在的网页

### path

请求 path 限制

### Same-Site

是否允许跨站请求时携带,值有 Strict、Lax、None

默认为 Lax

当我们要进行跨站请求时，需要设置 Same-Site 为 None, 同时 Secure 要设置为 true

### iframe 设置 cookie

iframe 设置 cookie 时

第三方域名：
设置 cookie 时,需要设置 Same-Site 属性为 None，否则 Set-cookie warning，写入失败
同时，需要设置 Secure 为 true
