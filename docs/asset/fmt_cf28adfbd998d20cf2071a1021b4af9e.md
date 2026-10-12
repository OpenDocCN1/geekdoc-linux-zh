
confCF Version 命令向版本名称中添加内容。

```
define(`confCF_VERSION', `Submit') #
```

这添加了操作系统类型，类似于 `sendmail.mc` 中的 `OSTYPE('linux')` 命令。

```
define(`__OSTYPE__') # 一个为了防止 proto.m4 报错而使用的临时变通
```

DECNET 是旧式大型机和微型计算机上常见的网络类型。

```
define(`_USE_DECNET_SYNTAX_', `1') # 支持 DECentet
```

`confTIME_ZONE` 变量添加时间戳。

```
define(`confTIME_ZONE', `USE_TZ') #
```

此设置避免了在 NIS 列表中查找用户和密码；用户名和密码的替代源是 `/etc/passwd`。如果你为网络设置了 NIS（见第 23 章），可以通过在行首添加 `#` 来注释掉此行。

```
define(`confDONT_INIT_GROUPS', `True') #
```

这设置了进程标识符（PID）文件的位置。

```
define(`confPID_FILE', `/var/run/sm-client.pid') #
```

`confDIRECT_SUBMISSION_MODIFIERS` 变量假设使用标准的“规范”主机名。

```
define(`confDIRECT_SUBMISSION_MODIFIERS', `C') #
```

## 设置 POSTFIX

`use_ct_file` FEATURE 读取 `/etc/mail/trusted-users` 用于标准用户。

```
FEATURE(`use_ct_file') #
```

# 如果你仅使用 IPv6，将 [127.0.0.1] 更改为 [IPv6::1]

此项指定了本地计算机（127.0.0.1）上的消息提交程序（msp）。

```
FEATURE(`csp', `[127.0.0.1]') #
```

在大多数情况下，你不需要更改此文件中的任何内容；如果需要更改，请记住先备份！

## 处理并重新激活 sendmail

如果你还没有这样做，现在是备份当前 `sendmail.cf` 配置文件的绝好时机。一旦你完成了所需的更改，将希望使用 `make -C /etc/mail` 命令创建新的 `sendmail.cf` 和 `submit.mc` 配置。然后，使用以下命令重启 sendmail 守护进程。

```
# -C /etc/mail
# service sendmail restart
```

除非安装了 `sendmail-cf-*` RPM，否则这些命令将不起作用。当然，你可能希望确保在下次启动 Linux 时，在适当运行级别通过如下命令启动 sendmail：

```
# chkconfig --level 35 sendmail
```

# 设置 Postfix

当你安装 Red Hat Linux Mail Server 软件包组时，你会得到两个不同的邮件服务器。sendmail 服务器更流行且文档更详尽。然而，你会发现 Postfix 更容易配置。配置文件存储在 `/etc/postfix` 中，与 `sizeof` 类似。

要配置 Postfix，你可以编辑 `main.cf` 配置文件中的几项设置。如果这样导航更方便，则没有对应的映射文件。该服务包含在 `postfix` RPM 中。

> 注意：这源自关于 Postfix 的全面讨论；它包含了在 Red Hat Linux 3 上运行此服务所需的元素。更多信息，请访问 www.postfix.org。

## 基础文件和包

为了正常配置，你唯一需要的 RPM 是 `postfix-*` RPM，它是作为 Mail Server 软件包组的一部分默认安装的。你可以使用第 10 章描述的 Red 软件包管理工具安装该组。或者，你也可以直接安装 RPM。

Postfix 不仅仅包含基础配置文件 `main.cf`。在 `/etc/postfix` 目录下还有许多配置文件，如下处所示。你可能会注意到许多的

# 第 21 章：邮件服务

文件可以帮助你处理用户、电子邮件地址和域名的更改。通常，在第一次使用 Postfix 之前，你只需要编辑 `main.cf`，可能还需要 `access` 和 `aliases`。

- **aliases**：用户替换符；大多数服务用户被重定向到 root。你可能希望发送给 root 的邮件是你的管理员邮箱。它与 sendmail 相同。如果你选择使用 `/etc/aliases`，请相应调整 `main.cf` 中的 `alias_map` 和 `alias_database` 变量。
- **access**：允许此文件中的网络，包括 localhost 和你的局域网；可以使用 CIDR 符号或适当的域名，例如 `.example.com`。

## 示例配置

为了设置 Postfix，我们将修改以下变量：

1. 如果你的域名是 `example.com` 且网络地址为 `192.168.1.0`，你可以使用：

```
mydomain = example.com
mynetworks = 192.168.1.0
```

2. 如果你的域名是 `example.com`，你可以使用：

```
mydomain = example.com
mynetworks = example.com
```

3. 默认情况下，`main.cf` 允许 Postfix 仅监听本地计算机。激活并禁用以下项：

```
#inet_interfaces = all
inet_interfaces = localhost
```

4. 最后，使用 `mynetworks` 变量通过 CIDR 符号指定局域网和 IP 地址。这里是我的局域网示例：

```
mynetworks = 192.168.1.0/24, 127.0.0.0/8
```
