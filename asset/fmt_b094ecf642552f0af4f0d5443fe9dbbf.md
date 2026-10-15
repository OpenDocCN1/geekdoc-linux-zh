
# Debian 软件包与 RPM 软件包不兼容

Debian 软件包与 RPM 软件包不兼容，但两种包类型的操作原理是相同的。像 RPM 一样，Debian 软件包包含依赖信息，Debian 软件包工具维护已安装软件包的数据库等。你使用 `dpkg` 命令来安装 Debian 软件包。该命令的语法与 `rpm` 类似：

```
dpkg [options][action] [package-files][package-name]
```

要执行的动作已在表 2.4 中总结。选项（表 2.5）修改操作的行为，类似于 `RPM` 的选项。

### 表 2.4 `dpkg` 主要动作

| 动作 | 说明 |
| :--- | :--- |
| `-i` 或 `--install` | 安装软件包 |
| `--configure` | 重新配置已安装的软件包：运行安装后脚本以设置特定站点选项 |
| `-r` 或 `--remove` | 移除软件包但保留配置文件 |
| `-P` 或 `--purge` | 移除软件包，包括配置文件 |
| `--get-selections` | 显示当前安装的软件包 |
| `-p` 或 `--print-avail` | 显示已安装软件包的信息 |
| `-I` 或 `--info` | 显示未安装软件包文件信息 |
| `-l` `pattern` 或 `--list` | 列出所有名称匹配 `pattern` 的已安装软件包 |
| `-L` 或 `--listfiles` | 列出与软件包相关的安装文件 |
| `-S` `pattern` 或 `--search` | 查找拥有 `pattern` 指定文件的 |
| `-C` 或 `--audit` | 搜索部分安装的软件包并建议处理方式 |

### 表 2.5 微调 `dpkg` 动作的选项

| 选项 | 用于动作 | 说明 |
| :--- | :--- | :--- |
| `--root=dir` | 所有 | 修改操作的行为，类似于 `RPM` 的选项 |
| `-B` 或 `--auto-configure` | 所有 | 禁用依赖其他的软件包 |
| `--force-depends` | 所有 | 覆盖会导致 `dpkg` 终止的默认设置 |
| `--ignore-depends=package` | 所有 | 在不安装的情况下检查依赖、冲突和问题 |
| `--recursive` | 所有 | 安装子目录中的所有内容 |
| `-G` | 所有 | 如果已安装则不安装软件包 |
| `-E` 或 `--skip-same-version` | 所有 | 如果有新版本则不安装软件包 |

与 `rpm` 一样，`dpkg` 在某些情况下期望包名。具体来说，`--install (-i)` 和 `--info (-n)` 都接受较短的名称。

例如，考虑以下命令，它安装了 `samba_2:3.6.3-ubuntu2.3`：

如果你正在升级软件包，可能需要在安装新包之前移除旧包。要执行此操作，使用 `dpkg` 的 `-r` 选项，如下：

```
# dpkg -i samba_2:3.6.3-ubuntu2.3_amd64.deb
```

要查找已安装软件包的信息，使用 `dpkg` 参数 `-p`，如列表 2.2 所示。此列表省略了关于软件包作用的扩展英文描述。

### 列表 2.2：`dpkg` 包查询

```
$ dpkg -p samba

Package: samba
Priority: optional
Section: net
Installed-Size: 22862
Maintainer: Ubuntu Developers <ubuntu-devel@lists.com>
Architecture: amd64
Version: 2.3.6-ubuntu2.3
Replaces: samba-common (<= 2.0.5a-2)
Depends: samba-common (>= 2.3.6-ubuntu2.3), libwclient0 (>= 2.3.6-2), libibac1 (>= 2.25-51), libattrr1 (>= 1.2.46-5), libc6 (>= 2.15), libcap2 (>= 2.10), libcomerr2 (>= 1.01), libcups2 (>= 1.4.0), libgssapi-krb5-2 (>= 1.10+dfsg), libkcrypto3 (>= 1.6.dfsg,2), krb5-3 (>= 1.10+dfsg), libiadap-2.4-2 (>= 2.4.7), libpam0g (>= 0.99.7), libdbtd1, liballoc2 (>= 2.4-git20101214), zlibg (>= 1.1.4), debconf (>= 0.5) debconf-2.0, up-tool, libpam-runtime (>= 1.0.1-11), libpam-modules, lib1-base (>= 3.2-13), procs, update-inetd, adduser, samba-common-bin
Recommends: logrotate, dbt-tools
Suggests: opensbsd-inetd | net-upserver, smbldap-tools, libdb-tools, ctd, ufw
Conflicts: samba4 (<< 4.0.0-alpha6)
Size: 8040212
```

# 使用 Debian 软件包

基于 Debian 的系统通常使用一对层次稍高的工具 `apt-get` 和 `dselect` 来处理软件包的安装和卸载。这些工具将在后文的“使用 `apt-get`”和“使用 `dselect`、`aptitude` 和 `Synaptic`”中进行描述。当你想要安装所有软件包时，它们的界面可能非常有用；而当你只操作一个或两个软件包时，`dpkg` 通常更方便。由于 `dpkg` 可以接受软件包文件名作为输入，因此它也是从非常规来源下载或自行创建的软件包的首选方法。

## 使用 `apt-cache`

`APT` 工具套包含一个名为 `apt-cache` 的程序，它专门用于提供有关 Debian 软件包数据库（在 Debian 术中称为软件包缓存）的信息。你可能对该工具的以下几个功能感兴趣：

*   显示软件包信息：使用 `show` 子命令，例如 `apt-cache showpkg samba`，显示有关软件包的信息。显示的信息与 `dpkg` 信息性操作返回的信息不同。
*   显示软件包统计数据：通过传递 `stats` 子命令，例如 `apt-cache stats`，你可以了解安装了多少个软件包、记录了多少依赖关系，以及关于软件包数据库的其他统计数据。
*   查找未满足的依赖项：如果程序缺少库或文件，输入 `apt-cache` 可能有所帮助；此功能返回有关未满足依赖项的信息，这可能帮助你追踪缺失文件问题的根源。
*   显示依赖项：使用 `depends` 子命令，例如 `apt-cache depends samba`，显示指定软件包的所有依赖项。这些信息对于追踪与依赖相关的问题很有帮助。`rdends` 命令查找反向依赖项——依赖于你所选软件包的软件包。
*   定位所有软件包：`pknames` 子命令显示系统上安装的所有软件包的名称。如果你包含第二个参数，例如 `apt-cache pknames sa`，程序将只返回以指定字符串开头的软件包。

虽然存在许多子命令和其他类似的子命令，但这些是你最可能使用的。某些 `apt-cache` 命令是为软件包维护者和调试严重的软件包数据库问题设计的，而不是为了日常系统管理工作。请参阅 `apt-cache` 的主页以获取更多信息。

### 使用 `apt-get`

`APT` 及其 `apt-get` 工具是 Debian 在某些基于 RPM 的发行版中等同于 `Yum`。这个元软件包工具允许你轻松地升级软件包，特别是当你拥有快速互联网连接时。基于 Debian 的系统包含一个 `/etc/apt/sources.list` 文件，该文件指定了可以从中获取重要软件包的位置。如果你是从 CD-ROM 驱动器安装的操作系统，该文件最初将列出安装 CD-ROM 上可以找到软件包的目录。顶部可能还有几行用井号 (`#`) 注释的行，指向 FTP 站点或网站上的目录，你可以从那里获取更新的软件包。（如果你最初是进行网络安装的，则可以取消这些行的注释。）

除非你确定某个站点可以信任，否则不要向 `/etc/apt/sources.list` 添加该站点。`apt-get` 工具执行自动和半自动升级，因此如果你在 `sources.list` 中添加了网络源，而该源包含不可靠的程序或带有安全漏洞的程序，在通过 `apt-get` 升级后，你的系统将变得脆弱。

![](img/1624483a11d032df045f9465e0d0144d_121_0.png)

尽管 `APT` 与 Debian 系统联系最为紧密，但也提供了基于 RPM 的系统移植版本。请检查 http://apt4rpm.sourceforge.net 获取有关该移植版本的信息。`apt-get` 工具的工作原理是从 `/etc/apt/sources.list` 中列出的源获取软件包信息，然后使用这些信息来升级或安装软件包。其语法与 `dpkg` 类似：

```
apt-get [options][command] [package-names]
```

表 2.6 列出了 `apt-get` 命令及其最常用的选项。在大多数情况下，你不会在 `apt-get` 中使用任何选项——只需一个简单的命令以及可能的一个或多个软件包名称。该工具特别常见的用途是让你的系统通过任何新软件包保持更新。如果 `/etc/apt/sources.list` 包含了指向最新文件存档站点的指针，以下两个命令将实现此目标：

```
apt-get update
apt-get dist-upgrade
```

### 表 2.6 `apt-get` 命令

| 命令 | 说明 |
| :--- | :--- |
| `update` | 获取从 `/etc/apt/sources.list` 中列出的安装源获取的可用软件包的更新信息。 |
| `upgrade` | 根据本地存储的可用软件包信息，将所有已安装的软件包升级到最新版本。 |
| `dselect-upgrade` | 执行运行 `dselect` 后未完成的软件包状态更改（安装、卸载等）。 |
| `dist-upgrade` | 与 `upgrade` 类似，但执行“智能”冲突解决，以避免在这样做会破坏依赖关系时升级软件包。 |
| `install` | 按包名（而非文件名）安装软件包，从源获取软件包。 |
| `remove` | 按包名卸载软件包。 |
| `source` | 按包名检索源软件包。 |
| `check` | 检查软件包数据库的一致性和损坏的安装。 |
| `clean` | 清理已检索软件包以释放磁盘空间。 |
| `autoclean` | 与 `clean` 相似但仅删除不再下载的软件包。 |

### 表 2.7 `apt-get` 选项

| 选项 | 用于命令 | 说明 |
| :--- | :--- | :--- |
| `-d` `--download-only` | `upgrade` | 下载软件包但不安装。 |
| `-f` `--fix-broken` | `install` | 尝试修复依赖关系不满足的系统。 |
| `-m` `--ignore-missing` | `upgrade` | 忽略无法检索的软件包（由于网络错误）。 |
| `-q` `--quiet` | 所有 | 省略某些进度指示。可以双写（例如 `-qq`）以产生更少的信息。 |
| `-s` `--simulate` `--just-print` `--no-act` | 所有 | 执行模拟而不实际修改、安装或删除。 |
| `-y` `--yes` `--assume-yes` | 所有 | 对安装脚本中的任何否否回答“是”。 |
| `-b` `--compile` `--build` | `source` | 检索后编译软件包。 |
| `--no-upgrade` | `install` | 如果已安装旧版本，则导致 `apt-get` 不升级该软件包。 |

![](img/1624483a11d032df045f9465e0d0144d_123_0.png)

如果你使用 `APT` 自动升级所有软件包，你实际上是将控制权交给了发行版维护者。Debian 或其他发行版维护者不太可能以此方式入侵你的计算机，缺乏监督的自动更新很容易破坏你的系统，特别是当你从非常规来源获取软件包时。

在练习 2.2 中，你将熟悉 Debian 软件包系统。

### 练习 2.2

# 管理 Debian 软件包

要管理 Debian 软件包，请遵循以下步骤：

1.  以普通用户登录 Linux 系统。
2.  获取一个用于测试的软件包。你可以尝试使用发行版中你确定没有安装的软件包；但如果你尝试一个随机软件包，可能会发现它已经安装或有未满足的依赖。本实验以安装 `zsh_4.3.17-ubuntu1_amd64.deb` 为例，这是一个大多数系统默认安装的 shell，是在 Ubuntu 12.04 系统上使用 `-d` 选项获取的。如果你在测试中使用另一个软件包、发行版或架构，必须根据需要调整命令。
3.  如果使用了 GUI 登录，请从桌面环境菜单中启动 `xterm`。
4.  获取 root 权限。你可以通过在 `xterm` 中输入 `su`、在 Console 窗口中选择 Session > New Root Console，或使用 `sudo`（如果已配置）来运行后续步骤中的命令。
5.  输入 `dpkg -L zsh` 来验证该包是否已安装。如果已安装，该命令将列出与该包相关的文件列表；如果没有安装，则会显示错误信息 `Package zsh-amd64` is not installed`。
6.  输入 `dpkg -I zsh_4.3.17-ubuntu_amd64.deb`（如果包文件不在当前目录，您需要添加包文件的完整路径）。系统应响应显示有关软件包的信息，例如版本号、依赖关系、软件包维护者名称以及软件包描述。
7.  输入 `dpkg -i zsh_4.3.17-ubuntu_amd64.deb`。系统应该安装该包并显示一系列总结其执行操作的列表。
8.  输入 `dpkg -p zsh`。系统应响应与第 6 步中显示的类似的软件包信息。
9.  输入 `zsh`。这将启动一个 shell，其功能与更常见的 `bash` 和 `tcsh` shell 相似。你可能会看到命令提示符发生细微变化，但你可以执行大多数在 `bash` 或 `tcsh` 中可以使用的命令。
10. 输入 `dpkg -P zsh` 从系统中删除该软件包，包括配置文件。它可能会产生一系列关于无法删除的非空目录的警告。注意，你正在正在运行 `zsh` 程序时删除 `zsh` 软件包。Linux 会继续运行你正在使用的 `zsh` 软件包，但你将无法启动该程序的新实例。某些程序可能会异常，因为它们在删除删除包后将会消失。
11. 输入 `exit` 退出 `zsh` 并返回你的正常 shell。
12. 输入 `dpkg -L zsh`。系统应响应 `Package zsh is not installed` 错误，因为你刚刚卸载了它。
13. 输入 `apt-get install zsh` 使用 `APT` 系统安装 `zsh`。根据你的配置，系统可能会从互联网网站下载包，或要求你插入 CD-ROM。如果提示插入 CD-ROM，请插入它并按回车键。系统应该安装该包。
14. 输入 `dpkg -p zsh`。系统应响应与第 6 步或第 8 步中显示的类似的软件包信息。
15. 输入 `dpkg -P zsh`。此命令如第 10 步所述从系统中删除该软件包。

## 使用 `dselect`, `aptitude` 和 `Synaptic`

`dselect` 程序是一个高层软件包浏览器。使用它，你可以从 `/etc/apt/sources.list` 中定义的 `APT` 归档中选择要安装到系统上的软件包，检查系统中已安装的软件包，卸载软件包以及升级软件包。总的来说，`dselect` 是一个强大的工具，但对于没有经验的人来说，它可能令人敬畏，因为它使用文本模式的交互式用户界面呈现了一系列并不明显的选项。

尽管 `dselect` 支持某些选项（例如设置颜色方案），但它们是最晦涩或细微的（详情请参考 `dselect` 的 man 页）。要使用该程序，输入 `dselect`。结果是 `dselect` 主菜单，如图 2.1 在 KDE `Konsole` 窗口中运行所示。

# 图 2.1 `dselect` 工具通过菜单系统提供对 `APT` 支持。

![](img/1624483a11d032df045f9465e0d0144d_125_0.png)

另一个基于文本的 Debian 软件包管理器是 `aptitude`。在交互模式下，`aptitude` 在粗程度上类似于 `dselect`，但通过按下 `Ctrl+T` 访问的 `aptitude` 菜单重新排列了功能。你也可以在命令行上向 `aptitude` 传递各种命令，例如 `aptitude search samba`，它会搜索与 `Samba` 相关的软件包。从命令行（或交互界面）可以访问的功能包括：

*   **更新软件包列表 (`Update Package Lists`)**：你可以通过输入 `aptitude update` 从 `APT` 软件库更新软件包列表。
*   **安装 (`Install`)**：`install` 命令行选项用于安装命名的软件包。该命令有几种变体名称和语法，可以修改其操作。例如，输入 `aptitude install zsh` 安装 `zsh` 软件包，但输入 `aptitude install zsh-`（带有尾连字符）和 `aptitude remove zsh` 都会卸载 `zsh`。
*   **升级软件 (`Upgrade Software`)**：`full-upgrade` 和 `safe-upgrade` 都会升级所有已安装的软件包。`safe-upgrade` 在删除包或安装新包方面较为保守，可能会失败；`full-upgrade` 对这些操作不那么保守，因此更有可能完成任务，但在过程中可能会损坏软件。
