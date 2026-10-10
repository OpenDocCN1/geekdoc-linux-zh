

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_358_0.png)

开启，并连接到你的笔记本上。同时确保从墙壁插座引出的电话线已正确连接到调制解调器。

# 使用 Red Hat 的 modemtool 命令创建 /dev/modem

以 root 用户身份运行 modemtool 命令，为 Linux 创建一个默认的 /dev/modem 设备。在 X11 终端窗口的命令行中输入 modemtool。按下回车键后，你将看到图 15.1 中所示的对话框。

选择一个用于你调制解调器的串行端口，然后单击“确定”按钮。你也可以使用 ln 命令手动创建此链接。例如，如果你的调制解调器连接到对应于 DOS COM1 的端口，你会输入

```
# ln -s /dev/ttyS0 /dev/modem
```

然后 ls 命令将验证这个新的符号链接：

```
# ls -l /dev/modem
lrwxrwxrwx    1 root root    10 Mar 23 09:44 /dev/modem -> /dev/ttyS2
```

# 使用通信程序拨号

Miquel van Smoorenburg 的 minicom 程序位于 /usr/bin 目录下。它是一个友好的通信程序，你可以用它来测试你的串行端口和调制解调器。以 root 用户身份，从 X11 终端窗口的命令行启动 minicom 的 X11 版本，名为 xminicom（实际上是一个 shell 脚本，用于在单独的终端窗口中启动 minicom），就像这样使用其 -s（设置）选项：

```
# xminicom -s
```

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_359_0.png)

图 15.2 创建默认的 minicom 设置以使用你的调制解调器。

如果你是在控制台且未运行 X11，只需使用 minicom 命令加上 -s 选项即可。按下回车键后，你将看到图 15.2 中所示的窗口。向下滚动以选择 Serial port setup 并按下回车键。然后，你可以按 A 键输入串行设备，如图 15.3 所示。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_359_1.png)

图 15.3 通过输入正确的设备（例如 /dev/modem）为 minicom 配置串行端口。

输入 `/dev/modem` 后，按下回车键。你还可以通过按 E 或 F 键更改其他设置，如速度或握手。完成后，按下回车键。如果已结束，使用“Save setup as default”菜单项，然后选择 Exit 选项。这将保存你的更改，使其成为 minicom 的默认设置。

然后，你可以使用一个简单的 `at` 命令行，配合 `dt` 选项和你的 ISP 电话号码来进行拨号。例如，输入以下内容：

```
atdt555-1212
```

`dt` 命令告诉你的调制解调器在呼叫时使用拨号音。请查阅你的调制解调器手册以获取其完整命令列表。按下回车键后，你应该能听到调制解调器正在拨打电话号码。如果没有，请返回并重新检查你的连接和端口设置。要退出 minicom，请按 Alt+X 然后回车。

# 使用 netcfg 连接

若要使用 Red Hat 的网络配置工具 `netcfg` 设置 PPP 连接，请以 root 身份登录，启动一个 X11 会话，并从 Red Hat 的控制面板或 X11 终端窗口的命令行运行如下命令：

```
# netcfg &
```

按下回车键后，你将看到一个对话框。单击顶部的 Interfaces 选项卡，然后你将看到窗口变为类似图 15.4 的样子。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_360_0.png)

图 15.4 单击“添加”按钮以开始使用 netcfg 配置 PPP 连接。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_361_0.png)

图 15.5 在 netcfg 的 Interface Type 对话框中选择 PPP 按钮。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_361_1.png)

图 15.6 输入你的 ISP 电话号码以及你的用户名和密码。

在 *netcfg* 主窗口底部一行按钮中，单击“添加”按钮。图 15.5 中所示的弹出窗口将出现。

单击 PPP 按钮，然后在小对话框中单击“确定”。你将看到如图 15.6 所示的 Create PPP Interface 对话框。

输入你的 ISP 电话号码，以及你的用户名和密码，然后单击 Customize 按钮。你将看到如图 15.7 所示的对话框。

单击选择连接速度，并为你的调制解调器端口输入 /dev/modem。接下来，选择 Communication 选项卡。你将看到如图 15.8 所示的对话框。此对话框用于输入你的 ISP 电话号码和你的登录脚本，以及调制解调器初始化和拨号字符串（ATZ 用于复位，ATDT 用于音拨号）。例如，如果你使用 minicom 拨打你的 ISP，在与你的 ISP 计算机建立连接后，你应该看到 login: 提示符。输入你的用户名并按下回车键后，你应该看到 Password: 提示符。netcfg Communication 选项卡的对话框用于记录此事务，并且当你拨出时，生成的脚本将由 netcfg 回放。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_362_0.png)

图 15.7 使用 Edit PPP Interface 对话框设置你的连接端口和速度。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_362_1.png)

图 15.9 在 Communication 选项卡对话框中输入你的登录脚本。

该脚本（使用截断的 login: 和 Password: 短语的后半部分）应该已经为你创建好了，但你也可以修改它。首先，输入你的 ISP 电话号码。接下来，高亮显示 ogin: 脚本条目并单击 Edit 按钮。你将看到如图 15.9 所示的小对话框。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_363_0.png)

图 15.9 在 Edit Chat Entry 对话框的 Send script transaction 中输入你的用户名。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_363_1.png)

图 15.10 选择 ppp0 接口，然后单击 Activate 按钮以启动你的 PPP 连接。

在 Send 字段中输入你的用户名，然后单击 Done 按钮。接下来，单击 ord: 条目，单击 Edit，并在 Send 字段中输入你的密码。单击 Done 完成。请注意，该脚本只需要识别短语的一部分，例如 login: 的 ogin:，但要求输入你的完整用户名和密码。如果脚本看起来没问题，单击 Done，验证保存，然后再次单击 Done。然后你将看到如图 15.10 所示的主要 netcfg 窗口。

要启动你的 PPP 连接，请单击选择 ppp0 接口，然后单击 Activate 按钮。你应该能听到调制解调器正在拨号（特别是如果你使用 `ATM11kW` 命令设置音量并保存设置）。要结束你的 PPP 会话，选择该接口，然后单击 Deactivate 按钮。

# 解决 /etc/resolv.conf 中的问题

你可能还需要编辑系统的 /etc/resolv.conf 文件，以添加你的 ISP 域名服务计算机的 IP 地址。如果你已连接到你的 ISP，但发现无法 ping 远程计算机或浏览网页，请检查 /etc/resolv.conf 文件，确保你的 ISP 的 DNS IP 已按以下方式输入（你的数字会有所不同）：

```
nameserver 151.168.2.201
nameserver 191.168.2.202
```

# 使用 kppp 连接

*kppp* 客户端包含在 K 桌面环境中，该环境运行在 X 窗口系统和 Linux 之上。此客户端与 *netcfg* 非常相似，但仅用于设置 PPP 连接。然而，*kppp* 允许你在笔记本上保存多个配置和不同的账户。如果你在国内各地奔波或在家和工作场所使用不同的 ISP，这将非常有用；你可以使用不同的电话号码，甚至不同的用户名和密码来保存账户定义！

首先，确保你的调制解调器在 Linux 下正常工作。接下来，从 KDE 桌面面板启动 *kppp* 客户端，方法是选择 Application Starter 菜单项中的 Internet。你也可以从 X11 终端窗口的命令行启动 *kppp*，就像这样：

```
# kppp &
```

按下回车键后，你将看到一个快速通知对话框，然后是如图 15.11 所示的 *kppp* 主入口窗口。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_364_0.png)

图 15.11 在 kppp 对话框中单击 Setup 按钮以开始。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_365_0.png)

图 15.12 在 kppp Configuration 对话框中，单击 New 按钮。

在 kppp 对话框中单击 Setup 按钮以开始配置你的 PPP 连接。然后你将看到如图 15.12 所示的 kppp Configuration 对话框。

单击 New 按钮以创建你的账户。你将看到如图 15.13 所示的 New Account 对话框。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_365_1.png)

图 15.13 输入你的账户名称和你的 ISP 电话号码，并选择一种连接类型。

