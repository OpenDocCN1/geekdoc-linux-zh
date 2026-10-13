
```
:sd=/var/spool/lpd/lp:
:mx=0:
:sh:
:lp=/dev/lp/lp1:
:if=/var/spool/lpd/lp/filter:
:af=/var/spool/lpd/lp/accounting:\
```

使用时，打印机将自动记录使用情况。运行 `pac-Php` 将生成用户列表，以及任何运行作业的数量和成本值。

# 将 Samba 作为文件服务器

Samba 作为文件服务器的配置已在第 4 章介绍；某些高级主题未包含在内，因此在此进行讨论。

## 配额 (Quotas)

在许多用户可能使用价值资源的系统上，Linux 提供了实施配额的能力。配额通过多种方式限制硬盘空间的使用量。配额可以按组、组 ID (`GID`) 甚至单个用户设置。如果系统包含许多关键系统，在将用户文件保存到相同位置时，使用配额将是一个无价的帮助。

配额的管理和使用由列表 10.5 所示的程序组执行。

运行 `quota -u username` 将显示该用户文件系统的详情以及当前的配额水平，如列表 10.9 所示。

### 列表 10.9 为用户 testq 编辑用户配额。

```
#quota -u testq

Quotas for user testq:

/dev/hda3: blocks in use: 0, limits (soft = 5000, hard = 10000)

inodes in use: 1, limits (soft = 500, hard = 1000)

/dev/hdb1: blocks in use: 0, limits (soft = 5000, hard = 10000)

inodes in use: 0, limits (soft = 500, hard = 1000)
```

可以直接编辑软限制和硬限制的大小以及文件数量限制值。通过保存文件，这些限制将被激活。在这种情况下，用户 `testq` 被赋予了 500 个文件和 5MB 的软限制，以及 1,000 个文件和 10MB 的硬限制。其影响是，如果用户创建的文件大小或数量大于其中任何一个数值，配额系统就会激活。如列表 10.10 所示，使用 `edquota -t username` 可以设置软限制。

### 表 10.5 配额管理命令。

| 命令 | 描述 |
|---|---|
| `quota` | 返回系统的配额信息。选项有： |
| `quota [-guqvV]` | |
| `quota [-qv] -u username` | |
| `quota [-qv] -g groupname` | |
| `quotaon` | 启用配额 |
| `quotaoff` | 关闭配额 |
| `repquot` | 报告配额 |
| `edquota` | 编辑用户配额 |
| `quotacheck` | 检查文件系统的配额使用情况 |

### 列表 10.10 设置配额宽限期。

```bash
$edquota -t testq
```

时间单位可以是：天、小时、分钟或秒。
强制执行用户软限制之前的宽限期：
`/dev/hda3`: 块宽限期: 0 天，文件宽限期: 0 天
`/dev/hdb1`: 块宽限期: 1 天，文件宽限期: 1 天

用户将被允许在文件数量或大小限制的宽限期时间内突破软限制。如果发生了突破硬限制的操作，系统将返回与列表 10.11 所示类似的消息作为响应。

### 列表 10.11 复制文件时超出配额的消息。

```
Red Hat Linux release 5.2 (Apollo)

Kernel 2.0.36 on an 1486

login:

Last login: Aug 5 22:42:34 from ntwdev02

[test]@linuxserver testq]$ ls

[test]@linuxserver testq]$ cd .

[test]@linuxserver /home]$ cp /tmp/files.tgz ~/

/home: warning, user disk quota exceeded

/home: write failed, user disk limit reached.

cp: /home/test/files.tgz: Disc quota exceeded

[test]@linuxserver /home]$
```

当用户连接到启用了配额的 Samba 服务器时，系统上设置的配额将生效；如果尝试任何突破配额的操作，就会出现错误消息，与图 10.3 所示类似。

系统在消息中不区分不同的配额限制。

![](img/166cd29830b01a9e3eceb33240be1bcf_416_0.png)

图 10.3 因突破配额导致的 Windows 消息。

# 将 Samba 作为传真服务器

在以 Windows 为主的网络中将 Samba 作为传真服务器并不困难。Linux 发行版中提供了许多不同的传真软件套件，可以作为起点。我将重点关注从大多数 Linux 镜像站提供的 `mgetty+sendfax` 软件包。我假设 Linux 服务器已经有了一个功能正常的调制解调器。重要的点是，它必须是传真/调制解调器，并且能够与 Linux 操作。有几种传真/调制解调器设备依赖软件驱动（通常仅适用于 Microsoft Windows），可能无法在 Linux 上运行。

此外，为了获得最佳结果，必须获取并安装以下软件，因为你的目标是将传真服务器配置得像 PostScript 打印机：

- Ghostscript 软件包
- PostScript 打印机过滤器软件包
- pdm 图像

这些内容作为 Red Hat 标准发行版的一部分可用。

## 配置 mgetty+sendfax

`mgetty+sendfax` 分发版不是以二进制形式提供安装，因此你需要为系统编译 `mgetty+sendfax`。首先，将分发包提取到 `/usr/src`。在编译之前，你需要确定调制解调器的初始化字符串、传真运行的电话号码以及传真使用的 COM 端口。获取这些信息后，从 `/usr/src/mgetty+sendfax` 目录编辑 `policy-h` 文件，替换 `modem_init_string`、`fax_station_id` 和 `fax_modem_ttys` 的值，并将内容复制到 `mgetty.h`。列表 10.12 显示了 33.6Kbps 传真/调制解调器的示例值，地址为 555-123-4567，使用 COM2 覆盖 COM3。

### 列表 10.12 mgetty+sendfax policy.h 文件。

```bash
#define MODEM_INIT_STRING "AT&FACID\0357=55"
```

```bash
#define FAX_STATION_ID "555-123 4567"
```

```bash
#define FAX_MODEM_TTYS "ttyS2"
```
