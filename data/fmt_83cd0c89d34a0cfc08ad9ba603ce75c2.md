
## 配置 `workers.properties`

`workers.properties` 文件包含定义所有 worker 的初始内容。以下是该文件的默认部分：

```properties
worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\classes

worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\ajp.jar

worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\parser.jar

worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\jasper.jar

worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\servlet.jar

worker.inprocess.class_path=$(workers.tomcat_home)\(ps)\lib\ps\webserver.jar

worker.inprocess.class_path=$(workers.java_home)\(ps)\lib\(ps)tools.jar

worker.inprocess.cmd_line=-config

worker.inprocess.cmd_line=$(workers.tomcat_home)/conf/jni_server.xml

worker.inprocess.cmd_line=-home

worker.inprocess.cmd_line=$(workers.tomcat_home)

worker.inprocess.jvm_lib=$(workers.java_home)\(ps)\jre\bin\classic\jvm.dll

worker.inprocess.stdout=$(workers.tomcat_home)\(ps)inprocess.stdout

worker.inprocess.stderr=$(workers.tomcat_home)\(ps)inprocess.stderr

worker.inprocess.sysprops=tomcat.home=$(workers.tomcat_home)
```

该默认属性文件定义了一个 `ajp12` worker、一个 `ajp13` worker、一个 `jni` worker 和一个 `lb` worker。这些 worker 类型之间的区别如表 17-1 所示。

### 表 17-1 Worker 类型

| **Worker 类型** | **描述** |
|---|---|
| `ajp12` | 此 worker 使用 `ajp12` 协议将请求转发给使用 `ajp12` 协议的进程外 Tomcat worker。 |
| `ajp13` | 此 worker 使用 `ajp13` 协议将请求转发给使用 `ajp12` 协议的进程外 Tomcat worker。由于 `ajp13` 是比 `ajp12` 更新的协议，`ajp13` 类型的 worker 可以实现比 `ajp12` 类型 worker 更好的性能。此外，`ajp13` 提供 SSL 支持。 |
| `jni` | 通过使用 Java Native Interface (JNI)，这种类型的 worker 可以将请求转发给进程内 Tomcat worker。进程内 worker 运行在 Apache 自身内存空间中打开的 JVM 内。 |
| `lb` | 通过使用简单的轮询负载均衡方案，此 worker 可以转发请求。 |

`workers.properties` 文件有一些对所有类型 worker 都是“全局”的设置。例如：

```properties
workers.tomcat_home=c:\jakarta-tomcat

workers.java_home=c:\jdk1.2.2

ps=\

worker.list=ajp12, ajp13
```

这些设置是全局的。第一个设置 Tomcat 的主目录。这应该设置为环境变量 `$TOMCAT_HOME` 的值。由于 Tomcat 的默认安装在 Linux 系统下创建 `/var/tomcat` 作为目录，你应该将默认值（`c:\jakarta-tomcat`）修改为如下所示：

```properties
workers.tomcat_home=/var/tomcat
```

类似地，`workers.java_home` 设置 JDK 安装目录的顶层路径，在 Linux 下是 `/usr/java/jdkversion`（例如，对于 JDK 1.3，这是 `/usr/java/jdk1.3.0_02`）。因此，应将其设置为：

```properties
workers.java_home=/usr/java/jdk1.3.0_02
```

下一行告诉 Tomcat 使用什么分隔符来分隔目录元素。默认值 `\` 适用于 Windows 系统，因为在 Windows 平台上目录名是用 `\` 分隔的。在 UNIX 系统上，应该是 `/`。因此，将此行设置为如下所示：

```properties
ps=/
```

`worker.list` 告诉 Tomcat 你想定义多少个 worker。默认列表将 `ajp12` 和 `ajp13` 定义为两个 worker。

这些 worker 中的每一个都可以通过 `worker.<worker_name>.properties=value` 行设置自己的属性。例如，在默认文件中，`ajp13` worker 设置了以下属性：

```properties
worker.ajp12.port=8007

worker.ajp12.host=localhost

worker.ajp12.type=ajp12

worker.ajp12.lbfactor=1
```

第一行设置端口号，这是 `ajp12` worker 用于监听请求的。第二行定义此 worker 监听连接的主机名。第三行定义 worker 的类型。我认为将 worker 命名为 `ajp12` 而它的类型也是 `ajp12` 是一个糟糕的选择。只要名称由字母和数字组成，你可以将 worker 命名为任何名称。第四行为负载均衡目的给 worker 赋予一个权重评分。较高的数字表示功能更强大的机器，当多个机器参与负载均衡场景时，负载均衡 worker 会首先选择具有最高 `lbfactor` 的 worker。

`workers.properties` 文件中的接下来四行定义了 `ajp13` worker 的相同属性。

接下来的两行定义了一个名为 `loadbalancer` 的 worker，其类型为 `lb`，并使用轮询模式平衡 `ajp12` 和 `ajp13` worker。这两行是：

```properties
worker.loadbalancer.type=lb

worker.loadbalancer.balanced_workers=ajp12, ajp13
```

接下来的两行定义了一个类型为 `jni` 的名为 `inprocess` 的 worker。在 Linux 系统上，通过将该行设置为 `/var/tomcat/classes` 来定义此 worker 的 `class_path`：

```properties
worker.inprocess.type=jni

worker.inprocess.class_path=${workers.tomcat_home}${ps}${ps}classes
```

接下来的六行将六个库文件添加到类路径中：

```properties
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}jaxp.jar

worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}parser.jar

worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}jasper.jar

worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}servlet.jar

worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}webserver.jar

worker.inprocess.class_path=${workers.java_home}${ps}lib${ps}tools.jar
```

`inprocess` worker 的最终类路径（在 Linux 上）看起来如这里所示：

```text
/var/tomcat/classes:/var/tomcat/lib/jaxp.jar:/var/tomcat/lib/parser.jar:/var/tomcat/lib/jasper.jar:/var/tomcat/lib/servlet.jar:/var/tomcat/lib/webserver.jar:/usr/java/jdk1.3.0_02/lib/tools.jar
```

如下所示的接下来四行为 `inprocess` worker 定义了一组命令行选项：

```properties
worker.inprocess.cmd_line=-config

worker.inprocess.cmd_line=${workers.tomcat_home}/conf/jni_server.xml

worker.inprocess.cmd_line=-home

worker.inprocess.cmd_line=${workers.tomcat_home}
```

下一行定义了 JVM 库路径：

```properties
worker.inprocess.jvm_lib=$(workers.java_home)$(ps)jre$(ps)bin$(ps)classic$(ps)jvm.dll
```

JVM 库路径（在 Linux 上）是 `/usr/java/jdk1.3.0_02/jre/lib/i386/classic/libjvm.so`。因此你必须将上述 `jvm_lib` 行更改为：

```properties
worker.inprocess.jvm_lib=$(workers.java_home)$(ps)jre$(ps)lib$(ps)i386$(ps)classic$(ps)libjvm.so
```

接下来的两行定义了用于写入 `inprocess` worker 的 STDOUT 和 STDERR 的文件名：

```properties
worker.inprocess.stdout=${workers.tomcat_home}$(ps)inprocess.stdout

worker.inprocess.stderr=${workers.tomcat_home}$(ps)inprocess.stderr
```

在 Linux 系统上，STDOUT 写入 `/var/tomcat/inprocess.stdout`，STDERR 写入 `/var/tomcat/inprocess.stderr`。

最后一行定义了 `inprocess` worker 的一个系统属性。以下行设置的默认属性是在 Linux 上值为 `/var/tomcat` 的 `tomcat.home`：

```properties
worker.inprocess.sysprops=tomcat.home=${workers.tomcat_home}
```

## 配置 Tomcat 以使用 Java Security Manager

Java Security Manager 强制实施所有 Java 相关对象的安全限制，包括 applet、servlet、JSP，甚至 Tomcat 本身。通过使用 Java Security Manager，你可以控制每个应用程序可以做或不能做什么。表 17-2 显示了你可以设置的权限类型。

### 表 17-2 Java 安全管理器权限类型

| 权限类型 | 含义 |
| :--- | :--- |
| `java.util.PropertyPermission` | 控制对 JVM 属性（如 `java.home`）的读/写访问权限。 |
| `java.lang.RuntimePermission` | 控制某些系统或运行时功能（如 `exit()` 和 `exec()`）的使用。 |
| `java.io.FilePermission` | 控制文件和目录的权限。 |
| `java.net.SocketPermission` | 控制网络套接字的使用。 |
| `java.net.NetPermission` | 控制多播网络连接的使用。 |
| `java.lang.reflect.ReflectPermission` | 控制使用反射进行类内省的操作。 |
| `java.security.SecurityPermission` | 控制对安全方法的访问。 |
| `java.security.AllPermission` | 允许所有操作，这实际上等同于不使用 Java 安全管理器。 |

Tomcat 的安全策略在 `/var/tomcat/conf/tomcat.policy` 文件中定义。该文件通常使用以下语法来授予权限：

```
grant codebase code_source {

    permission_type_class [name [, action_list]];

};
```

例如，默认的 `/var/tomcat/conf/tomcat.policy` 文件授予以下权限：

```
// Example webapp policy

// By default we grant read access to webapp dir and

// write to workdir

grant codebase "file:${tomcat.home}/webapps/examples" {

    permission java.net.SocketPermission "localhost:1024-",

        "listen";

    permission java.util.PropertyPermission "*", "read";

};
```

`${tomcat.home}/webapps/examples`（即 `/var/tomcat/webapps/examples`）中的文件被授予权限，可以使用网络套接字在本地主机（`localhost`）上监听 1024 或更高的端口，并且仅允许对所有 JVM 属性进行读访问。

如果你希望名为 `/var/tomcat/webapps/your_app_name` 的应用程序通过 TCP 端口 389 连接到轻量级目录访问协议（LDAP）服务器，你需要授予以下权限：

```
grant codeBase "file:${tomcat.home}/webapps/your_app_name" {

    permission java.net.SocketPermission "localhost:389",

        "connect";

    permission java.util.PropertyPermission "*", "read";

};
```

默认情况下，Tomcat 的 Java 安全管理器是禁用的。你必须按以下方式启用它：

- 在 `/var/tomcat/conf/server.xml` 文件中，你应该找到以下内容：

```
<!-- Uncomment out if you have JDK1.2 and want to use policy

    <ContextInterceptor

        className="org.apache.tomcat.context.PolicyInterceptor" />

    -->
```

此默认设置禁用了安全管理器，因此你必须移除注释，使其变为以下内容：

```
<ContextInterceptor

    className="org.apache.tomcat.context.PolicyInterceptor" />
```

- 使用 `-security` 选项重启 Tomcat。例如，运行 `/usr/bin/tomcat -security` 将在启用 Java 安全管理器的情况下重启 Tomcat。

当 Java 安全管理器拦截到违反安全策略的操作时，JVM 会抛出 `AccessControlException` 或 `SecurityException`。

### 为 Servlet 和 JSP 配置 Apache

启动 Tomcat 时，它会创建一个名为 `/var/tomcat/conf/mod_jk.conf-auto` 的配置文件。为了让 Apache 与 Tomcat 进行交互，你需要让 Apache 加载此文件。为此，请修改 `httpd.conf` 并添加以下行：

```
Include /var/tomcat/conf/mod_jk.conf-auto
```

自动生成的 `mod_jk.conf-auto` 文件存在一个问题。它指示 Apache 从服务器根目录（由 `httpd.conf` 中的 `ServerRoot` 指令指定）下名为 `libexec` 的子目录中加载 `mod_jk.so` 模块。不幸的是，该目录并不存在，而 `mod_jk.so` 安装在 `/usr/lib/apache` 目录中。因此，你有两个选择：

你可以不通过 `Include` 指令指向 `/var/tomcat/conf/mod_jk.conf-auto` 文件，而是将此文件复制为另一个名称（例如 `mod_jk.conf`），并使用：

```
Include /var/tomcat/conf/mod_jk.conf
```
