

## 表 4-4 一些流行的计算机安全测试工具

| 类型 | 工具名称 |
| :--- | :--- |
| 端口扫描器 | nmap, Strobe |
| 漏洞扫描器 | Nessus Security Scanner, SAINT, SARA, Whisker (CGI 扫描器), ISS Internet Scanner, CyberCop Scanner, Vetescan, Retina Network Security Scanner |
| 网络实用工具 | Netcat, hping2, Firewall, Cheops, ntop, ping, ngr ep, AirSnort (802.11 WEP 加密破解工具) |
| 主机安全工具 | Tripwire, lssof |
| 数据包嗅探器 | tcpdump, Etherleak, dsniff, sni ff it |
| 入侵检测系统 (IDS) | Snort, Abacusporsentry, scanlogd, NFR, LIDS |
| 密码检查工具 | John the Ripper, LC4 |
| 日志分析和监控工具 | log colourise, tcpdstat s, nlog, logcheck, LogWatch, Swatch |

## Nmap

Nmap（network mapper，网络映射器的缩写）是一种端口扫描工具。它可以快速扫描大型网络，并确定网络上有哪些可用的主机、它们提供什么服务、它们运行什么操作系统（以及操作系统版本）、使用了哪种类型的包过滤器或防火墙，以及数十种其他特征。Fedora Core 附带安装了 nmap。您可以在 www.insecure.org/nmap 上阅读更多关于 nmap 的信息。

如果您想尝试使用 nmap 扫描您的局域网，只需键入类似以下命令（请将 IP 地址范围替换为您网络中适当的地址）：

```
nmap -0 -sS 192.168.0.2-10
```

以下是该命令的一个典型输出列表：

```
Starting nmap 3.50 ( http://www.insecure.org/nmap/ ) at 2004-04-14 21:01 EDT
Interesting ports on 192.168.0.2:
(The 1654 ports scanned but not shown below are in state: closed)
PORT STATE SERVICE
135/tcp open msrpc
139/tcp open netbios-ssn
445/tcp open microsoft-ds
1025/tcp open 955-or-IIS
5000/tcp open UPnP
Device type: general purpose
Running: Microsoft Windows 95/98/ME/NT/2K/XP
OS details: Microsoft Windows Millennium Edition (Me), Windows 2000 Professional
or Advanced Server, or Windows XP
```

```
Interesting ports on 192.168.0.6:
(The 1654 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
111/tcp   open  rpcbind
32771/tcp open  sometimes-rpc5
Device type: general purpose
Running: Linux 2.4.X/2.5.X
OS details: Linux 2.5.25 - 2.5.70 or Gentoo 1.2 Linux 2.4.19 rc1-rc7)
Uptime 5.015 days (since Wed Apr 10 20:41:00 2004)
(1 lines deleted...)
Nmap run completed -- 9 IP addresses (3 hosts up) scanned in 167.191 seconds
```

如你所见，*nmap* 显示开放端口的名称，并猜测操作系统的名称和版本号。

## Nessus

Nessus 安全扫描器是一种模块化的安全审计工具，它使用用 Nessus 脚本语言编写的插件来测试各种各样的网络漏洞。Nessus 采用客户端-服务器软件架构，有一个名为 *nessusd* 的服务器和一个名为 *nessus* 的客户端。

![](img/9f89727199836b0f871f1745838aa8b2_616_0.png)

在尝试安装 Nessus 之前，您必须安装 *sharutils* RPM。该包包含 Nessus 安装脚本所需的 *udecode* 实用工具。*sharutils* 包未随任何标准包组一起安装，因此您需要自己安装它。

要安装 *sharutils*，请挂载附带 DVD 并使用以下命令进行安装：

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh sharutils*.rpm
```

要下载并安装 Nessus，请遵循以下步骤：

1. **阅读 www.nessus.org/download.html 上的说明。** 然后按照链接到您想要下载的包。按照说明下载文件 `nessus-installer.sh` 和 MD5。
2. **键入以下命令来安装 Nessus（您必须已安装开发工具，包括 GIMP Toolkit）：**
   ```
   sh nessus-installer.sh
   ```
   响应安装脚本的提示以完成安装。通常您可以按 Enter 键接受默认选择。

安装完成后，请遵循以下步骤使用 Nessus：

1. **以 root 身份登录**，并键入以下命令以创建用于 Nessus 客户端和 Nessus 服务器之间安全通信的 Nessus SSL 证书：
   ```
   nessus-mkcert
   ```
2. **提供所需的信息**以完成证书生成过程。
3. **使用以下命令创建 nessus 账户**：
   ```
   nessus-adduser
   ```
4. **根据提示输入您的用户名、密码和任何规则**（如果您不知道该输入什么规则，请按 Ctrl+D）。然后按 Y 键。
5. **如果需要，您可以通过编辑配置文件 /usr/local/etc/nessus/nessusd.conf 来配置 nessusd。**
   如果您想试用 Nessus，可以使用默认配置文件继续操作。
6. **使用以下命令启动 Nessus 服务器**：
   ```
   nessusd -D
   ```
7. **在终端窗口中键入以下命令运行 Nessus 客户端**：
   ```
   nessus
   ```
   出现 Nessus 设置窗口。
8. **输入 nessusd 用户名和密码**，然后单击 **Log In（登录）** 按钮（如图 4-1 所示）。
9. **当 Nessus 显示用于建立安全连接的证书并询问您是否接受时，单击 Yes（是）。**
   客户端连接到服务器后，Log In 按钮变为 Log Out（注销），其左侧出现 Connected（已连接）标签。
10. **在 Target Selection（目标选择）选项卡中，输入一个 IP 地址范围以扫描**网络中的所有主机。
    例如，要扫描私有网络 192.168.0.0 中的前八个主机，我输入的地址为：
    ```
    192.168.0.0/29
    ```
11. **单击 Start the Scan（开始扫描）。**
    Nessus 开始扫描 IP 地址并检查许多不同的漏洞。进度条显示扫描状态（见图 4-2）。

图 4-1：用户登录前 Nessus 客户端屏幕看起来像这样。

![](img/9f89727199836b0f871f1745838aa8b2_618_0.png)

图 4-2：Nessus 通过进度条显示扫描状态。

![](img/9f89727199836b0f871f1745838aa8b2_618_1.png)

在 Nessus 完成主机的漏洞扫描后，它以图形和文本格式的良好组合显示结果（见图 4-3）。报告是交互式的——您可以选择一个主机地址来查看该主机的报告，并且可以深入查看特定的漏洞（包括标识该漏洞的 CVE 编号）。

![](img/9f89727199836b0f871f1745838aa8b2_619_0.png)

## SAINT

Security Administrator’s Integrated Network Tool（SAINT，安全管理员集成网络工具）扫描各种主机安全漏洞。对于发现的漏洞，SAINT 会显示 Common Vulnerabilities and Exposures（CVE，通用漏洞和暴露）标识符。旧版本的 SAINT 是免费的，但最新版本仅对购买 SAINTWriter 或 SAINTxpress 的用户可用。

您可以从 `www.saintcorporation.com/products/download.html` 下载有限制（仅限于扫描两个主机）的 15 天 SAINT 试用版本，看看它能做什么。您可以决定是否购买完整版。

我不描述下载和安装试用版本的步骤。您可以在下载 SAINT 免费试用版本的页面上找到说明。

## SARA

Security Auditor's Research Assistant（SARA，安全审计员研究助理）是基于 SAINT 的漏洞扫描工具。SARA 扫描已知漏洞，包括 CVE 列表和 SANS Top 20 List（www.sans.org/top20/）中的漏洞。

要试用 SARA，请从 www.arc.com/sara/downloads/ 下载最新版本的 SARA。下载压缩的 tar 文件后，使用以下步骤构建和安装软件：

1. 使用以下命令解包 tar 文件：
   ```
   tar zxvf sara*
   ```
2. 要配置 SARA，键入以下命令：
   ```
   cd sara*
   ./configure
   ```
3. 要构建软件，键入
   ```
   make
   ```

构建 SARA 后，使用以下命令运行它：

```
./sara
```

SARA 启动 Web 浏览器并在 Web 浏览器中显示其用户界面。

您可以通过单击 Web 浏览器左侧的链接来执行各种任务。例如，要执行漏洞扫描，请单击 Target Selection（目标选择）链接。SARA 显示一个表单，您可以在其中提供有关要扫描的主机和网络的信息。您还可以指定扫描级别——从轻度到极端。

填写完信息后，单击表单底部的 Start the Scan（开始扫描）按钮。SARA 开始执行漏洞扫描。在扫描过程中，SARA 显示一个数据收集页面，指示扫描进度。

扫描完成后，您可以继续数据分析并查看漏洞信息。

