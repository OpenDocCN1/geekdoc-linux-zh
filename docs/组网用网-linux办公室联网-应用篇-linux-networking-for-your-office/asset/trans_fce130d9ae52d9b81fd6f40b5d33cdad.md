
随书光盘上的目录。像安装其他任何 RPM 文件一样安装它，使用 rpm 命令行实用程序或 gnorpm GUI 工具。如果你想找到 X-ISP 的更新版本，可以查看 X-ISP 主页 http://users.hol.gr/~dbouras/。

## NOTE

X-ISP 软件包会用它自己的增强版本替换 /etc/ppp/ip-up 和 /etc/ppp/ip-down 文件。rpm 实用程序会提醒你这一事实，除非你包含 --force 标志，否则它不会允许安装 X-ISP。如果你卸载 X-ISP 并需要原始的 ip-up 和 ip-down 文件，可以在名称分别为 ip-up.rpmsave 和 ip-down.rpmsave 下找到它们。

默认情况下，X-ISP 的安装方式仅允许 root 使用它。如果你希望其他用户也能拨号，请按以下步骤操作：

- 1. 将你希望能够拨号的用户添加到组 uucp，该组应已存在于你的系统上。（这些用户可能需要注销后重新登录，变更才会生效。）
- 2. 切换到 /usr/sbin 目录并执行以下命令：

```
chown root.uucp chat pppd
chmod 4550 pppd
chmod 550 chat
```

## NOTE

linuxconf 实用程序倾向于重置 pppd 和 chat 文件的权限，因此你在使用 linuxconf 后可能需要再次执行此操作。如果你发现这是个问题，可以创建一个设置文件权限和所有权的 shell 脚本，并在必要时调用该脚本。

除了安装和配置 X-ISP 外，你还需要创建 /etc/ppp/pap-secrets 或 /etc/ppp/chap-secrets 文件，如本章前面 “PPP Authentication” 部分所述。

完成此操作后，你可以在 xterm 窗口中输入 xisp 启动 X-ISP，Linux 会启动该程序，如图 8.2 所示。

![](img/5d4d3092919d1d16884788127447cc6d_222_0.png)

## FIGURE 8.2

X-ISP 在拨号窗口中提供有用信息，例如调制解调器连接速度和 IP 地址。

你需要通过从 Options 菜单中选择项目来输入你的 ISP 信息。先选择 Options, Account Information，这会弹出 Account Information 对话框（见图 8.3）。在此对话框中单击 Add 以输入你的 ISP 名称，此后你可以输入诸如电话号码（你可以输入多个，用分号分隔，X-ISP 会按顺序拨号，直到找到不忙的号码）、用户名等信息。在大多数情况下，你应在 User/Name 字段中输入你的 ISP 账户的用户名，并选择 PAP-Secrets 或 CHAP-Secrets 作为认证方法。如果你选择 None 作为认证方式，必须使用 Options, Dialing and Login 菜单项创建 select/send 对以进行手动登录。PAP 选项（但不是 PAP-Secrets）与随 Red Hat Linux 6.0 发行的 pppd 版本不兼容。

![](img/5d4d3092919d1d16884788127447cc6d_222_1.png)

## FIGURE 8.3

你可以在 Account Information 对话框中输入 ISP 的基本信息。

你可能不需要调整 Options, Dialing and Login 菜单项提供的任何选项，但应尝试 Options, Communication Options，这会弹出 Communication Options 对话框，如图 8.4 所示。检查调制解调器设备是否为你的调制解调器所连接的设备，并将 Serial Port Baud Rate 设置更改为 115200。如果你愿意，可以通过更改 Reset 字段的内容来调整调制解调器初始化字符串。如果你将调制解调器设备从 `/dev/modem` 更改，X-ISP 会警告你必须在 `/etc/ppp/peers` 目录中创建对等信息文件。你可以使用 `/etc/ppp/peers/xisp_modem` 文件作为模型——复制它，然后编辑它并将对 `/dev/modem` 的引用更改为适当的设备。

![](img/5d4d3092919d1d16884788127447cc6d_223_0.png)

## FIGURE 8.4

*你可以在 Communication Options 对话框中调整串口和调制解调器选项。*

你需要做的最后一步配置是在 TCP/IP Options 对话框中，如图 8.5 所示，通过选择 Options, TCP/IP Options 获取。你可能可以保持 Addressing/Routing 设置不变，除非你知道需要更改它们。你可能应该在 DNS support 区域选择 Yes，并输入由你的 ISP 提供的一个或两个 DNS 服务器的 IP 地址。如果你愿意，可以像为以太网设备配置 DNS 一样进行配置，如第 7 章所述，在这种情况下你应选择 No 以关闭 DNS 支持。

在输入这些信息并创建 PAP 或 CHAP secrets 文件后，你可以尝试拨号你的 ISP。在主 X-ISP 窗口中单击 Connect。你的调制解调器应开始拨号，你应该会在 X-ISP 消息字段中看到与连接状态相关的消息。当你看到 IP 地址出现时，你应该能够使用正常的 Internet 工具，如 Netscape Navigator、ftp 等。

