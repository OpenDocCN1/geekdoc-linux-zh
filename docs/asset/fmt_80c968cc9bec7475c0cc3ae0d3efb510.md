
中央邮件中枢中继配置将用于你的服务器，其分配的任务是为你网络中可能的所有本地或邻近客户端及服务器邮件机器发送、接收和中继邮件。本地或邻近客户端服务器指的是所有运行 `Sendmail` 并将所有出邮件发送到中央中枢以便后续交付的其他本地服务器或客户端。这种内部网络从不通过互联网直接接收邮件；相反，所有计算机的邮件都保存在邮件服务器上。为所有计算机使用一个中央邮件中枢是一个好主意；这种架构将限制服务器和客户端的任务管理，并提高你站点的安全性。

你可以配置邻近 `Sendmail`，使其仅接受本地生成的邮件，通过隔离邻近邮件机器来提高安全性。网关服务器（位于防火墙外或作为防火墙的一部分）充当代理，根据其防火墙规则接收从外部进入内部递送的邮件，并将其转发到中央邮件中枢服务器。请注意，网关服务器的配置方式类似于邻近 `Sendmail` 服务器，从不接受来自外部（互联网）的入站邮件。

`openmail.com` 域中的所有邮件仅通过 `openmail.com` 邮件服务器访问。

这是我们书中使用的 `Sendmail` 配置的图形化表示。我们尝试在不同的服务器上展示不同的设置（中央邮件中枢中继、本地或邻近客户端和服务器）。存在许多可能性，取决于你的需求和网络架构。

# 服务器软件（邮件网络服务）

## 第 5 章

这些安装说明假设：

- 命令与 `Unix` 兼容。
- 源码路径为 `/var/tmp/`（也可能是其他路径）。
- 安装已在 `RedHat Linux 6.1` 和 `6.2` 上通过测试。
- 安装过程中的所有步骤将在超级用户权限下进行。
- `Sendmail` 首页：`http://www.sendmail.org`
- `Sendmail` 站点：`[URL 缺失]`

### 软件包

为所有计算机使用一个中央邮件中枢是一个好主意；这种架构将限制服务器和客户端的任务管理，并提高你站点的安全性。

### 压缩包

解压 `tar` 包。

```
tar xzvf sendmail.gz
```

### 配置

步骤 1：编辑配置文件。

```
# define PATH="/usr/bin"
```

步骤 2：编辑配置文件。

```
# define PATH="/usr/bin"
```

### 编译与优化

步骤 1：编辑配置文件。

```
# define PATH="/usr/bin"
```

# 服务器软件（邮件网络服务）

## 第 5 章

此宏选项定义了传递给 `id` 的链接器选项。

`define('CONFMANROOT', '/usr/man/man')`

此宏选项定义了 `Sendmail` 手册页的安装位置。

`define('CONFMANOWN', 'root')`

此宏选项定义了所有安装的 `Sendmail` 手册页的所有者。

`define('CONFMANGRP', 'root')`

此宏选项定义了所有安装的 `Sendmail` 手册页的组。

`define('CONFMANMODE', '644')`

此宏选项定义了所有安装的 `Sendmail` 手册页的模式。

`define('CONFMAN1SRC', '1')`

此宏选项定义了安装在 `confMAN1` 中的手册页的源。

`define('CONFMANSRC', '5')`

此宏选项定义了安装在 `confMAN5` 中的手册页的源。

`define('CONFMAN8SRC', '8')`

此宏选项定义了安装在 `confMAN8` 中的手册页的源。

`define('CONFDEPEND_TYPE', 'CC-M')`

此宏选项指定了如何使用 `Sendmail` 构建依赖项。

`define('CONFNO_HELPFILE_INSTALL')`

此宏选项指定默认不安装 `Sendmail` 帮助文件。一些经验丰富的管理员建议这样做，以获得更好的安全性。

`define('CONFSBINGP', 'root')`

此宏选项定义了所有 `Sendmail` setuid 二进制文件的组。

`define('CONFUBINMODE', '6755')`

此宏选项定义了所有 `Sendmail` setuid 二进制文件的模式。

`define('CONFUBINOWN', 'root')`

此宏选项定义了 `Sendmail` 二进制文件的所有者。

`define('CONFUBGRP', 'root')`

此宏选项定义了 `Sendmail` 二进制文件的组。

`define('CONFEBDIR', '/usr/bin')`

此宏选项定义了从其他二进制文件执行时调用的二进制文件安装位置。在 `RedHat Linux` 上，该路径必须设置为 `/usr/bin` 目录。

第 2 步

现在我们在服务器上编译并安装 `Sendmail`：

```bash
[root@sendmail-8.10.1]# cd sendmail
[root@sendmail]# sh Build
[root@sendmail]# sh Build install
[root@sendmail]# cd ..
[root@sendmail-8.10.1]# cd mailstats
[root@mailstats]# sh Build install
[root@mailstats]# cd ..
```

© Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture ® and OpenDocs Publishing

```bash
[root@deepmail-8.10.1]# cd smrh
root@deep-smrh]## sh Build
root@deep-smrh]## cd
root@deepmail-8.10.1]## cd makemap (仅邮件枢 Hub 配置需要)
root@makemap]## sh Build (仅邮件枢 Hub 配置需要)
root@makemap]## cd
root@deepmail-8.10.1]## cd plaliases (仅邮件枢 Hub 配置需要)
root@plaliases]## sh Build (仅邮件枢 Hub 配置需要)
root@plaliases]## cd
root@deepmail-8.10.1]## ln -fs /usr/bin/sendmail /usr/lib/sendmail
root@deepmail-8.10.1]## chmod 511 /usr/bin/smrh
root@deepmail-8.10.1]## dm -m 755 /var/spool/mqueue
root@deepmail-8.10.1]## chown root:/var/spool/mqueue
root@deepmail-8.10.1]## mkdir /etc/smrh
```

`Build` 命令将在安装到你的系统之前，为 `Sendmail` 需要的不同二进制文件构建并制作必要的依赖项。

如果你使用此命令进行编译，`Build install` 命令将在你的系统上安装 `sendmail`、`mailosts`、`makemap`、`plaliases`、`smrh` 二进制文件以及相应的程序。

`ln -fs` 命令将为 `sendmail` 二进制文件在 `/usr/lib/` 目录中创建一个符号链接。这是必要的，因为某些程序希望在该目录（`/usr/lib`）中找到 `sendmail` 二进制文件。

`install` 命令将在 `var/spool` 下创建一个权限为 `755` 的 `mqueue` 目录。邮件消息可能由于各种原因暂时无法送达。为了确保此类消息最终能够送达，`Sendmail` 将其存储在队列目录中，直到能够成功送达。

`chown` 命令将在你的系统上创建 `/etc/smrh/` 目录。该目录是我们放置所有允许 `Sendmail` 运行管理器的地方。

注意：程序 `makemap` 和 `plaliases` 必须安装在中央邮件枢服务器（Central Mail Hub Server）上；`makemap` 允许你创建类似 `/etc/mail/aliases.db` 或 `/etc/mail/access.db` 的数据库映射。`plaliases` 显示将系统邮件 `/etc/mail/aliases` 文件的内容。由于在网络中最好只有一个地方（如中央邮件枢）来处理和管理所有的 db 文件更好，因此没有必要使用 `makemap` 和 `plaliases` 程序在网络中的任何其他主机上构建 db 文件。

# 配置

本书中描述的所有软件在名为 `floppy.tgz` 的 `tar` 压缩包中都有特定的目录和子目录，其中包含特定程序的配置文件。如果你获得了此存档文件，就不需要手动重现下面不同的配置文件。由于在网络中最好只有一个地方（如中央邮件枢）来处理和管理所有的 db 文件更好，因此没有必要使用 `makemap` 和 `plaliases` 程序在网络中的任何其他主机上构建 db 文件。

# 服务器软件（邮件网络服务）

## 第 5 章

本书中描述的所有软件在名为 `floppy.tgz` 的 `tar` 压缩包中都有特定的目录和子目录，其中包含特定程序的配置文件。如果你获得了此存档文件，就不需要手动重现下面不同的配置文件。无论你手动还是-
