
```html
<!--#if expr="test_condition" -->
<!--#elif expr="test_condition" -->
<!--#else -->
<!--#endif -->
```

`expr` 可以字符串（如果非空则视为真），或者两个字符串之间的各种比较。可用的比较运算符有 `=`, `!=`, `<`, `<=`, `>=`。如果第二个字符串具有 `/string/` 格式，则使用正则表达式与字符串比较。多个比较可以使用 `&&` (与) 和 `||` (或) 组合在一起。出现在 `if/else` 指令之间的任何文本将显示在生成的页面上。

这种流结构的示例下：

```html
<!--#set var="agent" value="HTTP_USER_AGENT" -->
<!--#if expr="$agent = /Mozilla/" -->
Mozilla!
<!--#else -->
```

# 配置服务

## 第二部分

其他内容！

```
<!--#endif ---->
```

如果你使用的浏览器在 `USER_AGENT` 字符串中传递了 Mozilla，则此代码将显示 "Mozilla!"，否则将显示 "Something else!"。

# 启动和停止服务器

此时，你已经安装了 Apache 服务器并按照你的要求进行了配置。现在是时候首次启动它了。

## 手动启动服务器

Apache 服务器 `httpd` 有几个命令行选项可以使用，用于设置某些默认值，指定 `httpd` 将读取哪些配置指令。Apache `httpd` 可执行文件理解以下选项：

```
httpd [-d directory] [-f file]
[-C 'directive'] [-c 'directive']
[-v] [-V] [-h] [-l] [-L] [-S] [-t]
```

`-d` 选项会将覆盖 `ServerRoot` 变量的值（Apache 服务器的安装目录）为你指定的任何路径。此默认值通常从 `httpd.conf` 中的 `ServerRoot` 指令读取。

`-f` 标志指定了主配置文件 `conf/httpd.conf` 的位置。它在启动时读取并执行 `ConfigurationFile` 中的配置命令。如果 `ConfigurationFile` 不是绝对路径（不以 `/` 开头），则其位置被认为相对于 `httpd.conf` 中 `ServerRoot` 指令指定的路径。默认情况下，此值被设置为 `ServerRoot/conf/httpd.conf`。

`-v` 选项打印 Apache 服务器的开发版本并终止进程。

`-V` 选项显示服务器编译时生效的所有设置。

用法：`httpd [-d directory] [-f file]`

```
[-C 'directive'] [-c 'directive']
[-v] [-V] [-h] [-l] [-L] [-S] [-t]
```

选项：

- `-d name`：为 `<IfDefine name>` 指令定义一个名称

- `-d directory`：指定备备的初始 `ServerRoot`

- `-f file`：指定一个备的 Server

- `-C 'directive'`：在读取配置文件之前处理指令

- `-c "directive"`：在读取配置文件之后处理指令

- `-v`：显示版本号

- `-V`：显示编译设置

- `-h`：列出可用命令行选项（本页）

- `-l`：列出编译的模块

- `-L`：列出可用的配置指令

- `-S`：显示解析后的设置（目前仅虚拟）

- `-t`：仅对配置文件运行语法测试

`-l` 选项列出了所有编译到你的 Apache 服务器中的模块。

`-L` 选项列出了可用模块提供的所有配置指令。

`-S` 选项列出了服务器的虚拟主机设置。

`-t` 选项非常有用。它对你的配置文件运行语法检查。在修改配置文件后，在重启服务器之前运行此检查是一个好主意。

### 注意

- 当从命令行手动启动服务器时，你需要以 root 身份操作。有两个主要原因：

- 如果你的独立服务器使用默认 HTTP 端口（80 端口），只有超级用户才能绑定低于 1025 的互联网端口。

- 只有属于 root 的进程才能按照 `User` 和 `Group` 指令更改 UID 和 GID。如果你在另一个 UID 下启动服务器，它将以启动进程的用户权限运行。

![](img/fbfff30e42d507bc7531108a281d6cf4_312_0.png)

## /etc/rc.d httpd 脚本

Red Hat Linux 使用 `/etc/rc.d` 目录中的脚本来控制服务的启动和关闭，包括 Apache Web 服务器。Apache Web 服务器安装的主脚本是 `/etc/rc.d/init/httpd`，如列表 9.1 所示。

### 注意

`/etc/rc.d/init/httpd` 是 shell 脚本，与位于 `/usr/sbin` 的 Apache 服务器不同。也就是说，`/usr/sbin/httpd` 是程序可执行文件，而 `/etc/rc.d/init/httpd` 是帮助控制该程序的 shell 脚本。更多信息见第 6 章。

# 配置服务

## 第二部分

你可以使用以下选项控制 Web 服务器：

- `start`：系统在启动期间使用此选项启动 Web 服务器。你作为 root 也可以使用此脚本启动服务器。

- `stop`：系统使用此选项优雅地停止 Web 服务器。你应该使用此脚本而不是 `kill` 命令来停止服务器。

- `reload`：你可以使用此选项向 http 服务器发送 HUP 信号，使其在修改后重新读取配置文件。

- `restart`：此选项是停止并立即启动 Web 服务器的方便方法。

- `status`：此选项指示服务器是否正在运行，如果是，它会提供每个服务器实例的各种 PID。

例如，要检查当前状态，请使用以下命令：

`/etc/rc.d/init.d/httpd status`

```
打印
httpd (pid 8643 8642 6510 6102 6101 6100 6099 6323 6322 6098 6097 6096
- 095 362 6094 6093) is running...
```

这表示 Web 服务器正在运行：事实上，有 16 个服务器正在运行。

> 提示

如果你对各种配置文件进行了更改，`reload` 选项通过让系统简单重新读取配置文件来节省停止和启动服务器的时间。如果你需要知道 PID，`status` 命令可以提供该信息。此外，系统将 PID（以及许多其他 PID）保存在位于 `/var/run` 的文件中。

# 列表 9.1 /etc/rc.d/init.d/httpd

```
#!/bin/sh
## Apache Web 服务器的启动脚本
#
# chkconfig: 345 85
# description: Apache 是万维 Web 服务器。用于提供 \
# HTML 文件和 CGI。
```

# Apache 服务器

第 9 章

# 配置服务

## 第二部分

```
<!--#endif ---->
```
