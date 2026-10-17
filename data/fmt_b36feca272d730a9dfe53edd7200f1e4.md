
从 RPM 提取数据的另一种方法是使用 `alien`，它将在后文“不同软件包格式之间的转换”中描述。该程序可以将 RPM 转换为 Debian 软件包或 tarball。

# 真实世界场景

# 使用高级别的 RPM 工具

为了方便系统管理，许多发行版现在都提供了更高级的 RPM 工具。`Yum` 程序（http://linux.duke.edu/projects/yum/）在这方面非常流行，并且是 `Red Hat` 和 `Fedora` `Updater Agent` 等 GUI 工具的基础。另一种选项是使用 Debian 的高级软件包工具（APT）；RPM 版本的端口称为 `apt4rpm`，可以从 http://apt4rpm.sourceforge.net 获取。

接下来的章节“使用 apt-get”描述了 APT，该描述同样适用于 `apt4rpm`，尽管你需要使用更传统的方法安装 APT 并找到适当的仓库站点（`apt4rpm` 首页可以帮助完成这些任务）。

高级工具的优势之一是它们允许轻松安装新软件，而无需翻找 CD-ROM；只需输入命令，如 `apt-get install someprogram`，`someprogram` 软件包就会安装到你的系统中（如果它存在）。另一个优势是这些工具有助于自动化系统更新。例如，输入 `apt-get update; apt-get dist-upgrade` 将你所有的软件包升级到最新版本。这种批量升级并非没有风险（有问题的程序可能会导致问题），但总的来说，方便的系统更新对系统管理是一个是幸。

### 配置文件

通常，你可能需要编辑配置文件来更改 RPM 的行为。这些文件位于多个位置。例如，系统级配置文件位于 `/etc/rpm.conf`，而用户特定的配置文件位于 `~/.rpm/conf`。

## Debian 发行版与惯

如其名所示，Debian 软件包源自 Debian 发行版。从那时起，该格式已被多个发行版采用，包括 `Libranet`、`Ubuntu` 和 `Xandros`。这些发行版都派自原始的 Debian，这意味着来自原始 Debian 的包可能在其他基于 Debian 的系统上良好运行。尽管 Debian 不强调 GUI 安装或配置工具，但它的派生版本——特别是 `Xandros`——在基础 Debian 系统上增加了 GUI 配置工具，这使得这些发行版对 Linux 用户更具吸引力。原始 Debian 倾向于一个尽可能自由的系统，并尽力严格遵守开源软件原则，而不是投资于 GUI 配置工具。原始 Debian 的不同寻之处在于，它由志愿者维护，这些志愿者的动力源于构建一个他们想要使用的产品，而不是受利润驱动的公司。

与 RPM 类似，Debian 软件包格式对操作系统和 CPU 类型都是中性的。Debian 软件包很少出现在 Linux 之外，尽管人们正努力创建一个使用 `GNU Hurd` 内核而非 Linux 内核的 Debian 发行版。这样的发行版将不像 Linux，但在操作和配置上可能类似于 Debian/Linux。

原始 Debian 发行版已移植到许多 CPU，包括 `x86`、`IA-64`、`PowerPC`、`Alpha`、`680x0`、`MIPS` 和 `SPARC`。原始架构是 `x86`，随后的移植处于不同的成熟度水平。派生发行版通常只在 `x86` 软件包上运行。当这些代码存在时，它们可能与 RPM 约定不同。例如，以 `.deb` 结尾的文件表示 `x86` 二进制文件，`powerpc.deb` 是 `PowerPC` 二进制文件，而 `all.deb` 表示与 CPU 无关的包，例如文档或脚本。与 RPM 软件包一样，这种文件命名约定仅仅是——约定。你可以根据自己的需要重命名文件，以包含或省略处理器代码。`deb` 源包没有相应的代码，因为正如接下来的章节“Debian 软件包与其他包格式的比较”所示，Debian 源包实际上由几个独立的文件组成。

### `dpkg` 命令集

Debian 软件包与 RPM 软件包不兼容，但基本原理在两种包类型之间是相同的。与 RPM 类似，Debian 软件包包含依赖信息，且 Debian 软件包工具维护着一个已安装包、文件等的数据库。你使用 `dpkg` 命令来安装 Debian 软件包。该命令的语法为：

```
dpkg [options] [action] [package-files|package-name]
```

`action` 是要执行的代码；常用操作总结在表 2.3 所示。`options`（表 2.4）修改操作的行为，类似于 `rpm` 的选项。

### 表 2.3 `dpkg` 主要操作

| 操作 | 描述 |
| --- | --- |
| `-i` 或 `--install` | 安装软件包 |
| `--configure` | 重新配置已安装的包：运行安装后脚本以设置特定站点的选项 |
| `-r` 或 `--remove` | 移除软件包，但保留配置文件不变 |
| `-P` 或 `--purge` | 移除软件包，包括配置文件 |
| `-p` 或 `--print-avail` | 显示已安装包的信息 |
| `-I` 或 `--info` | 显示未安装包的信息 |
| `-l pattern` 或 `--list pattern` | 列出所有名称匹配 `pattern` 的已安装包 |
| `-L` 或 `--listfiles` | 列出与包关联的已安装文件 |
| `-S pattern` 或 `--search pattern` | 查找拥有 `pattern` 指定文件的的包 |
| `-C` 或 `--audit` | 搜索部分安装的包并建议如何处理它们 |

### 表 2.4 用于微调 `dpkg` 操作的选项

| 选项 | 适用操作 | 描述 |
| --- | --- | --- |
| `--root=dir` | 所有 | 使用位于 `dir` 的根目录修改 Linux 系统。可用于维护独立于另一个 Linux 安装，例如在操作系统安装或紧急维护期间。 |
| `-B` 或 `--auto-deconfigure` | `-r` | 禁用依赖于正在移除的包的包。 |
| `--force-things` | 各 | 强制执行特定操作。详情请咨询 `dpkg` 手页关于 `things` 选项的作用。 |
| `--ignore-depends=package` | `-i`, `-r` | 忽略指定包的依赖信息。 |

### 表 2.4 用于微调 `dpkg` 操作的选项（继续）

| 选项 | 适用操作 | 描述 |
| --- | --- | --- |
| `--no-act` | `-i`, `-r` | 在不实际安装或移除包的情况下检查依赖、冲突和其他问题。 |
| `--recursive` | `-i` | 在指定目录及其所有子目录中安装所有匹配包名通配符的包。 |
| `-G` | `-i` | 如果已安装相同版本的包，则不安装该包。 |
| `-E` 或 `--skip-same-version` | `-i` | 如果已安装相同版本的包，则不安装该包。 |

与 `rpm` 类似，`dpkg` 在某些情况下需要包名，在其他情况下需要包文件名。具体来说，`--install` (`-i`) 和 `--info` (`-I`) 都需要包文件名，但其他命令使用较短的包名。

示例，考虑以下命令，它安装了 `samba-common_3.0.10-1_powerpc.deb`：

```
# dpkg -i samba_common_3.0.10-1_powerpc.deb
```

如果你正在升级一个包，可能需要在安装新包之前移除旧包。要执行此操作，请使用 `-r` 选项：

```
# dpkg -r
```

要查找已安装包的信息，使用 `-p` 参数，如 2.2 所示。这提供了关于该包的扩展描述。

```
$ dpkg -p samba
Package: samba-common
Priority: optional
Section: net
Architecture: powerpc
Version: 3.0.10-1
Maintainer: Eloy A. Paris <eloy@debian.org>
Size: 4824
Filename: pool/updates/samba/samba-common_3.0.10-1_powerpc.deb
```

如果你正在升级一个包，可能需要在安装新包之前移除旧包。要执行此操作，请使用 `-r` 选项：

```
# dpkg -r
```

### 列表 2.2：包查询输出

```
$ dpkg -I samba-common_3.0.10-1_powerpc.deb
```

### 使用 `apt-get`

基于 Debian 的系统使用一些更高级别的工具 `apt-get` 来处理包的安装和移除。当你想要安装多个包时，这些工具非常有用；处理一个或两个包时 `dpkg` 通常更方便。由于 `dpkg` 可以接受包作为输入，它也是从不寻来源下载或自行创建包的首选方法。
