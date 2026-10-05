

```
<!--#set var="agent" value="$HTTP_USER_AGENT" -->
<!--#if expr="$agent = /Mozilla/" -->
Mozilla!
<!--#else -->
Something else!
<!--#endif -->
```

# 启动和停止服务器

此时，你已经安装并按照你的要求配置了 Apache 服务器。
现在是首次启动它了。

# 手动启动服务器

Apache 服务器 (httpd) 有几个命令行选项可用于设置某些默认值，指定 httpd 读取其配置指令的位置。Apache httpd 可执行文件理解以下选项：

```
httpd [-d directory] [-f file]
  -C "directory" -c "directory"
  -v [-V] -h [-l] [-L] [-S] [-t]
```

-d 选项验证 ServerRoot 目录的位置。它将 ServerRoot 变量（Apache 服务器安装的目录）的初始值设置为你指定的路径。此默认值通常从 httpd.conf 中的 ServerRoot 指令中读取。

-f 标志指定主配置文件 `conf/httpd.conf` 的位置。它在启动时读取并执行 `ConfigurationFile` 中找到的配置命令。如果 Configuration 不是绝对路径（不以 / 开头），则其位置被认为相对于 httpd.conf 中 ServerRoot 指令所指定的路径。默认情况下，此值为 `ServerRoot/httpd.conf`。

-v 选项打印 Apache 服务器的开发版本并终止进程。

-V 选项显示服务器在编译时生效的所有设置。

-h 选项打印服务器的以下用法：

```
Usage: httpd [-d directory] [-f file]
  -C "directory" [-c "directory"
```

# 网络与互联网服务
第二部分

[-v] [-V] [-h] [-l] [-L] [-S] [-t]

+   选项列表：
- -D name :为 <IfDef name> 指令定义一个名称
- -d directory : 指定备选的初始 ServerRoot
- -f file : 指定读取配置文件的备选 `ConfigFile`
- -C 'directive' : 在读取配置文件之前处理指令
- -c 'directive' : 在读取配置文件之后处理指令
- -v : 显示版本号
- -V : 显示编译设置
- -h : 列出可用的命令行选项（本页）
- -l : 列出编译的模块
- -L : 列出可用的配置指令
- -S : 显示解析后的设置（目前仅显示主机）
- -t : 对配置文件运行语法测试

-l 选项列出编译到你的 Apache 服务器中的模块。
-L 选项列出你可用的模块所提供的所有配置指令。
-S 选项列出服务器的虚拟主机。
-t 选项非常有用。它对你的配置文件运行语法检查。在修改配置文件并重启服务器之前，运行此检查是一个极好主意。

> 注意事项
当你从命令行手动启动服务器时，需要以 root 身份运行。这有两个主要原因：
- 如果你的独立服务器使用默认 HTTP 端口（80 端口），只有超级用户才能绑定低于 1024 的互联网端口。
- 只有由 root 拥有的进程才能按照 User 和 Group 指令更改其 UID 和 GID。如果你在另一个 UID 下启动服务器，它将以启动进程的用户的权限运行。

# /sbin/init.d 脚本

SuSE 使用 `/sbin/init.d` 中的脚本来控制各种服务的启动和关闭，包括 Apache Web 服务器。为 Apache 服务器安装的主脚本是 `/sbin/init.d/apache`。SuSE 默认的 apache 脚本如列表 11.1 所示。如果你是从源码安装的 Apache，你可能想从 `/usr/local/apache/apachectl` 建立一个指向 `/sbin/init.d/apache` 的符号链接。

> 注意事项
`/sbin/init.d/apache` 是一个 shell 脚本，与位于 `/usr/sbin/httpd` 的 Apache 服务器程序可执行文件不同；`/sbin/init.d/apache` 是帮助控制该程序的 shell 脚本。

在执行 apache 脚本时，可以使用以下选项：

+   - start 系统使用此选项在启动期间启动 Web 服务器。
+   - stop 系统使用此选项优雅停止服务器。
+   - reload 你可以使用此选项向服务器发送 HUP 信号，以重新读取配置文件。
+   - restart 此选项是停止并立即启动服务器的方便方法。
+   - status 此选项显示服务器是否正在运行。

> 注意事项
当你从命令行手动启动服务器时，需要以 root 身份运行。这有两个主要原因：
- 如果你的独立服务器使用默认 HTTP 端口（80 端口），只有超级用户才能绑定低于 1024 的互联网端口。
- 只有由 root 拥有的进程才能按照 User 和 Group 指令更改其 UID 和 GID。如果你在另一个 UID 下启动服务器，它将以启动进程的用户的权限运行。

# 网络与互联网服务
第二部分

# Apache 服务器
第 11 章

# 列表 11.1
（注：原文此处大量重复 Apache 单词，已忽略冗余内容）

