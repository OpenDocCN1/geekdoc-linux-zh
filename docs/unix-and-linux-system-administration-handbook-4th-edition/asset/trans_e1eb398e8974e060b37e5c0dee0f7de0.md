

## 表 12.2 JumpStart sysidcfg 文件的独立关键字

| Keyword | What it specifies |
|---|---|
| keyboard | 键盘布局和语言 |
| name_service | NIS、DNS 或 LDAP 的名称服务配置 |
| network_interface | 网络连接详情：主机名、IP地址等 |
| nfs4_domain | 用于 NFS 版本 4 的域 |
| root_password | 加密的 root 密码 |
| security_policy | Kerberos 网络身份验证 |
| service_profile | 可用的网络服务 |
| system_locale | 系统语言 |
| terminal | 终端类型 |
| timeserver | 网络日期和时间服务器 |
| timezone | 系统时区 |

```
keyboard=US-English
system_locale=en_US
timezone=US/Mountain
terminal=sun/cmd
timeserver=time.nist.gov
name_service=DNS {domain_name=solaris.booklab.atrist.com
name_server=192.168.2.10
search=atrist.com,booklab.atrist.com}
nfs4_domain=dynamic
root_password=m4Q POWNY
network_interface=e1000g0 {hostname=sake
default_route=192.168.10.254
ip_address=192.168.10.15
netmask=255.255.255.0}
```

如果你将同一个 sysidcfg 文件分发给许多客户端，IP地址当然需要在系统之间有所不同。你可以省略网络接口详情以强制在系统首次启动时进行配置。或者，要从 DHCP 而不是静态分配获取网络地址，请使用以下行

```
network_interface=e1000g0 {dhcp}
```

在设置好规则文件、sysidcfg 文件和你的配置文件后，将它们全部复制到 /jumpstart/config 目录并运行 Sun 的检查工具，该工具会验证配置。检查脚本应从 config 目录运行，其使用是强制性的；它会创建一个 rules.ok 文件，向 JumpStart 证明文件在语法上是可接受的。不要跳过此步骤，否则 JumpStart 将无法工作。

```
solaris$ sudo cp /jumpstart/s10sparc/Solaris_10/Misc/jumpstart_sample/check /jumpstart/config
solaris $ sudo ./check
Validating rules...
Validating profile profile_A...
The custom JumpStart configuration is ok.
```

在配置过程结束时，你的 /jumpstart/config 目录应如下所示：

```
solaris$ ls -l
-rw-r--r-- 1 root root 52152 Aug 23 19:42 check
-rw-r--r-- 1 root root 413 Aug 23 19:29 profile_a
-rw-r--r-- 1 root root 48 Aug 23 19:13 rules
-rw-r--r-- 1 root root 62 Aug 23 19:43 rules.ok
-rw-r--r-- 1 root root 314 Aug 23 17:35 sysidcfg
```

你必须将每个通过 JumpStart 设置的客户端添加到安装服务器；这是一个两步过程。首先，将客户端的 MAC 地址添加到服务器的 /etc/ethers 文件中。其次，运行 add_install_client 工具将客户端添加到配置数据库，如下所示：

```
solaris$ cd /jumpstart/s10sparc/Solaris_10/Tools
solaris$ sudo /add_install_client -c server:jumpstart sake sun4v
```

在这种情况下，名为 sake 的客户端将使用主机 server 上的 JumpStart NFS 共享进行安装。你可以从 OBP 提示符开始客户端的实际网络安装：

```
ok boot net - install
```

这个复杂的过程以消耗一些脑细胞为代价，实现了高度定制化和灵活的安装。

## 使用 Automated Installer 进行网络安装

OpenSolaris 开发人员评估了 JumpStart 的复杂性，并决定为 OpenSolaris 创建一个新的部署工具。该工具 Automated Installer 在多种方式上模仿了 JumpStart 的风格，但通过一个名为 installadm 的便捷工具抽象掉了部分复杂性。在最简单的形式下，服务器安装现在可以用单个命令完成。开始使用 AI 所需的所有文件都包含在 SUNWinstalladm-tools 软件包中。

AI 服务器提供一个或多个“安装服务”，每个服务代表一个操作系统安装选项，并在启动时通过多播 DNS 被客户端发现。不同的服务可能满足不同的安装需求；例如，一个服务用于特定站点的 Web 服务器，另一个用于数据库服务器。

一旦客户端找到安装程序，它就会搜索与系统描述匹配的配置或清单。客户端使用清单文件中的数据执行安装。无需客户端配置，尽管如果需要，可以提供自定义客户端安装。

AI 服务器安装将所有必要部分捆绑在一个便捷的包中，包括 DHCP 和 TFTP 服务。在将这些服务添加到网络之前，请务必与你的网络管理员确认。

