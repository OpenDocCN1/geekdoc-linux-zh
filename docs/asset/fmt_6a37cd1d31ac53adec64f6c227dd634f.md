
```
domain linuxfriend.net
nameserver 10.1.2.3
nameserver 10.1.2.4
```

`domain` 行列出了你的计算机所属的域——本例中是虚构的 ISP `linuxfriend.net`。`nameserver` 行各自列出该 ISP 维护的一个名称服务器。

如果你愿意，也可以通过 `linuxconf` 来配置 DNS，甚至可以使用 BIND 包搭建自己的 DNS 服务器。有关这些主题的更多信息，请参阅第 7 章。

## 创建 `ppp-off` 脚本

建立 PPP 连接可能看起来是工作的重点，但它并不是唯一的部分。当你一段时间用完 Internet 后，必须断开连接。当然，如果你使用的是外部调制解调器，可以按下电源开关，但那样会让 Linux 认为它仍然连接着，这会在下次尝试连接时造成问题。如果你的调制解调器是内置型号，这种方法也无济于事。因此，还有第三个 PPP 脚本：`ppp-off`。内容如下：

```
#!/bin/sh
######################################################################
#
# Determine the device to be terminated.
#
if [ "$1" = "" ]; then
    DEVICE=ppp0
else
    DEVICE=$1
fi

######################################################################
#
# If the ppp0 pid file is present, the program is running. Stop it.
if [ -r /var/run/$DEVICE.pid ]; then
    kill -INT `cat /var/run/$DEVICE.pid`
#
# If the kill did not work, then there is no process running for this
# pid. It may also mean that the lock file will be left. You may wish
# to delete the lock file at the same time.
    if [ ! "$?" = "0" ]; then
        rm -f /var/run/$DEVICE.pid
        echo "ERROR: Removed stale pid file"
        exit 1
    fi
#
# Success. Let pppd clean up its own junk.
    echo "PPP link to $DEVICE terminated."
    exit 0
fi
#
# The ppp process is not running for ppp0.
echo "ERROR: PPP link is not active on $DEVICE"
exit 1
```

当你用完 Internet 连接时，或当链接意外中断时——电话调制解调器连接经常会出现这种情况——运行 `ppp-off`。

## 测试你的链接

要测试你的 PPP 脚本，以 `root` 身份输入 `ppp-on`（你可能需要加上脚本路径，如 `/usr/local/bin/ppp-on`）。短暂暂停后，你应该能听到调制解调器拨号（除非你关闭了扬声器）并与远程系统协商连接。几秒钟后，你应该可以访问 Internet。尝试使用 `ping` 检查基本连通性，使用你 ISP 机器之一的 IP 地址，例如其中一个 DNS 服务器。如果成功，再尝试使用 `ping` 检查通过机器名进行连通性，例如你 ISP 的邮件或新闻服务器。如果成功，你就不应该有问题使用 `ping` 检查更远的站点，例如 `www.linux.org`。如果所有这些测试都成功，你可以尝试使用更高级的功能，例如 Netscape Navigator 或新闻阅读器。

完成后，尝试输入 `ppp-off` 以关闭 PPP 链接。你可能会听到一声咔嗒声，调制解调器断开连接，如果你使用的是外部型号，应该会看到指示灯变化以表明载波丢失。

## 使用 GUI PPP 拨号器

使用本章迄今所述的脚本文件连接到你的 ISP，在配置好文件后可以很快，但有时你可能想要更多或更易访问的信息，或者你可能更喜欢在 GUI 环境中工作。因此，许多 GUI PPP 拨号器已经问世。事实上，一些桌面环境，例如 K 桌面环境（KDE），现在已包含 PPP 拨号器。讨论所有这些拨号器是不切实际的，所以我只在这里讨论其中一个：X-ISP。该拨号器不是标准 Red Hat 发行版的一部分，但在随书光盘上的目录 `sams-extras/ppp` 中有一个用于 X-ISP 的 Red Hat Package Manager（RPM）文件。

像安装其他任何 RPM 文件一样安装它，使用 `rpm` 命令行实用程序或 `gnorpm` GUI 工具。如果你想找到 X-ISP 的更新版本，可以查看 X-ISP 主页 `http://users.hol.gr/~dbouras/`。

### NOTE

X-ISP 软件包会用它自己的增强版本替换 `/etc/ppp/ip-up` 和 `/etc/ppp/ip-down` 文件。`rpm` 实用程序会提醒你这一事实，除非你包含 `--force` 标志，否则它不会允许安装 X-ISP。如果你卸载 X-ISP 并需要原始的 `ip-up` 和 `ip-down` 文件，可以在名称分别为 `ip-up.rpmsave` 和 `ip-down.rpmsave` 下找到它们。

默认情况下，X-ISP 的安装方式仅允许 `root` 使用它。如果你希望其他用户也能拨号，请按以下步骤操作：

1. 将你希望能够拨号的用户添加到组 `uucp`，该组应已存在于你的系统上。（这些用户可能需要注销后重新登录，变更才会生效。）

2. 切换到 `/usr/sbin` 目录并执行以下命令：

```
chown root.uucp chat pppd
chmod 4550 pppd
chmod 550 chat
```

### NOTE

`linuxconf` 实用程序倾向于重置 `pppd` 和 `chat` 文件的权限，因此你在使用 `linuxconf` 后可能需要再次执行此操作。如果你发现这是个问题，可以创建一个设置文件权限和所有权的 shell 脚本，并在必要时调用该脚本。

除了安装和配置 X-ISP 外，你还需要创建 `/etc/ppp/pap-secrets` 或 `/etc/ppp/chap-secrets` 文件，如本章前面 “PPP Authentication” 部分所述。

完成此操作后，你可以在 `xterm` 窗口中输入 `xisp` 启动 X-ISP，Linux 会启动该程序，如图 8.2 所示。

![](img/5d4d3092919d1d16884788127447cc6d_222_0.png)

### FIGURE 8.2

X-ISP 在拨号窗口中提供有用信息，例如调制解调器连接速度和 IP 地址。

你需要通过从 Options 菜单中选择项目来输入你的 ISP 信息。先选择 Options, Account Information，这会弹出 Account Information 对话框（见图 8.3）。在此对话框中单击 Add 以输入你的 ISP 名称，此后你可以输入诸如电话号码（你可以输入多个，用分号分隔，X-ISP 会按顺序拨号，直到找到不忙的号码）、用户名等信息。在大多数情况下，你应在 User/Name 字段中输入你的 ISP 账户的用户名，并选择 PAP-Secrets 或 CHAP-Secrets 作为认证方法。如果你选择 None 作为认证方式，必须使用 Options, Dialing and Login 菜单项创建 select/send 对以进行手动登录。PAP 选项（但不是 PAP-Secrets）与随 Red Hat Linux 6.0 发行的 `pppd` 版本不兼容。

![](img/5d4d3092919d1d16884788127447cc6d_222_1.png)

### FIGURE 8.3

你可以在 Account Information 对话框中输入 ISP 的基本信息。

你可能不需要调整 Options, Dialing and Login 菜单项提供的任何选项，但应尝试 Options, Communication Options，这会弹出 Communication Options 对话框，如图 8.4 所示。检查调制解调器设备是否为你的调制解调器所连接的设备，并将 Serial Port Baud Rate 设置更改为 115200。如果你愿意，可以通过更改 Reset 字段的内容来调整调制解调器初始化字符串。如果你将调制解调器设备从 `/dev/modem` 更改，X-ISP 会警告你必须在 `/etc/ppp/peers` 目录中创建对等信息文件。你可以使用 `/etc/ppp/peers/xisp_modem` 文件作为模型——复制它，然后编辑它并将对 `/dev/modem` 的引用更改为适当的设备。
