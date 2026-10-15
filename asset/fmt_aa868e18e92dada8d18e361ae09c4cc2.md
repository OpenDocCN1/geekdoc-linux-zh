
# 示例-6 JSP 中的数据库连接、查询和显示标签

```jsp
<%-- Connect to the database --%>
<% com.ibm.beans.DBConnection dsSpec = null; %>
<%
if (dsSpec == null) {
  <%--cust_info:config.getInitManagerSpec id="databaseConnection" scope="page"
      userId="<%=config.initParameter("username")%>"
      password="<%=config.initParameter("password")%>"
      driver="<%=config.initParameter("driverName")%>"
      url="<%=config.initParameter("url")%>""
  -->
  dsSpec = databaseConnection;
}
%>
```

```jsp
<%--Execute the query--%>
<dab_cust_info:select id="select_cust_info" scope="request" connectionSpec="<%=dsSpec%>">
<dab_cust_info:sql>
SELECT
ITSO.CUSTOMER.FIRSTNAME,
ITSO.CUSTOMER.LASTNAME,
....
</dab_cust_info:select>
```

```html
<table>
  <tr>
    <th>Name</th>
    <th>Address</th>
    <th>Checking Account</th>
    <th>Savings Account</th>
  </tr>
  <dab_cust_info:repeat id="select_cust_info" scope="request">
    <tr>
      <td><dab_cust_info:column name="FIRSTNAME"/></td>
      <td><dab_cust_info:column name="LASTNAME"/></td>
      <td><dab_cust_info:column name="CHECKING"/></td>
      <td><dab_cust_info:column name="SAVINGS"/></td>
    </tr>
  </dab_cust_info:repeat>
</table>
```

在上面的代码中，我们使用 `request.getParameter` 获取通常是用户响应的参数。通过使用 session Attribute，我们将其赋值给一个变量，稍后通过 `session.getAttribute` 将其设置为字符串变量。该字符串变量可以在 JSP 内部进一步处理。你也可以在 `page` 指令中将会话属性定义为 `true` 或 `false`。默认情况下，会话值为 `true`。等等，表格的文本非常乱码。让我根据提供的上下文重构表格结构。

## 4.4 Servlet

在本节中，我们将使用 ITSOBankWeb servlet `controller.java` 来解释 Servlet 的基础知识，以及 `web.xml`（Web 描述文件）。

Servlet 是可以跨平台迁移的 Java 程序。这些是运行在中间层的程序，作为来自 Web 浏览器、HTTP 客户端和数据库请求的控制器。Servlet 的主要组件是 `init`、`doGet`、`doPost`、`performServices` 和 `dispatch` 方法。以下是每个方法的简要描述。

### init 方法

该方法用于加载初始变量。在这种情况下，值存在部署描述符（Deployment Descriptor）或 servlet 标签中。你也可以指定初始化 Servlet 所需的其他变量。

#### 示例 4-7 Servlet 中的 init 方法

```java
public void init(ServletConfig config) throws ServletException {
  super.init(config);
}
```

### doGet 方法

当用户提交 HTML 表单时，它会指定方法是 HTTP get 还是 post。如果用户使用该方法，则应该使用 `doGet` 方法。`doGet` 两个参数：`HttpServletRequest` 和 `HttpServletResponse`，前者处理输入数据，后者处理输出数据。在我们的示例中，我们用 `performTask` 方法重写了该方法。

#### 示例 4-8 Servlet 中的 doGet 方法

```java
public void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  performTask(req, resp);
}
```

### doPost 方法

如果用户使用该方法，`doPost` 方法接收两个参数：`HttpServletRequest` 和 `HttpServletResponse`，前者处理输入数据，后者处理输出数据。这与其对应的 `doGet` 方法完全相同。在我们的示例中，我们用 `performTask` 方法重写了该方法。

#### 示例 4-9 Servlet 中的 doPost 方法

```java
public void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  performTask(req, resp);
}
```

## performServices 方法

`performServices` 方法用于执行用户身份验证。在我们的示例中，我们使用 JSP 来执行此操作。Servlet 用作网关，将用户的请求和响应从前端传递到后端，最后返回给用户。

#### 示例 4-10 servlet 中的 performServices 方法

```java
public void performServices(HttpServletRequest request,
    HttpServletResponse response) {

}
```

## performTask 方法

在我们的示例中，`performTask` 方法处理输入变量，但在在此之前，它会确保 `performServices` 方法没有任何需要为用户完成的服务。下一步将是获取 `nextPage` 变量，该变量将决定 servlet 将启动哪个页面，或者将通过 `dispatch` 方法执行什么操作。

#### 示例 4-11 servlet 中的 performTask 方法

```java
public void performTask(HttpServletRequest req,
    HttpServletResponse resp)
throws ServletException, IOException {
    String nextPage;
    try {
        performServices(req, resp);
        nextPage = getInitParameter(req.getParameter("command"));
    } catch (Exception ex) {
        nextPage = getInitParameter("error_page");
    }
    dispatch(req, resp, nextPage);
}
```

## dispatch 方法

`dispatch` 方法使用 `dispatch.forward` 函数传递输入变量。然后使用 `nextPage` 变量根据用户的请求启动下一个页面。

#### 示例 4-12 servlet 中的 dispatch 方法

```java
public void dispatch(
    HttpServletRequest req, HttpServletResponse resp, String nextPage)
throws ServletException, IOException {
    RequestDispatcher dispatch = req.getRequestDispatcher(nextPage);
    dispatch.forward(req, resp);
}
```
