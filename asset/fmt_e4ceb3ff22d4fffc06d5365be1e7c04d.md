
前两个命令设置设备名称和波特率，第三行拨号号码。第四行更改 `dip` 的操作模式。在这种模式下，来自远程主机的输入数据将显示在屏幕上，你从键盘输入的任何内容都将发送到远程主机。你可能会收到来自来自 ISP 的欢迎消息（他们通常不会打扰，因为这些消息通常会被丢弃）。但是，你会收到登录用户名和密码的提示：

此处显示的文本后面紧接着看起来像是一些乱码字符（ ）。它们中通常有很多右大括号 `}`。你看到的是由 PPP 服务器发布的协议流。每隔几秒，你就会看到字符重复出现，以不断尝试联系。如果在很短之后没有建立连接，PPP 服务器将直接断开连接。

服务器正在尝试建立连接，因此你需要在做出响应之前在你的这一端切换到 PPP 模式。要退出终端模式并返回 `dip` 命令模式，请按 `Ctrl+]`。

这是一个手动过程。你拦截了从服务器发送的两个 IP 地址，因此在移动到 PPP 之前需要输入它们，如下：

```
DIP> get locip 207.14.89.182

DIP> get remotip 207.14.89.6
```

此命令会导致守护进程启动。这是一个手动过程。你拦截了从服务器发送的两个 IP 地址，因此在移动到 PPP 之前需要输入它们，如下：

可以使用一些方法来确保连接已建立。其中之一是使用以下命令查看路由表：

```
netstat -r
```

| Destination | Gateway | Genmask | Flags | Iface |
| :--- | :--- | :--- | :--- | :--- |
| 127.0.0.1 | 0.0.0.0 | 255.0.0.0 | U | lo |
| 207.14.89.0 | 0.0.0.0 | 255.255.255.0 | UG | ppp |
| 0.0.0.0 | 207.14.89.6 | 0.0.0.0 | UG | ppp |

`netstat -r` 的输出如下。列表的前两个成员分别对应环回地址和以太网。标记为 `ppp` 的接口是使用 `dip` 建立的点对点连接。

真正的测试是你连接到互联网上的某个地方。实现此点最简单的方法是使用 `ping` 来检测远程主机的存在。选择一个你认为存在的 IP 地址并使用以下代码进行 `ping`：

```
ping 208.151.161.66
```

该命令持续发送短消息，如果连接成功，远程计算机将回这些消息。要断开互联网连接，请输入：

```
dip -k /modem
```

如果你想使用名称而不是数字访问互联网资源（谁不想呢），你需要告诉系统去哪里寻找域名服务器（DNS）。该域名服务器就像互联网电话簿——它接受互联网主机名称并返回相应的 IP 地址。DNS 地址存储在名为 `etc/resolv.conf` 的文件中。在示例中，ISP 的域名是 `xyz.net`，它既有主 DNS 服务器也有备 DNS 服务器：

```
search xyz.net

nameserver 207.14.89.2

nameserver 198.51.13.3
```

## [14] 使用拨号调制器在线

事实上，考虑到连接速度，将你的本地名称服务器列在第一个是有意义的。

有一种更快的解析地址的方法，但显然是手动操作的。在检查任何名称服务器之前，会先检查 `/etc/hosts` 文件。如果在文件中找到了所需的名称（sought-name），则不会查询任何名称服务器。

> 注意：你可能找不到 ISP（互联网服务提供商）提供的名称服务器。如果没有，你应该查看 ISP 的网站；很多 ISP 已经在那里发布了这些信息。如果没有，你将不得不联系 ISP 获取地址。大多数人通过 Windows 连接互联网，它会自动获取名称服务器的地址，因此某些 ISP 并不会特意发布这些信息。

现在你已经可以通过名称访问网络上的内容了。以下命令会在开始接收消息之前，先对 IP 地址发送 `ping` 请求：

```
ping belugalake.com
```

这个 `ping` 语句与之前的相同，不同在于它会首先查询名称服务器获取 IP 地址。你现在已经连接到互联网并可以访问其上的内容。

## 建立和断开连接命令

由于你现在能够手动连接互联网，你可能想要配置一种更简单的方法。实现此目的的一种方法是配置几个命令，让你随时可以建立和释放连接。可以使用 `ppp-on` 命令建立连接，并通过输入 `ppp-off` 来断开连接。

创建一个名为 `/etc/ppp/scripts` 的新目录。将以下三个示例脚本拷贝到文档目录下：

```bash
cp /usr/doc/ppp*/ppp-on /etc/ppp/scripts

cp /usr/doc/ppp*/ppp-off /etc/ppp/scripts

cp /usr/doc/ppp*/ppp-on-dialer /etc/ppp/scripts
```

`ppp-on` 和 `ppp-off` 是从命令行执行的用于建立和断开连接的脚本。`ppp-on-dialer` 脚本供 `ppp-on` 使用。确保脚本具有可执行权限，这样可以通过 `PATH` 变量找到脚本名称。你可以将此目录添加到你的路径中，或者在路径已有的某个目录中创建软链接，如下所示：

```bash
ln -s /etc/ppp/scripts/ppp-on /usr/sbin/ppp-on

ln -s /etc/ppp/scripts/ppp-off /usr/sbin/ppp-off
```

## ppp-on 脚本

你需要修改 `ppp-on` 脚本。该脚本的作用是以正确的设置启动 `ppp` 守护进程并让其建立连接。
最初，脚本如下：

```bash
#!/bin/sh

# 启动 ppp 连接的脚本。这是这对脚本的

# 第一部分。这并不是一对安全的脚本，因为代码

# 使用 'ps' 命令时是可见的。不过，它非常简单。

# 这些是参数。根据需要进行更改。

TELEPHONE=555-1212

# 登录的账号（例如 'George Burns'）

ACCOUNT=george

# 该账号的密码（以及 'Gracie Allen'）

PASSWORD=gracie

LOCAL_IP=0.0.0.0

# 如果已知本地 IP 地址。动态 = 0.0.0.0

REMOTE_IP=0.0.0.0

# 如果需要，远程 IP 地址。通常为 0.0.0.0

NETMASK=255.255.255.0 # 如果需要，正确的子网掩码

# 导出它们，以便在执行 'ppp-on-dialer' 时可用。

export TELEPHONE ACCOUNT PASSWORD

# 这是拨号电话并登录的脚本位置。

# 请使用绝对文件名，因为在 connect 选项中

#没有使用 $PATH 变量。（在 'root' 账户上执行此操作

# 会产生安全漏洞，所以不要尝试。）

DIALER_SCRIPT=/etc/ppp/ppp-on-dialer

# 发起连接

# 我必须在此命令中加入一些常用选项。请不要

# 忘记 'lock' 选项，否则程序如 getty

# 将无法工作。asyncmap 和 escape 将允许 PPP 链路与

# telnet 或登录连接配合。欢迎根据需要进行任何更改。

# 如果你当前有一个指向以太网网关的默认路由，

# 请使用 'defaultroute' 选项。

exec /usr/sbin/pppd debug lock modem crts /dev/ttyS0 9600 \
asyncmap 2A0A00 escape FP kdebug $LOCAL_IP:$REMOTE_IP \
noipdefault default NETMASK default connect $DIALER_SCRIPT
```

你需要编辑该文件以包含你 ISP 的电话号码以及你的登录名和密码。底部的 `exec` 命令使用了脚本前面定义的环境变量，并加入了一些它自己的值。参数列表上有很多参数，如果你遇到任何问题，可能想要更改其中一些。务必检查设备节点和请求的速度是正确的。你可以将 `/dev/ttyS0` 改为 `/dev/modem`，并将 `38400` 改为你之前在设置期间建立的速度。确保 `DIALER_SCRIPT` 设置为完整路径。

## [14] 使用拨号调制器上网

```bash
# 确定要终止的设备。
#
if [ "$1" = "" ]; then
    DEVICE=pp0
else
    DEVICE=$1
fi
```

```bash
################################################################################
# 如果 pp0 pid 文件存在则程序正在运行。停止它。
if [ -r /var/run/$DEVICE.pid ]; then
    kill -INT cat /var/run/$DEVICE.pid
#
# 如果 kill 未生效，则没有该进程在运行。
# 这可能意味着锁文件会被留下。你可能希望
# 同时删除锁文件。
if [ "$?" = "0" ]; then
    rm -f /var/run/$DEVICE.pid
    echo "ERROR: Removed stale pid file"
    exit 1
fi
```

```bash
# 成功。ppp 会清理它自己的垃圾。
echo PPPP link to $DEVICE terminated.
exit 0
```

```bash
# pp0 没有运行 ppp 进程
echo "ERROR: PPP link is not active on $DEVICE"
exit 1
```

如果你有多个拨号连接，可以指定其中哪一个。例如，如果要断开第三个连接：

`ppp-off pp3`

默认是 `pp0`，它也是建立连接时使用的默认名称。

### 网络配置器

如果你正在运行 Red Hat 并使用 X Windows，有一个工具可以让你配置自动 Internet 连接。要执行此操作，你必须拥有超级权限并以 root 身份登录。在主菜单中，在 Administration（管理）下，选择 Network Configuration（网络配置）。会出现一个窗口，顶部有一行按钮。Names（名称）按钮显示有关其他域名的信息（如果有的话）。Routing（路由）和 Hosts（主机）显示窗口允许编辑路由表和主机名列表。选择 Interfaces（接口）按钮，显示的窗口看起来类似于图 14.1。

## [第四部分] 使用 Linux 进行网络连接

### 图 14.1
激活和非激活接口的列表。

![](img/576b77705430d924d4e911445bf0a62d_339_0.png)

任何之前定义的地址将显示在窗口中。在这个示例中，有回环地址和以太网地址。底部的按钮可编辑条目。你想添加新条目，因此选择窗口底部的 Add（添加）按钮，这将出现图 14.2 中的对话框。选择 PPP 然后点击 OK。

### 图 14.2
可用的接口类型。

![](img/576b77705430d924d4e911445bf0a62d_339_1.png)

图 14.3 中的窗口出现，并提示 ISP 的电话号码，以及你的用户名和密码。输入请求的数据并选择 Customize（自定义）以显示图 14.4 所示窗口。

### 图 14.3
必要的 ISP 联系信息。

![](img/576b77705430d924d4e911445bf0a62d_339_2.png)

线速是你的计算机与调制器通信的速率。为了让调制器发挥最大的性能，速度设置必须至少与你的最大调制器速度一样，但也可以设置得更快。设置硬件流控制选项将根据需要切换数据流，防止数据溢出。

## [14] 使用拨号调制器上网

### 图 14.4
PPP 的调制器设置。

![](img/576b77705430d924d4e911445bf0a62d_340_0.png)

选择 Communications（通信）窗口将弹出图 14.5 所示的对话框。每次建立连接时，都会向调制器发送 Init 字符串。它的作用是将调制器初始化为已知状态。如果你使用的是标准调制器，可能不需要更改调制器初始化字符串或拨号命令，但某些调制器可能需要特殊的初始化设置。如果你也使用调制器发送传真，且传真软件未能自洁清理，就可能会发生这种情况。从历史上看，调制器已知进入需要特殊初始化才能恢复的状态，但现在已经不常见了。如果你遇到问题，请检查调制器手册以获取更稳健的初始化方法。

### 图 14.5
登录的命令序列。

![](img/576b77705430d924d4e911445bf0a62d_340_1.png)

图 14.5 中的 Expect（期望）和 Send（发送）列表定义了计算机登录到远程计算机的对话。登录过程从列表顶部开始并向下执行——它停留并等待传入的字符串与左侧的匹配，然后返回右侧的内容。图中的示例显示了登录和密码提示及其响应。最后，有一个五秒的超时设置，因为如果没有问题，远程 PPP 软件应该立即做出响应。

## [第四部分] 使用 Linux 进行网络连接

图 14.3 中的窗口出现，并提示 ISP 的电话号码，以及你的用户名和密码。输入请求的数据并选择 Customize（自定义）以显示图 14.4 所示窗口。

### 使用 dialad 进行自动拨号

图 14.3 中的窗口出现，并提示 ISP 的电话号码，以及你的用户名和密码。输入请求的数据并选择 Customize（自定义）以显示图 14.4 所示窗口。

### connect 文件

`connect` 文件中的许多内容可以保持原样，但有些内容必须更改。以下是 `connect` 文件的样子：

## 326 [第四部分] 与 LINUX 网络连接

```bash
# 如果你没有定义此项，脚本将假设
# 没有用于启动远程协议的命令
PROMPT="annex":
# 用于启动远程协议的发送命令
PROTOCOL_START="ppp"
```

```bash
# 该字符串将等待远程端协议
# 正常启动。如果此值为空，则将不进行任何检查。
START_ACK="Switching to PPP."
```

```bash
# 将消息传递给 dial 和系统日志。
function message () {
  [$FIFO] && echo "$*" $FIFO
  logger -p local2.info -t connect "$*"
}
```

```bash
# 初始化调制解调器。通常这会重置它。
message "Initializing Modem"
chat TIMEOUT 5 "$MODEM_INIT TIMEOUT 45 OK ""
if [ $? -ne 0 ]; then
  message "Failed to initialize modem"
  exit 1
fi
```

```bash
>/var/log/connect
```

```bash
# 拨号远程系统。
message "Dialing $PHONE_NUMBER"
chat -r /var/log/connect \
  REPORT CONNECT \
  TIMEOUT 45 \
  ABORT "NO CARRIER \
  ABORT BUSY \
  ABORT "NO DIALTONE \
  ABORT ERROR \
  " ATDT$PHONE_NUMBER \
  CONNECT ""
```

```bash
case $? in
  0) message "$(cat /var/log/connect)";
  1) message "Chat Error"; exit 1;;
  2) message "Chat Script Error"; exit 1;;
  3) message "Chat Timeout"; exit 1;;
  4) message "No Carrier"; exit 1;;
  5) message "Busy"; exit 1;;
  6) message "No DialTone"; exit 1;;
  7) message "Modem Error"; exit 1;;
esac
```

# 我们已经连接了，尝试登录。

## [14] 使用调制解调器上网

```bash
message 'Loggin in' \
chat \
    TIMEOUT 5 \
    $USER_CHAT_SEQ $USER_NAME \
    TIMEOUT 45 \
    $PWD_CHAT_SEQ $PASSWORD
if [ $? != 0 ]; then
    message 'Failed to log in'
    exit 1
fi
```

我们已经登录了，尝试启动协议（前提是用户已指定了如何操作）

```bash
if [ $PROMPT ]; then
    message 'Starting Comm Protocol'
    chat TIMEOUT 15 $PROMPT $PROTOCOL_START
    if [ $? != 0 ]; then
        message 'Prompt not received'
        exit 1
    fi
fi
```

```bash
if [ $START_ACK ]; then
    chat TIMEOUT 15 $START_ACK
    if [ $? != 0 ]; then
        message 'Failed to start Protocol'
        exit 1
    fi
fi
```
