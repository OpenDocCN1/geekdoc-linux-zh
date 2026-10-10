
这些测试非常重要，因为配置文件错误可能导致你在尝试重启服务器时服务器关闭。

# 注意

如果你从源码构建并安装 Apache，且不使用 Fedora 的 Apache RPM 文件，请手动以 root 身份从命令行启动服务器（例如在测试时）。你这样做有两个原因：

- 独立服务器使用默认的 HTTP 端口（端口 80），只有超级用户才能绑定 1024 以下的互联网端口。
- 只有由 root 拥有的进程才能更改 Apache 的 User 和 Group 指令所指定的 UID 和 GID。如果你在另一个 UID 下启动服务器，它将以待启动进程用户的权限运行。

请注意，尽管下面的一些示例展示了如何以 root 身份启动服务器，但你应在构建和安装 Apache 后仅出于测试目的这样做。如果你使用 Fedora RPM 文件安装 Apache，Fedora 被设置为以 apache 用户运行 web 服务。

# 使用 /etc/rc.d/init.d/httpd

Fedora 使用 /etc/rc.d/init.d 目录中的脚本来控制各种服务的启动和停止，包括 Apache web 服务器。为 Apache web 服务安装的主要脚本是 /etc/rc.d/init.d/httpd，尽管实际工作是由随 Apache 附带的 apachectl shell 脚本完成的。

# 注意

/etc/rc.d/init.d/httpd 是一个 shell 脚本，与位于 /usr/sbin 的 Apache 服务器不同。也就是说，/usr/sbin/httpd 是程序可执行文件（服务器）；/etc/rc.d/init.d/httpd 是一个使用另一个 shell 脚本 apachectl 来控制服务器的 shell 脚本。参见第 11 章，了解 /etc/rc.d/init.d 下一些服务脚本的描述以及如何利用这些脚本来管理诸如 httpd 之类的服务。

你可以使用 /etc/rc.d/init.d/httpd 脚本及以下选项来控制 web 服务器：

- **start** — 系统使用此选项在启动时启动 web 服务器。作为 root，你也可以使用此脚本来启动服务器。
- **stop** — 系统使用此选项优雅地停止服务器。你应该使用此脚本而不是 kill 命令来停止服务器。
- **reload** — 你可以使用此选项向 httpd 服务器发送 HUP 信号，使其在修改后重新读取配置文件。
- **restart** — 此选项是停止并立即启动 web 服务器的一种便捷方式。如果 httpd 服务器未运行，则会启动它。
- **condrestart** — 与 *restart* 参数相同，除了只有在 *httpd* 服务器实际运行时才重启该服务器。
- **status** — 此选项指示服务器是否正在运行；如果是，则提供服务器每个实例的各种 PID。

例如，要检查服务器的状态，请使用命令

```
# /etc/rc.d/init.d/httpd status
```

这为我打印出以下内容：

```
httpd (pid 15997 1791 1790 1789 1788 1787 1786 1785 1784 1781) is running...
```

这表明 web 服务器正在运行；事实上，在此配置中当前有 10 个服务器实例正在运行。

除上述选项外，*httpd* 脚本还提供以下功能：

- **help** — 打印 *httpd* 脚本的有效选项列表（这些选项会被传递给服务器，就像从命令行调用一样）。
- **configtest** — 对服务器配置的简单测试，如果设置正确则报告状态为 *OK*。你也可以使用 *httpd* 的 *-t* 选项执行相同的测试，如下所示：

```
# httpd -t
```

- **fullstatus** — 显示详细的状态报告。
- **graceful** — 与 *restart* 参数相同，除了首先使用 *configtest* 选项且未中止打开的连接。

如果你正在对各个服务器配置文件进行大量更改，请使用 *reload* 选项。这可以通过让系统简单地重新读取配置文件来节省停止和启动服务器的时间。

## 使用 Fedora 的 *service* 命令控制 Apache

你可以使用 Red Hat 的 *service* 命令来启动、停止和重启 Apache，而不是直接调用 */etc/rc.d/init.d/httpd* 脚本。*service* 命令与服务的名称（列于 */etc/rc.d/init.d* 下）和可选的关键字一起使用：

例如，你可以将 `service` 与 `httpd` 以及上一节中讨论的任何选项一起使用，如下所示：

```
# service httpd restart
```

如果 Apache 正在运行，这会重启它；如果未运行，则启动服务器。

# 使用 Fedora 的 chkconfig 命令控制 Apache

`chkconfig` 命令提供基于命令行的界面来访问 Fedora 的 `service` 脚本。该命令可用于列出和控制哪些软件服务在特定系统状态（如启动时、重启或关闭时）和运行级别（如单用户模式、多任务网络或带 X 的图形登录）下被启动、重启和停止。

例如，要查看系统的当前设置，请使用 `grep` 命令查看在系统初始化表 `/etc/inittab` 中定义的 Fedora 默认运行级别：

```
# grep id:/etc/inittab
id:3:inittab:default:
```

此示例显示该 Fedora 系统启动到基于文本的登录而不运行 X11。然后你可以使用 `chkconfig` 命令查看 Apache 在该运行级别下的行为：

```
# chkconfig --list|grep httpd
httpd   0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

在这里可以看到 Apache 在运行级别 3 和 5 下是关闭的（在默认的 Fedora 系统中只有这两个实用运行级别，尽管你可以为 Apache 创建自定义的运行级别 4）。使用 `--level`、`httpd` 和控制关键字 `on` 来设置 Apache 在启动到运行级别 3 时自动启动：

```
# chkconfig --level 3 httpd on
```

然后你可以再次使用 `chkconfig` 来验证此设置：

```
# chkconfig --list|grep httpd
httpd   0:off 1:off 2:off 3:on 4:off 5:off 6:off
```

要让 Apache 也在系统启动到图形登录时启动，再次使用 `level`、`httpd` 和控制关键字 `on`，但这次指定运行级别 5，如下所示：

```
# chkconfig --level 5 httpd on
```

再次，要验证你的系统设置，请使用以下命令：

```
# chkconfig --list | grep httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

使用 off 关键字来阻止 Apache 在特定运行级别启动。

## Apache 的图形界面配置

Apache 的一些基本行为可以通过 Red Hat 的 `system-config-httd` 进行配置，这是 X 窗口系统的一个 GUI 工具。这是一种简单的方式来配置设置，例如 Apache 的用户和组名、PID 和进程锁文件的位置，或性能设置（如最大连接数），而无需手动编辑配置文件。

> #### 注意
> 如果你使用 `system-config-httd`，你不应该尝试手动编辑 `httpd.conf` 文件。如果你再次使用 `system-config-httd`，手动更改将被 GUI 客户端覆盖！

通过在你的 X 桌面面板的 Server Settings 的 HTTP Server 菜单项中或通过 X 终端窗口中的命令行启动此客户端，如下所示：
$ `system-config-httd` &
按下 Enter 后，你会被要求输入 `root` 密码。然后你会看到图 17.1 中所示的主要客户端窗口。

![](img/34e72348d53ca54c2a1d9c871316691b_393_0.png)

**图 17.1** `system-config-httd` 的主对话框提供了访问 Apache web 服务器基本配置的功能。

在 Main 选项卡中，你可以设置服务器名称，指示将发送给 webmaster 的邮件发往何处，并设置 Apache 使用的端口。如果需要，你还可以配置特定的虚拟主机以监听不同的端口。

### 配置虚拟主机属性

在 Virtual Hosts 选项卡中，你可以配置每个虚拟主机的属性。Name 列表框包含在 Apache 中运行的所有虚拟主机的列表。通过打开 Virtual Hosts Properties 对话框（如图 17.2 所示）来编辑虚拟主机。你通过在 Virtual Hosts 选项卡的 Name 列表框中高亮显示虚拟主机的名称，然后单击选项卡右侧的 Edit 按钮来完成此操作。使用 Virtual Hosts Properties 对话框中的 General Options 项来配置基本的虚拟主机设置。

![](img/34e72348d53ca54c2a1d9c871316691b_394_0.png)

**图 17.2** `system-config-https` 的 Virtual Host Properties 对话框提供了访问配置 Apache 虚拟主机属性的众多选项。

单击此对话框的 General Options 列表中的 Site Configuration 列表项以设置默认值，例如当 URL 中未指定文件时默认加载哪些文件（默认为 `index.*`）。

General Options 窗格中的 SSL 列表项提供了访问用于启用或禁用 SSL、指定证书设置以及定义 SSL 日志文件名和位置的设置的权限。选择 Logging 列表项以访问配置错误消息记录位置以及传输日志文件存储位置及其记录信息的选项。

