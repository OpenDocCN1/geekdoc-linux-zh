
> 在安装 PTF 之前，请确保 500 虚拟设备处于 R/W 模式。

## 9.7 将已维护的 z/VM 投入生产

在对 z/VM 进行维护服务后，需要进行 `IPL`，因为它可能是对 CP 的服务。

在方便时，根据您的服务时间或其他条件，对系统进行 `IPL`。与任何其他操作系统一样，所有用户，或在这种情况下，所有虚拟机，都会被关闭。z/VM 具有执行 `SHUTDOWN REIPL` 的能力，前提是它是由具有执行此操作适当特权类的虚拟机发出的¹。需要始终运行的虚拟机可以在 `IPL` 期间自动注销（`AUTOLOG`）。

¹ 不必像 z/OS `IPL` 那样从 HMC 控制台执行

## 交叉引用：z/OS、z/VM 和 Linux 命令

本附录提供了 z/OS 命令和概念与其 z/VM 和 Linux 对应的交叉引用。虽然这里没有列出所有命令和概念，但我们认为这对于 z/OS 系统程序员更熟悉 System z 上的 z/VM 和 Linux 来说是一个良好的开端。

在我们的示例中，我们在需要具体说明时引用 SLES10 命令。我们建议检查您的 Linux 发行版以验证命令是否保持不变。

本附录包含以下表格：

- Table A-1 on page 400, Commands for file editing
- Table A-2 on page 400, General commands
- Table A-3 on page 401, FTP and TCP/IP commands
- Table A-4 on page 401, General concepts

### Table A-1 Commands for file editing

| z/OS-ISPF Edit | z/VM CMS XEDIT | Linux vi | Description |
|---|---|---|---|
| `r` | `"` | `yy` | Repeat or copy a line |
| `d` | `d` | `dd` | Delete a line |
| `cc..cc` line command | `cc ...cc` | `:1,3co$` | Block copy |
| `mm...mm` line command | `mm...mm` | `:1,3m$` | Block move |
| `dd...dd` | `dd...dd` | `:1,3d` | Block delete |
| `find <xxxx>` | `/<xxxx>` | `/<xxxx>` | Find keyword (below) |
| `find <xxxx> prev` | `-/<xxxx>` | `?<xxxx>` | Find keyword (above) |
| `ex xxx` | — | — | Exclude lines containing a character string (xxx) |
| `del all excluded` | — | — | Delete the lines that you excluded using the command `ex xxx` |
| `)n` line command | — | — | Indent n spaces to the right |
| `(n` line command | — | — | Move n spaces to the left |

### Table A-2 General commands

| z/OS command | z/VM command | Linux command | Description |
|---|---|---|---|
| `d u,,b120,1` | `q b120` | `ls -la /dev/<device>` | Display a single device named `b120` (replace `b120` with your device) |
| `d u,,b120,8` | `q b120-b127` | `ls -la /dev/sd*` | Display string of devices |
| `v b120,online` | `vary on b120` | `mount /dev/<device> <mnt_point>` | Vary on a device |
| `v b120,offline` | `vary off b120` | `umount mnt_point` | Vary off a device |
| — | `q paths b120` | — | Display paths to a device |
| — | `q chpid 18` | — | Display devices on a chpid |
| `D M=CPU` | `q proc` | `cat /proc/cpuinfo` | Display number of processors |

### 表 A-3 FTP 和 TCP/IP 命令

| z/OS 命令 | z/VM 命令 | Linux 命令 | 描述 |
|---|---|---|---|
| `FTP hostname {port}` | `FTP hostname {port}` 如需选项列表，请输入：`FTP ?` | `ftp hostname <-P port>` | 连接到远程主机以获取或放置文件。默认端口为 21。 |
| `HOMETEST` | `HOMETEST` | `ping <gateway ip address>` | 验证 TCP/IP 配置。 |
| `NETSTAT option {TCP procname}` | `NETSTAT option` | `netstat` | 显示本地主机的网络状态。如需选项列表，请输入：`?` |

### 表 A-4 通用概念

| z/OS | z/VM | Linux |
|---|---|---|
| `IPL`(初始程序加载) | `IPL`(初始程序加载) | `boot` |
| Nucleus | Control Program (CP) | kernel |
| `HELP` 命令 | `HELP` 命令 | `man` 命令 |
| 数据集 `SYS1.UADS` | user directory | user registry |
| TSO 或 ISPF 编辑 | `XEDIT` | `vi` |
| TSO 或 ISPF | Conversational Monitor System (CMS) | shell |

## 规划工作表

填写此工作表以存储您计划用于 System z 上 z/VM 和 Linux 安装的值。

*表 B-1 读者资源工作表*

| 名称 | 值 | 注释 |
|---|---|---|
| LPAR 名称 |  |  |
| CPC 名称 |  |  |
| z/VM 系统名称 |  |  |
| TCP/IP 主机名 |  |  |
| TCP/IP 域名 |  |  |
| TCP/IP 网关 |  |  |
| DNS 服务器 1 |  |  |
| DNS 服务器 2/3（可选） |  |  |
| OSA 设备名称 |  |  |
| OSA 起始设备号 |  |  |
| TCP/IP 地址 |  |  |

## 相关出版物

本节列出的出版物被认为特别适合对本书涵盖主题进行更详细讨论。

### IBM Redbooks

有关订购这些出版物的信息，请参阅第 408 页的“如何获取 Redbooks”。请注意，此处引用的某些文档可能仅提供软拷贝。

- Introduction to the New Mainframe: z/VM Basics, SG24-7316
- Linux Handbook A Guide to IBM Linux Solutions and Resources, SG24-7000
- Linux on IBM System z: Performance Measurement and Tuning, SG24-6926-01
- Security on z/VM, SG24-7471
- z/VM and Linux on IBM System z: The Virtualization Cookbook for SLES 10, SG24-7493

### 其他出版物

这些出版物也是进一步信息来源的相关资料：

- EREP V3R5 User's Guide, GC35-0151
- Linux on IBM System z: Performance Measurement and Tuning, SG24-6926
- Linux on System z: Using the Dump Tools, SC33-8412
- System z Hardware Management Console Operations Guide, SC28-6867
- z/OS: MVS Initialization and Tuning Reference, SA22-7592
- z/OS V1R9.0 Planning for Installation, GA22-7504-17
