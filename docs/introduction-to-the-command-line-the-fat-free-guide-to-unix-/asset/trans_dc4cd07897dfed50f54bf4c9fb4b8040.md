

## lpg

**用途**：显示打印队列状态。

**用法语法**：`lpg [OPTIONS]`

```bash
$ lpg -a
Rank  Owner Job    File(s)      Total Size
1st   nick  2     hosts       1024 bytes
2nd   nick  3     hosts       1024 bytes
3rd   nick  4     hosts       1024 bytes
4th   nick  5     hosts       1024 bytes
5th   nick  6     hosts       1024 bytes
6th   nick  7     hosts       1024 bytes
7th   nick  8     hosts       1024 bytes
8th   nick  9     hosts       1024 bytes
9th   nick  10    hosts       1024 bytes
```

`lpg` 命令显示排队中的打印作业状态。它与 `lpstat` 命令类似，但提供更易读的输出。与 `lpstat` 命令不同，`lpg` 命令仅支持有限数量的命令行选项。

在上述示例中，执行 `lpg -a` 将显示所有排队中的打印作业。下一个示例演示了如何使用 `-P` 选项显示特定打印机的状态。

```bash
$ lpg -P HP-4350
HP-4350 is not ready
Rank  Owner Job    File(s)      Total Size
1st   nick  2     hosts       1024 bytes
2nd   nick  3     hosts       1024 bytes
3rd   nick  4     hosts       1024 bytes
4th   nick  5     hosts       1024 bytes
```

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `lpg -a` | 显示所有排队中打印作业的状态 |
| `lpg -P [PRINTER]` | 显示指定打印机的状态 |

## cancel

**用途**：取消并删除排队中的打印作业。

**用法语法**：`cancel [OPTIONS] [JOBID]`

```bash
$ lpq -P HP-4350
HP-4350 is not ready
Rank    Owner   Job     File(s)                   Total Size
1st     nick    6       hosts                     1024 bytes
2nd     nick    7       hosts                     1024 bytes
3rd     nick    8       hosts                     1024 bytes
4th     nick    9       hosts                     1024 bytes
5th     nick    10      hosts                     1024 bytes
$ cancel 10
```

使用 cancel 命令取消单个打印作业

`cancel` 命令删除排队中的打印作业。在上述示例中，通过指定作业 ID 号，使用 `cancel` 删除了单个作业。下一个示例演示了如何使用 `-a` 参数从指定打印机中删除所有排队中的打印作业。

```bash
$ lpq -P HP-4350
HP-4350 is not ready
Rank    Owner   Job     File(s)                   Total Size
1st     nick    6       hosts                     1024 bytes
2nd     nick    7       hosts                     1024 bytes
3rd     nick    8       hosts                     1024 bytes
4th     nick    9       hosts                     1024 bytes
$ cancel -a HP-4350
$ lpq -P HP-4350
HP-4350 is not ready
no entries
```

使用 cancel 命令取消打印机上的所有排队打印作业

> **注意**
> 某些 UNIX 系统可能使用 `lprmd` 命令来代替 `cancel`。

**常见用法示例：**

- `cancel [JOB]` — 取消指定的打印作业
- `cancel -a` — 取消所有打印机上的所有打印作业
- `cancel -a [PRINTER]` — 取消指定打印机上的所有作业

## enable / disable

**用途**：启用/禁用打印机。

**用法语法**：`enable [OPTIONS] [PRINTER]`

```bash
# enable HP-4350
# lpq
HP-4350 is ready
```

使用 enable 命令启用打印机

`enable` 命令用于启用打印机，使其可用于打印。在上述示例中，执行 `enable` 命令后，指定的打印机被启用并变得可用于打印。

`disable` 命令使打印机离线并禁用其打印功能，如下一个示例所示。

**用法语法**：`disable [OPTIONS] [PRINTER]`

```bash
# disable HP-4350
# lpq
HP-4350 is not ready
```

使用 disable 命令禁用打印机

当打印机被禁用时，大多数系统仍会继续接收打印请求。这些作业将保留在队列中，直到打印机被启用。

> **注意**
> 使用 CUPS（通用 Unix 打印系统）的系统将使用 cupsenable 和 cupsdisable 命令来代替 enable 和 disable。

| 常见用法示例： |
| :--- |
| `enable [PRINTER]` | 启用指定的打印机 |
| `disable [PRINTER]` | 禁用指定的打印机 |
| `disable -c [PRINTER]` | 禁用打印机并取消所有排队中的作业 |

## lpadmin

**用途**：管理打印机。

**用法语法**：`lpadmin [OPTIONS] [PRINTER]`

```bash
$ lpadmin -p HP-5200 -E -v socket://10.10.1.32
$ lpstat -a
HP-5200 accepting requests since Fri 16 Apr 2010 12:41:01 PM CDT
```

使用 lpadmin 命令添加打印机

`lpadmin` 命令用于管理 Unix、Linux 和 BSD 系统上的打印机。在上述示例中，使用 `lpadmin` 命令将一个 IP 地址为 `10.10.1.32` 的网络打印机添加到系统中。

下一个示例演示了如何使用 `lpadmin -x` 删除上一个示例中创建的打印机。

```bash
$ lpadmin -x HP-5200
$ lpstat -a
```

使用 lpadmin 命令删除打印机

> `lpadmin` 实用程序的命令行选项因平台而异。请查阅 `man lpadmin` 以获取特定于你系统的信息。

**常见用法示例：**

- `lpadmin -p [NAME] -v [DEVICE]` — 向系统中添加打印机
- `lpadmin -x [PRINTER]` — 从系统中移除打印机

## 第 14 节：软件安装

### 概述

软件安装是不同 Unix、Linux 和 BSD 系统之间差异最大的领域。每个发行版都有其独特的软件管理工具集。本节为每个平台提供了这些软件管理命令的概述。

本节涵盖的命令：

| 命令 | 用途 |
|:---|:---|
| dpkg | 安装/删除 Debian Linux 软件包。 |
| aptitude | 基于 Debian Linux 系统的自动化软件包管理器。 |
| rpm | 安装/删除 Red Hat Linux 软件包。 |
| yum | 基于 Red Hat Linux 系统的自动化软件包管理器。 |
| emerge | 安装/删除 Gentoo Linux 软件包。 |
| pkg_add pkg_delete | 安装/删除 BSD 软件包。 |
| pkg_info | 显示有关 BSD 软件包的信息。 |
| installp | 在 AIX 系统上安装软件包。 |
| lslpp | 列出 AIX 系统上已安装的软件。 |
| pkgr add pkg rm | 安装/删除 Solaris 软件包。 |
| pkginfo | 列出 Sun Solaris 系统上已安装的软件包。 |
| make | 从源代码编译并安装软件。 |

### 本节使用的术语表：

| 术语 | 定义 |
| :--- | :--- |
| A P T | （高级软件包工具）用于基于 Debian Linux 系统上的软件包管理器。 |
| 编译 | 将源代码转换为二进制/可执行文件的过程。 |
| 依赖项 | 另一个程序正常运作所需的程序或库。 |
| Makefile | 在软件编译期间使用的文件。 |
| 软件包 | 用于软件安装的自包含文件。 |
| Portage | 用于基于 Gentoo Linux 系统的软件包管理器。 |
| 存储库 | 软件包管理程序使用的软件包来源。 |
| RPM | （Red Hat 软件包管理器）由 Red Hat 公司创建的软件包格式。 |

## dpkg

**用途**：安装/删除 Debian Linux 软件包。

**用法语法**：`dpkg [OPTIONS] [FILE]`

```bash
# dpkg -i apache2_amd64.deb
Preparing to install apache2 (using apache2_amd64.deb).
Unpacking apache2.
Setting up apache2.
Processing triggers for man-db ...
Processing triggers for ufw ...
...
```

*使用 dpkg 安装 Apache Web 服务器软件包*

**dpkg** 是用于基于 Debian Linux 系统的传统软件包管理器。它可以在 Debian 和 Ubuntu 以及许多基于 Debian 核心的其他 Linux 发行版中找到。

使用 **dpkg**，你可以安装或删除专门为基于 Debian 的系统创建的程序。这些软件包通常具有 .deb 文件扩展名。上述示例演示了如何使用 **dpkg** 命令安装 Debian 软件包。

> **注意**
> 大多数基于 Debian 的系统现在利用名为 `aptitude` 的程序来执行软件安装任务。鉴于 `aptitude` 会自动下载并安装请求的软件包及其所有必需的依赖项，直接使用 `dpkg` 安装软件包的情况很少见。更多信息请参见第 234 页。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `dpkg -i [PACKAGE]` | 安装指定的软件包 |
| `dpkg -r [PACKAGE]` | 删除指定的软件包 |
| `dpkg -p [PACKAGE]` | 删除指定的软件包及相关配置文件 |
| `dpkg -l` | 列出所有已安装的软件包 |

