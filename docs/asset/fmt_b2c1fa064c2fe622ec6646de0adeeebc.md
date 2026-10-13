
`expr` 可以是一个字符串，如果非空则视为真，或者是两个字符串之间的各种比较。可用的比较运算符有 `=`, `!=`, `<`, `<=`, `>`, 和 `>=`。如果第二个字符串的格式为 `/string/`，则字符串将使用正则表达式进行比较。可以使用 `&&`（AND）和 `||`（OR）将多个连接起来。出现在 `if`/`elif`/`else` 指令之间的任何文本都将在生成的页面上显示。

此类流程结构的一个示例如下：

```
<!--#set var="agent" value="$HTTP_USER_AGENT" -->
<!--#if expr="$agent = /Mozilla/" -->
Mozilla!
<!--#else -->
Something else!
<!--#endif -->
```

如果你使用的是在 `USER_AGENT` 字符串中传递 `Mozilla` 作为一部分的浏览器，此代码将显示“Mozilla!”，否则将显示“Something else!”。

## PHP

`PHP` 在某种程度上可以看作是 `CGI` 和 `SSI` 的混合体。它像 `SSI` 一样嵌入在 `HTML` 中，但它提供了完整和丰富的语言特性。`PHP` 的语法主要受 `C` 和 `Perl` 启发。还有几个 `PHP` 特有的功能。它允许开发人员快速设计和编写用于 Web 的应用程序。

你可以用两种方式将 `PHP` 与 `Apache` 一起使用。第一种方法是将其作为以 `CGI` 程序方式运行的脚本引擎使用——与 `Perl` 通常用于 `CGI` 的方式非常相似。另一种方式，也是远为优越的方式，是使用 `mod_php` 方法。这将把 `PHP` 嵌入到 `Apache` 中。因此，在运行应用程序时不会启动 `PHP` 的开销。但是，它会增加 `Apache` 进程的内存占用。

`mod_php` 模块包含在 `Red Hat` 发行版中。你可以使用以下代码片段在你的 Web 中测试它是否已在系统上正确安装。

```html
<HTML>
<HEAD>
<TITLE>Testing PHP</TITLE>
</HEAD>
<BODY>
<H1>Testing PHP</H1>
<P>If you have PHP installed, you'll get a greeting:</P>
<?php print 'Hello world!'; ?>
</BODY>
</HTML>
```

`PHP` 的特性太多，本章无法一一介绍，特别是本章并不是关于编程的。不过，网上有一些优秀的 `PHP` 资源。最好的起点是 `http://www.php.net`。

## 启动和停止服务器

至此，你已经安装并配置好了 `Apache` 服务器，使其符合你的要求。现在是第一次启动它的时候了。

## 手动启动服务器

`Apache` 服务器 `httpd` 提供了若干命令行选项，您可以使用这些选项来设置一些默认值，以指定 `httpd` 读取其配置指令的位置。`Apache` `httpd` 可执行文件支持以下选项：

```text
httpd [-D name][-d directory] [-f file]
     [-C "directive"] [-c "directive"]
     [-v] [-V] [-h] [-l] [-L] [-S] [-t] [-T]
```

`-D` 选项定义一个名称，用于在配置文件中与 `<IfDefine name>` 指令配合使用。这允许您在启动服务器时有条件地包含或排除配置的部分。

`-d` 选项覆盖 `ServerRoot` 目录的位置。它将 `ServerRoot` 变量（`Apache` 服务器安装的目录）的初始值设置为您指定的路径。这个默认值通常从 `httpd.conf` 中的 `ServerRoot` 指令读取。

`-f` 标志指定主配置文件 `conf/httpd.conf` 的位置。它读取并执行启动时在 `ConfigurationFile` 中找到的配置命令。如果 `ConfigurationFile` 不是绝对路径（即不以 `/` 开头），则假定其位置是相对于 `httpd.conf` 中 `ServerRoot` 指令指定的路径。默认情况下，此值设置为 `ServerRoot/conf/httpd.conf`。

`-v` 选项打印 `Apache` 服务器的发展版本并终止进程。

`-V` 选项显示编译服务器时生效的所有设置。

`-h` 选项打印以下服务器使用说明：

```text
Usage: httpd [-D name] [-d directory] [-f file]
              [-C "directive"] [-c "directive"]
              [-v] [-V] [-h] [-l] [-L] [-S] [-t] [-T]

Options:
-D name     : define a name for use in <IfDefine name> directives
-d directory : specify an alternate initial ServerRoot
-f file     : specify an alternate ServerConfigFile
-C "directive" : process directive before reading config files
-c "directive" : process directive after reading config files
-v          : show version number
-V          : show compile settings
-h          : list available command line options (this page)
-l          : list compiled-in modules
-L          : list available configuration directives
-S          : show parsed settings (currently only vhost settings)
-t          : run syntax check for config files (with docroot check)
-T          : run syntax check for config files (without docroot check)
```

`-l` 选项列出编译进您的 `Apache` 服务器的模块。

`-L` 选项列出与编译进您的 `Apache` 服务器的模块配合使用的所有可用配置指令。

`-S` 选项列出服务器的虚拟主机设置。

`-t` 选项非常有用。它对您的配置文件进行语法检查。在修改配置文件后、重启服务器之前，运行此检查是个好主意。进行这样的测试特别重要，因为配置文件中的错误可能导致您在尝试重启时服务器关闭。

`-T` 选项与 `-t` 选项相同，但它不检查配置的文根目录。

### 注意

当您从命令行手动启动服务器时，需要以 `root` 身份进行。主要有两个原因：

- 如果您的独立服务器使用默认 `HTTP` 端口（端口 `80`），只有超级用户才能绑定到 `1024` 以下的互联网端口。

- 只有由 `root` 拥有的进程才能更改其 `UID` 和 `GID`，如 `user` 和 `Group` 指令所指定。如果您在另一个 `UID` 下启动服务器，它将以启动该进程的用户权限运行。

## `/etc/rc.d` 中的 `httpd` 脚本

`Red Hat Linux` 使用 `/etc/rc.d` 目录中的脚本来控制各种服务（包括 `Apache` Web 服务器）的启动和停止。为 `Apache` Web 服务器安装的主要脚本是 `/etc/rc.d/init.d/httpd`，其内容显示在列表 `12.2` 中。

### 注意

`/etc/rc.d/init.d/httpd` 是一个 `shell` 脚本，与位于 `/usr/sbin` 中的 `Apache` 服务器不同。也就是说，`/usr/sbin/httpd` 是程序可执行文件，而 `/etc/rc.d/init.d/httpd` 是一个用于帮助控制该程序的 `shell` 脚本。更多信息请参阅第 `9` 章“系统启动和停止”。

您可以使用以下选项来控制 Web 服务器：

- `start`— 系统使用此选项在启动时启动 Web 服务器。您作为 `root` 也可以使用此脚本来启动服务器。

- `stop`— 系统使用此选项优雅地停止服务器。您应使用此脚本而不是 `kill` 命令来停止服务器。

- `reload`— 您可以使用此选项向 `httpd` 服务器发送 `HUP` 信号，使其在修改后重新读取配置文件。

- `restart`— 此选项是停止并立即重新启动 Web 服务器的一种便捷方式。如果 `httpd` 服务器未在运行，它将启动服务器。

- `condrestart`— 与 `restart` 参数相同，区别在于它仅在 `httpd` 服务器实际运行时才重启。

- `status`— 此选项指示服务器是否正在运行，如果是，则提供服务器每个实例的各种 `PID`。

例如，要检查当前状态，请使用命令
