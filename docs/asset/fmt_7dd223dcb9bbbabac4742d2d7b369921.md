
输入你的用户名（如果提示密码）。如果密码通过，远程系统会指示文件已成功复制。同样，`sftp`与支持`ssh`连接的`FTP`服务器启动交互式`FTP`会话。许多具有安全意识的人倾向于使用`sftp`而不是其他`ftp`客户端，因为在你和远程主机之间提供了安全连接。这里有一个示例：

```bash
$ sftp ftp.handansonhistory.com
Connecting to ftp.handansonhistory.com
jake@ftp.handansonhistory.com: password: ********
sftp>
```

此时，你可以开始交互式`FTP`会话。你可以像使用任何`FTP`客户端一样对文件执行`get`和`put`命令，但由于知道自己正在安全连接上工作，会感到很安心。

![](img/d7f79c91d15076e71790c1b4e1d072d0_258_0.png)

`sftp`命令与`ssh`和`scp`一样，要求服务器上运行`sftp`服务。如果你无法使用`sftp`连接`FTP`服务器，则`ssh`服务可能可用。

## 无密码使用 ssh、scp 和 sftp

对于你经常需要访问的机器（特别是位于局域网防火墙后的机器），将它们设置为无需密码即可登录通常非常有帮助。下面的步骤显示了如何操作。

220

## 安全 Linux

这些步骤将引导你设置从一台机器到另一台机器的无密码认证。在这个示例中，本地用户是名为`host1`的计算机上的`chester`。远程用户也是名为`host2`的计算机上的`chester`。

- 1. 登录本地计算机（在本示例中，我以`chester`身份登录）。
- 2. 输入以下内容生成密钥：

```bash
$ ssh-keygen -t dsa
Generating unique key pair.
Enter file in which to save the key: /home/chester/.ssh/id_dsa
Enter passphrase (empty for none):
Enter same passphrase again (empty for none):
Your key has been saved in /home/chester/.ssh/id_dsa
Fingerprint xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx
Public key is now in /home/chester/.ssh/id_dsa.pub
```

- 3. 为了让`sshd`守护进程接受你创建的`authorized_keys`文件，你的主目录以及文件本身必须具有安全的权限。为了确保安全，输入以下内容：

```bash
$ ssh chester@host2 chmod 700 ~/.ssh
$ ssh chester@host2 chmod 600 ~/.ssh/authorized_keys
```

- 4. 输入以下内容将密钥添加到远程服务器：

```bash
$ ssh chester@host2 'cat /tmp/id_dsa.pub >> /home/chester/.ssh/authorized_keys'
```

- 5. 输入以下内容从临时目录恢复密钥：

```bash
$ ssh chester@host2 rm /tmp/id_dsa.pub
```

260

## 第二部分 演示

在之前的步骤中，你被要求输入密码。这没关系。

注意的是，一旦此功能生效，无论你的本地计算机`IP`地址更改多少次，它都将有效。`IP`地址与这种认证形式无关。

## 安全 Linux 服务器

在公网网上将你的`Linux`系统作为服务器开放，会在安全方面带来一系列新挑战。你的计算机不仅要拒绝几乎所有的入站请求，还要预期响应对支持的服务（如`Web`、`FTP`或邮件服务）的请求，提供信息或正确运行此类脚本。

整本书都充满了关于如何保护服务器安全的信息。许多运行在互联网服务器上的企业会分配全职管理员来监控其安全。因此，请将本节视为需要留意的某些攻击类型的概述，以及保护你`Linux`服务器的一些工具。

## 使用 TCP Wrappers 控制服务访问

完全禁用不使用的服务是可以的，但你真正需要的服务呢？你如何有选择性地允许和拒绝这些服务的访问？对于集成`TCP` wrapper支持的`Linux`系统，`/etc/hosts.allow`和`/etc/hosts.deny`文件决定何时为`rsh`、`telnet`、`finger`和`talk`等服务授予或拒绝特定的连接。

大多数`Linux`系统实现`TCP` wrapper是为了一组由名为`Internet`超服务器的单进程监听进程监控的服务。对于`Fedora`和`RHEL`系统，该服务器是`xinetd`守护进程，而在其他系统（如`Debian`）中使用`inet`守护进程。当一个

222

# 加固 Linux

当服务器进程请求依赖`TCP` wrappers的服务时，系统会扫描并检查`hosts.allow`和`hosts.deny`，查找与连接机器`IP`地址匹配的条目。这些检查发生在连接尝试发生时：

- 如果地址列在`hosts.allow`文件中，则允许连接且不检查`hosts.deny`。
- 如果地址在`hosts.deny`中，则拒绝连接。
- 如果地址在两个文件中都不存在，则允许连接。

请记住，对主机进行评估顺序非常重要。例如，你不能在`hosts.deny`文件中拒绝一个已经在`hosts.allow`文件中获得访问权限的主机。

没有必要（甚至不可能）列出所有想要连接到你计算机的地址。`hosts.allow`和`hosts.deny`文件允许你指定地址的子集和组。你可以使用关键字`ALL`指定所有可能的地址。你还可以限制这些文件中的条目，使其仅适用于特定的网络服务。查看一个典型的`hosts.allow`和`hosts.deny`文件对示例。这里是`/etc/hosts.allow`：

```
# hosts.allow This file describes the names of the hosts are
# allowed to use the local INET services, as decided
# by the '/usr/sbin/tcpd' server.

cups-lpd: 199.170.177., .linxtoys.net
vsftpd: ALL
```

这里是`/etc/hosts.deny`：

```
#
# hosts.deny This file describes the names of the hosts which are
# *not* allowed to use the local INET services, as decided
# by the '/usr/sbin/tcpd' server.

ALL: ALL
```

前面的示例是一个相当严格的配置。它允许来自某些主机的`cups-lpd`和`telnet`服务连接，但拒绝所有其他连接。它也允许所有主机连接`FTP`服务 (`vsftp`)。让我们详细解释这些文件。

通常情况下，以`#`字符开头的行是注释，`inetd`在解析文件时忽略它们。每行非注释行由由逗号分隔的守护进程列表组成，后面跟着一个冒号（`:`），然后是逗号分隔的待检查客户端地址列表。在此上下文中，客户端是指任何尝试访问你系统上网络服务的计算机。

## 第二部分 运行演示

客户端条目可以是数字`IP`地址（例如`199.170.177.25`），也可以是主机名（例如`jukebox.linxtoys.net`），但它通常是指定整个地址范围的通配符变体。每个客户端可以四种不同的形式。`hosts.allow`的在线手册页描述如下：

- 带有点（`.`）字符的字符串。如果主机名的最后部分与指定模式匹配，则匹配主机名。例如，`.tue.nl`匹配主机名`wzw.vnin.tue.nl`。
- 以点（`.`）结尾的字符串。如果其数字字段与给定字符串匹配，则匹配地址。例如，`131.155`匹配埃因霍芬科技大学（`Eindhoven University`）网络上的（几乎）每一个主机 (`131.155.-x.x`)。
- 以`@`符号开头的字符串被视为网络组（`netgroup`）。如果主机是指定网络组的主机，则匹配主机名。守护进程或客户端用户不支持网络组匹配。

示例`hosts.allow`包含了第一类客户端规范。条目`199.170.177.`将匹配任何以该字符串开头的`IP`地址，例如`199.170.177.25`。客户端条目`.linxtoys.net`将匹配类似于`jukebox.linxtoys.net`和`picframe.linxtoys.net`的主机名。
