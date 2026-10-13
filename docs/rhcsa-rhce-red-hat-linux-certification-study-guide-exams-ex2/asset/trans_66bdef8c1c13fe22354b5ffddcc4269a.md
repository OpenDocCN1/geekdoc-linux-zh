
## 更新和安全修复

Red Hat 在 http://rhn.redhat.com/errata/ 维护着一个公开的勘误表列表。此类勘误表按 RHEL 版本分类。如果您拥有 RHEL 订阅，受影响的软件包通常会通过 RHN 提供。您需要做的就是定期运行 yum update 命令。此列表对于使用 RHEL 源代码的第三方很有用，例如 CentOS、Scientific Linux，甚至 Oracle Linux。

## 软件包组和 yum

yum 命令还能做更多。它可以成组地安装和删除软件包。这些组在第 2 章所述的 xml 文件中定义。该文件的一个位置在 RHEL 6 DVD 上，位于 /repodata 子目录中。在大多数这些段的开头，您会看到 <id> 和 <name> XML 指令，它们为每个组列出两个标识符。

但要找到一个软件包组就很费劲了。yum 命令使它更简单。使用以下命令，您可以从已配置的存储库中识别可用的软件包组：

```
# yum grouplist
```

注意组是如何分为已安装组和可用组的。列出的某些组可能特别感兴趣，例如“Remote Desktop Clients”，其中一些您将在第 9 章中使用。要了解有关此组的更多信息，请运行以下命令，输出如 7-10 图所示。

```
# yum groupinfo "Remote Desktop Clients"
```

![](img/9139201cfcaf4292284a0eed074928e5_436_0.png)

注意所有软件包都列为“Optional Packages”。换句话说，它们通常不会随软件包组一起安装。因此，假设您运行以下命令：

```
# yum groupinstall "Remote Desktop Clients"
```

不会安装任何东西。此软件包组中的所需软件包必须明确命名才能使用如下命令进行安装：

```
# yum install rdesktop
```

但可选软件包并不是唯一类别。以下命令列出 Print Server 软件包组中的所有软件包，输出如 7-11 图所示。

```
# yum groupinfo "Print Server"
```

该组中的软件包分为另外两类。Mandatory 软件包始终与软件包组一起安装。Default 软件包通常与软件包组一起安装；但是，在 RHEL 安装过程中未进行更改的情况下，可以使用 -x 开关排除该组中的特定软件包。例如，以下命令安装两个 mandatory 和五个 default 软件包：

```
# yum groupinstall "Print Server"
```

### 图 7-11

Print Server 组中的软件包

```
[root@server1 yum.repos.d]# yum groupinfo "Print Server"
Loaded plugins: refresh-packagekit, rhnplugin
This system is not registered with RHN.
RHN support will be disabled.
Setting up Group Process

Group: Print Server
Description: Allows the system to act as a print server.
Mandatory Packages:
cups
printer-filters
Default Packages:
foomatic-db-ppds
gutenprint
gutenprint-cups
hpijs
paps
[root@server1 yum.repos.d]#
```

相比之下，以下命令将 paps 和 gutenprint-cups 软件包从要安装的列表中排除：

```
# yum groupinstall "Print Server" -x paps -x gutenprint-cups
```

除非有命令可以逆转该过程，否则 yum 命令的选项是不完整的。如名称所示，groupremove 选项会卸载所记录软件包组中的所有软件包：

```
# yum groupremove "Print Server"
```

使用 groupremove 开关时无法排除。如果您不想删除命令输出中列出的所有软件包，最好单独删除目标软件包。

## 更多 yum 命令

有许多额外的 yum 相关命令可用。其中两个可能对准备 Red Hat 考试的人特别感兴趣：yum-config-manager 和 yumdownloader，它们可以显示每个存储库的所有当前设置以及下载单个 RPM 软件包。另一个相关命令是 createrepo，它可以帮助您设置本地存储库。

## 使用 yum-config-manager 查看所有指令

在一定程度上，yum.conf 和相关配置文件中列出的指令仅提供了可用指令的一小部分快照。要查看指令的完整列表，请运行 yum-config-manager 命令。将其通过管道传递给 less 命令作为分页器。它包含 100 行。图 7-12 中所示的 [main] 存储库摘录基于与 RHN 的连接。

yum 的许多指令未填写，例如 assumeyes；有些其实并不重要，例如 color 指令。一些其他重要指令在表 7-5 中显示。这不是一个全面的列表。如果您对未显示的指令感兴趣，它在 yum.conf 文件的手册页中定义。

## 使用 yumdownloader 下载软件包

如名称所示，yumdownloader 命令可用于从基于 yum 的存储库下载软件包。这是一个相当简单的命令。例如，

### 图 7-12

yum 指令的完整列表。

```
diskspacecheck = True
distroverpkg = redhat-release
enable_group_conditionals = True
enabled = True
enablegroups = True
errorlevel = 2
exactarch = True
exactarchlist =
exclude =
failovermethod = priority
gaftonmode =
gpgcheck = True
group_package_types = mandatory,
  default
groupremove_leaf_only =
history_record = True
history_record_packages = yum,
rpm
http_caching = all
installonly_limit = 3
installonlypkgs = kernel,
  kernel-bigmem,
  kernel-enterprise,
  kernel-smp,
  kernel-debug,
  kernel-unsupported,
  kernel-source,
  kernel-devel,
  kernel-PAE,
```

以下命令检查已配置存储库中名为 cups 的软件包的内容。

```
# yumdownloader cups
```

要么 RPM 软件包下载到本地目录，要么命令返回以下错误消息：

```
No Match for argument cups
Nothing to download
```

有时需要更具体的信息。如果存储库中存储了软件包的多个版本，默认情况下会下载该软件包的最新版本。这可能并不总是您想要的。例如，如果您想使用最初发布的 RHEL 6 内核，以下命令将下载内核软件包的原始 RHEL 6 版本：

```
# yumdownloader kernel-2.6.32-71.el6
```

## 表 7-5 来自 yum-config-manager 的配置参数

| yum 中的配置指令 | 描述 |
|---|---|
| alwaysprompt | 在软件包安装或删除时提示确认。 |
| assumeyes | 默认设置为 no；如果设置为 1，yum 会自动进行软件包安装和删除。 |
| cachedir | 设置为数据库和下载的软件包文件的目录。 |
| distroverpkg | 指包含发行版名称的 /etc/redhat-release 文件。 |
| enablegroups | 支持 yum group* 命令。 |
| installonlypkgs | 列出永远不应更新的软件包；通常包括 Linux 内核软件包。 |
| logfile | 指定包含日志信息的文件名，通常为 /var/log/yum.log。 |
| pluginconfpath | 指出插件所在的目录，通常为 /etc/yum/pluginconf.d。 |
| reposdir | 指定存储库配置文件所在的目录。 |
| ssl* | 支持使用安全套接层 (SSL) 进行安全更新。 |
| tolerant | 确定 yum 在更新软件包名称时出错是否停止。 |

## 使用 createrepo 创建自己的存储库

RHEL 6 的 RHCE 目标的早期版本建议您应知道如何“创建私有 yum 存储库”。虽然该目标后来已被删除，但它是 Red Hat 考试的合乎逻辑的未来方向。

自定义存储库可以提供额外的控制。希望控制其 Linux 系统上安装的软件包的企业可以创建自己的自定义存储库。虽然它可以基于为发行版开发的标准存储库，但它可以包含额外的软件包，例如组织特有的自定义软件。同样容易地，它可以省略可能违反组织政策的软件包，例如游戏。对某些功能（如浏览器）的选择限制可以最大限度地减少相关的支持需求。

要创建自定义存储库，您需要在特定目录中收集所需的软件包。createrepo 命令可以处理该目录中的所有软件包。数据库以 XML 文件的形式创建在 repodata/ 子目录中。此软件包数据库的一个示例已存在于 RHEL 6 DVD 的 repodata/ 子目录中。

RHN 通过相关产品（包括 Red Hat Proxy Server 和 Red Hat Satellite Server）支持自定义存储库。更多
