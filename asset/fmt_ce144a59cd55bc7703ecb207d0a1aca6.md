
```
# yum install madwifi
Setting up Install Process
Parsing install arguments
fedora            100% |================| 2.1 kB 00:00
atrpms           100% |=========| 951 B 00:00
Reading repository metadata from local files
primary.xml.gz    100% |================| 2.5 MB 00:04
```

```
Transaction Summary
=================
Install 4 Package (s)
Update 0 Package (s)
Remove 0 (s)
Total download size: 17M
Is this ok [y/N]: y
Downloading Packages
```

从这个示例中可以看出，`yum` 为当前的 Fedora 版本检查了两个不同的软件仓库，Fedora 和 `atrpms` 软件包。在列出依赖项后，`yum` 询问是否安装它们。输入 `y`，软件包及其所有依赖项都将被安装。

某些软件包（包括上一个示例中的 `madwifi` 软件包）需要安装与你运行的内核相匹配的版本。因此，安装此类软件包可能会带带一个更新的内核包。

## 第 5 章：访问与运行应用程序 197

### 使用 yum 本地安装包

如果你想使用 `yum` 安装本地系统中可用的 RPM 包（通过插入 Fedora DVD 或将 RPM 复制到本地目录），你可以可以使用 `yum` 的 `localinstall` 选项。如果你插入了本书附带的 Fedora DVD（假设它已挂载在 `/media/disk`），你可以输入以下命令来安装 `gftp` 软件包：

```bash
# yum localinstall /media/disk/Fedora/Packages/gftp-*
yum localinstall /media/disk/Fedora/Packages/gftp-2.0.18-7.fc9.rpm
```

解析依赖关系

--> 运行事务检查

--> 包 `gftp.i386` 1:2.0.18-7.fc9 设置为更新

依赖关系已解决

| 架构 版本 | 存储库 | 大小 |
|---|---|---|---|

| `gftp` `i386` | 1:2.0.18-7.fc9 | `/media/disk/Fedora/Packages/gftp-2.0.18-7.fc9.rpm` | 946 k |

正在安装:

`gftp` `i386` 1:2.0.18-7.fc9 `/media/disk/Fedora/Packages/gftp-2.0.18-7.fc9.rpm` 946 k

| 事务摘要 | |
|---|---|

| 安装 | 1 个包 |
| 更新 | 0 个包 |
| 移除 | 0 个包 |

总下载大小为: 946 k

是否执行此操作？ [y/N]: y

使用 `yum localinstall` 而不是 `rpm` 命令安装 RPM 包的一个良好理由是，`yum` 会检查你正在安装的包是否依赖于已安装的其他任何包。如果 `yum` 发现需要其他包，它将搜索你配置的所有 `yum` 存储库（至少是 Fedora Fedora 存储库）来下载并安装你需要的内容。

在这个示例中，`yum` 发现 `gftp` 不需要任何额外的包。在提示符处输入 `y` 仅安装了该软件包。

### 使用 yum 列出软件包

除了下载和安装新的 RPM 包之外，`yum` 还可以列出可用的软件包以及已安装的软件包。以下示例说明了 `yum` 的一些用法。

如果你想查看从已配置的存储库中可以下载的软件包列表，请输入以下命令：

```bash
# yum list | less
```

末尾添加 `less` 命令可以让你滚动查看软件列表（取决于你指向的存储库，列表可能会很长）。如果你尝试安装一个包但失败并提示类似“package needs xyzfile (not provided)”的信息，你可以使用 `provides` 选项检查提供缺失文件的包：

```bash
# yum provides missingfile
```

使用 `provides` 选项，`yum` 将在你的存储库中搜索你输入的任何内容（而不是 `missingfile`），并返回它找到的包含该内容的任何包名。

要在存储库中搜索特定字符串描述，请使用 `search` 选项。例如，以下命令在任何包描述中搜索“arcade”（此搜索将找到一些结果）：

```bash
# yum search arcade
```

由于 `yum` 包在安装后不会被自动删除，你可能偶尔需要清理它们。要清除 `/var/cache/yum` 目录子目录下的包，请输入：

```bash
# yum clean packages
```

如果你想清除从主 Fedora 存储库之外的存储库中安装的 RPM 包，可以使用 `list` 选项。以下是一个示例：

```bash
# list extras
```

正在设置存储库
从本地文件读取存储库元数据
额外包
`AdobeReader_enu.i386`
`flash-plugin.i386` 9.0.48-release installed

该列表包含了 Acrobat（我从 Adobe 网站获取的），它在显示 PDF 文件方面做得很好。另一个包用于在 Firefox 浏览器中运行 Flash 插件。注意，此列表包含了你系统配置的、 Fedora 之外的存储库中的所有包（例如，如果配置了 Livna，它将列出从 Livna 安装的包）。

### 使用 yum-utils 软件包

`yum-utils` 软件包中包含了几种实用工具，用于处理 `yum` 存储库和管理软件包。要获取这些工具，请输入以下 `yum` 命令：

```bash
# yum install yum-utils
```

这些工具提供了多种清理存储库、在不安装的情况下获取包以及执行不同查询类型的方法。以下是一些示例：

- `package-cleanup` — 检查本地 RPM 数据库中的依赖问题和不需要的包。选项包括 `--problems`（检查 RPM 数据库中的依赖问题）、`--orphans`（列出在任何存储库中都不可用的包）和 `--kernels`（移除旧内核和内核-devel 包）。在运行 `--oldkernels` 时可以添加 `--keepdevel` 以保留相关的内核-devel 包。

- `repopulse` — 检查远程存储库的依赖问题。默认情况下，它会检查你机器的存储库。对于特定的存储库，使用 `-r avoid` 选项（从存储库的 `/etc/repos.d` 文件的第一行获取 avoid 内容）。其他选项包括 `-c file`（使用包含存储库的不同文件）或 `-a arch`（指定要为该存储库检查的基础架构）。注意，此命令消耗大量内存且运行可能需要很长时间。

- `yumdownloader` — 在不安装的情况下下载包。这在你想将包移动到另一台没有互联网的机器时非常有用。

- `repoquery` — 查询有关包的信息。它类似于 `rpm`，但提供了更强大的搜索选项。

- `queryform` — 查询包并以自定义格式输出。

- `needs-repoquery` — 检查哪个存储库提供了包的依赖。

- `provides-repoquery` — 查找哪个存储库提供了特定文件。

- `yum-manager` — 从 RPM 包目录创建新的存储库。

- `yum-creat` — 更新存储库的元数据。

# 202 第二部分：使用 Fedora 和 RHEL

注意：请注意，仓库中的所有包都会出现在左侧窗格显示的组中。因此，如果你认为某个包位于已启用的仓库中，但无法找到它，请使用查找框按其名称进行搜索。

“添加/删除软件”窗口如图 5-2 所示。在本示例中，在搜索 `xfce` 并在右列显示所有包含该术的包后，我选择了其中一个包。在右下角，可以看到包的描述、它包含的完整文件列表，以及该包依赖的或依赖它的任何包。

![](img/6a8f767dda2519b458f97c2e7f586576_243_0.png)

图 5-2：使用 PackageKit 添加/删除软件窗口获取额外的软件包。

## rpm 命令

用于处理 RPM 软件包文件的命令是 `rpm`。要管理 RPM 包，`rpm` 命令提供了多种选项，可以列出所有已安装包、将现有包升级到新版本，以及查询包的信息（例如软件包包含的文件或文档）。还有一个 `verify` 选项，用于检查组成包的所有文件是否存在且未被更改过。

`rpm` 命令具有以下操作模式：

- install (-i)

- upgrade (-U)

- freshen (-F)

- query (-q)

- verify (-V)

- signature check (--checksig)
