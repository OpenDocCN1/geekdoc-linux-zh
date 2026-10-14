
```xml
<xml version="1.0" encoding="ISO-8859-1"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
  version="2.5">
  <display-name>Yummy Pizzas</display-name>
  <context-param>
    <param-name>Owner</param-name>
    <param-value>raj@yummypizzas.com</param-value>
  </context-param>
  <servlet>
    <servlet-name>MenuServlet</servlet-name>
    <servlet-class>yummypizzas.MenuServlet</servlet-class>
    <init-param>
      <param-name>specials</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>MenuServlet</servlet-name>
    <url-pattern>menu/*</url-pattern>
  </servlet-mapping>
  <session-config>
    <session-timeout>10</session-timeout>
  </session-config>
  <welcome-file-list>
    <welcome-file>menu.jsp</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  <error-page>
    <error-code>404</error-code>
    <location>nosuchpizza.html</location>
  </error-page>
  <resource-ref>
    <description>Pizza Database</description>
    <res-ref-name>jdbc/pizzas</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
  </resource-ref>
</web-app>
```

为了实现快速开发，当 Web Server 的 Java Web 容器检测到应用程序的 `web.xml` 文件被修改时，可以在不重启服务器或不影响其他应用程序的情况下重新部署应用程序。关于此点的更多信息请见第 10.5.9 节，“动态重配置 Java Web 应用”。

图 10.7 展示了服务器如何使用 `web.xml` 中的信息初始化 Java Web 应用。Web Server 不包含创建或编辑 `web.xml` 文件的工具。流行的 Java 集成开发环境 `IDE` 如 NetBeans 和 Eclipse 包含了创建和打包 Web 应用及其关联部署描述符的支持。图 10.9 展示了如何使用 NetBeans 编辑示例 10.7 中的示例 `web.xml` 文件。

## 第 10 章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_462_0.png)

图 10.9 NetBeans 6.1 中的 web.xml 编辑

### 10.5.4 sun-web.xml 文件

`sun-web.xml` 文件是一个可选的部署描述符，专门 Sun 的 Web 层服务，即 Web Servlet 和 Application Server。该文件也是一个 XML 格式文档，指定了 Web Server 7.0 中包含的 Web 应用部署和配置信息。`sun-web.xml` 文件的格式和内容定义在《Java System Web Server 7.0 开发指南》的附录 A 中。如果存在，`sun-web.xml` 文件必须位于应用程序的 `WEB-INF` 子目录下。Web 应用并不要求包含 `sun-web.xml` 文件。

此此文件中的所有项目都根据 `sun-web.xml` 部署描述符的 XML 类型定义 `DTD` 进行验证，如下：

```xml
<!DOCTYPE sun-web-app PUBLIC
"//Sun Microsystems, Inc.//DTD Application Server 9.0 Servlet 2.5//EN"
"http://www.sun.com/software/appserver/dtds/sun-web-app_2_5-0.dtd">
```

除了 DODOCTYPE 声明中引用的 URL 外，还可以找到类型定义文件 `sun-web-app_2_5-0.dtd`。`sun-web.xml` 描述符是 `web.xml` 的辅助文件，指定了 Web Server 7.0 的 Web 应用部署和配置。`sun-web.xml` 中指定的类型包括：

- Servlet 定义和映射
- JSP 配置
- Servlet 过滤器定义和映射
- Session 配置
- 安全配置
- 欢迎文件顺序
- 应用 `ServletContext` 初始化参数和生命周期监听器
- 语言和编码映射
- 错误页面声明

示例 10.8 展示了一个示例 `sun-web.xml` 文件。

示例 10.8 示例 sun-web.xml 文件
