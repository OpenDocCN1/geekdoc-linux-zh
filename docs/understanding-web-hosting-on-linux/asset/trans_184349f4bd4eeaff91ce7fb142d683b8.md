

# 第106 页 第7 章

![](img/069cd06404ac5e90171e6d857bf3ad28_121_0.png)

## Tomcat 应用配置

将 Servlet 及其 PanelServlet 前端部署到 Tomcat 的简单方法是将编译后的 Java servlet `PanelServlet.class` 复制到 /opt/jakarta-tomcat/webapps/ROOT/WEB-INF/classes/。然后将 `Panel.html` 复制到 /opt/jakarta-tomcat/webapps/ROOT/。启动 Tomcat 服务器后，你应该可以通过 Netscape 使用以下 URL 请求调用 PanelServlet：

```
http://127.0.0.1:8080/Panel.html
```

如果 PanelServlet 应用是生产级的，你会在 Tomcat 的 web 目录下创建一个特定于应用的目录，并包含由 Sun Servlet 2.2 API 标准化的子目录。位于 /usr/local/tomcat/webapps/examples/ 的名为 "examples" 的 Tomcat Web 应用程序遵循了这一标准。

注意，为了能够编译 PanelServlet.java，你需要将 Tomcat 的 `servlet.jar` 文件添加到你的 Java CLSPATH 环境变量中，并在包含 PanelServlet.java 源文件的当前目录下编译 PanelServlet.java：

```
CLASSP=$CLASSP:/opt/jakarta-tomcat/lib/servlet.jar
javac PanelServlet.java
```

## JavaServer Pages (Java 器页)

在 Sun Microsystems 引入 Servlet API 后约 12 个月期间，servlet 被广泛采用为基于主机的互联网应用程序的标准。Java servlet 本质是嵌入了 HTML 的 Java。而 JavaServer Pages (JSP) 本质是嵌入了 Java 的 HTML。

你的 JSP 文件与 HTML 文件位于相同的目录中。与 HTML 一样，它们由用户在 Web 浏览器调用。唯一区别是 JSP 文件的扩展名是 .jsp 而不是 .html。当 Web 服务器看到 .jsp 时，它会将请求传递给 Web 应用服务器（如 IBM 的 WebSphere 或 Apache 的 Tomcat）。

学习 JSP 如何工作的最佳方法是遵循一个简单的示例。下面这一行文本包含了来自 Minimal.html 文件的完整 HTML 语法：

```html
<html><body>
Minimal HTML file
</body></html>
```

如果你将此 Web 文件放置在 Tomcat 的 ROOT 部署目录，它会处理 http://usr/local/tomcat/webapps/ROOT/ 的请求，并在 Web 浏览器通过 http://127.0.0.1:8080/Minimal.html 请求它，Tomcat 只会将该 HTML 文本文件发送到浏览器。然而，如果你将 Minimal.html 重命名为 Minimal.jsp，处理过程将完全不同。

当你请求 Minimal.jsp 时，Web 服务器看到 .jsp 扩展名，创建一个包含 JSP 完整 HTML 和 Java 语法的 Java 源文件，并将其编译为 Java servlet。例如，当我在 Netscape 浏览器中输入 http://127.0.0.1:8080/Minimal.jsp 时，Tomcat 创建了如图 7.10 所示的 Java servlet 源文件，将其编译为名为 Minimal_jsp_1.class 的 Java 类，然后执行它。该 servlet 直接将带有字符串 "Minimal HTML file" 的动态生成的 HTML 文件传回我的 Web 浏览器。

```java
public class _0002fMinimal_0002jspMinimal_jsp_0 extends JspBase {
    static { }
    public _0002fMinimal_0002jspMinimal_jsp_0() { }
    private static boolean jsp_init = false;
    public final void jsp_init() throws JasperException {
}

    public void jspService(HttpServletRequest request, HttpServletResponse response)
        throws IOException, ServletException {
        JspFactory _jspFactory_context = null;
        PageContext pageContext = null;
        HttpSession session = null;
        ServletContext application = null;
        ServletConfig config = null;
        JspWriter out = null;
        Object page = this;
        String _value = null;
        try {
            if (_jsp_init == false) {
                jsp_init();
                jsp_init = true;
            }
            _jspFactory = JspFactory.getDefaultFactory();
            response.setContentType("text/html;charset=8859-1", true);
            pageContext = _jspFactory.getPageContext(this, request, response, application);
            application = pageContext.getServletContext();
            config = pageContext.getServletConfig();
            session = pageContext.getSession();
            out = pageContext.getWriter();
            // // begin(file="minimal.jsp";from=(0,0);to=(1,0))
            out.write("<html><body>Minimal HTML file</body></html>\r\n");
        } catch (Exception ex) {
            if (out != null && out.getBufferSize() != 0) {
                out.clearBuffer();
            }
            pageContext.handleException(ex);
        } finally {
            out.flush();
            _jspFactory.releasePageContext(pageContext);
        }
    }
}
```

图 7.10：Web 应用服务器自动生成的 servlet 代码不应修改。

显然，这个编译过程需要相当的时间（可能几秒钟）。然而，当客户端下次请求同一个一个 JSP 文件时，服务器将提供之前创建的 servlet。同时，如果 Web 开发者修改了 JSP 文件，服务器会注意到变化，重新编译并提供新的 servlet。

要理解这项技术，你需要查看表 7.5 所示的 JSP 语法类型。

### 表 7.5 JSP 语法类型

| 类型 | 示例 |
| :--- | :--- |
| 表达式 (Expression) | `<%= new Date() %>` |
| 脚本段 (Scriptlet) | `<% for (int idx = 0; idx < 5; idx++) { ... %>` |
| 指令 (Directive) | `<%@ page import="java.util.*" %>` |
| 声明 (Declaration) | `<%! Connection con = null; %>` |
| 注释 (Comment) | `<% comment --%>`

## 表达式 (Expressions)

JSP 表达式用于将值输出到 HTML 中。下面的示例显示：

```html
<html><body>
今天的日期 <%= new Date() %>
</body></html>
```

## 脚本段 (Scriptlets)

当 <% 和 %> 之间包含多行 Java 代码时，该部分被称为脚本段。下面的示例显示了一个 Java for 循环：

```html
<html><body>
<% for (int idx = 0; idx < 3; idx++) { %>
当前索引为 <%=idx%> <br>
} %>
</body></html>
```

## 请求与响应 (Request and Response)

HttpServletRequest 提供了对所有信息（如 Cookie、标头和表单参数）的访问。下面的示例使用了：

```html
<html><body>
<%= request.getHeader("User-Agent") %>
</body></html>
```

## 指令、声明与注释 (Directives, Declarations, and Comments)

JSP 指令通过符号 <%@ 识别。指令通常用于指定要在 JSP 中使用的 Java 类包。

JSP 声明通过感叹号 <%! 识别。声明用于描述 JSP 文件中任何 Java 代码中使用的对象变量。

JSP 注释通过双连字符（%-- 和 --%）识别。当你不希望注释代码包含在发送到浏览器的 HTML 中时，请使用注释代码。

