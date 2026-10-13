
`dnf group remove` 命令不支持排除。如果您不想移除命令输出中列出的所有软件包，最好是逐个恢复目标软件包。

# 160 第 4 章 软件管理

## 更多 dnf 命令

还有许多额外的 `dnf` 相关的命令可用。其中两个命令对于正在准备红帽（Red Hat）考试的人可能特别感兴趣：`dnf config-manager` 和 `dnf download`，它们可以分别显示所有配置设置和下载单个 RPM 包。另一个相关的命令是 `createrepo`，它可以帮助你建立本地存储库。

## 使用 dnf config-manager 查看所有指令

在某种程度上，`dnf.conf` 及相关配置文件中列出的指令仅提供了可用指令的一个小快照。要查看完整的指令列表，请运行 `dnf config-manager --dump` 命令。由于其包含近 100 行内容，请将其通过到分页器（pager）中。图 4-11 所示的 `[main]` 部分节选包含了适用于所有配置存储库的设置。

| 图 4-11 | |
| :--- | :--- |
| `dnf` 指令的部分列表 | `color_update remote = bold,green` |
| | `config_path = /etc/dnf.conf` |
| | `countime = 0` |
| | `debug solver = 0` |
| | `debuglevel = 2` |
| | `defaults = 0` |
| | `deltarm = 1` |
| | `deltarm percentage = 75` |
| | `discludes =` |
| | `diskspace_check = 1` |
| | `enabled = 1` |
| | `enablegroups = 1` |
| | `errorlevel = 3` |
| | `exclude =` |
| | `exclude from weak =` |
| | `exclude from _weak_autodetect = 1` |
| | `excludepkgs =` |
| | `exit_on_lock = 0` |
| | `fastmirror = 0` |
| | `gpgcheck = 1` |
| | `gpgkey_dns view = 0` |
| | `group_package_types = mandatory, default, config` |
| | `history_list = commands` |
| | `history_record = 1` |
| | `history_record_packages = dnf, rpm` |
| | `ignorance = 0` |
| | `includepeps =` |
| | `install_weeps = 1` |
| | `installonly_limit = 3` |
| | `installonlykgs = kernel, KERN-PAE, installonlypkg(kernel), installonlypkg(kernel-module), installonlypkg(vm), multiversion(kernel)` |
| | `installroot = /` |
| | `ip_response = whatever` |
| | `keepcache = 0` |
| | `ocalpkg.gpgcheck = 0` |
| | `log_compress = 0` |

## 依赖与 dnf 命令

表 4-5 来自 `yum-config-manager` 的配置参数

| `dnf` 中的配置指令 | 说明 |
| :--- | :--- |
| 设置为默认；如果设置为 1，`dnf` 将自动进行包的安装和卸载。 |
| `cachedir` | 设置元数据和下载的包文件的目录。 |
| `enablegroups` | 支持 `dnf` 组命令。 |
| `installonlypkgs` | 列出默认包之外不应更新的包，这些通常包含 Linux 内核包。 |
| `installonly_limit` | 标识 `installonlypkgs` 列出的可以同时安装的最大包数。默认值为 3。 |
| `logdir` | 指定存储日志的目录名称，通常为 `/var/log/`。 |
| `pluginconfpath` | 标识插件所在的目录，通常为 `/etc/dnf/plugins`。 |
| `repos sslverify` | 设置为 1，将验证远程 SSL 证书。 |

某些指令没有默认值，某些被排除在外；有些则并不重要，例如颜色指令。表 4-5 显示了其中最重要的一些指令。这并不是一个完整的列表。如果你对未显示的指令感兴趣，那么它不可能是 `dnf.conf` 文件的合适对象。

## 使用 dnf download 下载包

正如建议所示，`dnf download` 命令可从基于 `yum` 的存储库下载包。这是一个非常简单的命令。例如，该命令会检查配置的存储库中是否存在名为 `cups` 的包：

- `dnf download cups`

要么 RPM 包被下载到本地目录，要么命令会返回以下错误信息：

- 没有可用的包 `cups`

有时，需要更具体的细节。如果存储库中存储了多个版本的包，默认值是下载该包的最新版本。这可能不是你想要的。如果你想使用特定版本的 RHEL 9，请使用以下命令：

- `dnf download kernel-5.14.0-284.111.1.el9_2`

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

## 使用 createrepo 创建你自己的存储库

早期版本的 RHEL 6 考试目标建议你应该知道如何“创建私有 `yum` 存储库”。虽然该目标已被移除，但它对于红帽系统工程师来说是一项必要的技能。

自定义存储库可以提供额外的控制。希望控制其 Linux 系统上安装的包的企业可以创建自己的自定义存储库。虽然这基于为发行版开发的标准存储库，但它也可以包含作为组织独特自定义软件的额外包。同样容易地，它可以省略可能违反组织策略的包（例如游戏）。对浏览器等功能的选择限制可以减少对相关软件的需求。

要创建一个自定义存储库，你需要在特定目录中收集所需的包。`createrepo` 命令可以处理该目录中的所有包。数据库会在 `repodata/` 子目录下的 XML 文件中创建。这种包数据库的示例已存在于 RHEL 9 DVD 的 `BaseOS/repodata/` 子目录中。

红帽门户通过相关产品（如 Red Hat Satellite Server）实现对自定义存储库的支持。有关存储库管理的更多信息，请参见

## 认证目标 4.0 模块流 (Module Streams)

正如建议所示，模块流（module stream）可用。RHEL 9 带有两个存储库：BaseOS 和 AppStream。BaseOS 包含了核心操作系统，而 AppStream 包含用户级应用程序，这些以模块的形式打包。RHEL 9 引入了 `dnf` 命令来管理模块流。这解决了 RHEL 7 中软件集合（software collections）解决的问题。事实上，软件集合允许安装同一个应用程序的多个版本，但模块流只允许一个版本。

## 获取模块流的信息

正如本章前面所述，RHEL 9 带有两个存储库：BaseOS 和 AppStream。为了熟悉模块的一些概念，请使用 `dnf list` 命令列出所有模块。图 4-12 显示了输出的一部分。

图 4-12 中的第一列显示模块名称，例如 `nodejs`。第二列 `Stream`（流）显示模块流，即你可以安装的应用程序特定版本。下一列 `Profiles`（配置文件）列出了每个模块流的可用配置文件列表。例如，`postgresql15` 模块流有两个配置文件：`client` 和 `server`。这意味着我们可以通过指定想要安装的配置文件，选择为服务器或为客户端安装 PostgreSQL。

注意，某些配置文件标记为默认值 `[d]`。这意味着如果你在安装时不传递配置文件的名称，`dnf` 默认将安装默认配置文件的 RPM 包。

## 模块流 (*)

幸运的是，红帽将 `nodejs18` 作为模块流分发。一些经验丰富的读者可能注意到，模块流解决了 RHEL 7 中软件集合解决的问题。事实上，软件集合允许安装同一个应用程序的多个版本，但模块流只允许一个版本。

# 图 4-12 列出模块流

```
[root@server1 ~]# dnf module list

Updating Subscription management repositories.

Last metadata expiration check: 1:556:59 Mon 15 May 2023 03:39:39 GMT

Name            Stream           Summary

maquen            3.8  common [d]        project management and project comprehension tool
```
