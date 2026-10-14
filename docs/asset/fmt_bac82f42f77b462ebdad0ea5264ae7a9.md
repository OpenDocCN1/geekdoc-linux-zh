
`load-modules` SAF 用于向 Web 服务器加载并注册插件。此函数最常用于将第三方插件加载到 Web 服务器中，以提供基础平台未包含的功能。此类示例可能包括一个用于为应用程序提供接口的插件。

此示例指定了在初始化过程中注册的三个插件。`lib2eeplugin.so` 和 `libfastcgi.so` 插件随 Web Server 7.0 一起包含。`myplugin.so` 插件是一个用户创建共享库，可以在 `/sun/webserver7/plugins/myplugin` 目录下找到。`shlib` 参数指定共享库的本地文件系统路径。

> 注意：如果你不在 `shlib` 参数中指定完全限定文件名，Web 服务器将在启动脚本（`startserv`）定义的 `SERVER_LIB_DIR` 变量指定的路径中搜索插件。如果你将 Web 服务器安装在 `/sun/webserver7` 目录，则 `SERVER_LIB_DIR` 的默认值为 `/sun/webserver7/lib`。

`shlib_flags` 参数（如第一个指令所示）指定了共享库如何被加载到 Web 服务器进程中。启动后，Web 服务器进程使用 `dlopen` 函数将额外的库文件加载到内存中。第一个指令中的 `global` 和 `now` 选项分别指的是 `dlopen` 选项 `RTLD_GLOBAL` 和 `RTLD_NOW`。你可以通过使用以下 UNIX 命令阅读更多这些及其他选项：

- `# man dlopen`

第三个 `Init` 指令还演示了注册特定插件内特定函数（即 `myfunc1` 和 `myfunc2`）的能力。前两个指令中没有指定 `functions` 参数，因此这些插件中定义的所有函数均可使用。

> 注意：有关 Web 服务器指令的更多信息，请参考《Sun Java Web Server 7.0 NSAPI 开发人员指南》（文档编号 819-2632）。

### 5.1.1 语法

表 5.2 提供了 `magnus.conf` 文件的通用语法。

表 5.2 `magnus.conf` 语法

| 语法 | 规则 |
| :--- | :--- |
| 大写敏感性 | `magnus.conf` 文件中的项对大小写敏感 |
| 注释 | 井号（`#`）用于标记 `magnus.conf` 文件中的注释。井号后面的文本会被忽略 |

## | MAGNUS.CONF 文件

| 语法 | 规则 |
| :--- | :--- |
| 指令 | `magnus.conf` 文件中的指令定义了值。错误可能会导致服务器无法正常运行 |
| 参数 | 对于预定义的 SAF，参数的数量和名称取决于函数 |
| 路径名称 | 在路径名称中，始终使用正斜杠（`/`）而不是反斜杠（`\`），即使在 Windows 平台上也是如此 |
| 引号 | 字符串包含空格时需要引号（`""`），否则是可选的。每个左引号必须与右引号匹配 |
| 空格 | `magnus.conf` 文件中的指令出现在其行中。在分隔名称和值的等号（`=`）前后不允许有空格。换行在示例 5.1 的前三个指令中有演示 |

### 5.1.2 上下文

管理节点可能包含多个已部署的配置。这些部署配置被称为实例。每个实例只能包含一个 `magnus.conf` 文件；因此，实例与文件之间是一一对应的。

### 5.1.3 修改

通过控制台或命令行界面进行的某些更改会更新 `magnus.conf` 文件。如果该文件通过这些接口进行了更新，你必须部署配置以使其在相应的管理节点上生效。如果你使用这些工具部署新配置，将提示你重启。

`magnus.conf` 文件在实例启动时被读取；因此，对 `magnus.conf` 的任何更改都需要重启才能生效。控制台和命令行界面会在部署过程中检测 `magnus.conf` 文件的更改。

## 5.2 server.xml 文件

`server.xml` 文件是 Web 服务器实例的主配置文件。它包含了安装过程中配置的监听套字、虚拟服务器和其他组件的初始值。它还包含了允许 Web 服务器在安装后立即运行的默认设置。你可以通过控制台或命令行界面修改这些设置的值，也可以通过编辑特定管理节点上的 `server.xml` 文件。

> 注意：`server.xml` 文件是最重要的配置文件之一。如果你决定手动编辑它，了解该文件的语法及其结构至关重要。

### 5.2.1 语法

正如名称所示，`server.xml` 文件以扩展标记语言（XML）格式包含信息。因此，理解基本的 XML 结构和术语对于理解 `server.xml` 文件至关重要。

XML 文档包含元素的值的层次结构。元素是 XML 数据单元，也是 XML 文档的基础构建块。元素可以关联值或其他子元素；从而形成父子关系。

## 5.2 SERVER.XML 文件

元素通过起始标签和结束标签分隔，其结构类似于你在查看 HTML 文档源代码时看到的结构（它们使用 `<` 和 `>` 括号）。元素以起始标签开始，例如 `<virtual-server>`，并结束标签结束，例如 `</virtual-server>`。标签是区分大小写的。

以下是运行在 64 位模式下的 Web 服务器的平台元素示例：

```
<platform>64</platform>
```

XML 文档必须包含一个根根元素，它是层次结构中的最顶层元素。与任何其他 XML 元素一样，根元素可以包含子元素。`<server>` 元素是 `server.xml` 文件的根元素。`<server>` 元素有许多子元素，其中许多子元素也有自己的子元素。

示例 5.2 展示了默认管理节点（Administration Node）的 `server.xml` 文件。

### 示例 5.2 示例 server.xml 文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
Copyright 2006 Sun Microsystems, Inc. All rights reserved.
Use is subject to license terms.
-->
<server>
  <cluster>
    <local-host>boulder.example.com</local-host>
    <instance>
      <host>boulder.example.com</host>
    </instance>
  </cluster>
  <log>
    <log-file>../logs/errors</log-file>
    <log-level>info</log-level>
  </log>
  <platform>64</platform>
  <temp-path>/tmp/https-boulder.example.com-6accbd0a</temp-path>
<jvm>
<java-home>/sun/webserver7/jdk</java-home>
<server-class-path>
/sun/webserver7/lib/webserver-rt.jar:${sun/java.home}/lib/tools.jar:
/sun/webserver7/lib/ant.jar:/sun/webserver7/lib/pwc.jar:
/sun/webserver7/lib/jstsearch.jar:/sun/webserver7/lib/webserver-jst1.jar:
/sun/webserver7/lib/jsf-impl.jar:/sun/webserver7/lib/jsf-api.jar:
/sun/webserver7/lib/webserver-jwsdsp.jar:/sun/webserver7/lib/
container-auth.jar:
/sun/webserver7/lib/mail.jar:/sun/webserver7/lib/activation.jar
</server-class-path>
<debug>false</debug>
<jvm-options>
-Xdebug -Xrunjdw:transport=dt_socket,server=y,suspend=n,address=7896
</jvm-options>
<jvm-options>-Djava.security.auth.login.config=login.conf
<jvm-options>-Xms128m -Xmx256m</jvm-options>
</jvm>
<thread-pool>
<max-threads>128</max-threads>
<stack-size>131072</stack-size>
</thread-pool>
<default-auth-db-name>keyfile/default-auth-db-name>
<auth-db>
<name>keyfile</name>
<url>keyfile</url>
<property>
