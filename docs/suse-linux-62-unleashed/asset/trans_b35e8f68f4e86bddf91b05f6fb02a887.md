
此对话框用于向 `wvdial.conf` 输入信息，chat chat将将使用这些信息来拨号、连接并登录您的 ISP 账户。突出“Phone Number”（电话号码）字段并按回车。您将看到一个如图 17.4 所示的对话框，在其中输入您 ISP 调制调器的电话号码。

# 图 17.4
输入您的 ISP 电话号码。

![](img/cbac72550c7126a22162e94d91a0c360_560_0.png)

输入 ISP 的电话号码，排除任何 AT 调制调器命令，例如 ATDT（尽管你可以使用数字字符串进行信用卡访问）。完成后点击 OK。再次向下滚动对话框（如图 17.3 所示），并输入如图 17.5 所示的账户名。

# 图 17.5
在配置对话框中输入由 ISP 分配给您的用户名（账户名）。

![](img/cbac72550c7126a22162e94d91a0c360_560_1.png)

# 网络与互联网服务
第二部分

您输入的名称应该是由 ISP 分配的名称。点击 OK，然后在主对话框中向下滚动并输入您的密码。如果您的 IP 地址是自动分配的，请确保“Automatic DNS”（自动 DNS）字段中的括号之间有一个星号 (**)。您可以通过按下空格键来切换此功能。完成后，您可以选择其他功能，例如分频拨号或脉冲拨号、PBX 或其他登录方法。您的配置对话框可能看起来如图 16.6 所示。

# 图 16.6
输入所有必需信息后配置完成。

![](img/cbac72550c7126a22162e94d91a0c360_561_0.png)

向下滚动到 login（登录）菜单项并点击 Select（选择）按钮。随后您会被要求（如图 17.7 所示）一种登录类型，例如 PAP/CHAP、CompuServe、德国 T-Online 或非标准登录。

完成后，点击 Select，您将进入图 17.5 所示的对话框。选择 Exit（退出）按钮并按回车。要启动并测试您的 PPP 连接，向下滚动到 Run Wvdial 菜单项并按回车。命令将启动 `wvdial` 命令来拨号并开始连接。

```
Using defaults found in /var/lib/wvdial/config
Preparing scripts: functions, parsing...done.
```

当出现“starting pppd”消息时，
等待几秒并检查连接是否建立。

```
--> WVdial: Internet dialer version 1.20
--> Initializing modem.
--> Sending: ATZ
```

ATZ *

# 互联网连接
第 17 章

OK
--> Sending: ATQ V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0
ATQ V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0

```
OK
--> Modem initialized.
--> Sending: ATDT 3214887
--> Waiting for carrier.
ATDT 3214887
CONNECT 115200
--> Carrier detected. Waiting for prompt.
** Ascend TNT13.BRD Terminal Server **
Login:
```

Login:
--> Looks like a login prompt.
--> Sending: bball
ball
Password:
--> Looks like a password prompt.
--> Sending: (password)
Enter PPP Session.
IP address is 207.172.118.178
MTU is 1006.
--> Looks like a welcome message.
--> Starting pppd at Sep 30 13:40:26 1999
```

FIGURE 17.7 选择您所需的 PPP 连接登录类型。

![](img/cbac72550c7126a22162e94d91a0c360_562_0.png)

您现在可以使用 SuSE Linux 带的其它工具测试连接。要断开连接，请在控制台按 Ctrl+C，wvdial 命令将退出。

# 网络与互联网服务
第二部分

如果按两次，yast 命令将询问您是否保存配置。选择 Yes 并按回车。然后您可以直接使用 wcdial 命令启动 PPP 连接：

```
# wcdial
```

# 设置 SLIP

SLIP 用于某些不支持 PPP 的 ISP（现已很罕见）。您可能发现某些不使用互联网的在线服务支持 SLIP，例如银行访问和股票交易。过去，SLIP 通常被编译进 Linux 内核，后来被称为 CSLIP（压缩 SLIP）。要使用 SLIP，您需要为它分配一个端口。这意味着由于 SLIP 处理端口的方式，如果与其他程序共享会导致冲突。

注意：新版本的 Linux 在安装内核时默认安装 SLIP。然而，在 SuSE Linux 中，SLIP 支持作为内核模块提供。如果您想在内核中安装 SLIP，则需要重新编译内核。检查 SLIP 是否安装的快速方法是检查 /proc/net/dev 文件是否存在以 s0 开头的行。如果行存在，则 SLIP 已安装。

# 配置 SLIP

配置 SLIP 的快速方法是使用 slattach 程序。这需要 SLIP 使用的端口名称（通常是连接的调制调器）。设置 slattach 的命令如下：

```
# slattach /dev/tty0 &
```

在这种情况下，您配置了 /dev/tty1 作为 SLIP 端口。您可以使用连接到系统的任何端口。末尾的 & 符号将 slattach 程序放在后台运行，这样您就可以返回 shell。当运行 slattach 时，端口被重命名为 /dev/s10，这表示它是第一个 SLIP 设备。如果您使用 /dev/ttyS2 等，可能会导致一些混乱。如果创建了多个 SLIP 端口，它们将递增编号为 /dev/s11、dev/s12 等。Linux 支持八个更多 SLIP 行，但您可能不需要这么多。

大多数 SLIP 行 默认使用 CSLIP，因为它在相同的空间内封装了更多信息。如果您的 ISP 或您连接的对象不支持 CSLIP，您可以强制 Linux 只使用 SLIP：

```
# slattach -p slip /dev/tty0 &
```

slattach 告诉您使用 SLIP 协议。p 之后的其他有效参数有 cslip、adaptive（根据另一端情况进行调整）、slip（SLIP 的旧版本）。现在 SLIP 设备已创建，您需要使用 ifconfig 程序让 Linux 内核知道它。建立接口的 ifconfig 行需要远程系统的名称：

```
ifconfig s0 machine-slip pointoint remotachine
```

s0 是接口名称（在这种情况下为 /dev/s10）；machine-slip 是 SLIP 接口的本地名称（应替换为机器名称，例如 Merlin-slip 或 darkstar-slip）；pointoint 告诉 ifconfig 该接口是点对连接（不要与 PPP 混淆），remotachine 是连接另一端机器的名称。例如，如果远程机器名为 darkstar 而您的机器名称为 dogbert，ifconfig 命令如下：

```
ifconfig s0 dogbert-slip pointoint darkstar
```

下一步是发布 route 命令将通的路由添加到系统数据库。语法与设置接口相同：

```
route add darkstar
```

在这种情况下，您正在为名为 darkstar 的远程机器添加路由。您应该替换为远程机器的名称。

注意：许多 ISP 不告诉您远程机器名称。没关系，因为这些机器名称只是占位符。您可以替换为任何想要标识连接另一端的名称。

# 设置拨号 PPP 服务器

您也可以在您的 Linux 系统上设置一个简单的服务，为拨号用户提供 PPP。虽然像 ISP 这样的商业实体必须投资租赁线路、交换服务、调制调器池和路由器，但您可以轻松配置一个独立的 Linux 设备来响应调制调器并启动 PPP。通用步骤可能包括：

- 选择电话线、调制调器和串口
- 正确配置调制调器以响应入站（使用 AT 命令并使用 AT&W 保存调制调器配置）
- 安装线路监控应用程序（如 getty）来监控串口（在 /initabb 中）
- 可能配置 DNS 服务器（更多信息请参见第 8 章“DNS”）
- 配置 Linux 在用户登录后自动设置 pppd 守护进程

通常情况下，对于许多情况，ATE10QV1&C1&S0=1&W 调制调器字符串将设置调制调器自动响应并使用不同的终端（某些 getty 有配置文件来为特定串口设置调制调器。）SuSE Linux 包含了多种线路监控程序。getty 命令在此应用程序中运行良好，其优点是无需单独设置调制调器——调制调器设置嵌入在 getty/initabb 项中。例如，可以在 SuSE Linux 的 /initabb 文件中使用适当的 getty：

```
2:123:respawn:/sbin/getty -w -I 'ATE00Q1D2&C1&S0=1&015' 11520 ttyS1 vt10
```

此项假设您连接到 /dev/ttyS1。w 选项将等待远程计算机的载波返回或换行符。您也可以尝试使用 -m 选项来同步远程调制调器传输的波特率。在修改 /initabb 后，可以通过以下命令强制其重新检查系统初始化表：

# telnet q

您应该从远程计算机拨号检查登录过程。下一步是创建一个用户来测试 PPP 服务。使用 yacht 命令创建一个名为 ppp 的用户并分配密码。虽然用户可以登录您的系统（假设已将 pppd 设置为 SUID），但您可以通过创建一个短 shell 脚本并在用户的 /etc/passwd 中分配该脚本，从命令行自动启动 pppd 守护进程：

