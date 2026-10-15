
## 通过 YaST 配置 ISDN 网络接口

配置完硬件部分后，您必须为 ISDN 接口配置网络层。`YaST` 使其变得容易。您只需要决定将使用哪种协议。这取决于您的 ISP。以下是三种主要的 ISDN 协议：
- `syncPPP`
- `rawIP HDLC`
- Terminal login (`x.75`)

设置前两种协议的步骤几乎相同。只有最后部分不同。

### ISDN syncPPP 协议

按照以下步骤设置 `syncPPP` 协议：
- 1. 以 `root` 身份启动 `YaST`。
- 2. 从菜单中选择 `System Administration`, `Network Configuration`, `Network Base Configuration`。`Selection of Network` 对话框出现（见图 23.15）。

FIGURE 23.15
ISDN network configuration via YaST.

![](img/659f91d9da7b29976c0625e2e9628511_462_0.png)

- 3. 选择一个空号码并按 `F5`。这将使您能够为网络接口选择合适的设备。
- 4. 选择 `ISDN syncPPP` 协议。这是使用 ISDN 连接时使用的协议之一。
- 5. 输入您的 IP 和您的 PtP IP（对方 IP）。如果您不知道这些 IP 或您使用 `syncIP` 的动态 IP，请使用任意值（`192.168.0.100` 和 `192.168.0.101` 就很好）。
- 6. 测试连接后，发出 `ifconfig` 命令并通过其输出获取您 ISP 的 IP。

7. 返回 `YaST` 中的设置并将 ISP 的 IP 改为正确的值。

8. 按 `F4` 激活网络设备。

9. 按 `F8` 进入你的连接以及以下 ISDN 信息（参见图 23.16）：
- `Your Telephone Number (MSN)`—本章末尾提供了 MSN 格式的列表。
- `Number to be Called`—这是主机 ISP 的号码。
- `Only Given Numbers are Allowed`—不允许用户拨打未提供的号码。这提高了安全性。
- `Dial Mode`—此选项定义连接应如何启动。你可以选择拨号模式为 Auto、Manual 或 Off。
- `Idle Time`—网络在未检测到活动时应保持开启的时间。
- `Name of PPP Login`—在此输入你的用户名。
- `Password of PPP Login`—在此输入你的密码。

## FIGURE 23.16 ISDN account information via YaST

![](img/659f91d9da7b29976c0625e2e9628511_463_0.png)

### CAUTION

对于使用 `syncPPP` 的用户，为了实现正确的 ISDN 连接，你应该在内核中关闭 BSD 压缩。

设置好账户后，点击 `Start` 测试配置。如果对配置满意，点击 `Save` 保存设置。

## The ISDN rawip Protocol

按照以下步骤设置 `rawip` 协议：
1. 以 `root` 身份启动 `YaST`。
2. 从菜单中选择 `System Administration`, `Network Configuration`, `Network Base Configuration`。会出现 `Selection of Network` 对话框（参见图 23.15）。
3. 选择一个空号并按 `F5`。这将使你能够为网络接口选择合适的设备。
4. 选择 `ISDN rawip` 协议。这是使用 ISDN 连接时可用的协议之一。
5. 输入你的 IP 和你的 PtP IP（对方 IP）。如果你不知道这些 IP 或你使用 `syncIP` 的动态 IP，请使用任意值（`192.168.0.100` 和 `192.168.0.101` 即可）。
6. 测试连接后，执行 `ifconfig` 命令并通过其输出获取 ISP 的 IP。
7. 返回 `YaST` 中的设置并将 ISP 的 IP 改为正确的值。
8. 按 `F4` 激活网络设备。
9. 按 `F8` 进入你的连接以及以下 ISDN 信息（参见图 23.16）：
- `Your Telephone Number (MSN)`—本章末尾提供了 MSN 格式的列表。
- `Number to be Called`—这是主机 ISP 的号码。
- `Only Given Numbers are Allowed`—不允许用户拨打未提供的号码。这提高了安全性。
- `Dial Mode`—选择 Auto、Manual 或 Off。
- `Idle Time`—网络在未检测到活动时应保持开启的时间。
- `Maximum Number of Tries`—这是拨号的尝试次数。
- `Name of PPP Login`—在此输入你的用户名。
- `Password of PPP Login`—在此输入你的密码。

填写完数据后，按 `Start` 测试新设置。如果没有问题，保存设置。如果出现错误，跳至“General ISDN Troubleshooting”部分。

保存设置后，启动 `Netscape` 并打开 `http://www.suse.com`。2-3 秒后你应该能看到 SuSE 网页。如果看不到，请阅读“General ISDN Troubleshooting”部分。

NOTE 为了在连接终止后正确设置默认路由，你必须编辑 `/etc/ppp/ip-down`。执行以下命令进行操作：
```
bash#/sbin/init.d/route restart
```

这将把路由表恢复到原始状态。

## The Terminal Login (X.75) Protocol

使用 `x.75` 协议设置终端登录是一个简单的过程。假设你的 ISDN 设备是 `/dev/tty0`。你可以使用 `minicom` 并将其配置为使用此设备，就像使用调制解调器一样。你会收到一条错误消息。安全地忽略它并执行以下命令：

```
ATZ

ATS14=0&Exxx  where xxx is your MSN number
```
