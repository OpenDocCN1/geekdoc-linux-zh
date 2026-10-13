
# 第 7 章：连接到 Internet

## 10. 最后，如果你希望在每次重启时启动它，则需要将启动脚本拷贝到 `/etc/rc.init.d/` 目录，并在启动运行级别目录中为其创建一个链接。（否则，只需输入 `dial` 即可手动启动。）

```bash
ln -s /etc/rc.init.d/dial /etc/rc.d/rc3/S91dial
ln -s /etc/rc.init.d/dial /etc/rc.d/rc5/S91dial
```

## 11. 默认的 `/etc/rc.init.d/dial` 启动脚本期望在 `/etc/dial/` 目录下看到 `dial-conf` 脚本。你应该在脚本中看到以下行。

```bash
-f /etc/dial/dial.conf || exit 0
```

然而，`dial` 程序本身期望看到 `/etc/dial.conf` 文件。修改脚本以反映这一差异。

```bash
-f /etc/dial/dial.conf || exit 0
```

## 12. 通过运行启动脚本来启动 `dial`。
`/etc/rc.init.d/dial start`

## 13. 运行 `ps x | grep dial` 命令，你应该能看到 `dial` 守护进程。
```
324 ? S 0:07 dial
```
`dial` 程序作为守护进程后台运行，并显示为网络中的 SLIP 设备 `sl0-to`。通常情况下，SLIP 设备是通往外部网络的默认路由。当发往外部网络的数据包出现在 SLIP 设备上时，`dial` 会启动一个脚本（chat script）与远程服务器协商登录过程。`dial` 守护进程可以建立 SLIP 或 PPP 连接，但最常用于 PPP。

`dial` 为你的网络提供了一个功能性的且有效连续的 Internet 连接。当然，数据包生成到最终交付的时间之间存在相当长的延迟，但至少你不需要手动处理连接。这在昂贵的全天候连接和手动操作之间是一个很好的折中。

# 229

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_258_0.png)

`dial` 守护进程负责设置你的默认路由——处理所有无法显式路由的数据包的路由。如果你的局域网（LAN）没有其他 Internet 连接，使用默认路由选项是一个好主意。（这就是为什么我在第 1 章的网络配置中建议你留空默认路由。）任何发往你网络的数据包，你可能都希望它们发往 Internet。虽然存在许多可能的例外，但这是一个良好的经验法则。

在数据包到达默认路由之前，什么都不会发生。尝试使用如 Telnet 等网络程序访问外部机器——即不在你局域网上的机器。你的 ISP 登录计算机是一个稳妥的选择。如果你在 X Window 环境中，打开另一个终端窗口或运行 `ps grep` 命令。如结果输出所示，`dial` 已派出一个脚本来拨号调制解调器并登录到你 ISP 的 PPP 服务器：

```
1030 ? S  0:00 dial
1045 ? S  0:00 sh /etc/pppd/connect
1049 ? S  0:00 chat -r /var/log/connect REPORT CONNECT TIMEOUT 45 ABORT NO
```

调制解调器启动并拨号你的 ISP。建立连接后，它会将你的用户名和密码发送给 `pppd` 守护进程并登录。要查看 `pppd` 守护进程正在运行，请运行以下命令：

```bash
ps -x | grep ppp
```

如下所示可以看到 `pppd` 守护进程（注意该行被截断了）：

```
1132 SO S  0:00 /usr/sbin/pppd -detach modem crcts mtu 1500 mru 1500 as
```

如果你足够快（或者运气好），你可以在 `pppd` 守护进程之前看到 `ppp.o` 内核模块。信息如下：

```
1203 ? R  0:00 modprobe k s ppp
```

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_258_1)

当然，在脚本文件中以明文形式留 PPP 用户名和密码可能是危险的。可能有我不知道的加密方法，但至少你应该只赋予 root 读取文件的权限。

## 使用 Network Configurator 建立 PPP 连接

Red Hat Network Configurator 提供了另一种建立 PPP 连接的方法。通过 Network Configurator，你可以配置 PPP 连接并只需点击即可激活。然而，它不会像 `dial` 那样按需连接。

1. 登录 root。
2. 点击 GNOME Start 按钮打开控制面板。
3. 点击 Interfaces（接口）按钮。
4. 点击 PPP 按钮。
5. 如果需要调整任何设置，点击 Customize（自定义）按钮。
6. 如果没有设置账户，点击 Networking（网络）按钮。
7. 如果需要设置默认路由，点击 Network（网络）按钮。
8. 最后，点击 Communication（通信）按钮。
9. 点击 Done（完成）按钮，弹出另一个窗口询问你是否保存或取消编辑。
10. 点击 Save（保存）按钮返回 Network Configurator。

# 第 7 章：连接到 Internet

# 231

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_260.png)

`dial` 守护进程负责设置你的默认路由——处理所有无法显式路由的数据包的路由。如果你的局域网没有其他 Internet 连接，使用默认路由是一个好主意。（这就是为什么我在第 1 章的网络配置中建议你留空默认路由。）任何发往你网络的数据包，你可能都希望它们发往 Internet。虽然存在许多可能的例外，但这是一个良好的经验法则。

在数据包到达默认路由之前，什么都不会发生。尝试使用如 Telnet 等网络程序访问外部机器——即不在你局域网上的机器。你的 ISP 登录计算机是一个稳妥的选择。如果你在 X Window 环境，打开另一个终端窗口或运行 `ps grep` 命令。如结果输出所示，`dial` 已派出一个脚本来拨号调制解调器并登录到你 ISP 的 PPP 服务器：

```
1030 ? S  0:00 dial
1045 ? S  0:00 sh /etc/pppd/connect
1049 ? S  0:00 chat -r /var/log/connect REPORT CONNECT TIMEOUT 45 ABORT NO
```

调制解调器启动并拨号你的 ISP。建立连接后，它会将你的用户名和密码发送给 `pppd` 守护进程并登录。要查看 `pppd` 守护进程正在运行，请运行以下命令：

```bash
ps -x | grep ppp
```

如下所示可以看到 `pppd` 守护进程（注意该行被截断了）：

```
1132 SO S  0:00 /usr/sbin/pppd -detach modem crcts mtu 1500 mru 1500 as
```

如果你足够快（或者运气好），你可以在 `pppd` 守护进程之前看到 `ppp.o` 内核模块。信息如下：

```
1203 ? R  0:00 modprobe k s ppp
```

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_258.png)

当然，在脚本文件中以明文形式留 PPP 用户名和密码可能是危险的。可能有我不知道的加密方法，但至少你应该只赋予 root 读取文件的权限。

## 使用 Network Configurator 建立 PPP 连接

Red Hat Network Configurator 窗口提供了另一种建立 PPP 连接的方法。通过 Network Configurator，你可以配置 PPP 连接并只需点击即可激活。然而，它不会像 `dial` 那样按需连接。

1. 登录 root。
2. 点击 GNOME Start 按钮打开控制面板。
3. 点击 Interfaces（接口）按钮。
4. 点击 PPP 按钮。
5. 如果需要调整任何设置，点击 Customize（自定义）按钮。
6. 如果没有设置账户，点击 Networking（网络）按钮。
7. 如果需要设置默认路由，点击 Network（网络）按钮。
8. 最后，点击 Communication（通信）按钮。
9. 点击 Done（完成）按钮，弹出另一个窗口询问你是否保存或取消你所做的编辑。
10. 点击 Save（保存）按钮返回 Network Configurator。

## 使用 dctrl

`dctrl` 脚本是一个非常好的基于 GUI 的拨号界面。它是 `dial` RPM 包的一部分，可以在 `/usr/bin` 目录下找到。要运行它，请以 root 身份登录并执行以下命令：

```
dctrl -dstatus -tload -gload -pqueue -dlog
```
