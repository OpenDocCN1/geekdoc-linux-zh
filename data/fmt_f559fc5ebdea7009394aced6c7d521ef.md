
同样，`sftp` 命令会与支持 SSH 连接的 FTP 服务器启动交互式 FTP 会话。许多注重安全的人倾向于使用 `sftp` 而其他 `ftp` 客户端，因为在你和远程主机之间提供了一个安全连接。这里有一个示例：

```bash
$ sftp ftp.handsonhistory.com
Connecting to ftp.handsonhistory.com
passwd: ********
sftp>
```

此时，你可以开始交互式 FTP 会话。你可以像使用任何 FTP 客户端一样对文件进行 `get` 和 `put` 操作，但又有知道正在安全连接上工作的舒适感。

> 提示：`sftp` 命令与 `ssh` 和 `scp` 一样，要求服务器上运行 SSH 服务。如果你无法使用 `sftp` 连接到 FTP 服务器，可能是 SSH 服务不可用。

# 无需密码使用 ssh、scp 和 sftp

对于你经常使用的机器，将它们配置为无需使用密码即可登录通常非常有帮助。下面的步骤将向你如何操作。

这些步骤将引导你完成从一台机器到另一台机器的无密码认证。在本示例中，本地用户是名为 `host1` 的计算机上的 `chuckw`。远程用户也是名为 `host2` 的计算机上的 `chuckw`。

- 1. 登录本地计算机（在本示例中，我以 `chuckw` 身份登录 `host1`）。

注意：仅在本地工作站上作为本地用户运行第 2 步。除非丢失了 `ssh` 密钥，否则不要再次运行。配置后续的远程服务器时，跳到第 3 步。

- 2. 输入以下内容生成 `ssh` 密钥：

```bash
ssh-keygen -t dsa
```

- 3. 按每个请求按回车接受默认设置。

- 4. 输入以下内容将密钥复制到远程服务器（将 `chuckw` 替换为远程用户名和主机名）：

```bash
cd ./.ssh
scp id_dsa.pub chuckw@host2
```

- 5. 输入以下内容将密钥添加到授权密钥（将 `chuckw` 替换为远程用户名和主机名）：

```bash
cat id_dsa.pub | ssh chuckw@host2 "authorized_keys"
```

- 6. 输入以下内容测试登录：

```bash
ssh -i ~/.ssh/id_dsa chuckw@host2
```

# 使用 Portentry 守护计算机

当 `Logentry` 收集入侵信息时，`Portentry` 了更主动的方法来保护你的系统。当 `Portentry` 感知到攻击时，它会以各种方式做出反应。默认情况下，`Portentry` 可以记录入侵尝试并阻止入侵者访问。`Portentry` 还提供了使用其他工具来响应入侵的方法，包括防火墙规则、路由更改和主机拒绝配置。

除了 `Portentry` 模式和被监控的端口外，你还可以选择计算机被扫描时的响应方式。`PortSentry` 对有关活动的日志消息进行排序。`Portentry` 运行在几种不同的模式下。这些模式中的每一种都可以应用于 TCP 和 UDP：

- Basic（基础）——这是 `Portentry` 使用的默认模式。选定的 UDP 和 TCP 端口会被 `PortSentry` 绑定。

- Stealth（隐身）——在这种模式下，`Portentry` 监听套字而不是绑定端口。`Portentry` 可以检测各种扫描技术（扫描式、SYN、NULL、XMAS），但因为它比基础模式更敏感，可能会产生误报。

- Advanced Stealth（高级隐身）——这种模式提供了与隐身模式相同的检测方法，但它监控所有指定的端口端口（默认1023）。你可以排除某些端口的监控。这种模式比隐身模式更敏感。

> 注意：当端口被 `Portentry` 或其他服务守护进程“绑定”时，来自网络的所有该端口的请求都由绑定进程处理。例如，如果 `http` 守护进程绑定端口80，网络 Web 服务请求将由 `httpd` 处理。

# 下载并安装 Portentry

`portsentry` 软件包未包含任何 Fedora 或 Red Hat Linux 发行版中。你可以从任何 Red Hat FTP 镜像站点或 `rpmfind.net` 网站下载软件包。本章使用的 `portsentry` 软件包是 `portsentry-1.0.11.i386.rpm`（Red Hat 作为 7.1 PowerTools 的最后一个版本）。下载 `Portentry` 后，在其目录下运行以下命令：

安装的 `portsentry` 软件包包含多个配置文件（位于 `/etc/portsentry` 目录）、`portsentry` 启动脚本 (`/etc/init.d/portsentry`) 以及 `portsentry` 命令（位于 `/usr/sbin/bin`）。在 `/usr/share/doc/portsentry*` 目录下也有感兴趣的 README 文件。

# 作为 Portentry 使用

与 `Logentry` 一样，安装 `Portentry` 后，你不需要进行任何操作即可使其工作。默认情况下，当你安装 `portsentry` 软件包时，`Portentry` 执行以下操作：

# 第三部分：管理 Fedora

- `/etc/init.d/portsentry` 启动脚本会在系统启动到运行级别 3、4 或 5 时自动运行（级别 3 和 5 最常用）。

- 以下端口号被配置为由 `PortSentry` 在基本模式进行监控：

TCP: 1, 11, 15, 143, 540, 635, 1080, 1524, 2000, 5742, 6667, 12345, 12346, 20034, 31337, 32771, 32772, 32773, 32774, 40421, 49724, 54320

UDP: 1, 513, 635, 640, 641, 32770, 32771, 32772, 32773, 32774, 31337

- 为了响应攻击（表现为对被监控端口的扫描），所有进一步尝试连接该协议（TCP 或 UDP）下任何服务的尝试都将被阻止。

被阻止访问你系统的计算机列在 `portsentry.blocked.tcp` 或 `portsentry.blocked.udp` 文件中（位于 `/var/portsentry` 目录），具体取决于扫描的是哪种协议（TCP 或 UDP）。通过从这些文件中删除条目，可以恢复被阻止计算机的访问权限。

# 配置 PortSentry

你可能想对 `PortSentry` 的运行方式进行一些更改。要更改 `PortSentry` 的行为，请修改 `/etc/portsentry/portsentry.conf` 文件。在该文件中，你可以选择要监控的端口、监控的模式以及在检测到扫描时采取的响应。

- 阻止远程计算机的访问

- 将来自远程计算机的消息重定向到死主机

- 添加防火墙规则以丢弃来自远程计算机的数据包

你可能还想更改的另一个文件是 `/etc/portsentry/portsentry.modes`。`portsentry.modes` 文件仅包含 `PortSentry` 可以运行的模式。

# 修改 portsentry.conf 文件

要以 root 用户身份编辑 `portsentry.conf` 文件，请使用任何文本编辑器打开 `/etc/portsentry/portsentry.conf`。以下章节描述了该文件中更改的信息。

# 选择端口

`portsentry.conf` 文件定义了在基本模式下监控哪些端口。默认情况下，只有基础 TCP 和 UDP 端口是激活的，因此只监控这些端口（除非你更改了其中一种隐身模式）。`TCP_PORTS` 和 `UDP_PORTS` 选项定义了要监控的端口。是它们在 `portsentry.conf` 文件中的显示方式：

```
TCPPORTS="1,11,15,143,540,635,1080,1524,2000,5742,6667,12345,12346,20034,31337,32771,32772,32773,32774,40421,49724,54320"
UDPPORTS="1,513,635,640,641,700,32770,32771,32772,32773,32774,31337,54321"
```

除非你是 TCP/IP 专家，否则你可能好奇这些端口代表什么。互联网数字分配机构 (IANA) 将服务分配给 UDP 和 TCP 端口。你可以在以下网络地址查看这些分配：

`www.iana.org/assignments/port-numbers`

Fedora 中的网络服务（以及其他 Linux/Unix 系统）从 `/etc/services` 文件分配端口号分配。因此，通常情况下，你只需检查 `/etc/services` 文件，就可以找到大多数分配到被扫描端口的服务。

用于监控的端口分配基于几个不同的标准。选择低端口（1, 11, 15 等）是为了捕获那些从端口 1 开始扫描并扫描几百个端口的端口扫描器。如果扫描器在访问端口 1 后被阻止，它将无法获取关于你计算机上可能存在的其他端口的信息。另一个标准是包含入侵者专门检查的端口，因为这些服务可能容易受到攻击。它们包括 `systat`（端口 11）和 `netstat`（端口 15）。

如果你实际上正在运行分配给某个端口的服务，则需要从 `portsentry.conf` 文件的列表中删除端口。相反，如果你对攻击感到偏执并希望获得更多覆盖，你可能想向列表中添加端口。`portsentry.conf` 文件包含一些示例，你可以取消注释（删除 `#` 符号）以便对这些端口进行监控。

如果你从基本扫描切换到隐身扫描（如本章稍后章节的“修改 portsentry.modes”部分所述），则被监控的端口由 `ADVANCED_PORTS_TCP` 和 `ADVANCED_PORTS_UDP` 选项定义。以下是这两个选项的默认设置：

```
ADVANCED_PORTS_TCP="1023"
ADVANCED_PORTS_UDP="1023"
```

前面的条目表示从 1 到 1023 的所有端口都将被监控。由于监控高端口可能会导致许多警报，因此不建议这样做。如果你发现误触发了 `ADVANCED_PORTS_TCP` 或 `ADVANCED_PORTS_UDP`，则可以更改它们。以下是这些选项的默认设置：

```
ADVANCED_PORTS_TCP="111,113,339"
ADVANCED_PORTS_UDP="520,138,67"
```

默认情况下，对于 TCP（111, 113, 339）和 UDP（520, 138, 67），`PortSentry` 的响应是重定向到死主机。

# 识别文件

你可以通过以下文件列出阻止访问你系统的计算机，取决于扫描的是哪种协议（TCP 或 UDP）。为了阻止远程计算机的访问：

- 阻止远程计算机的访问

- 将来自远程计算机的消息重定向到死主机

- 添加防火墙规则以丢弃来自远程计算机的数据包

设置上述选项后，`$TARGET` 将替换为入侵远程计算机的 IP 地址，并且引号中的行将添加到 `/etc/hosts.deny` 文件中。例如，如果远程计算机的 IP 地址为 10.0.0.59，那么在 `/etc/hosts.deny` 中出现的行将是：

```
ALL: 10.0.0.59
```

- `KILL_RUN_CMD` — 与其使用防火墙、重定向或 TCP wrappers 来阻止入侵计算机访问你的计算机，你可以根据需要选择任何方法作为响应。当 `BLOCK_TCP` 和 `BLOCK_UDP` 选项设置为 "2" 时，`KILL_RUN_CMD` 的值将在对你监控端口进行扫描时执行。

`KILL_RUN_CMD` 的值应该是你想运行的脚本的完整路径，加上任何选项。要包含远程计算机的 IP 地址或被扫描的端口号，请分别包含 `$TARGET` 或 `$PORTS` 变量。以下是你可能想要修改的示例：

`KILL_RUN_CMD=/path/here/script $TARGET $PORTS$`

> 警告：不要使用任何 `KILL_RUN_CMD` 对入侵的远程主机进行报复。首先，扫描你端口的计算机本身可能已经被破解，它不是报复的有效目标；其次，报复可能会激怒黑客对你进行进一步攻击。

- PORT BANNER — 你可以通过设置 `PORT_BANNER` 选项向触发 `PortEntry` 监控的人发送消息。默认情况下，没有定义任何消息。但是，你可以取消以下行的注释来使用该消息。（不建议使用侮辱性消息。）

`PORT BANNER="** UNAUTHORIZED ACCESS PROHIBITED ***

YOUR CONNECTION ATTEMPT HAS BEEN LOGGED. GO AWAY."`

`PortEntry` 在触发上述响应之前接受入侵计算机的扫描次数可以使用 `SCAN_TRIGGER` 选项进行设置。默认情况下，该选项设置如下：

```
SCAN_TRIGGER="0"
```

"0" 表示你不会接受来自入侵系统的扫描。换句话说，第一次扫描就会触发 `PortEntry` 监控。你可以增加此值以容忍一个或多次错误的扫描（你可能并不希望这样做）。

## 修改 portsentry.modes 文件

`/etc/portsentry/portsentry.modes` 文件定义了 `PortEntry` 命令在启动时运行的模式。该文件的内容如下所示：

```
tcp
udp
```

```
#stctp
#sudp
#atcp
#audp
```

`tcp` 和 `udp` 选项分别是针对 TCP 和 UDP 服务的基本 `PortSentry` 模式。你的其他选项包括隐身 TCP (`stctp`)、高级 TCP (`atcp`)、隐身 UDP (`sudp`) 和高级 UDP (`audp`)。只运行一个 TCP 服务和一个 UDP 服务。因此，如果你取消了隐身或高级服务的注释，请确保在相应的基础服务前面添加注释。

要激活新服务，请执行以下命令：

```
# /etc/init.d/portsentry restart
```

新的 `PortSentry` 模式将立即生效。这些新模式在计算机重启后仍然有效。

## 测试 PortSentry

你可以通过不同的方法测试端口是否得到了良好的保护。你想运行一个潜在入侵者会运行的程序，并查看它是否触发了 `PortSentry` 响应。例如，你可以使用端口扫描器查看你的端口在外部世界是如何显示的。你还可以使用如 `telnet` 等命令尝试触发特定端口以查看 `PortSentry` 是否捕获了它。

`nmap` 是一个扫描 TCP 和 UDP 端口的流行工具。你可以给 `nmap` 命令提供主机名或 IP 地址，它将扫描计算机上的约 1500 个端口，以查看哪些端口是开放的（并假设提供了可能被破解的服务）。

也有 `nmap` 的 RPM 包。你可以下载 `nmap-frontend` 包，它包含一个名为 `nmap` 的简单图形界面用于运行。我建议在运行 `PortSentry` 的系统以及局域网中的另一台系统（如果可用）上安装这些包。然后并在 `PortSentry` 系统上执行以下步骤进行测试：

1. 如果 `PortSentry` 正在运行，输入以下命令将其关闭：

   `# /etc/init.d/portsentry stop`

2. 输入以下 `nmap` 命令查看本地系统上开启了端口：

   `# nmap -sB -O 127.0.0.1`

   `# nmap -sU -O 127.0.0.1`

输出显示了你的计算机上目前分别为 TCP 和 UDP 协议提供服务的端口。

3. 如果有任何你不需要的服务，你应该使用 `chconfig service off`（将 `service` 替换为服务名称）关闭这些服务，或者通过编辑 `/etc/xinetd.d` 目录下代表该服务的配置文件并将 `disable = no` 更改为 `disable = yes`，或者更改防火墙设置。

- 如果你有想要从你的计算机提供的服务，请确保代表这些服务的端口号没有被 `PortSentry` 监控。从 `/etc/portsentry/portsentry.conf` 文件中的 `TCP_PORTS` 和 `UDP_PORTS` 选项中删除端口号。

- 重启 `PortSentry`：

`# /etc/init.d/portsentry restart`

## 第四部分

# Fedora 网络与服务器设置

第 15 章：设置局域网

第 16 章：连接互联网

第 17 章：设置打印服务器

第 18 章：设置文件服务器

第 19 章：设置邮件服务器

第 20 章：设置 FTP 服务器

第 21 章：设置 Web 服务器

第 22 章：设置 LDAP 地址簿服务器

第 23 章：设置启动服务器：DHCP 和 NIS

第 24 章：设置 MySQL 数据库服务器

第 25 章：通过 DNS 使服务器公开

第 26 章：从 Mac 使用 Linux 服务器

## 第 15 章

### 设置局域网

**本章**

- 了解局域网

- 设置有线以太网局域网

- 设置无线局域网

- 局域网故障排除

在家庭或小型企业中，对于网络连接，Fedora 可以帮助你连接到其他 Linux、Windows 和 Macintosh 计算机，以便共享你的计算设备（文件、打印机和设备）。添加互联网连接并在多个局域网之间进行路由（在第  6 章描述），Fedora 可以作为大型企业网络计算的中心。

本章将帮助你建立自己的局域网（LAN）。这里描述的程序为在家庭或组织中共享计算资源提供了基础。特别是本章描述了如何使用以太网卡、布线和协议来连接计算机。它将具体告诉你如何配置你的 Fedora 计算机，使其能够与其他计算机通信。

## 了解局域网

通过局域网（LAN）连接组织内的计算机可以节省大量的时间和金。你在网络硬件上投入的资金，即使在小型配置中（少于五六个用户），也能避免你购买多台打印机、备份介质和其他硬件。添加一个共享的互联网连接，你就不再需要多个介质和互联网账户了。

有了局域网，你不需要为了在朋友的打印机上打印文件而费地把整个文件带到磁盘。以前必须等待收发室分发的信息可以瞬间发送给局域网内的任何（（或所有人）。
