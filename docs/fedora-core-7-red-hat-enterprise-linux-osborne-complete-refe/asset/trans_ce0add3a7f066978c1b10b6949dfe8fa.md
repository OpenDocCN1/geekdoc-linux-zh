
## xinetd 网络安全

出于安全限制，您可以使用 `only_from` 来限制特定远程主机的访问权限。`no_access` 属性拒绝来自所列主机的访问，但允许其他主机访问。这些控制项将 IP 地址作为其值。您可以列出单个 IP 地址、IP 地址范围或网络（使用网络地址）。`instances` 属性限制特定服务可以同时运行的服务器进程数量。以下示例将访问限制在本地网络 192.168.1.0 和 localhost，拒绝来自 192.168.1.15 的访问，并使用 `instances` 属性将同一时间内的服务器进程数限制为 60：

```text
only_from = 192.168.1.0
only_from = localhost
no_access = 192.168.1.15
instances = 60
```

`xinetd` 程序还提供了一些内部服务，包括 `time`、`services`、`servers` 和 `xadmin`：`services` 提供当前活动服务的列表，`servers` 提供有关服务器的信息；`xadmin` 提供 `xinetd` 管理支持。

### xinetd 服务配置文件：/etc/xinetd.d 目录

与其为所有服务使用一个巨大的 `xinetd.conf` 文件，不如将服务配置拆分成多个配置文件，每个服务对应一个。`xinetd.conf` 文件通过 `includedir` 选项指定该目录。在以下示例中，`xinetd.d` 目录保存了像 swat 等服务器的 `xinetd` 配置文件。这种方法的优点在于，只需创建一个新的配置文件即可添加服务。修改某项服务只需编辑其配置文件，而不必编辑整个 `xinetd.conf` 文件。

作为一个示例，`xinetd.d` 目录中的 `swat` 文件展示如下。请注意，它默认是禁用的。

```text
# default: off
# description: SWAT is the Samba Web Admin Tool.\
# Use swat to configure your Samba server. \
# To use SWAT, connect to port 901 with your \
# favorite web browser.
service swat
{
    port            = 901
    socket_type     = stream
    wait            = no
    only_from       = 127.0.0.1
    user            = root
    server          = /usr/sbin/swat
    log_on_failure  += USERID
    disable         = yes
}
```

### 配置服务：xinetd 属性

`xinetd` 服务文件中的条目定义了请求激活的服务器，以及任何选项和安全预防措施。一个条目由针对不同功能定义的一组属性组成，例如服务器程序的名称、使用的协议以及安全限制。每个互联网服务（如服务器）的块之前都有关键字 `service` 以及您想要用于识别该服务的名称。属性块由一对花括号包围。每个属性条目以属性名称开头，后跟赋值运算符（如 `=`），然后是分配的值或值列表。由关键字 **default** 指定的特殊块包含服务的默认属性。语法展示如下：

```text
service <service_name>
{
    <attribute> <assign_op> <value> <value> ...
    ...
}
```

大多数属性采用单个值，使用标准赋值运算符 `=`。某些属性可以接受值列表。您可以使用 `=` 运算符赋值，也可以使用 `=+` 和 `=-` 运算符向这些列表中添加或移除项。使用 `=+` 添加值，使用 `=-` 移除值。您通常使用 `=+` 和 `=-` 运算符向可能在默认块中已分配初始值的属性中添加值。

属性列表见表 21-7。某些属性对于服务是必需的。这些包括 **socket_type** 和 **wait**。对于标准的互联网服务，您还需要提供 **user**（服务的用户 ID）、**server**（服务器程序名称）和 **protocol**（服务器使用的 IPPROTO）。使用 **server_args**，您还可以列出想要传递给服务器程序的参数（这不包括服务器名称）。如果未定义 **protocol**，则使用该服务的默认协议。

#### xinetd 属性

| 属性 | 描述 |
| :--- | :--- |
| log_on_success | 指定服务器启动和停止时记录的信息。您可以指定的信息包括 PID（服务器进程 ID）、HOST（远程主机地址）、USERID（远程用户）、EXIT（退出状态和终止信号）以及 DURATION（服务会话持续时间）。 |
| log_on_failure | 指定无法启动服务器时记录的信息。您可以指定的信息包括 HOST（远程主机地址）、USERID（远程用户的用户 ID）、ATTEMPT（记录失败的尝试）和 RECORD（记录来自远程主机的信息以监控对服务器的访问尝试）。 |
| rpc_version | 指定 RPC 服务的 RPC 版本。 |
| rpc_number | 指定未列出（UNLISTED）RPC 服务的编号。 |
| env | 为服务定义环境变量。 |
| passtenv | 列出从 xinetd 环境传递给服务器的环境变量列表。 |
| port | 指定服务端口。 |
| redirect | 允许将 TCP 服务重定向到另一主机。 |
| bind | 允许将服务绑定到机器上的特定接口。 |
| interface | bind 的同义词。 |
| banner | 当与远程主机建立该服务的连接时，要显示的文件的名称。 |
| banner_success | 当授予对远程主机该服务的连接时，要显示的文件的名称。 |
| banner_fail | 当拒绝与远程主机该服务的连接时，要显示的文件的名称。 |
| groups | 允许访问该服务有权访问的组（是或否）。 |
| enabled | 指定要启用的服务名称列表。 |
| include | 将指定文件的内容作为配置文件的一部分插入。 |
| includedir | 接受 includedir /etc/xinetd.d 形式的目录名。该目录内的每个文件都将按顺序读取为 xinetd 配置文件，组合形成 xinetd 配置。 |

*表 21-7：xinetd 属性*

### 禁用和启用 xinetd 服务

您可以手动打开或关闭服务，或者使用 system-config-services On Demand 面板。通过配置文件中的 **disable** 属性来开启和关闭服务。要启用服务，请将 disable 属性设置为 **no**，如下所示：

```text
disable = no
```

然后您需要重启 **xinetd** 以启动该服务。

```text
# /etc/rc.d/init.d/xinetd restart
```

> **提示** *Red Hat 或 Fedora 在安装 xinetd 时默认会禁用其最初设置的所有服务。要启用特定服务，您需要将其 disable 属性设置为 no。*

若要启用通过 **chkconfig** 进行管理，需要在每个服务段之前放置注释掉的默认值和描述条目。如果使用单独的文件，条目位于每个文件的开头。Red Hat 和 Fedora 已为其随发行版安装的服务（如 **ftp** 和 **SWAT**）提供了这些内容。默认条目可以是开或关。例如，FTP 服务的 **chkconfig** 默认值和描述条目展示如下：

```text
# default: off
# description: The tftp server serves files using the trivial file transfer \
#       protocol. The tftp protocol is often used to boot diskless \
#       workstations, download configuration files to network-aware printers, \
#       and to start the installation process for some operating systems.
```

如果您想要打开一个默认关闭的服务，可以将其 **disable** 属性设置为 **no** 并重启 **xinetd**（或者使用 **system-config-services On Demand** 面板）。**Tftp FTP** 服务器 **tftpd** 的条目展示如下。初始注释告诉您它默认是关闭的，但随后 **disable** 属性将其打开：

```text
service tftp
{
    socket_type       = dgram
    protocol          = udp
    wait              = yes
    user              = root
    server            = /usr/sbin/in.tftpd
    server_args       = -s /tftpboot
    disable           = yes
    per_source        = 11
    cps               = 100 2
    flags             = IPv4
}
```

### TCP Wrappers

TCP wrappers 为 **xinetd** 管理的服务器增加了另一层安全。实际上，服务器被包裹在中间的安全层中，监控连接并控制访问。通过 **xinetd** 建立的服务器连接会被监控，验证远程用户身份并检查他们是否发出有效请求。连接通过 **syslogd** 守护进程记录（见第 27 章），可能位于 **syslogd** 文件（如 */var/log/secure*）中。使用 TCP wrappers，您还可以通过远程主机限制对系统的访问。主机列表保存在 *hosts.allow* 和 *hosts.deny* 文件中。这些文件中的条目格式为 *service:hostname:domain*。域名是可选的。对于服务，您可以指定特定服务（如 FTP），或者输入 **ALL** 代表所有服务。对于主机名，您可以指定特定主机或使用通配符匹配多个主机。例如，**ALL** 将匹配所有主机。表 21-8 列出了可用的通配符。在以下示例中，第一个条目允许所有主机访问 Web 服务 **http**。第二个条目

#### TCP Wrapper 通配符

| 通配符 | 描述 |
| :--- | :--- |
| ALL | 匹配所有主机或服务。 |
| LOCAL | 匹配仅用主机名指定而没有域名的任何主机。用于匹配本地域中的主机。 |
| UNKNOWN | 匹配名称或地址未知的任何用户或主机。 |
| KNOWN | 匹配名称或地址已知的任何用户或主机。 |
| PARANOID | 匹配其主机名与其 IP 地址不匹配的任何主机。 |
| EXCEPT | 允许提供匹配例外的运算符。其形式为 list1 EXCEPT list2，其中在 list1 中匹配且在 list2 中也匹配的那些主机将被排除。 |

*表 21-8：TCP Wrapper 通配符*

