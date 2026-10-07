
我们现在必须修复 Windows 95 服务器的另一个 bug。从开始菜单，运行……并输入 `REGEDIT`。这将允许你编辑 Windows 95 注册表。打开分支 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\MSTCP`。在此所有子项中，将字符串 `%WINDIR%` 替换为你的服务器 Windows 95 目录。在我们的示例中，我们将 `HelperNameAndProviderPath` 更改为 `H:\softwarewin9\system\wock32.dll`。这样你的解析器在下次启动 Windows 95 时将有机会工作。

根据你的喜好自定义桌面。你可以安装额外的软件，但不要自找麻烦！例如，起初不要安装 Microsoft Office；你将在下文中找到关于它的更多信息。

### 2.3.4 将配置保存到服务器

当你对设置满意时，使用 Windows 95 启动盘重启电脑，但在启动时按下 `F8` 键。会出现启动菜单，选择“命令提示符”。然后用你的账户登录服务器，等待直到看到 DOS 提示符。

现在我们想将所有有用材料保存到服务器上的目录中，以便以后恢复。有两个问题：

- 不仅有隐藏文件，还有 `attrib` 无法保护的隐藏目录
- 存在长文件名，我们不希望在 Novel 服务器上保留它们。

由于不需要处理，解决第一个问题的简单方法是运行一个小型程序，它将在保持当前目录的同时递归隐藏文件。

所有文件保存后，进行清理。进入 `C:\WIN95` 目录并删除：

- `BACKUP` 目录，它包含与启动软盘相同的材料
- `SYSCONFIG` 目录，它包含之前的版本配置
- `.WP` 文件，它会自动生成
- 所有不需要的 `.BAK`、`.TXT` 和 `.DAO` 文件
- `.PWL` 文件，它包含你的网络密码（轻微加密）

现在在服务器的某处创建一个新目录来存储你的配置。我们使用

```
H:\SOFTWARE95\WIN95\PTASSIST.
```

在内部创建一个 `WIN95` 子目录，并使用 `xcopy` 等工具将 `C:\WIN95` 的完整内容复制到该子目录。

我们发现保存长文件名的最佳方法是使用 `DOSFNBK` 程序，它本质上与 Microsoft `LFNFBK` 相同——它在 DOS 下运行。这意味着，即使你没有运行 Windows 95，你也可以恢复长文件名。我们在 `H:\SOFTWARE\WIN95\DOSFNBK` 子目录内运行它，所有文件名都将被保存：

```dos
dosfnbk c:\ /f original /v original
```

这将所有文件名保存到文件 `ORIGINAL.LFN` 中，并向文件 `ORIGINAL.LOG` 写入日志以防万一。如果你将使用不同的配置，请将这些文件重命名为更具描述性的名称。

### 2.3.5 完成启动盘制作

你现在已准备好制作最终的启动盘镜像。修改你的 `autoexec.bat`，使其如下所示：

```batch
@echo off
mode codepage prepare=((850) ega.dpi)
mode codepage select=850
keyb sb,,keyboard.sys
snapshot /S /M:100
net start NWRed
net use * /d
cls

net use F: \SC1NOV1\SYS
net use H: \SOFTWARE\WIN95
H:\SOFTWARE\WIN95\COMMAND
PATH=H:\SOFTWARE\win95
set comspec=H:\software\win95\command.com
set PTASSIST=H:\software\win95
```

我们为 `snapshot` 添加了一个参数为驱动程序预留内存。我们还添加了环境变量 `PTASSIST`。该脚本如下：

```batch
@echo off
echo preparing Windows 95
if exist C:\WIN95\config.ip goto next
echo Please wait
timeout /t 5
goto loop
next:
cls
```

## XCIII. “远程启动微型指南” MARC STÜCKELBERG 和 SANDRO VIALE

`Class=Net`

`Driver=Net\0000`

`CompatibleIDs="SMC8416"`

`Mfg="SMC"`

`ConfigFlags-hex=10,00,00,00`

`HKEY_LOCAL_MACHINE\ISANP\SMC8416\BOOTREG:MACID:C0\LogConfig`

`0000*`=hex:00,00,04,00,00,02,00,00,10,00,00,00,04,00,00,00,00,a8,ae,e0,
00,20,00,00,00,02,00,00,01,00,00,00,00,00,00,e0,ff,20,
00,40,02,ff,03,00,00,04,03,2c,00,000000000000000,0,00,00,00,00,00,00,00,00,00,00,00,00,e0,ff,20,20,00,00,00,00,0c,00,ff,ff,00,00,00,

00,20,20,00,00,00,81,00,00,00,01,10,00,00,00,00,00,00,00,

00,00,e0,ff,ff,80,00,00,00,00,0c,0c,5f,10,00,00,00,00,00,00,

00

`HKEY_LOCAL_MACHINE\ISANP\SMC8416\Enum\BOOTREG:MACID:C0\Bindings`

`NWLINK\0000*`=""

`MST5CP\0000*`="

`HKEY_LOCAL_MACHINE\ISANP\SMC8416\BOOTREG:MACID:C1`

`HardwareID*="SMC8416, ISANP"`

`HWRevision="1.0.10"`

`DeviceDesc="SMC Ether(8416)"`

`Class="Net"`

`Driver=Net\0000`

`CompatibleIDs="SMC8416"`

`Mfg="SMC"`

`ConfigFlags-hex=10,00,00,00`

`HKEY_LOCAL_MACHINE\Enum\ISANP\SMC8416\BOOTREG:MACID:C1\LogConfig`

`0000*`=hex:00,00,04,00,00,02,00,00,10,00,00,00,04,00,00,00,00,a8,ae,e0,
00,20,00,00,00,02,00,00,01,00,00,00,00,00,00,e0,ff,20,
00,40,02,ff,03,00,00,04,03,2c,00,000000000000000,0,00,0,00,00,00,00,00,00,00,00,00,00,e0,ff,20,20,00,00,00,00,0c,00,ff,ff,0,,00,00,

00,20,20,00,00,00,81,01,00,00,01,10,00,00,00,00,00,00,00,,00,e0,ff0,ff,ff,00,00,00,00,0c,0c,5f,10,00,00,00,00,00,00,

00

`HKEY_LOCAL_MACHINE\Enum\ISANP\SMC8416\BOOTREG:MACID:C1\Bindings`

`NWLINK\0000*`=""

`MST5CP\0000*`="

`HKEY_LOCAL_MACHINE\TempKey\System\CurrentControlSet\Services\VxD\VNETUP`

`ComputerName="BOOTREG:MACHINE:"`

`Workgroup="University"`

`Comment="CUI"`

`HKEY_LOCAL_MACHINE\TempKey\System\CurrentControlSet\Control\ComputerName\ComputerName`

`ComputerName="BOOTREG:MACHINE:"`

如所示，网卡被描述了两次。这是因为根据配置的不同，它对 PnP 扫描会有不同的响应，分别通过 `C0` 和 `C1`。

你可能无法直接使用此文件，但你必须将其复制到你自己的网卡上。记住，如果硬件配置中更改了最重要的部分，Windows 95 将检测并丢弃启动。

## 讨论

例如，你可能需要在启用启动引导（Bootprom）的情况下进行配置，因为当启用启动引导时，`LogConfig` 字段会发生。

如果你配置 PnP，情况会安全得多；所有适配器（SVGA、网络、声卡……）都必须插入插槽，否则相应的设置将会丢失。通过这种方式，PnP 检测无法与你的鼠标配合……这是最后（也是最小）设置。现在，你的磁盘准备就绪。如果你发现网络安装可用，你仍然可以通过将所有二进制文件复制到网络目录并更改路径（使用 Windows 95 模式）来手动操作。

### 2.3 安装额外软件

如果你计划安装额外软件，请使用之前的配置启动机器，添加软件并首次保存配置。这将避免两个问题：

- 在运行安装之前，修复一个小 Bug。打开 DOS 窗口并使用 `attrib`，否则安装将失败。
- 安装后，客户端将能够从软盘启动，但无法从启动引导启动，因为注册表太大了。
- 理论上，你应该能够在不安装的情况下将此文件导入注册表。将其拆分为部分并分别导入。如果某部分失败，再次拆分并重复操作直到完成（最后部分仅包含一行）。

```
attrib H:\windows\system
```

完成后，你将拥有一个包含所有必要启动信息的注册表，但它比创建的要小得多。启动引导存在已久，但它们通常只用于无盘计算机。在我们看来，启动引导对于具有本地硬盘的计算机更有意义，因为：

- 启动引导使配置更健壮，无论分区崩溃，计算机都能以相同的方式启动。
- 本地硬盘使配置更高效，因为可以通过缓存减少网络流量，并允许交换。在加载操作系统之前就可以清理硬盘。

### 3.1 启动引导 vs 本地硬盘

PC 有多种启动引导。我们选择 TCP/IP 启动引导的原因有：

- 它是基于 RFC 公共定义的 BOOT 协议。定义规定当 BOOT 服务器收到未知请求时将不会响应。这避免了多个服务器之间的干扰，正如你在 MSD 服务器上可能经历的那样。此外，由于 IP 广播限制在本地子网内，它们产生的噪声比 IPX 对应物少。
- 它没有绑定到特定的操作系统。
- 可以请求技术信息和 API 信息。
- 启动过程可以通过许多方式参数化。具体来说，它允许我们在 BIOS 不包含此功能的旧式计算机上启动（例如 DOS 内存管理）。
- 提供了构建和维护启动菜单的工具。

### 3.2 哪种启动引导？

## XCIV

“Sendmail+UUCP 微型指南” Jamal Salim

`<jamal@gmail.com>`

## 目录

- 1 前提条件 ................................................. . . . . . . . . . . 141
- 2 设置 ................................................................................... . . . . . . 942

## 摘要

1996年10月25日

在冷静下来并仔细阅读（准确说是《Bast 书》）之后，我破解了这个秘密！下面的步骤适用于 RedHat 提供的二进制文件。也许我应该把这个提示也发给 Sendmail FAQ 的维护者，那里完全没有提到。这适用于仅通过 UUCP 发送邮件的用户。`myshost` 是在 uucp 文件设置的 ISP 主机名，而 `me.com` 是我们使用的主机名。

## 1 前提条件

如果你通常使用 uucp 邮件，那么你并不需要将 bind 编译进 DNS；Sendmail 通常会坚持进行查找。如果你获得了预编译的带 BIND 的 sendmail，你仍然可以接受它（如 RedHat 提供的 sendmail）。

- 1. 参考我基于描述的 m4 文件的解决方案。
- 2. 如果你联系我，我可以为你提供一个非 BIND 编译版本 (8.7.6)。也许 RedHat 应该考虑提供两个 sendmail 二进制文件（类似于 slik），一个带 BIND，另一个不带。
- 3. 获取无 bind 的 sendmail 最快的方法是编辑下面的 `src/conf.h` 行，如下所示：

```
conf.h: #ifdef NAMED_BIND
conf.h: #define NAMED_BIND 0  /* 使用伯克利互联网域名服务器 */
```

- 4. 使用 RFC1597 IP 地址（10.0.0.0-10.255.255.255, 172.16.0-172.31.255.255, 192.168.0.0-192.168.255.255）让 sendmail 满意。编辑 `/etc/hosts` 并添加以下内容作为主机 myhost 的示例：

```
10.0.0.1    myshost
```

# 1942 XCIV. “SENDMAIL+UUCP MINI-HOWTO” 作者 JAMAL HADI SALIM

## 2 设置

1. 使用你的编辑器创建 mc 文件：我将把此文件命名为 `my.mc`

```
==================== file my.mc ====================
include('../m4/cf.m4')
VERSIONID('me.com's setup with uucp created by xxxx')dnl
OSTYPE(linux)
FEATURE(nodns)dnl
FEATURE(nocanonify)dnl
FEATURE(always_add_domain)dnl
FEATURE(mailertable, hash /etc/mailertable)dnl
MAILER(local)dnl
MAILER(smtp)dnl
MAILER(uucp)
define('SMART_HOST', uucp-dom:mysmarthost)
======================================
```

让我们来分析一下这些：

```
include('../m4/cf.m4')
请求在 ..m4/cf.m4 中找到 m4 宏处理某些问题
VERSIONID('me.com's setup with uucp created by xxxx')dnl
```

这用于区分你可能创建的不同版本的 .cf 文件。

```
OSTYPE(linux)
```

这用于定义/重新定义 Linux 特有的内容。将其放在这里是安全的。

```
FEATURE(nodns)dnl
```

这表示我们没有 DNS 服务器（因此实际上我们只使用 uucp 发送邮件。编译 sendmail 时必须设为不使用 bind）。

```
FEATURE(nocanonify)dnl
```

这表示不要将地址传递给 [...] 进行规范化处理（canonification）。在通常情况下，如果你在 sendmail 中绑定了 BIND，它将帮助并使用 DNS 将别名/IP 地址扩展为标准名称。如果你只有通过 UUCP 连接到你的数据源，那么你就不需要这样做。

```
FEATURE(always_add_domain)dnl
```

这会在本地投递的邮件中添加本地主机名。虽然不是必须的，但我希望这样做：

```
FEATURE(mailertable, hash /etc/mailertable)dnl
```

`/etc/mailertable` 文件将是一个数据库，我们可以在其中存储某些站点的路由信息。如果你没有通过 uucp 接收的对象，那么你就不需要。稍后会详细介绍。

```
MAILER(local)dnl
MAILER(smtp)dnl
MAILER(uucp)
```

这些是我们使用的邮件传输器（mailers）。

```
define('SMART_HOST', uucp-dom:mysmarthost)
```

我们的智能主机（smart host）是我们的 ISP，它在 uucp 系统文件中被定义为系统 mysmarthost。任何我们无法处理的消息（即发往我们不认识域名或邮件传输器的邮件）将传递给我们的智能主机/ISP，由它们确定我们使用 uucp 作为邮件传输器。这个特定的传输器使用了 smtp 重写规则。

2. 创建你的 sendmail.cf 文件

# 设置

- 备份旧的 `/etc/sendmail.cf` 文件
- 永远不要用新文件覆盖 sendmail.cf：

  `m4 my.mc > /etc/sendmail.cf`
- 根据你的规格验证是否正确创建了 sendmail.cf 文件。我遇到的一些坑包括：

  缺少 uucp-dom 邮件传输器

这是因为我没有 smtp 邮件传输器项。实际上，在 uucp 之前定义它是非常重要的。

- 如果没有 uucp 站点向你提供数据，请创建 `/etc/mailertable`；否则跳过此步骤
- 创建/编辑文件 `/etc/mailertable`

```text
---------- sample /etc/mailertable ----------
system1.org          uucp-dom:system1
.system1.org         uucp-dom:system1
```

这意味着任何指向 system1.org 或 *.system1.org 的来自来自 ISP 还是本地的邮件，将使用 uucp-dom 邮件传输器到 system1（定义在 uucp 系统文件中），句话说，我们正在为 *.system1 进行邮件路由。

- 使用 makemap 创建数据库

```text
makemap hash /etc/mailertable /etc/mailertable
```

每次更改文件时都执行此操作。

4. 重启 sendmail

5. 使用 `sendmail -bt` 测试 sendmail，并使用 3,0 规则集输入各种地址以查看它们去向何处。
