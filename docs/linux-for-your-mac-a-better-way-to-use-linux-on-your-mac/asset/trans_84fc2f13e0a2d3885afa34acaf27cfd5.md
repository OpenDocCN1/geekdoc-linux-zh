

# 功成身退，但未曾被遗忘

在互联网尚处于幼年期时，传奇人物就会离我们而去，这实在令人难以置信。ping 命令的作者迈克尔·约翰·“迈克”·穆斯（Michael John "Mike" Muuss）于 2000 年 11 月 20 日在马里兰州的一起悲剧性车祸中去世。穆斯曾说道：“我根据声呐发出的声音给它命名，这一命名灵感源自回声定位的整体原理。” 截稿之时，他的个人主页 (http://ftp.arl.army.mil/~mike/) 仍然处于活动状态。

## 配置 PPP 脚本

为了连接互联网，你无需诉诸那些花哨的图形化连接程序。经验丰富的 Linux 拨号用户利用随每个 Linux 发行版安装的可用命令来构建连接脚本。这些命令包括：

- **chat**：用于通过串行端口建立链路并与远程计算机进行协商。
- **pppd**：这是 PPP 守护进程，负责处理通过连接过程中创建的内存接口传输的信息。
- **bash**：此命令或任何其他 Linux shell 用于运行这些脚本。

## 手动连接

若要手动连接，请使用 Al Longyear 的 *ppp-on* 和 *ppp-on-dialer* 脚本。这些脚本通常包含在 pppd 守护进程文档目录下的示例目录中（例如 */usr/share/doc/pppd* 或 */usr/share/doc/packages/pppd*）。以 root 操作员身份编辑这些脚本，以便根据你的系统和 ISP 进行自定义。

这些脚本应复制到 */etc/ppp* 目录中，然后进行编辑。第一个脚本 *ppp-on* 用于启动连接。该脚本的部分内容如下所示：

```
# These are the parameters. Change as needed.
TELEPHONE=2025551212		# The telephone number for the connection
ACCOUNT=yourname		# The account name for login (as in 'George Burns')
PASSWORD=mypassword	# The password for this account (and 'Gracie Allen')
LOCAL_IP=0.0.0.0        # Local IP address if known. Dynamic = 0.0.0.0
REMOTE_IP=0.0.0.0       # Remote IP address if desired. Normally 0.0.0.0
NETMASK=255.255.255.0  # The proper netmask if needed
#
...
```

在这个示例中，脚本已编辑以添加远程 ISP 的电话号码，以及 ISP 分配的用户名和密码。你可能想做的唯一其他更改是文件中稍后详述的默认调制解调器速度。脚本的这一部分看起来是这样的：

```
exec /usr/sbin/pppd lock modem crtscts /dev/modem 115200 \
asyncmap 20a0000 escape FF $LOCAL_IP:$REMOTE_IP \
noipdefault netmask $NETMASK defaultroute connect \
$DIALER_SCRIPT &
```

在这个示例中，调制解调器（位于 /dev/modem 上）的默认速度设置为 115200。进行任何所需的更改并保存文件。然后，你可以使用 ppp-on 脚本以 root 身份创建到你远程 ISP 的 PPP 连接，如下所示：

```
# /etc/ppp/ppp-on
```

## 配置 kppp 客户端

如果你在 X 会话中使用 K 桌面环境，你可能希望设置 *kppp* 客户端来替你进行拨号。本节包含设置简单 PPP 连接的说明。只需几个步骤，你就可以配置系统以拨号并连接到你的 ISP。*kppp* 客户端是一个成熟、稳定且稳健的拨号器，已被 KDE 爱好者使用多年。如果你使用 KDE，你一定会爱上 *kppp*！

从桌面面板菜单或 X 终端的命令行启动客户端，如下所示：

```
$ kppp &
```

按下 Enter 键后，你会看到一个小对话框。要设置你的连接，请单击“Setup”（设置）按钮。然后你会看到一个“Account setup”（账户设置）对话框。单击“New”（新建）按钮开始，系统会询问你是否希望使用 *kppp* 的向导设置。除非你居住在美国以外，否则请勿选择向导设置，因为该配置是针对国外用户的。相反，请单击“Dial Setup”（拨号设置）按钮，你会看到如图 9.2 所示的对话框。

在“Connection”（连接）字段中单击，并给该账户起一个名字。接下来，单击“Add”（添加）按钮，并输入一个可以连接到远程 ISP 的电话号码。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_213_0.png)

*图 9.2 通过输入名称和电话号码，开始使用 kppp 配置你的拨号账户。*

如果你的连接需要特殊的登录序列，请单击“Authentication”（身份验证）下拉菜单，并选择基于脚本或基于终端的登录。大多数现代 ISP 使用 PAP（*Password Authentication Protocol*，密码身份验证协议），尽管一些可能使用 CHAP（*Challenge Handshake Authentication Protocol*，质询握手身份验证协议）。这些协议用于协商和验证希望启动 PPP 会话的远程登录。

接下来，单击对话框中的“IP”选项卡，你会看到一个对话框，如图 9.3 所示，询问你将在连接中使用动态还是静态 IP 分配。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_213_1.png)

*图 9.3 选择动态或静态 IP 分配。*

如果你使用静态 IP 地址，请在此处输入。很可能你的 ISP 会动态分配你的 IP 地址。然而，这是一个方便的设置，特别是如果你已配置系统允许拨号用户并分配了静态 IP。参见第 15 章“管理服务”，了解如何执行此操作。完成后，单击“DNS”选项卡，你会看到如图 9.4 所示的对话框。

你的 ISP 也很可能提供 DNS 服务。这几乎是强制性的，尤其是对于大型服务提供商。在“DNS IP Address”（DNS IP 地址）字段中单击，输入 IP 号码，然后完成后单击“Add”（添加）按钮。kppp 将保存这些设置，当你尝试连接时，它会临时将这些设置放置在你的系统 /etc/resolv.conf 文件中。

完成后，单击“OK”（确定）按钮保存你的设置。你将返回到“Account Setup”（账户设置）对话框。若要检查调制解调器速度设置，请单击“Device”（设备）选项卡，你会看到如图 9.5 所示的对话框。

尽管如今很少有 ISP 收取每分钟费用，但大多数 Linux 用户希望拥有可用的最快连接。检查你的设备设置，使用你的调制解调器支持的最快速度。完成后，单击“OK”（确定）按钮。然后你将位于 kppp 的主窗口，如图 9.6 所示。

> 尽管 iBook 和 TiBook 拥有 56K 调制解调器，你可以尝试在设备对话框中将速度设置为 115200，看看是否能获得稍快的连接。此外，探索“Misc”（杂项）选项卡，查看诸如将 kppp 图标对接到连接后桌面面板的选项（然后显示一个带有闪烁红灯和绿灯的微缩调制解调器）。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_214_0.png)

*图 9.4 输入你的 ISP 提供的 DNS IP 地址。*

![](img/1ea833f5a3e3c1547e3dd2891f52804a_215_0.png)

*图 9.5 检查你的调制解调器设置，以确保最快的连接。*

![](img/1ea833f5a3e3c1547e3dd2891f52804a_215_1.png)

*图 9.6 首次连接时，勾选“Show Log”（显示日志）复选框，然后在按下“Connect”（连接）按钮前输入你的用户名和密码。*

确保在下拉菜单中选定了你的新服务，然后输入你的用户名和密码（由你的 ISP 分配，而非用于 Linux）。勾选“Show Log Window”（显示日志窗口）复选框以监视拨号进度。要连接，请单击“Connect”（连接）按钮。你会在一个新窗口中看到拨号和协商过程，如图 9.7 所示。

在 kppp 连接并且你的用户名和密码通过身份验证后，连接对话框将最小化并对接在你的桌面面板中。

## 使用 Red Hat 的拨号命令

如果你使用基于 Red Hat 的 PPC Linux 发行版，你可以使用 Red Hat 的拨号配置和连接工具来创建账户并实现连接。该软件包的主要组件是 ppp-config 客户端和 ppp-setup 连接工具。这些图形配置工具可以快速轻松地引导你完成上网的步骤。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_216_0.png)

![](img/1ea833f5a3e3c1547e3dd2891f52804a_216_1.png)

*图 9.7 在前几次使用 kppp 时，监视你的连接和协商。*

一如既往，你必须拥有一个被正确识别和配置的调制解调器才能使用连接。你可以通过运行 ppp-config 命令开始使用 Red Hat 的工具，该命令可以从桌面面板菜单（如果你是 GNOME 用户）或 X11 终端窗口的命令行运行，如下所示：

```
# ppp-config &
```

按下 Enter 键后，你会看到初始窗口，如图 9.8 所示。单击“Next”（下一步）按钮开始。如果你尚未使用此客户端配置调制解调器，系统会要求你单击另一个“Next”（下一步）按钮开始配置。软件将搜索你的系统，寻找要配置和使用的调制解调器。如果未找到调制解调器，系统将要求你手动配置调制解调器

![](img/1ea833f5a3e3c1547e3dd2891f52804a_216_2.png)

*图 9.8 Red Hat 的 PPP 配置工具易于使用。*

