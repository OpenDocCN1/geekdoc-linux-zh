

如果你想要通过 DHCP 配置的网络接口不是 `eth0`，当然，你需要将其替换为你想要配置的设备的实际名称。另一个常见的网络设备名称是 `fxp0`。

如果 `/etc/rc.conf` 中已经存在针对你要配置的设备的一行，且该行包含其他内容，则该设备当前可能配置为使用静态 IP。在这种情况下，你可以删除现有行并用之前提到的行替换它，或者在现有行前添加一个井号（#）将其注释掉，然后添加上面的行。

在对 `/etc/rc.conf` 文件进行此更改后，请重启系统以使新的 DHCP 配置生效。

## The dhclient 程序

`dhclient` 程序是 DHCP 的客户端部分。如果你有任何配置为使用 DHCP 的网络接口，该程序会在每次系统启动时自动运行。

如果需要修改 `dhclient` 的默认行为，可以通过在 `/etc/rc.conf` 中提供选项向该程序传入标志来实现。

如果你确实需要修改 `dhclient` 的默认行为，应在 `/etc/rc.conf` 中配置 DHCP 接口的 `ifconfig` 行下方添加以下行：

```
dhcp_flags="flags"
```

这里，`flags` 是 `dhclient` 的选项列表。表 34.1 展示了可以使用的有效选项。

| 选项 | 操作 |
| :--- | :--- |
| -d | 此选项将强制 `dhclient` 在前台保持运行，而不是在获取配置信息后切换到后台。此选项仅应用于调试目的，且最好不要从 `/etc/rc.conf` 中使用 |
| -cf filename | 默认情况下，`dhclient` 从文件 `/sbin/dhclient-script` 中读取操作系统特定的配置信息。可以使用 `-cf` 选项告诉 `dhclient` 从不同的配置文件中读取，其中 `filename` 是该文件的名称和路径 |
| -lf filename | 默认情况下，`dhclient` 将其租约信息存储在文件 `/var/db/dhclient.leases` 中。可以使用 `-lf` 选项告诉 `dhclient` 使用不同的文件来存储此信息，其中 `filename` 是应存储此信息的文件的名称和路径 |
| -pf filename | 默认情况下，`dhclient` 将其进程 ID (PID) 信息存储在 `/var/run/dhclient.pid` 中。可以使用 `-pf` 选项更改此设置。这里，`filename` 是应使用来存储此信息的文件的名称 |
| -q | 此选项告诉 `dhclient` 运行时保持安静。换句话说，`dhclient` 在打印消息时将不会那么冗长 |
| -1 | 此选项使 `dhclient` 仅尝试一次获取 IP 地址租约。如果失败，`dhclient` 将以状态 2 退出。注意，这是数字 1，而不是小写字母 *l* |

## /sbin/dhclient-script

这是 *dhclient* 的操作系统特定配置文件。你通常不需要对此文件进行任何更改，除非你确定知道自己在做什么，否则最好保持原样。

## /etc/dhclient.conf

这是 *dhclient* 的配置文件，你可以在其中控制其行为的各个选项。该文件必须存在 *dhclient* 才能运行，尽管默认情况下，该文件只包含注释。*dhclient* 具有合理的默认值，这对大多数用户都能正常工作，因此大多数用户无需担心此文件。

然而，你应该了解此文件中可以控制的一些选项。表 34.2 列出了其中的一些。

**表 34.2 部分 `dhclient.conf` 选项**

| 选项 | 操作 |
|:-------|:-------|
| `timeout n` | 这里，*n* 是 *dhclient* 在尝试联系 DHCP 服务器时等待响应放弃并决定服务器不可用之前的秒数。默认情况下，这是 60 秒 |
| `retry n` | 这里，*n* 是如果第一个请求超时，*dhclient* 在尝试再次联系 DHCP 服务器之前等待的秒数。默认情况下，它将等待五分钟 |
| `select-timeout n` | 某些网络可能拥有一个以上的 DHCP 服务器。在这种情况下，客户端可能会收到多个配置信息报价。收到的第一个报价并不总是最佳报价（例如，如果收到的第二个报价包含客户端已有的相同 IP 地址，它比 IP 地址不同的报价更可取）。这里，*n* 是 *dhclient* 在收到第一个报价后等待是否还有其他服务器以报价做出响应的秒数 |
| `reboot n` | 当 *dhclient* 启动时，它会尝试获取上次相同的 IP 地址。如果无法获取相同地址，它将接受不同的地址。这里，*n* 是 *dhclient* 在放弃并决定无法获取上次相同的 IP 地址之前等待的秒数。默认值是 10 秒 |
| `request option` | 客户端将从 DHCP 服务器请求指定选项的信息。有关可用选项的信息，请参阅 `dhcp-options` 手册页 |
| `require option` | 客户端将要求从 DHCP 服务器获取指定选项的信息。如果未提供所需信息，客户端将拒绝该报价。有关可用选项的信息，请参阅 `dhcp-options` 手册页 |
| `default option value` | 如果 DHCP 服务器未提供指定选项的信息，则使用该选项的 `value` 值。有关可用选项的信息，请参阅 `dhcp-options` 手册页 |
| `supersede option value` | 指定选项将始终使用 `value`，即使 DHCP 服务器为该选项发送了不同的值。有关可用选项的信息，请参阅 `dhcp-options` 手册页 |
| `reject address` | 任何从 DHCP 服务器发送的带有 `address` IP 地址的报价都将被拒绝 |

在 `/etc/dhclient.conf` 配置文件中可以使用更多选项。有关此文件中可用选项的更多信息，请参阅 `dhclient.conf` 手册页。此外，有关可从 DHCP 服务器请求或必需的 DHCP 选项的更多信息，请参阅 `dhcp-options` 手册页。

如前所述，大多数用户无需对 `/etc/dhclient.conf` 进行任何更改，因为默认的 `dhclient` 值通常能正常工作。

## DHCP 服务器守护进程

FreeBSD 并不附带运行 DHCP 服务器所需的软件。然而，FreeBSD ports 集合中提供了用于运行 DHCP 服务器的自由软件。该端口称为 `isc-dhcp3`，位于 ports 树的 net 目录中。有关如何安装 ports 的信息，请参阅第 14 章，“安装附加软件”。

此外，一个名为 `dhcpconf` 的程序（也可以在 FreeBSD ports 集合的 net 目录下找到）有助于创建在 FreeBSD 上运行 DHCP 服务器所需的配置文件。

安装 `isc-dhcp3` 后，它会在 `/usr/local/etc/rc.d` 中创建一个名为 `isc-dhcpd.sh.sample` 的启动文件。下次重启系统时，该文件将使 DHCP 服务器在系统启动时自动启动。默认的启动文件对于基本的 DHCP 服务器配置可以正常工作。有关 `dhcpd` 的各种可用选项，请参阅 `dhcpd` 手册页。

你可能希望将 `/usr/local/etc/rc.d` 中的启动文件重命名为更易于记忆和输入的名称。例如，你可以将其命名为 `dhcpd`。假设你已重命名它，现在你可以使用以下命令以 root 身份控制 DHCP 服务器的操作。

第一个命令将启动 DHCP 服务器：

```
/usr/local/etc/rc.d/dhcpd start
```

下一个命令将停止当前正在运行的 DHCP 服务器：

```
/usr/local/etc/rc.d/dhcpd stop
```

最后，此命令将停止并重新启动当前正在运行的 DHCP 服务器：

```
/usr/local/etc/rc.d/dhcpd restart
```

在你第一次启动 DHCP 服务器之前，你需要为其创建一个配置文件。

## 配置 dhcpd 配置文件

DHCP 服务器的配置文件，名为 *dhcp.conf*，位于 `/usr/local/etc` 中。当你安装 *dhcpd* 时，它会在该目录中放置一个示例配置文件，名为 *dhcpd.conf.sample*。

你可以手动配置 *dhcpd.conf* 文件，也可以使用 *dhcpconf* 程序进行配置。如果你从未配置过 *dhcpd*，建议你安装并使用 *dhcpconf* 程序。然后你可以浏览 *dhcpconf* 创建的 *dhcp.conf* 文件，看看该文件的样子。

> **注意**
> 本节中提供的说明应能帮助你完成基本的 DHCP 服务器设置。要进行更高级的配置，请参阅 *dhcpd* 的手册页以及 *dhcpd.conf* 的手册页，后者包含了可以在 *dhcp.conf* 配置文件中配置的所有选项。

## 安装和启动 dhcpconf 程序

*dhcpconf* 是一个由菜单和对话驱动的程序，有助于设置基本的 DHCP 服务器配置。安装后，你可以以 root 身份在命令提示符下输入 *dhcpconf* 来启动它。你会看到一个“关于”对话框，简要介绍该程序。按 Enter 键继续进入主屏幕。图 34.3 显示了 *dhcpconf* 的主屏幕。

