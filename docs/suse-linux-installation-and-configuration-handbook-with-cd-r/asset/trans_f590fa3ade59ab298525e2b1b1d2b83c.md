

幸运的是，SuSE Linux 包含一个用于配置 WvDial 的 YaST 模块。下一节将说明如何手动配置 WvDial 以及使用 YaST 模块进行配置。

## 使用 YaST 配置 WvDial

你可以使用 YaST 配置调制解调器连接，而无需费力地编辑文件和配置设备。YaST 使用交互式菜单从头开始设置连接。要使用 YaST 设置连接，请按照以下步骤操作：

- 1. 启动 YaST。
- 2. 打开 系统管理，网络配置，配置一个 PPP 网络。这将调出 SuSE WvDial 配置窗口（见图 23.3）。

### FIGURE 23.3
SuSE WvDial 配置窗口。

![](img/659f91d9da7b29976c0625e2e9628511_444_0.png)

### SuSE WvDial 配置

WvDial 配置的第一步是配置它以检测你的调制解调器。为此，突出显示 自动检测调制解调器 选项并按 Enter。WvDial 将尝试扫描你的串行端口以寻找调制解调器。找到后，WvDial 将尝试与调制解调器通信并找到与调制解调器一起使用的最佳初始化和拨号字符串。向下滚动输出窗口以检查 wvdialconf 程序的输出。

接下来，你必须通过突出显示 配置当前配置文件 选项并按 Enter 来编辑连接配置文件。进入 配置当前配置文件 菜单后，填写以下值（见图 23.4）：

- - 电话号码—你的 ISP 电话号码。
- - 区号—你的 ISP 的区号。如果你从同一地区拨号，可以将此字段留空。
- - 账户名—你用于连接到此 ISP 的用户名。
- - 密码—你的密码。

### FIGURE 23.4

你可以使用当前配置文件窗口配置新的连接。

![](img/659f91d9da7b29976c0625e2e9628511_445_0.png)

自动 DNS—如果你的 DNS 在你连接时为你提供 DNS，请选中此框。

拨号方法—从 拨号音 或 脉冲拨号 中选择拨号方法。

调制解调器在 PBX 上（无拨号音）—如果你的调制解调器在 PBX 上或你收到错误提示没有拨号音，请选中此框。注意，如果你选中此框，你的调制解调器在电话线未连接时不会发出投诉。

身份验证模式—选择你的 ISP 使用的身份验证模式。WvDial 识别许多 ISP 使用的大多数身份验证模式。你有以下选项：

- - PAP/CHAP
- - Compuserve
- - Germany:T-Online
- - 非标准登录

专家菜单—使用此菜单，你可以更改正在使用的调制解调器的类型（见图 23.5）。你还可以更改在初始化调制解调器时发送到调制解调器的初始化字符串。

### FIGURE 23.5

使用专家菜单，你可以设置调制解调器类型和调制解调器高级设置。

![](img/659f91d9da7b29976c0625e2e9628511_446_0.png)

- - 初始化字符串 2—当 WvDial 收到第一个初始化字符串的 OK 回复时，此字符串将被发送到调制解调器。
- - 串行端口—如果 WvDial 未能正确检测到你的调制解调器端口，你可以使用此字段手动指定它。
- - 波特率—你可以在此字段中编辑要使用的默认波特率。

如果你的 ISP 没有自动为你分配 DNS，你应该通过突出显示 使用 YaST 配置 DNS（仅在非自动 DNS 时） 选项并按 Enter 来配置 DNS。这将调出 YaST DNS 配置，该配置已在“设置 YaST（域名服务器）”部分中讨论过。

完成 WvDial 配置后，通过突出显示 运行 WvDial 选项并按 Enter 来测试你的新连接。如果你的连接完美无缺，按 Esc。你将被提示保存设置。保存设置并退出。

以后，当你想要建立连接时，输入以下命令：

```
bash$wvdial
```

你的调制解调器将开始拨号你的 ISP 并建立连接。

## 手动配置 WvDial

要配置 wvdial，你必须登录到 X 会话（通过 xdm 或 startx）。进入 X 后，启动一个 xterm 并按照以下步骤操作：

- 1. 通过在 xterm 中发出以下命令，使 localhost 能够连接到 X 服务器：
- xhost +localhost
- 2. 切换到超级用户，例如以下：
- su -l

3. 发出以下命令：

```
wvdialconf /etc/wvdial.conf
```

你应该得到如下输出：

```
bash# wvdialconf /etc/wvdial.conf
Scanning your serial ports for a modem.

Port Scan<*1>: Ignoring ttyS0 because /dev/mouse is a link to it.
ttyS1<*1>: AT -- AT -- AT -- nothing.
ttyS2<*1>: AT -- OK
ttyS2<*1>: ATZ -- OK
ttyS2<*1>: ATQ0 -- OK
ttyS2<*1>: ATQ0 V1 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 -- OK
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0 -- OK
ttyS2<*1>: Modem Identifier: ATI -- 33600
ttyS2<*1>: Speed 2400: AT -- OK
ttyS2<*1>: Speed 4800: AT -- OK
ttyS2<*1>: Speed 9600: AT -- OK
ttyS2<*1>: Speed 19200: AT -- -- OK
ttyS2<*1>: Speed 38400: AT -- OK
ttyS2<*1>: Speed 57600: AT -- -- OK
ttyS2<*1>: Speed 115200: AT -- OK
ttyS2<*1>: Speed 230400: AT -- OK
ttyS2<*1>: Max speed is 230400; using 115200 to be safe.
ttyS2<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0 -- OK

Found a modem on /dev/ttyS2.
ttyS2<Info>: Speed 115200; init "ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0"
+FCLASS=0"
```

通过此操作，wvdialconf 已找到你的调制解调器，猜测了拨号字符串，猜测了速度，并编写了相应的配置文件。

- 4. 将超级用户的 DISPLAY 导出为等于当前 X 会话，例如：
- export DISPLAY=:0
- 5. 启动 wdial.tcl 并填写配置对话框中的信息（见图 23.6）。
- 6. 按 保存 以保存当前配置文件。你也可以点击 拨号 来测试连接。如果它说你已建立连接，请跳到“测试现有连接”部分。

下次你尝试连接时，你必须打开一个终端或一个普通控制台并启动 wvdial。要断开连接，激活窗口/控制台并按 Ctrl+C。

### FIGURE 23.6
wvdial.tcl 脚本。使用此脚本可以轻松修改 wvdial 配置文件。

![](img/659f91d9da7b29976c0625e2e9628511_448_0.png)

## 使用 minicom

minicom 被认为是测试和排除调制解调器故障的主要程序之一。事实上，你可能会发现自己在调制解调器卡住且无法挂断时使用 minicom，或者你可能会将其用作主要拨号程序。当你第一次启动 minicom 时，你应该以 root 身份使用 -s 参数启动它（见图 23.7）。此参数会调出 minicom 的设置菜单，在其中你应该指定用于调制解调器的串行端口。

### FIGURE 23.7
使用 -s 命令行参数启动 minicom 会调出 minicom 的配置屏幕。

![](img/659f91d9da7b29976c0625e2e9628511_448_1.png)

如前所述，调制解调器的串行端口已变为 /dev/modem。你可能想要更改 调制解调器和拨号 设置以适应你的调制解调器配置，在这种情况下，你将参考你的调制解调器手册。完成 minicom 的设置后，你应该保存设置。通过保存设置，minicom 将更改为终端屏幕，在该屏幕上你可以直接向调制解调器发送命令或调出 minicom 设施。

你可以在表 23.5 中查找 mini 调制解调器命令。minicom 帮助对话框可以通过 Alt+Z 调出，其中显示了可用命令的菜单。

要使用 minicom 建立连接，请使用以下步骤：

- 1. 按 Alt+D 调出拨号目录。
- 2. 按 添加，通过使用左右箭头移动光标。
- 3. 使用上下箭头选择新条目（见图 23.8）

### FIGURE 23.8

在 minicom 拨号目录中添加新条目。

![](img/659f91d9da7b29976c0625e2e9628511_449_0.png)

4. 按 编辑。

5. 按如下方式更改适用的条目（见图 23.9）：

- - A—连接名称
- - B—电话号码
- - C—拨号脚本编号

### FIGURE 23.9

编辑新连接中的正确条目。

![](img/659f91d9da7b29976c0625e2e9628511_449_1.png)

minicom 可以自动化连接，但本章未解释此操作。有关使用脚本自动化连接的更多信息，请参阅 minicom 手册。

