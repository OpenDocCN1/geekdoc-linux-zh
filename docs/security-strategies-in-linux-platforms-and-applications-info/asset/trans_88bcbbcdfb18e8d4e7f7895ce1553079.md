

# 第 14 章 | 检测与响应安全漏洞

- 1. 下载并解压包含 Sleuth Kit 文件的 tar 包。该文件通常为 tar.gz 格式。使用从 http://www.sleuthkit.org/ 提供的 GNU 隐私保护 (GPG) 密钥验证下载。

- 2. 使用以下命令解压 `sleuthkit-*.gz`。版本号由 `*` 表示；字符`*`在命令中有效。压缩包中的文件应该出现在 `sleuthkit-` 目录中。

```
$ tar xzf sleuthkit-.tar.gz
```

- 3. 进入 `sleuthkit-*` 目录。如 INSTALL .txt 文件所述，编译和构建所需的命令还需要额外的三个步骤。

- 4. 运行 `./configure` 脚本使用本地可用库配置软件包。

- 5. 运行 `make` 命令构建软件包。

- 6. 运行 `make install` 命令编译软件包；默认情况下，命令会被写入 `/usr/local/bin/`。

当然，你可能希望将 `/usr/local/bin/` 目录下的可执行文件写入 CD 或 DVD 等只读介质。确保已写入相应的命令和媒体库，然后你就可以在受感染的系统上挂载介质，并使用此过程构建的命令。Sleuth Kit 提供的一些命令如表 14-2 所示。从这些命令可以看出，其中许多也适用于在系统关机后进行分析。

# Master Key Linux

Sleuth Kit 的问题之一是它目前仅以 tar 包的形式分发。配置、编译并从合适的介质中拷贝命令仍然需要你来完成。如果这看起来很麻烦，一种选择是 Master Key Linux。它是一个实盘 CD，已经设置好了前面描述的命令（以及其他一些命令）。你只需要挂载 CD 并从相应的子目录运行命令即可。目前，该项目由英国科特文里大学（UK）的学生领导，没有商业支持。但如果你对此感兴趣，可以从 http://www.masterkeylinux.com/ 获取该软件。

# 构建自己的介质

构建自己的介质可能是最好的选择。当从源代码编译时，你可以在 CD 或 DVD 等只读介质上设置命令，并包含可靠运行命令所需的所有库。正如 Symantec 网站 http://www.symantec.com/connect/articles/forensic-analysis-live-linux-system-pt-1 上 Mariusz Burdach 文章所述，你可能希望在该介质中包含表 14-3 列出的命令。下载软件包时请注意，许多相关服务器并没有按日期组织软件包。因此，软件包的最新版本可能出现在列表中间。

![](img/c0608a8c8a0777903dfec4ff61fdffa1_458_0.png)

# 第 3 部分 | 构建分层 Linux 安全策略

| 表 14-3 取证工具工具包中应包含的命令 |
| 命令 | 描述 |
| :--- | :--- |
| cat | cat 命令来自 coreutils 软件包。更多信息请参阅 http://www.gnu.org/software/coreutils/ |
| date | date 命令来自 coreutils 软件包。 |
| dd | dd 命令来自 coreutils 软件包。 |
| dmesg | dmesg 命令来自 util-linux-ng 软件包，该包可以从 Linux 内核服务器 http://ftp.kernel.org/pubinux/lutils/util-linux-ng/ 下载。 |
| nc | 虽然 nc 命令来自多种来源，但其选项与 nmap 命令相关联，可以从 http://nmap.org/download.html 在线获取。 |

安装软件包所需的步骤与 Sleuth Kit 描述的相似。详细说明应位于解压后的源代码目录中名为 `INSTALL` 的文件中。可能需要进行一些自定义，例如：配置源代码通过类似下面的命令将工具重定向到特定目录是有帮助的：

```bash
# ./configure --prefix=/tools
```

一旦将给工具写入 CD 或 DVD，你就可以在可疑系统上挂载介质，并放心地知道此类介质的命令不会被更改。

# 取证实盘介质

许多小组都创建了用于取证数据恢复的实盘介质。虽然这些选项中很少支持对 `/proc/` 目录下的文件等易失数据的恢复，但大多数选项都为想要创建可疑硬盘副本并详细分析这些硬盘数据的调查人员提供了极佳的支持。表 14-4 列出了几种取证实盘介质的选项。其中一些选项包含了从微软操作系统恢复易失数据的命令。大多数选项可以启动到加载在 RAM 中的自定义 Linux 版本，并带有可以诊断和其他检查本地设备上与 Linux 或微软系统相关文件的工具。通常，在加载实盘 CD 或 DVD 时，硬盘不会被挂载。此列表不包括包含额外取证工具的实盘 CD/DVD 发行版。事实上，大多数实盘 CD/DVD 发行版都包含有助于取证分析的命令行工具。但请注意，标准的实盘 CD/DVD 发行版可能会使用或覆盖交换分区上的信息。在启动取证

![](img/c0608a8c8a0777903dfec4ff61fdffa1_459_0.png)

# 第 14 章 检测与响应安全漏洞 435

| 表 14-4 取证实盘介质选项 |
| 名称 | 描述 |
| :--- | :--- |
| BackTrack | 一个可启动 DVD 发行版，可以在不干扰交换分区的情况下启动，来自 http://www.backtrack-live.org。 |
| CAINE | 计算机辅助调查环境，来自 http://www.caine-live.net/ |
| Chaox | 基于 Arch Linux，Chaox 专注于渗透测试和取证工具。更多信息请参阅 http://blag.chaos.net/ |
| Damn Vulnerable Linux (DVL) | 基于 Slack Linux，DVL 是由德国 Cognitive Core 赞助的国际培训认证使用的教学工具。它包含了 BackTrack 和额外的安全工具。更多信息请访问 http://www.damnvulnerablelinux.org/ |
| DEFT Linux | 基于 Ubuntu Linux，包含许多从活动微软操作系统恢复数据的实盘工具，来自 http://www.deftlinux.net/ |
| FCCU Linux | 比利时的一个发行版，基于 Debian Linux 构建，来自 |
| Network Security (NST) | 基于 Fedora 构建，NST 提供了许多 |
| Internet Protocol Security (IPSec) | 当有充分理由避免安全更新时 |
| Network Monitoring (NSM) | 一种基于 Debian 的发行版，旨在 |


