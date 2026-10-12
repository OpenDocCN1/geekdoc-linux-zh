
# 设置拨号 PPP

点对点协议 (PPP) 用于在串行线上建立互联网协议 (IP) 连接。通常，串行连接是通过调制解调器建立的；不过，它也可以通过串行电缆（空接线电缆）或数字线路（包括 ISDN 和 DSL 数字介质）工作。PPP 是将单台计算机或局域网连接到 TCP/IP 广域网（如互联网）的一种常见方式。

尽管在通过调制解调器建立 PPP 连接时，一方必须拨出电话，而另一方必须接听电话，但在连接建立后，信息可以双向流动。然而，为了清晰起见，我将拨打呼叫的计算机称为客户端，将接听呼叫的计算机称为服务器。

为了简化配置 PPP（以及其他网络接口）的过程，Red Hat Linux 为 GNOME 和 KDE 界面都提供了拨号配置工具。这些界面分别如下：

- **Internet Configuration Wizard（互联网配置向导）** — 从 GNOME 桌面菜单中，选择“程序”→“系统”→“Internet Configuration Wizard”。出现的“Internet Connection（互联网连接）”窗口允许你配置和测试你的拨号 PPP 连接。
- **Kppp 窗口** — 从 KDE 桌面菜单中，选择“Internet（互联网）”→“KPPP”。这将运行 `kppp` 命令。从 KPPP 窗口，你可以设置并启动一个 PPP 拨号连接。

在开始以下两种拨号程序中的任意一种之前，请物理上将调制解调器连接到你的计算机，插上电源，并将其连接到你的电话线。如果你使用的是内置调制解调器，你可能会在计算机背面看到一个电话端口，你需要连接它。在连接好调制解调器后，重启 Red Hat Linux 以便其能够自动检测并配置你的调制解调器。

# 从 GNOME 创建拨号连接

要从 GNOME 桌面配置拨号网络，你应该使用“Dialup Configuration（拨号配置）”窗口。要启动它，请从 GNOME 菜单中选择“程序”→“系统”→“Internet Configuration Wizard”。此时会出现一个“Add new Device Type（添加新设备类型）”窗口，以帮助你为互联网连接选择设备（在本例中为拨号调制解调器），如图 16-1 所示。

![](img/1744bde8c889adfab3fc911e1687fecf_679_0.png)

图 16-1：Internet Configuration Wizard 帮助你设置 PPP 互联网连接。

请按照以下程序从第一个“Add new Device Type”窗口开始配置你的拨号连接。

1. 从出现的“Add new Device Type”窗口中，选择“Modem Connection（调制解调器连接）”并点击“Next（下一步）”。向导将搜索调制解调器，并出现“Select Modem（选择调制解调器）”窗口。
2. 选择以下调制解调器属性并点击 **Next（下一步）**：
    - **Modem（调制解调器）** — 如果调制解调器连接到你的第一个串行端口 (COM1)，你可以选择 `/dev/tty/S0`；对于第二个串行端口 (COM2)，请选择 `/dev/tty/S1`。（按照惯例，设备通常链接到 `/dev/modem`。输入 `ls -l /dev/modem` 以查看它是否链接到一个 tty 设备。）
    - **Baud Rate（波特率）** — 这是计算机与调制解调器通信的速率（通常比调制解调器通过电话线通信的速率快得多）。默认的 115200 可能就可以了。
    - **Flow Control（流控）** — 查阅调制解调器文档，查看调制解调器是否支持硬件流控 (CRTSCTS)。如果不支持，请选择软件流控 (XON/XOFF)。
    - **Modem Volume（调制解调器音量）** — 默认情况下这是关闭的，因为调制解调器的噪音可能很烦人。然而，我在设置调制解调器时通常选择中等音量。一旦一切正常工作，我就将其关闭。如果你无法建立连接，声音可以给你一个感知，告诉你事情在哪里停止了。
    - **Use touch tone dialing（使用双音多频拨号）** — 在大多数情况下，请保持此复选框勾选。如果你的电话系统由于某种原因不支持双音多频拨号，你可以关闭它。
3. 出现“Select Provider（选择提供商）”窗口。
4. 输入以下提供商信息并点击“Next（下一步）”：
    - **Internet Provider（互联网提供商）** — 如果你正在使用互联网提供商窗口中显示的任何国家/地区的互联网服务，请选择该国名称旁边的加号。如果你的互联网提供商出现在“National（国家级）”列表中，请选择它。该提供商的信息会自动填入。点击“Next（下一步）”。
    - **Phone Number（电话号码）** — 输入你想拨入的 ISP 的电话号码。（如果需要拨 9 或其他号码以获取外线拨号音，有一个可选的前缀可用。）
    - **Provider Name（提供商名称）** — 互联网服务提供商的名称。
    - **Login Name（登录名）** — ISP 分配给你的登录名。ISP 可能将登录名称称为登录 ID 或类似的东西。
    - **Password（密码）** — 与登录名关联的密码。
    - 出现“Create Dialup Connection（创建拨号连接）”窗口，显示你刚刚输入的信息。
5. 如果所有信息看起来都正确，请点击“Finish（完成）”（否则，点击“Back（后退）”按钮更改任何信息）。窗口将关闭。
6. 出现“Network Configuration（网络配置）”窗口，理想情况下，窗口中会出现一个新的调制解调器类型的 ppp 连接。（如果没有出现，请选择“程序”→“系统”→“Network Configuration”。）
7. 点击 ppp 设备名称并点击“Activate（激活）”按钮。互联网拨号器启动并拨号你的 ISP。

如果一切正常，你应该看到你的登录名和密码被接受，并且 PPP 连接已完成。尝试打开 Netscape Communicator，看看你是否可以访问互联网上的某个网站。如果第一次不奏效，请不要气馁。有很多事情需要检查才能使你的拨号 PPP 连接工作。跳过前面的内容，前往“Checking your PPP connection”部分。

# 从 KDE 创建拨号连接

要从 KDE 桌面配置拨号 PPP 连接，你可以使用 kppp 窗口。要打开该窗口，请从 KDE 菜单中选择“Internet（互联网）”→“Internet Dialer（互联网拨号器）”。然后点击“Setup（设置）”按钮。将出现一个 kppp 配置窗口，如图 16-2 所示。

> **注意：** 除了使用 Internet Dialer (kppp) 窗口，你还可以使用“Creating a dial-up connection from GNOME”部分中描述的“Dialup Configuration（拨号配置）”窗口。要通过选择 KDE 菜单中的“Internet（互联网）”→“Dialup Configuration”从 KDE 桌面打开“Dialup Configuration”窗口。

![](img/1744bde8c889adfab3fc911e1687fecf_681_0.png)

**图 16-2：** 使用 *kppp* 配置窗口从 KDE 配置 PPP 连接。

1. 从 *kppp* 配置窗口（“Accounts（账户）”选项卡）中，点击“New（新建）”。一个弹出窗口询问你是否希望使用向导创建一个新的账户。
2. 点击 **Dialog Setup（对话框设置）**。将出现一个新账户窗口。
3. 从新账户窗口的 **Dial（拨号）** 选项卡中，添加以下信息：
    - **Connection Name（连接名称）** — 输入你选择的任何名称来标识该连接。通常，该名称会标识你的 ISP。
    - **Phone Number（电话号码）** — 点击“Add（添加）”按钮，输入 ISP 调制解调器池的电话号码，然后点击“OK（确定）”。
    - **Authentication（认证）** — 从你的 ISP 确定用于建立连接的认证类型。许多 ISP 使用 PAP 或 CHAP 类型的认证（这些认证用于 Windows NT 和其他类型的服务器），而使用 UNIX 和 Linux 服务器的大学和其他站点倾向于使用 Terminal（终端）和 Script-based（基于脚本的）认证。
    - **Customize pppd arguments（自定义 pppd 参数）** — 点击此按钮，输入你想要添加的参数，点击“Add（添加）”，对额外参数重复此操作（可选），然后点击“OK（确定）”。这些参数传递给 *pppd* 守护进程（该守护进程建立和维护你的 PPP 连接）。其中一些参数将在后面的“Checking your PPP connection”部分中描述。请参阅 *pppd* 手册页（输入 `man pppd` 以获取有关可用参数的信息）。
4. 点击 **IP** 选项卡。ISP 很可能会使用动态 IP 地址。如果 ISP 给了你一个静态 IP 地址，请点击“Static IP Address（静态 IP 地址）”复选框并输入 ISP 给你的地址和子网掩码。你也可以点击“Autoconfigure hostname...（自动配置主机名...）”复选框，让主机名从你的 ISP 自动分配。

