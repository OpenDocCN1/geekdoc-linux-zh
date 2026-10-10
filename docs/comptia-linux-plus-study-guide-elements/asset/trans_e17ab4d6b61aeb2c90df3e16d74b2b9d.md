
还有一种永久禁用服务的方法值得一提：将其从计算机上完全移除。你可以使用包管理系统，或者追踪并删除该程序的二进制文件，以确保服务永不运行。如果计算机确实不需要再运行该程序，这无疑是完成此任务的最佳方式，因为它能节省磁盘空间，并防止因配置错误而不必要地启动不需要的服务器——除非重新安装该服务器。

## 使用超级服务器

超级服务器通常用于启动较小且不常用的服务器。在 Linux 上，有两个广受欢迎的超级服务器：inetd 和 xinetd。你应当了解这两个系统，包括它们的基本配置及相关的安全问题。

务必编辑正确的配置文件！熟悉一种工具的 administrators 在处理使用另一种超级服务器的系统时常常会感到困惑。管理员可能会编辑错误的配置文件，从而发现更改没有生效。理想情况下，系统中不应存在未安装的超级服务器的配置文件，但有时这些文件确实存在，尤其是在发行版升级到改变了超级服务器的新版本时。

## 编辑 inetd.conf 或 inetd.d 文件

你可以通过 /etc/inetd.conf 文件或 /etc/inetd.d 子目录中的文件来控制经由 inetd 启动的服务器。inetd.conf 文件由一系列行组成，每行对应一个服务器。典型的行类似于以下内容：

```
ftp   stream  tcp  nowait  root  /usr/sbin/tcpd /usr/sbin/in.ftpd  -l
```

此及后续的几个示例都引用了 in.ftpd，这是一个曾经相当流行但如今在许多系统上正被其他 FTP 服务器替代的 FTP 服务器。其中一些服务器无法从超级服务器运行，因此在这些情况下使用其他服务器可能行不通。

较新版本的 inetd 支持将 inetd.conf 文件拆分为 /etc/inetd.d 中的多个文件。这种方法使得软件包能够包含相应的配置文件，结果是服务器在安装软件包并重新加载 inetd 后即可立即正常工作；如果软件包提供了必要的文件，在安装服务器后便无需手动编辑 /etc/inetd.conf。为简洁起见，下文提及 inetd.conf，但 /etc/inetd.d 中文件的格式是相同的。

每行由若干个以一至多个空格分隔的字段组成。表 4.1 总结了这些字段的含义。基本格式如下：

*service* *socket* *protocol* *wait*/*no-wait* *user* *server* *parameters*

**表 4.1 inetd 配置文件字段含义**

| 字段 | 含义 |
|---|---|
| *service* | 第一个字段（前例中的 *ftp*）是 */etc/services* 文件中显示的服务名称。 |
| *socket* | 套接字类型条目告知系统预期的连接类型——可靠的双向连接（*sstream*）、开销较低的较低可靠性连接（*dgram*）、网络底层连接（*raw*）或其他各种类型。这些类型之间的差异非常技术性；编辑此条目时，主要关注点应是正确输入服务器文档中指定的值。 |
| *protocol* | 这是所使用的 TCP/IP 协议类型，通常是 *tcp* 或 *udp*。 |
| *wait*/*nowait* | 对于 *dgram* 套接字类型，此条目指定服务器是连接其客户端并释放套接字（*nowait*），还是处理其所有数据包然后超时（*wait*）。使用其他套接字类型的服务器应在此字段中指定 *nowait*。 |
| *user* | 这是用于运行服务器的用户名。*root* 和 *nobody* 用户是常见选择，但也可选择其他用户。 |
| *server* | 这是服务器的文件名。在前面的示例中，服务器指定为 */usr/sbin/tcpd*，即 TCP Wrappers 二进制文件。该程序提供了一些安全检查，使你能根据来源等因素限制对服务器的访问。接下来的部分“控制超级服务器安全”将更详细地介绍 TCP Wrappers。 |
| *parameters* | 服务器名称之后的所有内容都是传递给服务器的参数。如果你使用 TCP Wrappers，则在此字段中传递真实目标服务器（例如 */usr/sbin/in.ftpd*）的名称及其参数。 |

井号（#）是 */etc/inetd.conf* 的注释符号。因此，如果服务器通过 *inetd* 运行且你希望禁用它，可以在行首放置一个井号。如果你想在 *inetd.conf* 中添加服务器，则需要为其创建一个条目。大多数可以通过 *inetd* 运行的服务器都在其文档中包含了示例条目。许多发行版提供的 *inetd.conf* 文件也包含常见服务器的条目，尽管其中许多被注释掉了；移除行首的井号即可激活该服务器。

修改 inetd.conf 后，必须重启 inetd 超级服务器本身。该超级服务器通常作为标准 SysV 服务运行，因此你可以输入类似以下命令来重启它：

```
# /etc/rc.d/init.d/inetd restart
```

或者，你可以让 inetd 重新加载其配置，方法是向 SysV 启动脚本传递 reload 参数而不是 restart。restart 选项会关闭服务器然后再次启动它。当你使用 reload 时，服务器不会停止运行；它只是重新读取配置文件并实施任何更改。实际上，两者非常相似。使用 restart 更有可能正确实施更改，但也更有可能中断现有连接。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_194_0.png)

通常建议在 inetd.conf（如果你使用 xinetd，则为 xinetd 配置文件）中禁用尽可能多的服务器。作为一个通用规则，如果你不了解某个服务器的功能，就禁用它。这将通过消除可能存在 bug 或配置错误的服务器来提高系统的安全性。

## 编辑 xinetd.conf 或 xinetd.d 文件

xinetd（发音为“zi-net-dee”）程序是一个扩展的超级服务器。它提供了 inetd 的功能，以及类似于 TCP Wrappers 的安全选项。发行版正逐渐从 inetd 转向 xinetd，尽管有些仍然默认使用 inetd 或至少将其作为选项提供。如果愿意，你可以在任何发行版上用 xinetd 替换 inetd。

/etc/xinetd.conf 文件控制 xinetd。不过，通常该文件仅包含全局默认选项以及对存储在 /etc/xinetd.d 中的包含文件的引用。每个应通过 xinetd 运行的服务器随后在 /etc/xinetd.d 中安装一个包含其自身配置选项的文件。

无论服务器条目位于 /etc/xinetd.conf 还是 /etc/xinetd.d 中的文件，其内容都与 inetd.conf 文件中的信息类似。xinetd 配置文件将信息分散在多行中，并更明确地标记它们。列表 4.1 展示了一个与之前 inetd.conf 条目等效的示例。此条目提供与 inetd.conf 条目完全相同的信息，只是它不包含对 TCP Wrappers 二进制文件 /usr/sbin/tcpd 的引用。由于 xinetd 包含类似的功能，通常不会将其与 TCP Wrappers 一起使用。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_194_1.png)

接下来的部分“控制超级服务器安全”涵盖了 xinetd 的安全特性。

**列表 4.1：xinetd 配置条目示例**

```python
service ftp
(
    socket_type    = stream
    protocol       = tcp
    wait           = no
    user           = root
    server         = /usr/sbin/in.ftpd
    server_args    = -l
)
```

另一个重要的 xinetd.conf 参数是：disable。如果你在服务器定义中包含 disable = yes 这一行，xinetd 将忽略该条目。许多服务器安装在 /etc/xinit.d 中的启动文件默认将此选项设置为 yes；你必须编辑文件并将该条目更改为 disable = no 才能启用服务器。你还可以通过在主 xinetd.conf 文件的 default 部分的 disabled 行中列出服务器名称来禁用一组服务器，例如 disabled = ftp shell。

与 inetd 一样，在对 xinetd 的配置进行更改后，你必须重启超级服务器。你通过输入类似用于重启 inetd 的命令来完成此操作。与那条命令一样，你可以使用 reload 或 restart，效果类似。例如：

```sh
# /etc/rc.d/init.d/xinetd restart
```

## 控制超级服务器安全

第 12 章“保护 Linux”涵盖了许多 Linux 安全问题。不过，由于此处描述了超级服务器，在此章节中描述它们的安全特性也是合适的。你可以使用名为 TCP Wrappers 的包与任何一种超级服务器配合使用以增强安全性，但它更常与 inetd 一起使用。xinetd 超级服务器在其基本功能集中包含类似于 TCP Wrappers 的功能。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_195_0.png)

尽可能应用冗余的访问控制。例如，你可以同时使用防火墙和 TCP Wrappers 或 xinetd 来阻止对特定服务器的不当访问。这样做有助于防止 bug 和配置错误——例如，如果防火墙配置中出现問題，二级阻断措施通常会阻止入侵者。如果你仔细配置系统，此类访问通常也会留下日志文件消息，你会看到这些消息，从而得知防火墙未正常工作。

## 通过 TCP Wrappers 控制访问

inetd 超级服务器可以与 TCP Wrappers 配合使用。该包使用一个名为 tcpd 的程序。inetd 不再直接调用服务器，而是调用 tcpd，后者执行两项操作：检查客户端是否被授权访问服务器，如果客户端拥有此授权，tcpd 则调用服务器程序。

