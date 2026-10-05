

# 服务端：Java • 99

![](img/069cd06404ac5e90171e6d857bf3ad28_114_0.png)

图 7.6：HTML 表单 action 处理器中限定的 servlet 通过动态构建 HTML 响应来处理用户请求。

## Servlet API

图 7.5 和图 7.6 所示的示例使用了 HTML 文件 `Panel.html` 和名为“PanelServlet”的 Java servlet。该 servlet 通过 URL 请求 `http://127.0.0.1:8080/servlet/PanelServlet` 触发。PanelServlet 动态地构建 HTML 响应。

Servlet 是一个构建在通用 `HttpServlet` 之上的 Java 类。`HttpServlet` 为常用提供了代码实现，其中我们已经提到的两个是 `doGet` 和 `doPost`。`HttpServlet` 对 `doGet` 和 `doPost` 的实现什么都不做。它们利用了 Java 的一项特性——继承。这很重要，因为 servlet 引擎会调用所有拥有这些方法的 servlet，其顺序基于面向对象的特性，该特性取决于 HTML 表单标签中限定的 HTTP 方法类型。确保你的 servlet 使用了适当的方法的一种方法是编写一个 `doPost`，它简单地调用 `doGet` 方法。

我们在测试时喜欢使用 HTTP GET 请求，但在生产环境中使用 HTTP POST 请求。使用这个简单的小技巧，当我们把 HTML 表单的 method 选项改为 POST 时，servlet 不需要任何更改。

`HttpServlet` 类还有一个名为 `init` 的方法。servlet 引擎在 servlet 第一次被请求时调用 `init`。对于 servlet，你可能想使用你的 `init` 方法来加载 Java 数据库连接 (JDBC) 驱动程序并初始化 JDBC 连接变量。

## 用于 PANEL.HTML 的 Servlet

第 6 章介绍了 HTML，更具体地说，是 HTML 表单。PanelServlet 示例的代码设计用于响应第 6 章讨论的表单（为了方便起见，该表单显示在图 7.7 中）。

## 100 · 第 7 章

```html
<HTML>
<HEAD>
<TITLE>Example HTML Panel</TITLE>
</HEAD>
<BODY>
<CENTER><h1>Example HTML Panel Design</h1></CENTER>
<CENTER><h3>Please complete the following skill survey/</h3></CENTER>
<FORM ACTION="/servlet/PanelServer" METHOD="GET">
<BR>
<B name="name" />
<INPUT type="text" name="name" MAXLENGTH=25 SIZE=25>
<BR>
<B>I know the following computer languages/</B>
<BR>
<INPUT type="checkbox" name="rpg" value="RPG">RPG
<INPUT type="checkbox" name="cobol" value="COBOL">COBOL
<INPUT type="checkbox" name="java" value="Java">Java
<INPUT type="checkbox" name="vb" value="Visual Basic">Visual Basic
<INPUT type="checkbox" name="cpp" value="C++">C++
<BR>
<B>I have been programming for:</B>
<BR>
<INPUT type="radio" name="exp" value="5">less than 5 years
<INPUT type="radio" name="exp" value="5-10">5 to 10 years
<INPUT type="radio" name="exp" value="10-15">10 to 15 years
<INPUT type="radio" name="exp" value="15-">15 or more years
<BR>
<B>My titles are "prof":</B>
<BR>
<SELECT name="title">
<OPTION value="Programmer Analyst" SELECTED="SELECTED">Programmer Analyst</OPTION>
<OPTION value="Systems Manager">Systems Manager</OPTION>
<OPTION value="Senior Programmer">Senior Programmer</OPTION>
<OPTION value="Web Master">Web Master</OPTION>
</SELECT>
<BR>
<CENTER>
<INPUT type="SUBMIT" name="Submit" value="Submit">
</CENTER>
</FORM>
```

图 7.7：HTML。
