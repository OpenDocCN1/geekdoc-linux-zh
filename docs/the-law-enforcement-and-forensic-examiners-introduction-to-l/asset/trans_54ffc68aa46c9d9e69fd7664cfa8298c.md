

# 关于包管理的一个说明。系统上安装的所有软件包完整列表维护在 `/var/log/packages` 中。你可以浏览该目录来查看你安装了哪些内容，也可以查看文件本身以查看软件包中安装了哪些文件。使用 SlackBuilds 的一个优点是包名中会添加一个 SB 标签。我们可以在 `/var/log/packages` 中 `grep` 搜索这个标签，并准确看到我们通过 SlackBuilds 安装了哪些外部软件包。与直接从源码编译并安装软件相比，使用包管理器的巨大优势之一就是……能够追踪安装了哪些版本的软件包。

我们使用来自 SlackBuilds.org 的构建脚本安装了三个软件包。一个通过手动下载（sbotools），另外两个通过 sbotools 安装（clamav 和 lshw）。我们使用 `grep` 查看 `/var/log/packages` 目录的内容（假设这是一个干净的 Slack 系统，且你没有安装任何 .tgz 或 .txz 格式的 Slack 软件包）：

```bash
root@forensic1:~ ls /var/log/packages/ | grep SB
clam-0.99.2-x86_64-1_SB
sbotools-2.3-noarch-1_SB
lshw-B.02.18-x86_64-1_SB
```

当涉及到升级（或检查更新）通过 sbotools/SlackBuilds 安装的软件时，你可以使用 `sbocheck`。运行此命令将从 SlackBuilds.org 获取最新的 SlackBuild 树，并将你的软件包与当前可软件包进行比较。

```bash
root@forensic1:~ sbocheck
Updating SlackBuilds...
0 0% 0.00kB/s 0:00:00 (ifr#0,to-chk=0/39799)
Checking for updated SlackBuilds...
```

sbotools 2.3 < 需要更新（SBO 中的 2.4）

上述结果的副本保存在 `/var/log/sbocheck.log` 中。

我们可以从输出中看到新版本的 sbotools。要进行升级，我们只需使用 `sbupgrade` 命令，这里我们正在使用 sbotools 来升级 sbotools：

```bash
root@forensic1:~ sbupgrade sbotools
sbotools (ports-like interface to SlackBuilds.org)
Package sbotools-2.4-noarch-1_SBo.tgz installed.
```

sbotools-2.0-noarch-1_SBo 已用新软件包 /tmp/sbotools-2.4-noarch-1_SBo.tgz 升级。

正在为 sbotools-2.4 进行清理……

```bash
root@forensic1:~# sboinstall -v
sbotools version 2.4
licensed under the WTFPL
<http://sam.zoy.org/wtfpl/COPYING>
```

不要被我们在这里正在升级 sbotools 的事实所困惑。你可以使用 `sbocheck` 和 `sbupgrade` 来安装你之前通过 SlackBuilds 安装的任何软件（大部分情况下如此……也有例外）。这为我们提供了一种简单的方法来安装和升级外部软件包，格式符合 Slack 习惯，且极少繁琐。

早前的警告仍然有效。确保你理解你正在安装的内容，并始终阅读 `README` 文件。

# VII. Linux 与取证

## 证据获取

在本节中，我们将介绍几个我们可用的获取工具。我们将涵盖一些收集问题、设备信息、镜像验证以及更高级的挂载选项等。显然，我们需要确保的第一件事是确保有一个合适的地方来输出镜像和分析的结果。

在阅读后续章节时，请尝试使用一个旧的（较小的）硬盘来跟随操作。找一个旧的 SATA 硬盘（我正在使用的是 40GB 的）将其连接到你的计算机，既可以直接连接到 SATA 总线，也可以通过 USB (3.x) 驱动器。这样你就可以跟随命令，并将输出结果与我们的进行对比。你甚至可以使用 USB 优存盘，但某些媒体信息收集章节的输出将无法提供可比的输出。学习这些材料最好的方法是实际操作并进行实验。

## 分析组织

在开始收集可能在法庭或行政听证中实用的证据镜像和信息之前，我们可能希望确保以组织化的方式存储所有这些数据。显然，这不是 Linux 特有的，但我们需要确保有几个系统位置来存储和检索数据：

- 1. 用于存储特定案件取证镜像的案件特定目录或卷。
- 2. 用于存储取证软件和主题信息的案件特定目录。
- 3. 用作证据镜像挂载点的特定目录。
- 4. 我们的操作日志文件。文档编写和记录是妥当取证不可或缺的一部分。

无论你将案件数据存储在何处，都希望保持其组织良好。在大多数情况下，当你进行分析时，你会希望保持其有序。

