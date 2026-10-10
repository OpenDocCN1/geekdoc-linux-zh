
- **打印 (Printing)**：配置打印机。

- **root (Root)**：配置 root 设置。

- **Samba**：配置 Samba 共享。

- **声卡 (Soundcard)**：更改声卡设置。

- **日志 (Log)**：显示日志消息。

- **用户与组 (Users & Groups)**：更改用户和组。

- **启动文件 (Kickstart)**：创建启动文件。

- **磁盘使用 (Disk Usage)**：分析磁盘使用。

## 462 第 10 章：理解系统管理 421

- **系统监控 (System Monitor)**：显示运行进程和资源使用。

## 管理命令

许多命令仅供 root 使用。当你作为 root 登录时，你的 `$PATH` 会包含某些命令所在的目录。这些包括：

- `/sbin`：包含修改磁盘分区（如 `fdisk`）、更改引导程序（`grub`）和更改状态（`init`）的命令。

- `/usr/sbin`：包含管理用户帐户（如 `useradd`）和检查网络流量（`wireshark`）的命令。作为守护进程运行的命令也包含在该目录。

某些管理命令位于普通用户目录，如 `/bin` 和 `/usr/bin`。这对于所有人可用的某些命令尤其如此。例如 `/bin/mount` 命令，任何人都可以列出挂载的文件系统，但只有 root 可以挂载它们。

要查找主要用于系统管理员的命令，请查看第 8 部分帮助页（通常位于 `/usr/share/man/man8`）。它们包含了大多数 Linux 命令的描述和选项。例如，要查看 `fdisk` 命令的帮助页（`/usr/share/man/man8/fdisk.8.gz`），输入：

```
$ fdisk
```

第三方应用程序会将命令添加到不在 `PATH` 中的目录中。例如，应用程序可能会将其放在 `/usr/local/bin`（最常见位置）、`/opt/bin` 或 `/usr/local/sbin`。虽然 `/usr/local/bin` 和 `/usr/local/sbin` 分别已在每个用户的路径中，你可能需要将 `/opt/bin` 或其他目录添加到你的 `PATH` 中。

## 配置文件

配置文件是 Linux 管理另一个支柱。你为特定计算机设置几乎一切——用户帐户、网络地址或 GUI 偏好——都存储在纯文本文件中。这有优点也有缺点。

纯文本文件的优点是容易阅读和修改。任何文本编辑器都可以。然而，缺点是，当你编辑配置文件时，没有任何错误检查。你需要运行读取这些文件的程序（如守护进程或 X 桌面）以检查你是否正确设置了文件。逗号或引号的位置不正确可能会导致整个界面运行失败。

在本书中，我描述了设置不同功能（构了 Fedora 和 RHEL 系统）时需要的配置文件。然而，从配置文件的通用角度来看，在 Fedora 或 RHEL 文件系统中有几个位置存储了配置文件。以下是一些主要位置：

- `$HOME` — 所有用户都在其家目录中存储了信息，这些信息指导了其登录账户的行为。`$HOME` 中的大多数配置文件以点（/）开头，因此当你使用标准的 `ls` 命令时，它们不会显示为用户目录（你需要输入 `ls -a` 才能看到它们）。点文件定义了每个用户的 shell 行为、桌面的外观和感受，以及使用文本编辑器的选项。甚至还有文件（如 `.ssh/*` 和 `.bashrc`）可以为每个用户配置网络权限。

- `/etc` — 此目录包含了大多数基础 Linux 系统配置文件。以下 `/etc` 配置文件值得关注：

    - `adjtime` — 存储调整硬件时钟的数据（参见 `hwclock` 页面）。

    - `aliases` — 可以包含 Linux 邮件服务使用的发行列表。

    - `bashrc` — 为 bash shell 用户设置全局默认值。（默认情况下，它将 shell 提示设置为包含当前用户名、主机名、当前目录和其他值。）

    - `cdrecord.conf` — 包含刻录 CD 的设置。

    - `crontab` — 包含运行自动化任务的 cron 环境和时间。

    - `csh.cshrc` (或 `cshrc`) — 为 csh (C shell) 用户设置全局默认值。

    - `dovec` — 包含支持 do IMAP4/POP3 邮件服务所需的信息。

    - `esd.conf` — 设置 Enlightenment Sound Daemon 使用的选项，将多个流混合到单个音频输出中。

    - `exports` — 包含本地目录列表，这些目录可以通过网络文件系统 (NFS) 供远程计算机共享。

    - `fedora-release` — 包含识别当前 Fedora 版本的字符串。对于 RHEL 版本，该文件名为 `redhat-release`。

    - `fstab` — 识别常见存储媒体（硬盘、软盘、CD-ROM 等）的设备以及它们在 Linux 系统中的挂载位置。这被 `mount` 命令用于选择挂载哪些文件系统。

    - `group` — 识别系统上定义的组名和组 ID (GIDs)。Linux 中的组权限由与每个文件和目录关联的三组 rwx（读、写、执行）位中的第二组位定义。

    - `gshadow` — 包含组的影子密码。

    - `host.conf` — 设置在为 TCP/IP 网络（如互联网）搜索域名（例如，`redhat.com`）的位置。默认情况下，会搜索本地 `hosts` 文件，然后是 `resolve.conf` 中的任何名称服务器条目。

    - `hosts` — 包含从你的计算机可以的 IP 地址和主机名（通常此文件用于存储局域网或小型私有网络上的计算机名称）。

    - `hosts.allow` — 列出允许使用本地计算机某些 TCP/IP 服务的主机计算机。

    - `hosts.deny` — 列出不允许使用本地计算机某些 TCP/IP 服务的主机计算机（默认不存在）。

    - `inittab` — 包含定义 Linux 启动、关机或进入不同状态（运行级别）时启动和停止哪些程序的信息。这是启动 Linux 最基本的配置。

    - `issue` — 包含当终端准备好让你从本地终端或文本模式控制台登录 Fedora 或 RHEL 系统时显示的行。

    - `issue.net` — 包含显示给尝试使用 telnet 服务从网络上的计算机登录 Linux 系统的用户的登录行。

    - `mail.rc` — 设置与使用邮件相关的全局参数。

    - `man.conf` — 用于 `man` 命令用于确定帮助页位置的默认路径。

    - `modprobe.conf` — 包含与你的计算机使用的可加载内核模块相关的别名和选项。

    - `mtab` — 包含当前已挂载的文件系统列表。

    - `mtools.conf` — 包含 Linux 中 DOS 工具使用的设置。

    - `named.conf` — 如果你正在运行 DNS 服务器，则包含 DNS 设置。

    - `ntp.conf` — 包括运行网络时间协议 (NTP) 所需的信息。

    - `passwd` — 存储系统所有有效用户的账户信息。还包括其他信息，如家目录和默认 shell。

    - `printcap` — 包含为你的计算机配置的打印机定义。

    - `profile` — 为所有用户设置全局环境和启动程序。该文件在用户登录时被读取。

    - `protocols` — 设置各种互联网服务的协议编号和名称。

    - `redhat-release` — 包含识别当前 Red Hat 版本的字符串。此文件存在于 Red Hat Linux 和 Red Hat Enterprise Linux 系统上。在 Fedora 系统上，此文件作为指向 `fedora-release` 文件的链接，以便在 `redhat-release` 文件中查找信息的应用程序不会失败。

    - `resolv.conf` — 识别使用 TCP/IP 将 host.domain 域名转换为 IP 地址的 DNS 名称服务器的位置。

    - `rpc` — 定义远程过程调用名称和数字。

    - `services` — 定义 TCP/IP 服务及其端口分配。

    - `shadow` — 包含组的影子密码。（等等，通常 shadow 用于用户的，gshadow 是用于组的；根据上下文纠正：shadow 包含用户的密码）。

    - `shells` — 列出系统可用的 shell。

    - `sudoers` — 包含谁可以使用 sudo 命令的文件。

    - `syslog.conf` — 包含日志记录的配置。

    - `termcap` — 终端定义。

    - `xorg.conf` — 包含 X 窗口系统的配置。

    - `alternatives` — 包含不同版本软件链接。

    - `amanda` — 包含用于备份的文件。

# 第三部分：管理 Fedora RHEL

- `/etc/uucp` — 包含用于 Taylor UUCP 的配置文件（uucp 设施的一个非标准版本，用于与其他计算机创建调制解调器、直接线路和其他串行连接）。
