
假设在 URI `/bookstore` 部署了一个 Java 应用程序，并且假设该应用程序的 `web.xml` 文件未指定任何欢迎页，处理请求 `http://www.example.com/bookstore` 时，`obj.conf` 文件中的哪些指令将被执行？参考示例 10.2 中指定的 `obj.conf` 文件，服务器将按（此顺序）处理以下指令：

```
10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" names="index.html,home.html,index.jsp"
18 ObjectType fn="type-j2ee"
19 ObjectType fn="type-by-extension"
29 Service fn="service-j2ee" method="*"
25 AddLog fn="flex-log"
```

### 10.3.4 带有欢迎页的 Java 应用程序中的目录请求

示例 10.3 提供了 `web.xml` 片段片段展示了 Java Web 应用程序如何在其部署符中指定欢迎页。

**示例 10.3** `web.xml` 文件片段

```
<welcome-file-list>
  <welcome-file>home.jsp</welcome-file>
  <welcome-file>home.html</welcome-file>
</welcome-file-list>
```

# 第 10 章通过 JAVA 提供动态内容

```
10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" index-names="index.html,home,index.jsp"
18 ObjectType fn="type-j2ee"
19 ObjectType fn="type-by-extension"
29 Service fn="service-j2ee" method=""
25 AddLog fn="flex-log"
```

这些指令与在没有欢迎页的 Java Web 应用中请求目录时的指令相似（参见“在 Java Web 应用中请求目录”章节），不同之处在于 `find-index-j2ee`（第 16 行）成功地将请求的 URI 映射到 Web 应用程序文档根目录中的欢迎页，因此 `find-index`（第 17 行）不起作用，因为它仅对目录请求起作用。

## 10.3.5 在 Java Web 应用中请求 MIME 映射的内容

示例 10.4 提供了一个 `web.xml` 文件的片段，演示了 Java 如何指定扩展名与多用途互联网邮件扩展（MIME）类型之间的映射。

示例 10.4 `web.xml` 文件的片段

```xml
<mime-mapping>
<extension>pdf</extension>
<mime-type>application/pdf</mime-type>
</mime-mapping>
```

如果上一节引入的 `/bookstore` 应用指定了如示例 10.4 所示的 MIME 映射，并且应用程序的根目录下确实包含一个名为 `book.pdf` 的文件，那么 `obj.conf` 文件中的哪些指令将被执行以处理 `http://www.example.com/bookstore/book.pdf` 的请求？参考示例 10.2 中指定的 `obj.conf` 文件，服务器将处理以下指令（按此顺序）：

```
10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" index-names="index.html,home,index.jsp"
```

这些指令与在没有欢迎页的 Java Web 应用中请求目录时的指令相似，不同之处在于 `find-index-j2ee`（第 16 行）成功地将请求的 URI 映射到 Web 应用程序文档根目录中的欢迎页，因此 `find-index`（第 17 行）不起作用，因为它仅对目录请求起作用。

## 10.3.6 Java 配置

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 `JVM`
- 配置全局 Web 设置

通常，Java 开发者指定 Java 配置，而管理员指定部署环境。Java 容器配置在以下文件中指定：

表 10.3 配置文件

| 文件名 |  |
| :--- | :--- |
| `default.xml` | Java 容器的全局配置。 |
| `login.xml` | 特定于实例的配置。 |
| `obj.conf` | 实际上控制服务器的配置。 |
| `server.policy` | 安全设置的配置。 |
| `server.xml` | 应用程序的主部署文件。 |

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 `JVM`
- 配置全局 Web 设置

## 10.4 Java 配置

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 `JVM`
- 配置全局 Web 设置

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 `JVM`
- 配置全局 Web 设置

表 10.4 配置文件

| 文件名 | 说明 |
| :--- | :--- |
| `default.xml` | Java 容器的全局配置。 |
| `server.xml` | 特定于实例的配置。 |
| `obj.conf` | 实际上控制服务器的配置。 |

### 10.4.1 全局启用/禁用 Java

当你创建一个新的服务器配置时，Java 容器默认是启用的，如图 10.4 所示。

`https://example.com/image10.4.png`

图 10.4 管理控制——新配置

### 10.4.2 启用/禁用 Java

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 `JVM`
-

你也可以通过服务器的管理界面在现有配置中启用或禁用 Java 容器。图 10.5 高亮了屏幕上用于启用或禁用配置 Java 容器的复框框

`https://example.com/image10.5.png`

图 10.5 管理控制——JVM 普通设置

注意：本章包含了超出本书范围的 Java 配置示例。这些信息可以在《Sun Java Server 7.0 管理员指南》中找到。

下面的 shell 示例显示了如何使用 `wadm` 脚本的 `enable-java` 和 `disable-java` 命令来配置 Java 容器的状态。

```bash
wadm> disable-java --config=test
CLI201 Command 'disable-java' ran successfully
wadm> deploy-config --restart test
CLI201 Command 'deploy-config' ran successfully
wadm>
wadm> enable-java --config=test
CLI201 Command 'enable-java' ran successfully
wadm> deploy-config --restart test
CLI201 Command 'deploy-config' ran successfully
```

## 第 10 章通过 JAVA 提供动态内容
