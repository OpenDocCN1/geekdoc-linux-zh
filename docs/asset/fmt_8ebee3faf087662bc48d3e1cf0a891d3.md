
```
# description: The Telnet server serves Telnet sessions; it uses
# unencrypted username/password pairs for authentication.
service telnet
{
    flags           = REUSE
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/in.telnetd
    log_on_failure  += USERID
    disable         = yes
}
```

文件名（在本例中为 `telnet`）可以是任意名称；重要的是文件中 `service` 关键字旁边出现的服务名称。在本例中，行 `service telnet` 告诉 `xinetd` 服务的名称。`xinetd` 使用此名称从 `/etc/services` 文件中查找端口号。要在 `/etc/services` 文件中查找 `telnet`，请键入以下命令：

```
grep "^telnet" /etc/services
```

该命令显示以下行：

```
telnet      23/tcp
telnet      23/udp
telnets     992/tcp
telnets     992/udp
```

列出以 `telnet` 开头的两行显示 `TELNET` 服务的端口号为 `23`。这告诉 `xinetd`，任何到达 `23` 端口的连接请求都是针对 `TELNET` 服务的。配置文件 `/etc/xinetd.d/telnet` 然后告诉 `xinetd` 如何处理这些服务请求。

`/etc/xinetd.d/telnet` 中的属性，用大括号括起来，具有以下含义：

- `flags` 属性提供了关于如何运行 `xinetd` 启动的服务器的具体说明。`REUSE` 标志意味着即使 `xinetd` 重启，服务也会保持运行。请注意，`REUSE` 标志现在被隐式假定为所有服务都已设置。

- `socket_type` 属性设置为 `stream`，这告诉 `xinetd` `TELNET` 服务使用面向连接的 `TCP` 套接字与客户端通信。对于使用无连接 `UDP` 套接字的服务，此属性将设置为 `dgram`。

- `wait` 属性设置为 `no`，这告诉 `xinetd` 为每个请求启动一个新服务器。如果此属性设置为 `yes`，`xinetd` 会等待服务器退出后才再次启动服务器。

- `user` 属性提供了 `xinetd` 用于运行服务器的用户 `ID`。在此情况下，服务器以 `root` 身份运行 `TELNET` 服务器。

- `server` 属性指定为此服务运行的程序。在此情况下，`xinetd` 运行 `/usr/sbin/in.telnetd` 程序以提供 `TELNET` 服务。

- `disable` 属性如果设置为 `yes` 则关闭服务。默认情况下 `disable` 属性设置为 `yes`，`TELNET` 被关闭。

浏览您 `Red Hat Linux` 系统上 `/etc/xinetd.d` 目录中的文件，以了解 `xinetd` 设置为启动的服务类型。其中一些服务，例如 `finger`，会提供入侵者可能用来入侵系统的信息。如果它们尚未被禁用，您可能希望通过在包含所有属性的大括号内放置以下行来关闭这些服务：

```
disable      = yes
```

另一方面，如果您似乎无法使用 `telnet` 连接到 `Red Hat Linux` 系统，请检查 `/etc/xinetd.d` 目录中的相应文件，并确保 `disable` 属性设置为 `no`，或者该行已被注释掉（通过在行首放置 `#` 将代码行更改为不运行的注释）。

当您对 `xinetd` 配置文件进行此类更改时，您必须通过键入以下命令重新启动 `xinetd` 服务器：

```
/etc/init.d/xinetd restart
```

如果您想输入更少的内容，请使用执行完全相同操作的以下命令：

```
service xinetd restart
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_629_0.png)

您还可以使用 `chkconfig` 命令禁用和启用由 `xinetd` 启动的服务。例如，要启用 `TELNET` 服务，以 `root` 身份登录并键入以下命令：

```
chkconfig telnet on
```

要再次关闭 `TELNET`，键入 `chkconfig telnet off`。

## 运行独立服务器

通过 `xinetd` 启动服务器是一种明智的方法，但如果服务必须经常启动，则效率不高。如果 `Web` 服务器由 `xinetd` 控制，您会遇到服务器经常启动的情况，因为每次用户点击网页时，都会为 `Web` 服务发出请求。对于此类高需求服务，最好以独立方式启动服务器，作为守护进程运行——一个持续运行且永不终止的进程。这意味着服务器监听分配的端口，每当请求到达时，服务器通过复制自身来处理它。这样，服务器只要机器在运行就会保持运行——理论上是永远。一种更高效的策略，用于 `Web` 服务器，是运行服务器的多个副本，让每个副本处理部分传入请求。

您可以轻松配置 `Red Hat Linux` 系统以自动启动各种独立服务器。我将在本节中向您展示如何操作。

### 手动启动和停止服务器

要启动未运行的服务，请使用服务器命令。例如，如果 `Web` 服务器（`httpd`）未运行，您可以通过运行以下命令的特殊 shell 脚本来启动它：

```
/etc/init.d/httpd start
```

该命令使用 `start` 作为参数运行 `/etc/init.d/httpd` 脚本。如果 `httpd` 服务器已在运行并且您想停止它，请使用 `stop` 作为参数运行相同的命令，如下所示：

```
/etc/init.d/httpd stop
```

要再次停止并启动服务器，只需使用 `restart` 作为参数：

```
/etc/init.d/httpd restart
```

`Red Hat Linux` 包含另一个名为 `service` 的脚本，它执行相同的任务，但更容易记住。基本上，您可以去掉 `/etc/init.d` 并将其替换为 `service` 后跟一个空格。因此，要启动 `httpd`，您应键入以下内容：

```
service httpd start
```

您能启动和停止的所有服务是什么？答案在 `/etc/init.d` 目录中的文件里。要查看它，请键入以下命令：

```
ls /etc/init.d
```

通过此命令列出的所有文件都是安装在 `Red Hat Linux` 系统上的服务——您可以根据需要启动和停止它们。例如，以下是 `Red Hat Linux` 系统上典型的服务列表：

```
aep1000 functions keytable nfs lock saslauthd tux
anacron gpm killall nscd sendmail vsftpd
apmd halt kudu ntpd single winbind
atd httpd lisa pcmcia smartd xfs
autofs lpd messagebus postgresql smb xinetd
bcm2... iptables named postfix smb xinetd
...
```

这超过 50 个服务！

### 启动时自动启动服务器

您可以使用 `/etc/init.d` 目录中的脚本手动启动、停止和重新启动服务器，但您希望某些服务在启动 `Red Hat Linux` 系统时立即启动。您可以使用 `chkconfig` 命令或图形服务器配置实用程序配置服务器在启动时自动启动。

### 使用 chkconfig 命令

`chkconfig` 程序是用于检查和更新 `Red Hat Linux` 中服务器当前设置的命令行实用程序。各种服务器组合被设置为在不同的运行级别自动启动。每个运行级别代表一种系统配置，其中选定的进程集运行。您通常关心运行级别 `3` 和 `5`，因为运行级别 `3` 用于文本模式登录，运行级别 `5` 用于通过图形界面登录。

`chkconfig` 命令使用简单。例如，假设您想在运行级别 `3` 和 `5` 自动启动 `named` 服务器。您所需要做的就是以 `root` 身份登录并在 shell 提示符下键入以下命令：

```
chkconfig --level 35 named on
```

要查看 `named` 服务器的状态，请键入以下命令：

```
chkconfig --list named
```

您应该会看到类似以下内容的输出行：

```
named 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

输出显示了运行级别 `0` 到 `6` 下 `named` 服务器的状态。如您所见，`named` 被设置为在运行级别 `3` 和 `5` 运行。

如果您想关闭 `named`，可以使用以下命令：

```
chkconfig --level 35 named off
```
