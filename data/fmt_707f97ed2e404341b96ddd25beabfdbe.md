
```
/usr/bin/tomcat $1
```

# end

将此脚本存储在 `/usr/bin` 中，并通过运行`chmod 755 /usr/bin/tomcatctl`命令启用执行权限后，你可以在不担心环境变量的情况下启动或停止 Tomcat。例如，要启动 Tomcat，你可以运行`tomcatctl start`命令；要停止，运行`tomcatctl stop`命令；要在前景中运行，运行`tomcatctl run`命令。

二进制 RPM 包还会安装`/etc/rc.d/init.d/tomcat`脚本。该脚本被符号链接到适当的运行级别，以便每次重新启动系统时，Tomcat 都会自动启动和停止。但是，`/etc/rc.d/init.d/tomcat`中`JAVA_HOME`的默认值和 JDK 路径可能并不适合所有人。例如，该脚本中为这两个变量设置的默认值如下所示：

```
export PATH=$PATH:/opt/IBMJava2-13/bin:/opt/IBMJava2-13/jre/bin

export JAVA_HOME=/opt/IBMJava2-13
```

这些似乎是 RPM 开发人员自己的设置。如果你按照我之前的说明从 Sun Microsystems 的 Web 站点下载 JDK，你的 JDK 安装路径将不同。因此，务必修改`/etc/rc.d/init.d/tomcat`脚本中的这两个设置。例如，正确的值是：

```
export PATH=$PATH:/usr/java/jdk1.3.0_02/bin:/usr/java/jdk1.3.0_02/jre/bin

export JAVA_HOME=/usr/java/jdk1.3.0_02
```

### 运行 Java Servlet

在本节中，我将讨论如何设置 Tomcat 以运行随附的示例 Servlet，并向你展示如何运行你开发或从 Internet 下载的自己编写的 Servlet 或 JSP 页面。

## 运行 Web 应用程序

> **注意** 永远不要以 root 身份运行 Tomcat。创建一个名为`tomcat`的新用户和组，并使用`chmod -R 755 /var/tomcat`命令更改`/var/tomcat`的文件和目录权限。

### 通过 Tomcat 运行 Java 示例 Servlet

要运行 Java Servlet，你不需要 Apache。你可以使用 Tomcat，它是一个名为`容器`的开源 Java 运行时环境，用于 Java Servlet。Tomcat 可以与你的 Web 服务器并行安装，它可以处理静态和 Servlet 请求。然而，当涉及到配置和提供静态请求时，Tomcat 的通用性要低得多。它并不是高度可配置的 Apache Web 服务器的替代品。不过，如果你想使用 Tomcat，本节就是为你准备的。

默认情况下，当 Tomcat 启动时，它从端口 8080 处理 Servlet 请求。启动 Tomcat 后，如果你在 Tomcat 服务器上运行 Web 浏览器，你应该能够使用`http://localhost:8080`访问示例 Servlet 和 JSP 页面。或者，你可以使用`http://your_web_server_hostname:8080`从另一台机器访问它。当你访问默认的 Tomcat 服务器时，该页面看起来类似于图 17-1。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_516_0.png)

单击 JSP 示例链接，你将看到一个如图 17-2 所示的页面。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_517_0.png)

有许多 JSP 示例页面可以尝试，以测试你的安装。例如，单击日期 JSP 页面的“执行”链接。你应该看到一个类似于图 17-3 所示的输出页面。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_517_1.png)

此 JSP 页面的 JSP 代码存储在`/var/tomcat/webapps/examples/jsp/dates/date.jsp`中，如清单 17-3 所示。

### 清单 17-3: date.jsp

```html
<html>

<!--

 Copyright (c) 1999 The Apache Software Foundation. All rights

 reserved.

-->

<%@ page session="false"%>

<body bgcolor="white">

<jsp:useBean id="clock" scope="page" class="dates.JspCalendar" type="dates.JspCalendar" />

<font size=4>

<ul>

<li> Day of Month: is  <jsp:getProperty name="clock" property="dayOfMonth"/>

<li> Year: is    <jsp:getProperty name="clock" property="year"/>

<li> Month: is   <jsp:getProperty name="clock" property="month"/>

<li> Time: is    <jsp:getProperty name="clock" property="time"/>

<li> Date: is    <jsp:getProperty name="clock" property="date"/>

<li> Day: is     <jsp:getProperty name="clock" property="day"/>

<li> Day Of Year: is <jsp:getProperty name="clock" property="dayOfYear"/>

<li> Week Of Year: is <jsp:getProperty name="clock" property="weekOfYear"/>

<li> era: is     <jsp:getProperty name="clock" property="era"/>

<li> DST Offset: is  <jsp:getProperty name="clock" property="DSTOffset"/>

<li> Zone Offset: is  <jsp:getProperty name="clock" property="zoneOffset"/>

</ul>

</font>

</body>

</html>
```

你可以看到，JSP 代码使用`<jsp:getProperty name="name" property="property_name" />`标签嵌入在 HTML 中。

如果你返回到顶级页面并单击 Servlet 示例链接，你将看到一个如图 17-4 所示的页面。

单击“Hello World” Servlet 的“执行”链接，你应该看到一个如图 17-5 所示的输出页面。

使用 Web 浏览器的后退按钮返回前一页，并单击“Hello World”的“源代码”链接以查看此 Servlet 的简化源代码。源代码如图 17-6 所示。

图 17-4：Servlet 列表示例。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_519_0.png)

图 17-5：`/examples/servlet/HelloWorldExample`的输出。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_519_1.png)

如你所见，这是一个相当简单的 servlet——它只是打印出一堆 HTML 标签以创建输出。

### 运行你自己的 Servlet 或 JSP

本节教你配置自己的 servlet 以通过`mod_jk`运行。假设你的 servlet 名为`myapp`。以下是让 Apache 和 Tomcat 协同工作所需完成的步骤：

1. 在`/var/tomcat/conf/server.xml`中创建以下配置：

```xml
<Context path="/myapp"
    docBase="/var/tomcat/webapps/myapps"
    debug="0"
    reloadable="true" >
  </Context>
```
