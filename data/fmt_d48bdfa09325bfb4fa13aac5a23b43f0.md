
动作在表 5.3 中总结。选项（表 5.4）改变动作的行为。

**表 5.3：dpkg 主要动作**

| 动作 | 描述 |
|---|---|
| `-i` 或 `--install` | 安装软件包 |
| `--configure` | 配置已安装的软件包：运行脚本 |
| `-r` 或 `--remove` | 软件包，但保留配置文件 |
| `-P` 或 `--purge` | 软件包，包括配置文件 |
| `-p` 或 `--print-avail` | 显示已安装软件包的信息 |
| `-I` 或 `--info` | 显示未安装软件包的信息 |

| 动作 | 描述 |
|---|---|
| `-l pattern` 或 `--list` | 列出所有匹配模式的已安装软件包 |
| `-L` 或 `--listfiles` | 列出与软件包相关的安装文件 |
| `-S pattern` 或 `--search` | 查找拥有指定文件的软件包 |
| `-C` `--audit` | 搜索部分安装的软件包并建议如何处理 |

**表 5.4：微调 dpkg 动作的选项**

| 选项 | 适用动作 | 描述 |
|---|---|---|
| `--root=dir` | 所有 | 使用位于 `dir` 的根目录修改 Linux 系统 |
| `-B` 或 `--auto-deconfigure` | `-r` | 禁用依赖正在删除的包 |
| `--force-things` | 各种 | 强制执行特定操作。请阅 `dpkg` 手页了解此选项执行的操作 |
| `--ignore-depends=package` | `-i`, `-r` | 忽略指定软件包的依赖信息 |
| `--no-act` | `-i`, `-r` | 检查依赖、冲突和其他问题，但不实际安装或删除软件包 |
| `--recursive` | `-i` | 安装指定目录及其子目录下所有匹配名称通配符的软件包 |
| `-G` | `-i` | 如果已安装更高版本的软件包，则不安装 |
| `-E` 或 `--skip-same-version` | `-i` | 如果已安装相同版本的软件包，则不安装 |

## 250 第 5 章 软件包与进程管理

与 `rpm` 一样，`dpkg` 在某些情况下期望包名，而在其他情况下期望包文件名。具体来说，`--install` (`-i`) 和 `--info` (`-i`) 都需要包文件名，但命令本身可以使用较短的包名。

例如，考虑以下命令，它安装了 `samba-common_2.2.3a-i12.3_i386.deb` 包：

```bash
# dpkg -i samba-common_2.2.3a-i12.3_i386.deb
```

如果你正在升级一个软件包，可能需要在安装新包之前删除旧包。要执行此操作，对 `dpkg` 使用 `-r` 选项，如下：

```bash
# dpkg -r samba
```

要查找已安装软件包的信息，请对 `dpkg` 使用 `-p` 参数，如列表 5.2 所示。该列表省略了关于软件包作用的英文描述。

### 列表 5.2：dpkg 软件包信息查询输出

```bash
$ dpkg -p samba-common

Package: samba-common
Priority: optional
Section: net
Installed-Size: 5156
Maintainer: Eloy A. Paris <peloy@debian.org>
Architecture: powerpc
Source: samba
Version: 2.2.3a-12.3
Replaces: samba (<= 2.0.Sa-2)
Depends: debconf, libpam-modules, libc6 (<= 2.2.4-4), libcupsys2
(>= 1.1.13-1), libpam0 (>= 0.72-1)
Filename: pool/updates/main/s/samba/samba-common_2.2.3a-12_powerpc.deb
Size: 1036524
```

基于 Debian 的系统通常使用名为 `dselect` 的高级实用程序来处理软件包的安装和删除。`dselect` 实用程序提供了已软件包以及从指定源（如 CD-ROM 光盘或 FTP 站点）提供的可用软件包的文本模式列表，并允许你选择想要安装和删除哪些软件包。当你想要安装多个软件包时，此界面非常有用，但在仅操作一两个软件包时，`dpkg` 通常更方便。因为 `dpkg` 可以接受包文件名作为输入，它也是安装从非常规源下载或自己创建的软件包的首选方法。

## 使用 apt-get

Debian 软件包管理的另一种选择是高级软件包工具 (APT) 实用程序，特别是 `apt-get`。该工具使你能够轻松地升级软件包，特别是当你拥有快速互联网连接时。基于 Debian 的系统包含一个 `/etc/apt/sources.list` 文件，该文件指定了从哪些位置获取重要的软件包。如果你是从 CD-ROM 驱动器安装的操作系统，此文件最初将列出安装 CD-ROM 上可以找到软件包的目录。顶部附近可能还有几行用哈希标记（#）注释掉的内容，指示了可以从 FTP 或 Web 获取更新软件包的条目。（如果你最初是进行网络安装的，这些行可能可以取消注释。）

尽管 APT 与 Debian 系统联系最紧密，但也提供了基于 RPM 的系统的移植版本。请查看 `http://apt4rpm.sourceforge.net` 获取有关该移植的信息：

![image](img/a1f029e559a80f8f50e10faa08e48080_292_0.png)

除非你确定它是受信任的，否则不要向 `/etc/apt/sources.list` 添加站点。`apt-get` 实用程序执行自动和半自动升级，因此如果你在 `sources.list` 中添加了带有安全漏洞的不可靠程序的网络源，你的系统在通过 `apt-get` 升级后将变得脆弱。

`apt-get` 实用程序通过从 `/etc/apt/sources.list` 中列出的源获取可用软件包的信息，然后使用这些信息升级或安装软件包。其语法与 `dpkg` 类似：

```bash
apt-get [options] [package-names]
```

表 5.5 列出了 `apt-get` 命令，表 5.6 列出了最常用的选项。在大多数情况下，你实际上并不会在 `apt-get` 中使用选项，只需要单个命令和一个或多个包名。该实用程序特别常见的用法是保持你的系统更新任何新软件包。如果 `/etc/apt/sources.list` 包含了指向最新文件存档 FTP 站点的指针，以下两个命令将实现这一目标：

```bash
# apt-get update
# apt-get dist-upgrade
```
