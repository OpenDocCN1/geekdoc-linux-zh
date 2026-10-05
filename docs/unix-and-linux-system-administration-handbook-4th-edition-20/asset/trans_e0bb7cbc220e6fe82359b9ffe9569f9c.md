

# 使用 JumpStart 进行网络安装

规则文件的语法简单但强大。系统可以通过网络、主机名、型号、域名或许多其他属性进行标识。以下规则文件为 192.168.10.0 网络上的系统指定了一个配置，为具有 2–4 GiB 内存的 SPARC 系统指定了另一个配置：

```
network 192.168.10.0 - profile_a -
arch sparc && memory size 2048-4096 begin profile end
```

在网络示例中，没有自定义脚本，使用的是名为 `profile_a` 的安装配置。另一个示例脚本调用了 `begin` 和名为 `profile_b` 的配置。

配置文件同样简单。关键词（有许多）指定了文件和安装类型。一个示例配置可能如下：

```
install_type initial_install
system_type standalone
partitioning default
filesys any 512 swap
cluster SUNWPCall # Specify size /swap
```

`initial_install` 从纯净状态开始，而不是执行升级。此配置使用了磁盘分区方案。`cluster SUNWPCall` 行识别要安装的软件包“安装组”在这种情况下，是所有可用的 Solaris 包。

`sysidcfg` 文件预配置了安装的其他方面，由格式所示的行组成

```
keyword=value
```

关键词不区分大小写，且除 `network_interface` 关键词外只能使用一次。如果一个关键词出现多次，则只有第一个实例生效。

某些关键词依赖于其他关键词，并括在花括号中。除非指定了相应的父（独立）关键词，否则无法使用这些依赖关键词。下一页的表 12.2 列出了独立关键词。

作为 `sysidcfg` 的替代方案可以通过 DHCP 或 DNS 等网络服务指定有限的预配置选项。然而，我们推荐使用 `sysidcfg`，因为替代路径提供的选项有限。

以下 `sysidcfg` 示例配置了一个有一个网络接口的系统。

- + 1. 在 Google 搜索“Custom JumpStart and Advanced Installations”以访问 Sun 的指南，其中包含了规则文件和配置文件的完整细节。

## 表 12.2 JumpStart syscidcfg 文件的独立关键词

| 关键词 | 指定的内容 |
|---|---|
| keyboard | 键盘布局和语言 |
| name_service | NIS、DNS 或 LDAP 的服务配置 |
| network_interface | 连接详情：主机名、IP 地址等 |
| nfs4_domain | 用于 NFS 版本 4 的域 |
| root_password | 加密的 root 密码 |
| security_policy | Kerberos 网络身份认证 |
| service_profile | 可用的网络服务 |
| system_locale | 系统语言 |
| terminal | 终端类型 |
| timeserver | 网络日期和时间服务器 |
| timezone | 系统时区 |

```
keyboard=US-English
system_locale=en_US
timezone=US/Mountain
terminal=sun-cmd
timeserver=time.nist.gov
name_service=DNS [domain=solaris.booklar.atrust.com]
name_server=192.168.2.10
search=atrust.com,booklar.atrust.com]
nfs4_domain=dynamic
root_password=m4QPFOWNY
network_interface=e1000g0 [hostname=sake
default_route=192.168.10.254
ip_address=192.168.10.155
netmask=255.255.255.0]
```

如果你将 `syscidcfg` 文件分发给许多客户端，则系统之间的 IP 地址需要不同。你可以省略网络接口详情，以强制它们在系统首次启动时进行配置。或者，为了从 DHCP 获取网络地址而不是静态分配，请使用行
`network_interface=e1000g0 (dhcp)`

设置好规则文件、`sysidcfg` 文件后，将它们全部拷贝到 `/jumpstart/config` 目录并运行 `sun check` 以验证配置。check 脚本应该在 config 目录下运行，并且是强制性的；检查一个规则文件以证明 JumpStart 文件在语法上是可以接受的。不要跳过。

```
solaris $ cp /jumpstart/config/* /jumpstart/config/
solaris $ check
rules file is syntactically acceptable
```

## 使用自动安装程序进行网络安装

在过程结束时，你的 `/jumpstart/config` 应该像这样：

```
solaris $ ls -l
```

AI 通过自动化配置简化了该过程。在这种情况下，我们使用 `addadm` 创建一个新服务。

