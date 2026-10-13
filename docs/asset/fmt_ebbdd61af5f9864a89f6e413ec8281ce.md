
```
tar xzvf nessus-libraries-1.0.7a.tar.gz
tar xzvf libnasl-1.0.7a.tar.gz
tar xzvf nessus-core-1.0.7a.tar.gz
tar xzvf nessus-plugins-1.0.7a.tar.gz
```

这些命令没有提取 `nessus-libraries`、`nessus-core` 和 `nessus-plugins` 目录中的所有源代码。软件版本为 `1.0.7a`。

2. 切换 `nessus-libraries` 目录并运行 `./configure && make && make install`。

3. 添加 `/etc/ld.so.conf`。

4. 切换 `libnasl` 目录并运行 `./configure && make && make install`。

5. 切换 `nessus-core` 目录并运行 `./configure && make && make install`。

6. 切换 `nessus-plugins` 目录并运行 `./configure && make && make install`。

# 配置 NESSUS

Nessus 配置存储在 `/usr/local/etc/nessus`。一旦启动扫描，你会看到每个主机的图形状态。扫描完成后，会出现报告窗口显示所有结果。对于每个主机，你都有一份详细报告，它还指出了解决方案和/或常见漏洞披露（CVE）标识。

# 使用 NESSUS 进行扫描

按照以下步骤配置 Nessus：

1. 从命令行运行 `nessus`。

2. 使用之前创建的用户名/密码登录。

3. 选择你想要执行的安全检查插件。要了解更多检查信息，点击插件名称将显示更多信息。某些插件可能要求在插件级别输入额外信息。

5. 点击 `Target` 按钮定义目标系统。切换 `nessus-core` 目录并运行 `./configure && make && make install`。对于高级隐身检测模式，`PortSentry` 列出了它不监听的端口。这是一种反向绑定。

现在查看当另一个主机尝试连接受监控端口会发生什么，请执行以下操作：

1. 在运行 `PortSentry` 的系统上运行 `tail -f /var/log/messages`。

2. 从网络中另一个不在 `portsentry.ignore` 列表中的主机，连接到受监控的端口，并观察 `PortSentry` 机器上的日志窗口。

# 第 V 部分：防火墙

- 4. 对于高级模式，你可以 `telnet` 到任何被排除的端口以触发警报。如果你断开连接并尝试再次 `telnet`，你会发现目标系统已不可用。

要让 `PortSentry` 在每次启动系统时运行，请在 `/etc/rc.d/rc.local` 脚本中添加以下行。别忘记将模式参数更改为六种模式之一。

```
/usr/local/psionic/portsentry mode
```

# 使用安全扫描器

安全扫描器是一个客户端/服务器审计工具。

- 服务器 `nessusd` 负责审计。
- 客户端 `nessus` 通过 X11/GTK+ 界面或命令行与用户交互。

# 编译并安装 NESSUS

以下是安装和运行此扫描器的方法。

- 1. 成为 root 用户。从 http://www.nessus.org 下载四个文件的最新版本：`nessus-libraries-version.tar.gz`、`libnasl-version.tar.gz`、`nessus-core.version.targz` 和 `nessus-plugins.tar.gz`。你必须按此顺序编译。使用 `tar xzvf filename.tar.gz` 命令提取每个文件：

```
tar xzvf nessus-libraries-1.0.7a.tar.gz
tar xzvf libnasl-1.0.7a.tar.gz
tar xzvf nessus-core-1.0.7a.tar.gz
tar xzvf nessus-plugins-1.0.7a.tar.gz
```

这些命令没有提取 `nessus-libraries`、`nessus-core` 和 `nessus-plugins` 目录中的所有源代码。软件版本为 `1.0.7a`。

- 2. 切换 `nessus-libraries` 目录并运行 `./configure && make && make install`。
- 3. 添加 `/etc/ld.so.conf`。
- 4. 切换 `libnasl` 目录并运行 `./configure && make && make install`。
- 5. 切换 `nessus-core` 目录并运行 `./configure && make && make install`。
- 6. 切换 `nessus-plugins` 目录并运行 `./configure && make && make install`。

# 配置 NESSUS

Nessus 配置存储在 `/usr/local/etc/nessus`。一旦启动扫描，你会看到每个主机的图形状态。扫描完成后，会出现报告窗口显示所有发现。对于每个主机，你都有一份详细报告，它还指出了潜在解决方案和/或常见漏洞披露（CVE）标识。

# 使用 NESSUS 进行扫描

按照以下步骤配置 Nessus：

- 1. 从命令行运行 `nessus`。
- 2. 使用之前创建的用户名/密码登录。
- 3. 选择你想要执行的安全检查插件。要了解更多检查信息，点击插件名称将显示更多信息。某些插件可能要求在插件级别输入额外信息。

# 使用 Strobe

`Strobe` 是一个高速 TCP 端口扫描器。你可以从 http://www.insecure.org/nmap/scanners 下载。一旦下载了源码分发，可以在新的 `strobe` 子目录中提取并运行 `make install`。你可以从此目录使用 `./strobe hostname -f` 命令运行 `strobe`。例如：

```
strobe nano.nitec.com -f
```

# 第五部分：防火墙

之前的命令以快速模式 `-f` 扫描名为 `nano.nitec.com` 的主机。

以下是示例输出：

```
strobe 1.03 (c) 1995 Julian Assange (proff@suburbia.net),
nano.nitec.com echo         7/tip Echo [95,JBP]
nano.nitec.com discard      9/tip Echo Discard [94,JBP]
nano.nitec.com daytime     13/tip Daytime [93,JBP]
nano.nitec.com qtdt        17/tip Quote of the Day [100,JBP]
nano.nitec.com charger     19/tip tytyst Source Generator
nano.nitec.com ftp          21/tip File Transfer [Control] [96,JBP]
nano.nitec.com smtp        25/tip Simple Mail Transfer [102,JBP]
nano.nitec.com nameserver 42/tip Host Server [99,JBP]
nano.nitec.com domain      53/tip Domain Server [81,PM1]
nano.nitec.com kerberos   88/tip Kerberos [BCN]
nano.nitec.com loc-srv     135/tip Location Service [JXP]
nano.nitec.com netbios-ssn 139/tip NETBIOS Session Service [JBP]
nano.nitec.com ldap        389/tip Lightweight Directory Access Protocol
nano.nitec.com microsoft-ds 515/tip spooler (lpd)
nano.nitec.com nterm       1026/tip remote_login network_terminal
nano.nitec.com irc-serv     6666/tip Internet relay chat server
nano.nitec.com afs3-bos   7007/tip basic oversee process
```

你还可以使用 `-s` 选项生成扫描统计数据。

# 使用日志监控和分析工具

日志在发现安全问题方面非常有价值。通常黑客在进入之前会进行多次失败尝试。有时我见过黑客持续多天的失败尝试，在任何人进入之前，我们需要修复一个或多个安全问题。监控日志并使用工具分析日志是一项很好的安全措施。在这里我将讨论日志监控和分析工具。

# 使用 logcheck 检测异常日志记录
