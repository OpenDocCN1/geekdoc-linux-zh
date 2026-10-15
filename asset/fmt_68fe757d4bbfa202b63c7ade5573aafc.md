
`-h` - 打印此屏幕

`-s` - 速度/波特率 默认 `[1200]` `[IAX2 模式禁用]`

`-p` - 校验位（无/偶/奇奇） `[串口默认: 'N']` `[IAX2 模式禁用]`

`-d` - 数据位 `[串口默认: 8]` `[IAX2 模式禁用]`

`-u` - 使用软（调制调器） `[串口默认: /dev/ttyS0]` `[IAX2 模式禁用]`

`-c` - 使用软件控制（开启/关闭） `[串口为硬件流控]` `[IAX2 模式禁用]`

`-f` - 输出日志文件 `[默认: iwar.log]`

`-g` - 拨号前字符串/号码 `[可选]`

`-i` - 拨号范围 `[可选]`

`-t` - 音调连接（音调方法） `[串口默认]` `[IAX2 模式禁用]`

`-r` - 扫描范围（例如 `- 5551212-113`）

`-x` - 顺序拨号 `[默认: 随机]`

`-F` - 完整日志（忙忙、信载、超时、跳过、等.）

`-b` - 禁用横幅检查 `[串口默认: 开启]` `[IAX2 模式禁用]`

`-o` - 禁用记录 `[串口默认: 开启]` `[IAX2 模式禁用]`

`-L` - 从文件加载要拨打的号码

`-l` - 加载状态文件（之前拨打过的号码）

要求

不需要特殊设备：你只需要一台 Linux 机器和一个调制调器。根据你想要使用的功能，你可能需要软件/硬件。你可以从 `http://freshmeat.net/projects/ward/` 下载它。

## ward

`ward` 由著名的 Marcus Ialdi (`raptor@deadbeef.info`) 编写，是一个相当老老的自动拨号工具。考虑到它的年代，它应该运行在从最旧到最新的所有 Linux 发行版上。它支持随机和顺序扫描。你也可以强制指定范围，但这是在顺序扫描下进行的。对于随机扫描，使用 `-r`；否则，默认将是顺序的。如果没有指定配置文件，输出将写入屏幕，但你可以通过 `-L` 指定日志文件或在配置文件中更改它（参见帮助）。如果启用了 `-d`（守护进程模式）选项，程序将在后台运行，这样你就可以做其他事情；它仍然记录到 `/dev/tty`。`-c`（配置文件）选项允许 `ward` 从配置文件读取。该文件可以是任何格式，并将使用多个字符串作为页码。

要求

你只需要一个调制调器和一条电话线。你可以从 `http://www.ward.org/` 下载它。

`ward` 是一个为 UNIX 系统编写的非常好、轻量且快速的 C 语言自动拨号工具，其特殊之处可以在 PSTN、ISDN 和 GSM 网络上运行。由 Marcus Ialdi 编写。

# PSDN 测试工具

本节详细介绍了我们识别出的几个开源工具，可供你在执行 PSDN 渗透测试时个人或专业用途使用。

X.25 世界的扫描方法与 PSTN 和 ISDN 世界截然不同：X.25 地址不是公开的，且不应泄露。此外，X.25 网络上的攻击者通常具有极高水平，因为 X.25 客户主要是金融机构、政府、军事机构以及各类企业和跨国公司。

正因如此，只有两个开发者决定在公开领域发布他们的 X.25 扫描器。年前，我编写了世界上第一个 VAR/VMS X.25 扫描器，此后其他朋友也为 *NIX 和 Linux 平台 编写了类似的软件。本节还描述了其他几个用于 *NIX 的 X_25 扫描器。希望你的地下关系足够强大，能够获取它们。

## admx25

`Admx25` 是地下世界最流行的 X.25 扫描器之一，但它不对公开放。如果你恰好认识 antilove 或 ADM 的某些成员，可以向他们索要这个强大工具的副本。

## Anonymous 编写的 Solaris 多线程多通道 X.25 扫描器

这个工具非常私密，甚至没有正式名称。我们个人认识编写代码的人，并可以证实它的运行效果优于任何扫描器。它可以作为你的 Solaris 机器使用许多 X.25 逻辑线路，从而实现极快速的大规模扫描：该工具可以在几小时内扫描整个 X.25 网络（比比一个国家）。

尽管它运行在 Solaris 上，但我们决定提到这个工具，因为它确实是全球范围内最好的。

## vudu

`vudu` 是一个用于 Unix 系统的简单 X.25 NUA 扫描器，由 Marco “Raptor” Ivaldi 编写。他的主要目标是可移植性，因此使用 shell 脚本语言编写，没有任何花哨功能。该工具已经在 Sun Solaris 上经过了广泛测试。

记得更改变量以适应你操作系统的需求。不用说，你需要执行脚本的 Linux 或 *NIX 机器必须配备配置恰当的 X.25 卡和活跃的 X.25 链路，并在现有物理通道上有一个或多个逻辑通道。

使用方法：

```
./vudu 020805740 535 542 [谁能忘记 QSD? :)]
```

你可以在 `http://www.deadbeef.info/code/vudu` 下载它。

# 第 6 章：非常规的数据攻击向量

## TScan

`TScan` 是一种 X.25 扫描器，专门用于通过 X.28 拨号扫描 SprintNet（前身为 GTE TeleNet）X.25 网络。你可以轻松地将其适配到你喜欢的 X.25 网络，即使由于 SprintNet 的特殊性，它依赖于你启动回程付费扫描。许多其他网络也允许此功能，因此你应该仔细测试 `TScan` 在 X.25 网络上的可移植性。

要使用 `TScan`，请找到一个连接到 PAD 的本地拨号电话。当你需要时，将你喜爱的终端软件（micom, seyon, telix 等）的设置设置为 7 数据位、1 停止位和偶数校验（扫描器默认使用此设置）。

当以低于 1200 波特的速率连接到本地拨号/PAD 时，你需要发送几个“回车键”。当在高速率（9600+）下连接时，发送一个 `@` 后跟一个回车键。

`TScan` 已经在 Intel 平台的 FreeBSD 和 OpenBSD 上经过测试。它在 Sun Spark OpenBSD 安装上似乎也能良好编译（并可能正常工作）。`TScan` 由 `beanie@softwink.com` 编写。你可以从 `http://www.vistech.net/users/beave/tscan-0.2.tar.gz` 或 `ftp://ftp.vistech.net/pub/tscan` 下载（后者会不在线）。

## 常见 banner（BANNERS）

接下来是一些常见的 banner及其对应的操作系统。通过这些 banner，你可能会发现仍然可用的默认账户。在任何情况下，请记住识别你正在处理的连接类型，这意味着 RAS 不仅仅是一个 RAS，还可能是 IT 管理的 RAS、警报拨号，或本章前面提到的任何其他类型的拨号连接。

**Cisco 路由器** 在处理属于中小企业和公司的网络时，Cisco 路由器经常用作 PSTN、ISDN 或 X 接入服务器。

它将以以下方式自我介绍（banner 可能存在也不存在）：

```
***********************************************

Access to this computer system is limited to authorised users only. *

Unauthorised users may be subject to prosecution under the Crimes *

*

*

* Act or State legislation

*

*

*

**Please note, ALL CUSTOMER DETAILS are confidential and must** *

**not be disclosed.********************

************************************************

User Access Verification
Password:
Password:
Password:
% Bad passwords
```

也可能得到不同的输出，在仅请求密码的地方，你可能会发现：

```
#### [公司名称] [国家] [节点号] #####
###### [网络和/或服务名称] ######
################# In case of problems, ############
################ contact Mr. Joe Doe ############
################ at extension n. 2222 ############
####################################

User Access Verification

Username:
```

在处理属于中小企业（SME）和公司的网络时，Shiva LAN 路由器经常被用作 PSTN 或 X.25 接入服务器。

它将以以下方式自我介绍（banner 可能存在也不存在）：

```
***********************************************
Access to this computer system is limited to authorised users only. *
Unauthorised users may be subject to prosecution under the Crimes *
*
*
* Act or State legislation
*
*
*
**Please note, ALL CUSTOMER DETAILS are confidential and must** *
**not be disclosed.********************
************************************************

User Access Verification

Password:

Password:

Password:

Password:

% Bad passwords
```

（注：提供的 OCR 文本在第 186-187 页关于重复章节包含了一些重复/不连续。我已根据提供的文本结构维护了逻辑流。）

# 第 6 章：非常规的数据攻击向量

已连接到节点 "XXX" 控制端口，时间为 2002年10月10日10:33:22

Codex 6505 PAD, 版本 V.13

Copyright (C) 1989-1992 Motorola Information Systems

Enter Password:

```
+   Node: XXX Address: 3110210000 Date: 10-OCT-2002 Time: 10:35:21
Menu: Main Path: (Main)
1. Logout
2. Examine
3. List
4. Monitor
5. Status/Statistics
6. Configure
7. Boot
8. Update System Parameters
9. Copy/Insert Record
10. Delete Record
11. Port/Station/Channel Control
12. Diagnostics
13. Default Node
14. Print Configuration
15. Configuration Save/Restore
```

Digital Equipment Corporation DECServer DECServer 正如其名，是由数字设备公司（后被 Compaq 收购，后被 HP 收购）制造的服务器，也就是我们使用的 VAX 和 Alpha 机器的同一公司。

DECServer 常见于 PSTN 和 X.25 网络。在请求用户名时，你可以输入任何值，因为系统不会进行检查。

```
****************************************************************

Welcome to [公司名称] DEC Server 3100 on Node XYZ

Username:
```

Stratus Vatus VOS 是 Stratus Inc. 的一种操作系统。它通常用于不停机环境中的重型分析和生产任务，例如信用卡管理、大型机软件开发以及一般的银行应用程序。

在公共和私有 X.25 网络上进行 PSDN 扫描时，可以对其进行攻击。

```
System/32, Release 10.4, Module %acme#ml
#bsh01#ml
23:22:47

Login:

Password:

login: Access denied.

Maximum number of access attempts has been exceeded. %bsh01#vt_open_1
```

# 攻防破解 Linux：Linux 安全秘密与解决方案

PRIMOS 由 Prime Inc. 开发。运行在 Prime 公司的主机上，Primos 操作系统被相当广泛地，通常出现在全球的 PSDN 中，尽管主要由电信运营商使用。

```
PRIMENET 23.3.0 INTENCOM!
```

HP3000 是惠尔公司的一台老式机器，运行在 MPE/V、iX、X 或 XL OS 上。它可以在 PSTN 和 X.25 网络上找到，通常没有横幅显示（banner）。更多信息可以访问 `http://docs.hp.com/` 和 `http://en.wikipedia.org/wiki/HP3000`。

```
MPE:

EXPECTED A :HELLO COMMAND (CIERR 6057)

MPE:

EXPECTED [SESSION NAME],USER.ACCT[,GROUP] (CIERR 1424)

or

EXPECTED HELLO, :JOB, :DATA, OR (CMD) AS LOGON. (CIERRR 1402)

MPE: HELLO FIELD.SUPPORT

Password = =
```

VCX Pad，VCX Pad 可以在全球的 X.25 网络上找到，在欧洲、美国、某些非洲和亚洲国家、澳大利亚和新西兰特别盛行。

VCX PAD NODE SFFERANET
否则，你可能会遇到一个通用的提示符，没有横幅请求：

```
[company_name] orig-
Or also:

VCX Pad

Release 1.3.9.7

Service name?
```

## 第 6 章：非常规的数据攻击向量

Pick Systems 由 Dick Pick 先生创建（没开玩笑！）。这些机器在 70 年代到 80 年代前半叶被广泛分发。Pick Systems 公司总部位于加利福尼亚州尔新市，在英国、法国、南非和新加坡设有销售和支持办公室。这些也是你在 X.25 网络上找到 Pick 机器的国家。

你可以通过其登录提示符轻松识别 Pick 系统，该提示符通常包含小时、日期和登录请求。

更多信息可以访问 `http://www.picksys.com/index.html` 和 `http://en.wikipedia.org/wiki/Pick_operating_system`。

UN 2001 07:05:54 Logon please:

IBM VM/CMS 代表虚拟虚拟机/CMS，是 IBM 的一台 S/390 主机。VM/CMS 通常连接到 SIM3270、3278、VTAM 和 ISM 系统。它们主要用于教育环境（美国的大学）、大型公司和金融环境。

或

.Please Logon:

但也有（在其标准版本中）：

```
VM/ESA ONLINE--XXXX --BREAK KEY TO BEGIN SESSION.__

HCPCF015E Command not valid before LOGON: _______

输入以下命令之一：

  LOGON userid           (Example: LOGON VMUSER1)

  MSG userid message      (Example: MSG VMUSER2 GOOD MORNING)

  LOGOFF
```
