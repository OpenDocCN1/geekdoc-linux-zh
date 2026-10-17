
## 检查默认路由

检查默认路由是否已使用 `route -n` 设置。

```
# route -n Kernel routing table
Destination     Gateway         Genmask         Flags Metric        MTU      Ref    Cost    Ref Iface
0.0.0.0         0.0.0.0         0.0.0.0         UG        0      0      0      0      0      eth0
192.168.0.0     0.0.0.0         255.255.255.0   U         0      0      0      0      0      lo
```

## 启动你的 PPP 连接

一旦你配置了一个可以工作的 PPP 连接，你就可以设置它从桌面轻松启动。方法如下：

- 从 Panel ⊒ Applet ⊒ Network ⊒ 选择 Panel ⊒ Add to Panel（添加到面板），从 KDE 菜单中选择 RH PPP Dialer。当 Choose（选择）弹出窗口时，点击你想要使用的接口并点击 OK。你可以选择现在开始连接或以后。无论哪种情况，在你完成该步骤后，面板上会出现一个图标，你可以点击它立即连接到 ISP（点击绿色按钮）。
- 从 KDE 桌面，右键点击桌面并创建 New（新建） ⊒ Link to Application（指向应用程序的快捷方式）。输入名称 `Dialup.kdelink`。点击 Execute 选项卡，然后在 execute 框中输入 `kppp`。点击 OK。你的 KDE 桌面上会出现一个名为 `Dialup` 的图标。点击它打开 kppp 窗口。从 Connection 框中选择你的 ISP 并连接到你的 PPP 连接。

从现在起，桌面上会出现图标，你可以选择这些图标通过你配置的拨号连接立即连接到 ISP。Gnome 和 KDE 支持拖放，因此你可以将拨号图标拖到桌面以便更方便使用。

## 检查你的 PPP 连接

为了调试你的 PPP 连接或更好地理解它的工作原理，你可以运行以下步骤。这些步骤将帮助你理解信息存储在何处以及如何使用工具跟踪这些信息。

### 检查你的 PPP 接口是否正常

实现此目的的方法之一是使用 `ping` 命令。从 Terminal（终端）窗口，ping 你知道的任何互联网地址。例如：

```
$ ping www.hansonhistory.com

PING hansonhistory.com (198.60.22.8) 192.168.0.43 : icmp_seq=0 ttl=240 time=10 msec

64 bytes from hansonhistory.com (198.60.22.8) : icmp_seq=1 ttl=240 time=116 msec

64 bytes from hansonhistory.com (198.60.22.8) : icmp_seq=2 ttl=240 time=120 msec

64 bytes from hansonhistory.com (198.60.22.8) : icmp_seq=3 ttl=240 time=120 msec
```

```
--- www.hansonhistory.com ping statistics ---

 packets transmitted, 3 packets received, 25% packet loss
```
