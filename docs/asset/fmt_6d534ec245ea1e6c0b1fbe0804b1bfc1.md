
当你第一次使用 `kppp` 拨号器时，你会看到一个空白的连接窗口。收集你从 ISP 收集的信息、你关于调制解调器收集的数据，然后单击设置按钮开始配置过程。你的第一个任务是单击设备选项卡并设置调制解调器。使用你从 `dmesg` 命令收集的信息，从下拉列表中选择调制解调器设备。选择连接速度时，如果你有 28.8 或 33.6 调制解调器，使用 57600 的速度，如果你有 56K 或 V.90 调制解调器，使用 115200 的速度。要测试设置并确保 `kppp` 能找到调制解调器，请单击调制解调器选项卡并查询调制解调器。

在你配置调制解调器并确定 `kppp` 识别它之后，告诉拨号器如何连接到你的 ISP。单击账号选项卡并单击新建按钮。新建账号窗口（图 21.3 所示）是你输入拨号 ISP 并执行必要握手所需信息的地方。

### 图 21.3

输入 ISP 提供的用户名、密码和 DNS 地址。

![](img/782ecfdc0b083a767896cc983e10427f_331_0.png)

首先：命名连接。你可能想使用 ISP 的名称，或者如果你有多个账号，使用一个描述性的名称来说明账号的用途（是个人使用还是商业使用）。接下来，输入用于访问 ISP 服务器的电话号码以及认证协议（PAP、CHAP 等）。然后，点击 DNS 选项卡并输入 ISP 所需的主 DNS 和辅助 DNS 地址。全部输入完成后，点击确定。你将被返回到 `kppp` 配置窗口，并且会在账号列表中看到连接名称。

拨号连接几乎准备就绪。再次点击确定，返回到主 `kppp` 窗口（见图 21.4），你会再次看到连接名称。你所需要做的只是输入用户名和密码，然后点击连接按钮。调制解调器建立连接后，你就可以尽情上网了。

### FIGURE 21.4

输入用户名和密码并上网！

![](img/782ecfdc0b083a767896cc983e10427f_332_0.png)

图 21.5 显示了出现的连接窗口。使用此窗口控制你的在线时间。在浏览时，你可以通过点击详细信息按钮查看通过电话线收发的数据量。

### FIGURE 21.5

`kppp` 连接窗口显示你在线的时间。

![](img/782ecfdc0b083a767896cc983e10427f_332_1.png)

## Task: Using Scripts to Connect to Your ISP

与其使用图形工具创建到 ISP 的连接，你可以创建三个不同的 shell 脚本来为你建立连接。第一步是编写一个脚本来执行建立计算机与 ISP 服务器之间 PPP 连接所需的握手。然后你将编写一个脚本拨号到 ISP 并启动 `pppd` 守护进程。最后，你将编辑另一个文件并添加 ISP 的域名服务器名称。

![](img/782ecfdc0b083a767896cc983e10427f_333_0.png)

> 此任务假定你正在使用 `vi` 文本编辑器。如果你愿意，也可以使用其他文本编辑器。

- 1. 登录到超级用户账号。
- 2. 使用 `ls` 命令查看 `ppp-on` 和 `ppp-on-dialer` 文件是否位于 `/etc/ppp` 目录中。制作这些文件的备份副本。

![](img/782ecfdc0b083a767896cc983e10427f_333_1.png)

> 如果这些文件不在那里，你可以在 `/usr/doc/ppp-2.3.11/scripts` 目录中找到示例脚本。（在 TurboLinux 中，你可以在 `/usr/share/doc/packages/ppp-2.3.1/scripts` 目录中找到它们。）将这两个文件复制到 `/etc/ppp` 目录。

3. 编辑 `/etc/ppp/ppp-on` 文件。输入 `vi /etc/ppp/ppp-on` 并按回车。示例脚本显示在列表 21.1 中。用 ISP 提供的加粗斜体信息替换其中的信息。完成后不要忘记保存工作并关闭文件。

### LISTING 21.1 The Script for the /etc/ppp-on File

```
#!/bin/bash
#
# Script to initiate a ppp connection.
# Change these parameters as needed.
TELEPHONE=555-1212      # The telephone number for the connection
ACCOUNT=username        # The account name for logon
PASSWORD=password       # The password for this account
LOCAL_IP=0.0.0.0        # Local IP address (Dynamic = 0.0.0.0)
REMOTE_IP=0.0.0.0       # Remote IP address if desired. Normally 0.0.0.0
NETMASK=255.255.255.0   # The proper netmask if needed
```

### LISTING 21.1 continued

```
#
# Export them so that they will be available at 'ppp-on-dialer' time.
export TELEPHONE ACCOUNT PASSWORD
#
# This is the location of the script which dials the phone and logs.
DIALER_SCRIPT=/etc/ppp/ppp-on-dialer
#
# Initiate the connection
exec /usr/sbin/pppd debug lock modem crtscts /dev/ttyS0 115200 \
asyncmap 20A0000 escape FF kdebug 0 $LOCAL_IP:$REMOTE_IP \
noipdefault netmask $NETMASK defaultroute connect $DIALER_SCRIPT &
```

将 `TELEPHONE` 字段更改为用于拨号到 ISP 的号码。`ACCOUNT` 字段是你的用户名，而 `PASSWORD` 显然是访问 ISP 账号所需的密码。

> 如果密码包含任何 shell 元字符（例如星号或与号），你可能希望在密码周围加上引号。

脚本中间有一个 `DIALER SCRIPT` 字段。你将下一步编辑此文件。确保这是正确的目录路径。

在脚本的最后一部分，输入调制解调器的设备名称和调制解调器连接的最大速度。

- 4. 使文件可执行。输入 `chmod 755 /etc/ppp/ppp-on` 并按回车。
- 5. 你复制的 `/etc/ppp/ppp-on-dialer` 文件不需要任何更改。如果你没有此脚本的副本，示例脚本显示在列表 21.2 中。

### LISTING 21.2 The Script for the /etc/ppp-on-dialer File

```
#!/bin/bash
#
# This script performs the connection protocol.
#
exec chat -v \
TIMEOUT 3 \
ABORT '\nBUSY\r' \
ABORT '\nNO ANSWER\r' \
ABORT '\nRINGING\r\n\r\nRINGING\r' \
'' '\rAT' \
'OK-+++\c:OK' 'ATH0'
```

### LISTING 21.2 continued

```
TIMEOUT 30 \
OK ATDT$TELEPHONE \
CONNECT \
ogin:--ogin: $ACCOUNT \
assword: $PASSWORD
```

6. 使文件可执行。输入 `chmod 755 /etc/ppp/ppp-on-dialer` 并按回车。
7. 配置 ISP 使用的 DNS 地址号码。输入 `vi /etc/resolv.conf` 并按回车。此文件的示例出现在列表 21.3 中。

### LISTING 21.3 Edit Search and Nameserver Information in the /etc/resolv.conf File

```
search myisp.net
nameserver 255.255.255.244
nameserver 255.255.255.245
```

在第一行，输入 ISP 的域名。在第二行，输入主 DNS 号码。在第三行，输入辅助 DNS 号码。完成后，保存并关闭文件。
8. 拨号到你的 ISP。输入 `/etc/ppp/ppp-on` 并按回车。你应该能听到调制解调器拨号的声音。
9. 当你准备断开与互联网的连接时，输入 `/etc/ppp/ppp-off`。你会看到一条消息，内容为

```
PPP link to ppp0 terminated.
```

## Summary
