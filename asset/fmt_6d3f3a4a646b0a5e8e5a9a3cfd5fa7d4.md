
```java
import java.net.Socket;
import java.net.URL;
import java.net.MalformedURLException;
```

![](img/fbfff30e42d507bc7531108a281d6cf4_1144_0.png)

# 在 Linux 下编程

## 第四部分

```java
import java.io.PrintWriter;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.InputStream;
```

![](img/fbfff30e42d507bc7531108a281d6cf4_1144_0.png)

# 在 Linux 下编程

## 第四部分

```java
// 这是一个使用 Java 编写的简单 Web 客户端，它通过 socket 连接到 80 端口的 Web 服务器，
// 80 端口是服务器监听请求端口。
import java.io.
```

```java
public class WebSocket {

    private PrintWriter writer;

    private BufferedReader reader;

    private Socket sock;

}
```

```java
public static void main(String[] args) {

    // 通过命令行参数创建 URL 对象

    try {

        new WebSocket(new URL(args[0]));

    } catch (MalformedURLException mfu) {

        System.err.println("无效 URL 格式");

        System.err.println("用法: WebSocket [url]");

    }

}
```

```java
public WebSocket(URL webadd) {

    try {

        // 在 80 端口打开一个新的 socket 连接

        sock = new Socket(webadd.getHost(), 80);

        // 创建 Reader 和 Writer

        writer = new PrintWriter(sock.getOutputStream());

        reader = new BufferedReader(new InputStreamReader(sock.getInputStream()));

        // 通知 Web 服务器你想要的文件

        sock.println("GET " + webadd.getFile());

        writer.flush();

        // 将服务器返回的 HTML 打印到控制台

        for (String line = reader.readLine(); line != null; line = reader.readLine()) {

            System.out.println(line);

        }

    } catch (IOException ioe) {

        System.err.println("连接主机 " + webadd.getHost() + " 时出错");

    }

}
```

## Java 编程

### 第 35 章

你已经看到如何使用 applet 在 Web 浏览器中使用 Java 进行编程。由于带宽限制，applet 可能会臃肿且加载缓慢。在 Web 上动态加载 HTML 可能更符合你的需求。自从 Web 存在以来，实现此点的常用方法是使用 Perl 或 C/C++ CGI。

你也可以使用 servlet。Java servlet 提供了一种扩展 Web 服务器功能的机制，就像 CGI 脚本一样。此外，它们还提供了 Java 提供的所有优势，如可性和多线程。

`servlet` 模型与 `applet` 模型相似。有一个 servlet 引擎作为 Web 服务器的一部分运行。该引擎可以嵌入你的 Web 服务器中，也可以作为应用程序服务器作为插件出售。应用程序服务器提供了 servlet 引擎功能以及帮助你构建动态网站的功能。一些流行的插件 引擎或应用程序服务器如下：

- Java-Apache 项目的 JServ 模块。这是 Apache 为流行的 Web 服务器开发的开源 servlet 引擎。http://java.apache.org。
- IBM 的 WebSphere 服务器。这是 IBM 支持流行的 Web 服务器的应用程序服务器。http://www.software.ibm.com/websphere。
- BEA Weblogic 应用服务器。这是 WebLogic 用于 Java servlet 的应用程序服务器。http://www.beasys.com/linux/
- Live Software 的 JRun Servlet 引擎。JRun 是随 Red Hat 6.0 发行版提供的 Java servlet 引擎。http://www.jrun.com。

> 注意
> Red Hat 6.0 发行版在 Linux 应用光盘中包含了 Live Software JRun 的完整版本。

Servlet 引擎加载扩展 `HttpServlet` 基类的 servlet。该基类位于 `java.servlet` 包中。当 Web 页面调用 servlet 时，请求会被格式化为 `HttpServletRequest`，其中包含了请求的参数和其他信息。随后 Servlet 引擎加载并调用 `doPost` 或 `doGet` 方法。Hello There servlet 演示了一个简单的 Java servlet：

```java
import javax.servlet.*;
import javax.servlet.http.*;
```

```java
public class HelloThereServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res )
            throws ServletException, IOException {
        // 获取传入的参数
        String name = req.getParameter("name")[0];
        PrintWriter servant = res.getWriter();
        // 设置内容类型
        res.setContentType("text/html");
        servlet.println("<html>");
        servlet.println("<HEAD>");
        servlet.println("<TITLE>Hello There Servlet</TITLE>");
        servlet.println("<body>");
        servlet.println("Hello There, " + name + "");
        servlet.println("</body>");
        servlet.println("</html>");
    }
}
```

以下是调用该 servlet 的 HTML 代码：

```html
<HTML>
<HEAD>
<TITLE>Hello There Servlet</TITLE>
</HEAD>
<body
<FORM METHOD=GET ACTION="/servlet/HelloThereServlet">
What is your name? <INPUT TYPE=TEXT NAME='name' SIZE=25>
<INPUT TYPE=SUBMIT VALUE="Say Hello There!">
</FORM>
</body>
</HTML>
```
