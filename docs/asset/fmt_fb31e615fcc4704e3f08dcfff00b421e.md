
```bash
export PATH=$PATH:$JAVA_HOME/bin
```

此行必须跟在上一节讨论的 `$JAVA_HOME` 行之后。

## 6. 测试 JDK 安装

通过运行 `java -version` 命令来测试 JDK 安装。你应该看到类似以下输出：

```bash
java version "1.3.0_02"

Java(TM) 2 Runtime Environment, Standard Edition (build 1.3.0_02)

Java HotSpot(TM) Client VM (build 1.3.0_02, mixed mode)
```

### 安装软件

将所有上述文件下载到一个新建的临时目录中，并以 `root` 用户身份从该目录运行 `rpm -ivh tomcat*.rpm` 命令来安装所有软件。

默认情况下，`Tomcat` 安装在 `/var/tomcat` 目录中。你需要在 `~/.bashrc` 文件中添加以下环境变量：

```bash
export TOMCAT_HOME=/var/tomcat
```

通过运行 `source ~/.bashrc` 命令在当前 shell 中加载该变量。

## 配置 Tomcat

在本节中，我将讨论如何为 Apache 配置 Tomcat，以及如何使用 Java Security Manager 工具管理 Tomcat 的安全性。

### 为 Apache 配置 Tomcat

Tomcat 的主要配置文件是 `/var/tomcat/server.xml`。从扩展名可以看出，它是一个 XML 文件。

Tomcat 可以使用两种类型的连接处理器：Ajp13 和 Ajp12 协议。Ajp13 协议是较新的协议，提供了更好的性能，并且支持安全套接层（SSL）连接。

要在 Tomcat 中激活基于 Ajp13 协议的连接处理器，你应该确保 `server.xml` 文件中的以下连接器配置未被注释掉：

```xml
<Connector className="org.apache.tomcat.service.PoolTcpConnector" > 
    <Parameter name="handler" 
        value="org.apache.tomcat.service.connector.Ajp13ConnectionHandler"/>
    <Parameter name="port" value="8009"/>
</Connector>
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_503_0.png)

`server.xml` 文件应该已经包含了一大块用于 8007 端口上 Ajp12 连接的类似代码。即使你计划使用基于 Ajp13 的连接器，也不应删除此连接器。这是关闭 Tomcat 所必需的。

名为 `worker` 的 Tomcat 实例属性定义在 `/var/tomcat/conf/workers.properties` 文件中。默认文件（不含注释）包含列表 17-1 中显示的属性。

### 列表 17-1：默认的 Tomcat (worker) 属性

```properties
workers.tomcat_home=c:\jakarta-tomcat
workers.java_home=c:\jdk1.2.2
ps=\
worker.list=ajp12, ajp13

    worker.ajp12.port=8007
    worker.ajp12.host=localhost
    worker.ajp12.type=ajp12
    worker.ajp12.lbfactor=1

    worker.ajp13.port=8009
    worker.ajp13.host=localhost
    worker.ajp13.type=ajp13
    worker.ajp13.lbfactor=1

    worker.loadbalancer.type=lb
    worker.loadbalancer.balanced_workers=ajp12, ajp13

    worker.inprocess.type=jni
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
