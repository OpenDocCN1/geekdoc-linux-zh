
# 第 6 章 软件安装与管理

如果你不信任你的软件包源，可以考虑自动下载所有更改的软件包但不安装它们。使用 `apt --download-only` 选项来请求此行为，然后手动检查并安装你想要更新的软件包。下载的软件包被放在 `/var/cache/apt/` 中，随着时间的推移这个目录可能会变得非常大。使用 `apt-get autoclean` 清理此目录从未使用的文件。

## yum: 用于 RPM 的发布管理

`yum`（Yellowdog Updater, Modified）是一个基于 RPM 的元软件包管理器。将 `yum` 称为 APT 的克隆可能有点不太公平，但它们在主题和实现上是相似的，尽管在实践中 `yum` 更整洁但速度更慢。

在服务器端，`yum-arch` 命令从一组软件包（通常是整个发布版本）编译出头文件信息数据库。然后，该头文件数据库随软件包通过 HTTP 共享。客户端使用 `yum` 命令来获取和安装软件包；`yum` 会处理依赖关系限制，并完成安装请求包所需的任何额外工作。如果请求的包依赖于其他包，`yum` 也会下载并安装这些包。

`apt` 和 `yum` 之间的相似性延伸到了它们支持的命令行选项。例如，`yum install` 会下载并安装 foo 包的最新版本（如果有必要，还有其依赖项）。然而，至少存在一个危险的区别：`apt update` 刷新 `apt` 的包缓存，而 `yum update` 会更新系统上的每个软件包（它类似于 `apt upgrade`）。更增加混乱的是，`yum upgrade` 等于启用了过时处理的 `yum update`。

除非包含通配符字符（如 `*` 和 `?`）来显式请求此行为，否则 `yum` 不会对包名进行匹配。例如，`yum update lib*` 会刷新所有以 "lib" 开头的包。记住给通配符加上引号，以免 shell 干扰它们。

与 `apt` 不同，`yum` 默认在每次运行时根据网络仓库的内容更新其包信息。使用 `-C` 选项防止验证，并使用 `yum makecache` 更新本地缓存（运行需要一段时间）。遗憾的是，`-C` 选项并没有提高 `yum` 的缓慢性能。

正在开发的 DNF 是 Fedora 的默认包管理器，并将完全取代 `yum`。DNF 具有更好的依赖解析能力和改进的 API 等功能。访问 dnf.baseurl.org 了解更多信息。

`yum` 的配置文件是 `/etc/yum.conf`。它包含了通用选项和软件包仓库的指针。可以同时激活多个仓库，且每个仓库可以与多个 URL 关联。

## FreeBSD 软件管理

FreeBSD 在几个版本中一直拥有软件包设施，但现在才开始过渡到完全以包为中心的发行模型，其中核心操作的大部分软件元素都被定义为包。FreeBSD 最近的发布将软件分为三大类：

- “基础系统”，包括一组捆绑的核心软件和工具

- 一组用 `pkg` 命令管理的二进制包

- 一个独立的“ports”系统，用于下载源代码、应用 FreeBSD 特有的补丁并进行编译

从 FreeBSD 11 开始，这些领域之间的界限变得更加模糊。基础系统已经包化，但将基础系统作为一个单元管理的旧方案仍然存在，因此软件包既可以作为二进制包也可以作为 ports 安装，结果基本相同，但对未来的更新有不同影响。然而，交叉覆盖并不完全；某些内容只能作为 port 或包安装。

FreeBSD 12 的项目定义之一是将系统果断地转向通用包管理。基础系统和 ports 可能都会以某种形式继续存在（目前还过早判断结果将如何），但未来的方向是明确的。

因此，请尽可能使用 `pkg` 管理附加软件。除非你没有包化的版本或需要自定义编译选项，否则请避免使用 ports。

大型 UNIX 的另一个奇特遗迹是 FreeBSD 坚持包是“本地”的，尽管它们是由 FreeBSD 编译并作为官方包仓库的一部分发布的。软件包将二进制文件安装在 `/usr/local` 下，大多数配置文件以 `/usr/local/etc` 结尾而不是 `/etc`。

## 基础系统

基础系统作为一个单元进行更新，在功能上与任何附加包不同（至少在理论上如此）。基础系统维护在 Subversion 仓库中。你可以在 svn.freebsd.org 浏览源码树，包括所有的分支。

定义了几个开发分支：

- `CURRENT` 分支仅用于活跃开发。它是第一个接收新功能和修复的分支，没有经过用户社区的广泛测试。

- `STABLE` 分支定期更新旨在下一个主要版本的改进。它包含新功能，但维护了包的兼容性并经过了一些测试。它可能会引入错误或破坏性更改，仅建议给冒险者使用。

- `RELEASE` 分支在达到发布目标时从 `STABLE` 分叉出来。它保持基本静态。`RELEASE` 的唯一更新是安全修复和严重错误修复。官方的 ISO 镜像源自 `RELEASE` 分支，而该分支是唯一建议用于生产系统的分支。

运行 `freebsd-update` 命令使你的系统保持最新包更新。获取更新和安装更新是独立的操作，但你可以将两者合并为一条命令：

```
$ sudo freebsd-update fetch install
```

此命令检索并安装最新的基础二进制文件。它仅适用于 `RELEASE` 分支；`STABLE` 和 `CURRENT` 分支不构建二进制文件。你可以使用相同的工具在系统的不同版本之间升级。例如：

```
$ sudo freebsd-update -r 11.1-RELEASE upgrade
```

## pkg: FreeBSD 包管理器

`pkg` 直观且快速。它是安装未包含在基础系统中的软件最简单的方法。使用 `pkg help` 快速查阅可用的子命令，或使用 `pkg help` 命令显示特定子命令的菜单。表 6.2 列出了一些最常用的子命令。

当使用 `pkg install` 安装时，`pkg` 会咨询本地包目录，从 FreeBSD.org 仓库下载请求的包。软件包被安装后，注册在位于 `/var/db/pkg/local/sqlite` 的 SQLite 数据库中。注意不要删除此文件，否则将无法跟踪已安装哪些包。使用 `pkg backup` 子命令创建数据库备份。

`pkg version` 是一个比较包版本的子命令，具有特殊的语法。它使用 `=`, `<`, 和 `>` 字符来显示当前包、旧于最新可用版本的包或新于当前版本的包。使用该命令列出有更新的包：

```
freebsd$ pkg version -vIL
dri-11.2.2,2      needs updating (index 13.0.4,2)
gbm-11.2.2         needs updating (index 13.0.4)
harbuzz-1.4.1     needs updating (index 13.0.4)
libEGL-11.2.2      needs updating (index 13.0.4)
```

### 表 6.2 示例 pkg 子命令

| 命令 | 功能 |
|---|---|
| `pkg install -package` | 安装时不询问任何“你确定吗？” |
| `pkg backup` | 制作软件包数据库备份 |
| `pkg info` | 列出所有已安装包 显示包的扩展信息 |
| `pkg search -i package` | 搜索包仓库（忽略大小写） |
| `pkg audit -F` | 显示具有已知安全漏洞的包 |
| `pkg which file` | 移除哪个包拥有命名文件 |
| `pkg autoremove` | 移除未使用包 |
| `pkg delete package` | 卸载软件包（同 `remove`） |
| `pkg clean -ay` | 移除 `var/cache/pkg` 中的缓存包 |
| `pkg update` | 更新本地包目录副本 |
| `pkg upgrade` | 将包升级到最新版本 |

此命令将所有已安装的包与索引 (-I) 进行比较，寻找不是 (-L) 当前版本 (=) 的包，并打印详细信息 (-v)。

`pkg search` 查找包比 Google 更快。例如，`pkg search` 可以找到所有名称中包含 "dns" 的包。搜索词是正则表达式，因此你可以搜索类似 `pkg search ^apache` 的内容。详情见 `pkg help`。

## ports 集合

FreeBSD ports 是 FreeBSD 可以从源码构建的所有软件集合。初始化 ports 树后，你将在 `/usr/ports` 的分类目录下找到所有可用软件。要初始化 ports 树，请使用 `portsnap` 工具：

```
freebsd portsnap fetch extract
```

要用一条命令更新 ports 树，请使用 `ports fetch update`。

下载元数据需要一些时间。下载包含了所有 ports 的源码指针，以及与 FreeBSD 相关的补丁。元数据安装完成后，你可以搜索并构建安装任何需要的软件。
