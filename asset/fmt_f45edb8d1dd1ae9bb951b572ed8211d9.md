
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

现在该文件将清除屏幕并显示消息“You have successfully logged out。”可以使用许多其他命令，但 `clear` 命令应该包含在，以便注销后移除用户屏幕上的工作。

### 3. 如果从 `.bash_logout` 文件中删除了 `clear` 命令，注销时会发生什么？

# 答案

+ 1. `umask` 参数将被设置为 `000`。
+ 2. 选项是 `-h`。
+ 3. 将显示“You have successfully logged out”行，而不会先清除屏幕。

# 进阶问题

+ 1. `profile` 文件中的 `USER='id -un'` 这一行实现了什么功能？
+ 2. 你如何在命令行提示符中显示日期和时间？
+ 3. `BASH_ENV` 指的是什么？

# 实验 VII
## netstat

### 目的

本实验的目的是结合 `netstat` 工具和 `inetd.conf` 来启动和关闭被认为不必要的服务。

### 理论

`netstat` 应用用于显示当前主机的网络信息，例如网络连接、路由表和接口统计数据。系统管理员可以使用这些信息来确定系统上在使用哪些服务。然后，管理员通过编辑 `inetd.conf` 文件并关闭不需要的服务来配置 `inetd` 守护进程。

`netstat` 工具遵循 Linux 命令的标准格式。然而，由于 `netstat` 可以执行的操作有很多，因此有多种可用选项和格式。关于 `netstat` 工具的更多详细信息可以在 Linux man 页面中找到。

启动 `inetd` 没那么困难。`/etc/rc.local` 通常在启动时运行 `inetd`，它很少从命令行执行。

+ `inetd -di -q <length> <configuration file>`
  - `-d` 开启调试。
  - `-i` 不在后台运行（当从 init 运行时使用）。
  - `-q` 设置 socket 监听队列的大小。

最后一个选项 `<configuration file>` 用于指定 `inetd` 读取其配置信息的文件。默认情况下，该文件为 `inetd.conf`。
接下来的实验练习将讨论如何使用 `netstat` 重新配置系统服务，通过编辑 `inetd.conf` 文件删除该服务，并重启 `inetd` 以显示该服务已不再运行。

### 实验练习

通过以下步骤使用 `netstat` 禁止对 `finger` 服务的访问：

+ 1. 执行 `netstat -p` 并确定 `finger` 服务是否正常工作。
+ 2. 如果你可以访问另一台机器，请使用它对特定用户进行 finger 查询。例如：
  ```
  finger tom@model.starvars.com
  ```
+ 3. 编辑 `inetd.conf` 文件并找到 `finger` 服务的条目。
+ 4. 在 `inetd.conf` 中找到对应于 finger 的条目。该条目现在应该类似于：
  ```
  finger stream tcp nowait nobody /usr/sbin/tcpd /usr/sbin/in.fingerd
  ```
+ 5. 找到 `inetd` 进程的 PID 并向其发送 SIGHUP 信号，让 `inetd` 感知到配置文件的更改。命令是：
  ```
  kill -s SIGHUP <pid of inetd process>
  ```
+ 6. 再次执行 `netstat -p` 检查 `finger` 服务是否正在运行。
+ 7. 从另一台机器执行 `finger` 以确定服务是否已禁用。

### 问题

+ 1. 以下 `inetd.conf` 中的各个字段代表什么含义？
  ```
  finger stream tcp nowait nobody /usr/sbin/tcpd /usr/sbin/in.fingerd
  ```

### 答案

+ 1. `inetd.conf` 文件中的每个条目都有多个字段，表示服务、连接类型（流或数据报）、协议类型（tcp 或 udp）、socket 连接状态、执行该服务时的 ID 以及相应的守护进程。

### 进阶问题

+ 1. 向 `inetd` 守护进程发送 SIGHUP 信号的目的是什么？

# 实验 VIII
## swatch

### 目的

本实验演示了用户有效获取、安装和配置 `swatch` 工具监控日志文件的能力。用户将被配置 `swatch` 来监控位于 `/var/log/` 目录下的消息日志。

### 理论

`swatch` 工具对特定日志执行日志文件监控，如果在文件中发现任何异常条目，将会通知用户。它可以两种模式运行：第一种模式持续监控日志文件，第二种模式允许用户查看日志并退出。对于用户想要监控的每个日志文件，必须设置并配置 swatch，除非日志被记录到中央计算机，否则每台计算机都需设置。尽管可能存在这种不便，但 swatch 可以实时提供可疑事件的通知，并在 GPL 协议下免费分发。

### 获取 swatch

为了本实验，将使用 `swatch 3.0`；此版本可以在其主 FTP 站点 `ftp://ftp.stanford.edu/general/security-tools/swatch/` 找到，或者在任何浏览器中搜索关键词 `swatch 3.0`。找到合适的下载位置后应下载以下项目：

+ FILES
  ```
  swatch-3.0.tar.gz
  ```

FILES 文件包含检索必要的 PGP 密钥的信息。`swatch` 还需要 Perl 模块 `Time:HiRes`, `Date:Calc`, `File:Tail`。如果系统尚未安装这些模块，`swatch` 在调用安装程序时将尝试安装它们。阅读随 `swatch` 下载包一起的所有文档文件是一个良好的习惯。

### 安装

一旦成功下载 `swatch` 分发包，将需要将其解压并从 tar 包中提取。要解压 `swatch` 包，只需输入以下命令：

```
$ gzip -d swatch-3.0.tar.gz
```

接下来，要从 tar 包中提取 `swatch`，输入：

```
$ tar -xf swatch-3.0.tar
```

解压并提取后，移动到 `swatch` 目录。使用 `perl Makefile` 命令安装 `swatch`。为了获取所有所需的 Perl 模块，可能需要多次执行 `perl Makefile`。根据权限限制，用户可能需要 root 权限来安装 `swatch`。对于 Linux 系统，在运行 `swatch` 之前必须编辑文件。如果未这样做，`swatch` 将产生错误或转储。使用编辑器打开文件并将第一行

```
#! /bin/sh -
```

改为

```
#! /usr/bin/perl
```

### 配置

必须配置 `swatch` 以知道在日志文件中查找什么以及采取哪些操作。可以使用命令行选项来增加 `swatch` 的灵活性。用户将指定每个日志配置文件的保存位置、是否持续监控该日志以及何时启动。如前所述，必须为监控的日志创建一个配置文件。

### 命令行选项

`swatch` 的命令行参数格式如下：

```
swatch [options] [input-source]
```

一个用于监控 `/var/log/` 文件的命令示例类似于：

```
swatch -f /var/log/messages -c /usr/local/etc/swatchrc.messages -r 05:00
```

`-f`、`-c` 和 `-r` 是运行 `swatch` 时可以使用的一些命令行参数。`f` 切换到通过 `swatch` 运行 `/var/log/messages` 文件内容以持续监控该文件。`c` 切换将 `/var/log/messages` 文件的配置文件保存到 `/usr/local/etc/swatchrc.messages`。`r` 参数切换到在 `05:00` 完成所有后续操作（如果在 `hh:mm` 字段后省略 A.M. 或 P.M. 则假设使用 24 小时制）。其他命令行选项包括：

```
--input-record-separator=regular_expression
```

根据 `regular_expression` 分隔日志记录。默认是回车。

+ `-help`

此打印关于如何使用 `swatch` 的信息。

```
--dump-script=[filename]
```

这用于调试，并将打印生成的 Perl 代码而不是运行它。

### 编辑 swatch 配置文件

要编辑任何 `swatch` 配置文件，只需使用任何文本编辑器（如 `Vi`、`Emacs` 或 `Pico`）打开该文件。配置文件的每一行（由 `#` 分隔的注释行除外）都是类似于 Perl 正则表达式表达式，表示 `swatch` 在日志文件中查找或匹配的内容。其后面跟着制表符和分隔符，格式如下：

```
/pattern[/,pattern/...] action[action,action,... [[HH:MM]:SS]

[start:length]
```

此表达式允许你查找多个模式，以及当匹配到其中一个模式时 `swatch` 可以采取的多个动作。最后两个字段允许用户控制输出哪一个 `swatch`，并且它们是可选的。这两个字段中的第一个允许用户指定 `swatch` 何时开始，第二个则用于修改重复循环的输出。例如，如果 `swatch` 监控以下文本：
