
如前两个以 `telnet` 开头的项所示，`Telnet` 服务的端口号为 `23`。这表示 `telnet` 被列出在端口 `23` 以处理 `Telnet` 服务请求。

`/etc/xinetd.kb5-telnet` 文件中用大括号括起的属性具有以下含义：

- `flags` 属性提供了关于如何运行 `inetd` 启动的服务器的特定指令。`REUSE` 标志意味着如果重启，该服务将保持运行状态。注意，现在默认认为所有服务都使用 `REUSE` 标志。
- `socket_type` 属性设置为 `stream`，这告诉 `telnet` 服务使用面向连接的 `TCP` 套接字与客户端通信。对于使用无连接 `UDP` 套接字的服务，这将 `dagram`。
- `wait` 属性设置为 `no`，这告诉 `telnet` 为每个请求启动一个新服务器。如果此属性设置为 `yes`，`telnet` 将等待服务器退出后再再次启动。
- `user` 属性提供了 `telnet` 运行服务器时使用的 `UID`。在此情况下，以 `root` 身份运行 `Telnet` 服务器。
- `server` 属性指定了为此服务运行的程序。在此情况下，运行 `/usr/kerberos/sbin/telnet` 程序来响应 `telnet` 服务的请求。
- `log_on_failure` 属性告诉 `telnet` 在无法启动服务器时记录什么。在此情况下，该属性将 `USERID` 标志追加到 `HOST` 的默认设置中（通过 `/etc/xinetd.conf` 中的 `defaults` 块设置）。结果是，如果 `Telnet` 服务失败，`telnet` 将记录请求的远程主机名称以及远程用户的用户 `ID`。
- `disable` 属性如果设置为 `yes` 则会关闭服务。默认情况下，`disable` 属性设置为 `yes` 并被关闭。

`xinetd` 服务器使用 `libwrap` 库（称为 `TCP` wrapper）的功能，为互联网服务提供访问控制机制。`TCP` wrapper 可以保护 `FTP` 和 `telnet` 等其他服务，但在启动服务之前，它会读取 `/etc/hosts.allow` 文件以检查请求服务的的主机是否被允许。如果 `/etc/hosts.allow` 中没有相关内容，`TCP` wrapper 将检查 `/etc/hosts.deny` 文件以查看该服务是否应该被拒绝。如果两个文件都为空，`TCP` wrapper 将允许主机访问请求的服务。您可以在 `/etc/hosts.deny` 文件中放置 `ALE:ALL` 行来拒绝所有主机访问任何内容，然后通过在 `hosts.allow` 文件中列出特定服务来启用其访问（参见相关章节以了解更多关于这些访问控制的内容）。继续。

## 第一部分：设置 Linux

继续

除了通过访问控制（通过 `hosts.allow` 和 `hosts.deny`）提供的访问控制外，您还可以通过配置文件中的以下属性来控制服务：

- `only_from` 属性指定了允许连接的 `IP` 地址列表。
- `no_access` 属性指定了不允许连接的主机。例如，要禁用 `telnet`，写入 `no_access = 192.168.1`。

在 `/etc/xinetd.d` 目录下的文件中，`xinetd` 可以启动哪些服务以及每个服务是如何配置的。

- `cps = 25 30 line xinetd` 允许每个服务最多有 `25` 个连接。如果达到此限制，该服务将关闭 `30` 秒。

每个文件指定了某个服务的属性。如此列表所示，`xinetd` 可以启动两个以上的服务。是否所有服务都已启用，取决于每个配置文件中的设置。

你应该研究 `/etc/xinetd.d` 目录下的文件，以了解 `xinetd` 可以启动哪些服务以及每个服务是如何配置的。您可以通过编辑 `/etc/xinetd.d` 中的服务配置文件来启用或禁用服务（您也可以通过 `chkconfig` 命令执行此任务，如在下文所示）。

以下是 `Fedora Linux` 系统上 `/etc/xinetd.d` 目录下的文件列表：

```
ls /etc/xinetd.d

chargen daytime klogin talkk time-udp

charg-udp uptime-udp eklogin kb5-telnet rsync

cvs echo gssftp kshell time
```

每个文件指定了某个服务的属性。如此列表所示，`xinetd` 可以启动两个以上的服务。是否所有服务都已启用，取决于每个配置文件中的设置。

## 理解 xinetd 配置文件

例如，下面的列表显示了 `/etc/xinetd.d/kb5-telnet` 文件的内容，该文件指定了 `telnet` 服务的 `xinetd` 配置（使用 `Kerberos` 验证用户验证的 `telnet` 版本）：

（此处省略代码块内容，保持原样，见上文翻译）

## 第 6 章：网络设置

如果您使用 `grep` 命令在 `/etc/services` 文件中查找 `telnet`，将会发现以下内容：

（此处省略代码块内容，保持原样，见上文翻译）

```text
telnet      23/tcp
telnet      23/udp
elnet      107/tcp      # Remote Telnet
elnet      107/udp
telnets     992/tcp
telnets     992/udp
```
