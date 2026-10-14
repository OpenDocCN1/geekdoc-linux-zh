
| `web.xml` | 是 | Web应用程序部署描述符。由 Java Servlet 2.5 定义。 |

| `sun-web.xml` | 是 Web Server（以及 Sun 应用程序服务器）特定的 Web应用程序部署描述符。由《Sun Java Web Server 7.0 Java Web开发指南》定义。 |

| `*.tld` | 是 | 标签库。由 Java Pages 2.1 定义。 |

| `classes` | 是 | 包含应用程序服务端 Java 类（如 servlet、工具类和 JavaBean）的目录。Java 包名必须反映在此目录结构中。例如，名为 `com.example.TestServlet` 的类需要存储在 `WEB-INF/classes/com/example/TestServlet` 文件中。Web应用程序的类加载器会在加载 `WEB-INF/lib` 目录中的 JAR 文件之前，加载 `WEB-INF/classes` 目录下的所有类。 |

| `lib` | 是 | 包含封装为 Java 归 (JAR) 文件的应用程序服务端类的目录。 |

| `tags` | 是 | 包含应用程序 JSP 标签文件的目录。 |

## 10.5 Java Web 应用

如果使用标准的 `jar` 工具对目录层次进行归档，可以将 Web 应用程序封装成 Web 归档（WAR）文件。当 Web 应用封装成 Web 归档（WAR）文件格式时，会创建一个 `META-INF` 目录。它包含了 Java 归档工具有用的清单信息。

除了支持文件和目录存在于文件系统的“未解包” Java Web 应用外，Web Server 7.0 还支持部署封装为 WAR 文件的 Java Web 应用。

下一节将描述 Web Server 如何使用部署描述符来指定 Web 应用的配置。

### 10.5.3 Web Server 中的 Java Web 应用配置

Java Web 应用配置的不同方面在以下配置文件中指定：

- `server.xml`
- `default-web.xml`
- `web.xml`
- `sun-web.xml`

图 10.7 展示了 Web Server 如何使用这些文件中的信息来初始化和加载 Java Web 应用。

本节的其余部分将详细描述这些文件。

#### 10.5.3.1 server.xml 文件

`server.xml` 是 Web Server 的主配置文件，位于每个服务器实例的 `config` 子目录中。它包含的信息包括部署在每个虚拟服务器中的 Java Web 应用。`server.xml` 中的 `web-app` 元素在 `virtual-server` 元素内部配置 Java Web 应用映射。`web-app` 元素是 `virtual-server` 元素的子元素，并且可以在 `virtual-server` 元素中出现 0 次或多次。表 10.7 列出了 `server.xml` 文件中 `web-app` 元素的子元素。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_454_0.png)

**图 10.7** Java Web 应用初始化

## 10.5 JAVA WEB APPLICATIONS

### 表 10.7 server.xml 中的 web-app 子元素

| 元素 | 是否强制 | 描述 |
| --- | --- | --- |
| `description` | 否 | Web 应用程序的文本描述。旨在为网站管理员提供参考。 |
| `enabled` | 否 | 控制在运行时是否启用该 Web 应用的布尔值。可用于在运行时临时禁用 Web 应用，而无需移除 `web-app` 元素。默认值为 `true`。 |
| `path` | 是 | Web Web 应用内容的文件系统路径。可以是绝对路径，也可以是相对路径。相对路径相对于服务器的 `config` 目录。 |
| `uri` | 是 | 访问 Web 应用的上下文路径。 |

第 10.5.4 节“将 Java Web 应用部署到 Web Server”包含了更多关于 Web Server 7.0 管理 `server.xml` 中 `web-app` 元素的管理接口的信息。

#### 10.5.3.2 default-web.xml 文件

`default-web.xml` 文件包含了所有部署到服务器的 Java Web 应用共享的 Web 应用配置。该文件位于每个服务器实例的 `config` 子目录中。

该文件是一个 XML 格式的文件，其内容根据标准 XML 数据类型定义 (DTD) 进行验证，该 DTD 验证 `web.xml` 文件如下：

```
<!DOCTYPE web-app
PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
  "http://java.sun.com/dtd/web-app_2_3.dtd">
```

如 10.7 所示，此文件可为所有 Web 应用指定通用配置，否则这些配置将在每个 Web 应用的部署描述符文件——`web.xml` 中重复。单个 Web 应用始终可以覆盖此文件中指定的任何设置。

本节的其余部分描述了为每个配置创建的 `default-web.xml` 文件的内容，并描述了 Web Server 管理框架中包含的该文件的支持。元素的顺序和分组已更改，以便将相关的配置放在一起。

如前所述，Web Server 7.0 的 Java Web 容器包含对 Java Pages (JSP) 支持。Web Server 7.0 中的 JSP 引擎包含一个将 JSP 脚本编译为 servlet 的 JSP 编译器，以及一个执行这些编译脚本的 JSP 运行时。默认情况下，Web Server 7.0 中的所有 Web 应用都使用 Web Server 的 JSP 引擎处理 Java Pages 的请求。Web Server 的 JSP 引擎通过 `jsp` servlet 及其映射提供给 Web 应用，这些在 `default-web.xml` 中的定义如下：

```
<servlet>
<servlet-name>jsp</servlet-name>
<servlet-class>org.apache.jasper.servlet.JspServlet</servlet-class>

<init-param>
<param-name>httpMethods</param-name>
<param-value>GET,HEAD,POST</param-value>
</init-param>
<init-param>
<param-name>fork</param-name>
<param-value>false</param-value>
</init-param>
<init-param>
<param-name>mappedfile</param-name>
<param-value>false</param-value>
</init-param>
<load-on-startup>3</load-on-startup>
</servlet>

<servlet-mapping>
<servlet-name>jsp</servlet-name>
<url-pattern>*.jsp</url-pattern>
</servlet-mapping>

<servlet-mapping>
<servlet-name>jsp</servlet-name>
<url-pattern>*.jspx</url-pattern>
</servlet-mapping>
```

默认 servlet 处理不映射到 Web 应用中任何其他 servlet 的请求，例如静态内容（HTML 文件、图像等）的请求。Web Server 的默认 servlet 与服务器的 NSAPI 引擎紧密集成，使 Java Web 容器可以使用服务器的文件缓存来高效地提供静态内容。Web Server 7.0 中的默认 servlet 实现还促进了 Java 和非 Java 动态内容（如 JSP、包括 CGI 程序、Servlet 以及 HTML 文件）的无缝集成。默认 servlet 及其映射在 `default-web.xml` 中的定义如下：

```
<servlet>
  <servlet-name>default</servlet-name>
  <servlet-class>com.sun.webservices.servlets.DefaultServlet</servlet-class>
  <load-on-startup>1</load-on-startup>
</servlet>
```

```
<servlet-mapping>
  <servlet-name>default</servlet-name>
  <url-pattern>/*</url-pattern>
</servlet-mapping>
```

客户端通过指定 URI 模式访问 servlet。servlet 映射指定在 `web.xml` 中，即 Web 应用的部署描述符。示例 10.6 是 `web.xml` 的片段，展示了 `HelloServlet` 的映射。
