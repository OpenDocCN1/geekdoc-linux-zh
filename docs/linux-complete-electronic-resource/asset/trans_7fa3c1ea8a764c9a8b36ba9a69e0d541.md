

第二种是默认路由（通过给 pppd 添加选项 **default route** 来建立）。这条路由指示我们的 Linux 系统将任何*未* destined 给本地以太网（对此我们有具体的网络路由）的数据包发送到 PPP 服务器本身。PPP 服务器随后负责将我们的数据包路由到互联网，并将返回的数据包路由回给我们。

如果你没有看到包含两个条目的路由表，那么说明有问题。特别是如果你的 syslog 显示一条消息，告知 pppd 正在替换现有的默认路由，那么说明你有一条指向以太网接口的默认路由——这**必须**被具体的网络路由所替换：**你只能拥有一条默认路由！！**

你需要检查系统初始化文件，以找出这条默认路由是在哪里设置的（它将使用 *route add default*… 命令）。将此命令更改为类似 *route add net*… 的内容。

现在通过*ping* 服务器来测试链路，使用其由 *ifconfig* 输出报告的那个 IP 号，即：

```
ping 10.144.153.51
```

你应该会收到类似这样的输出：

```
PING 10.144.153.51 (10.144.153.51): 56 data bytes

64 bytes from 10.144.153.51: icmp_seq=0 ttl=255 time=328.3 ms
64 bytes from 10.144.153.51: icmp_seq=1 ttl=255 time=190.5 ms
64 bytes from 10.144.153.51: icmp_seq=2 ttl=255 time=187.5 ms
64 bytes from 10.144.153.51: icmp_seq=3 ttl=255 time=170.7 ms
```

此列表将持续不断——要停止它，请按 **Ctrl-C**，此时你会收到更多信息：

```
--- 10.144.153.51 ping statistics ---

4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 170.7/219.3/328.3 ms
```

目前为止一切顺利。

现在尝试通过名称*ping* 一个主机（不是 PPP 服务器本身的名称，而是位于另一个站点、你*知道*很可能正在运行的主机……）。例如：

```
ping MetaLab.unc.edu
```

这一次会稍微停顿一下，因为 Linux 会从你在 */etc/resolv.conf* 中指定的 DNS 获取你 ping 的全限定主机名的 IP 号——所以不要担心（但你会看到调制解调器的指示灯闪烁）。很快你会收到类似这样的输出：

```
PING MetaLab.unc.edu (152.2.254.81): 56 data bytes

64 bytes from 152.2.254.81: icmp_seq=0 ttl=254 time=190.1 ms
64 bytes from 152.2.254.81: icmp_seq=1 ttl=254 time=180.6 ms
64 bytes from 152.2.254.81: icmp_seq=2 ttl=254 time=169.8 ms  
64 bytes from 152.2.254.81: icmp_seq=3 ttl=254 time=170.6 ms  
64 bytes from 152.2.254.81: icmp_seq=4 ttl=254 time=170.6 ms
```

同样，按 Ctrl-C 停止输出并获取统计信息。

```
--- MetaLab.unc.edu ping statistics ---  
5 packets transmitted, 5 packets received, 0% packet loss  
round-trip min/avg/max = 169.8/176.3/190.1 ms
```

如果你没有收到任何响应，请尝试 ping 你的 ISP 站点上的 DNS 服务器的 IP 地址。如果你从这个操作中得到了结果，那么看起来你遇到了 `/etc/resolv.conf` 方面的问题。

如果这也不起作用，说明你有路由问题，或者你的 ISP 在将数据包路由回给你时存在问题。检查上面所示的路由表，如果没问题，请联系你的 ISP。测试 ISP 的一个好方法是使用另一种操作系统进行连接。如果你可以用它绕过你的 ISP，那么问题就在你这边。

如果一切正常，通过输入以下命令关闭连接：  
`ppp-off`

短暂的停顿后，调制解调器应该会自行挂断。

如果不起作用，要么关闭你的调制解调器，要么启动你的通信软件，输入 `+++` 中断调制解调器，然后在收到调制解调器的 OK 提示时输入 `ATH0` 挂断。

你可能还需要清理由 `pppd` 创建的锁文件  
`rm -f /var/lock/LCK..ttySx`

## 自动化您的连接——创建连接脚本

虽然你可以继续像上面那样手动登录，但设置一些脚本来自动执行此操作要整洁得多。

一组脚本可以自动完成登录和 PPP 启动，这样你只需（作为 root 或作为 PPP 组的成员）发出单个命令即可启动你的连接。

## 用于用户名/密码身份验证的连接脚本

如果你的 ISP 不要求使用 PAP/CHAP，那么这些就是适合你的脚本！

如果 PPP 包安装正确，你应该有两个示例文件。对于 PPP 2.1.2，它们在 /usr/sbin 中；对于 PPP 2.2，它们在 /etc/ppp/scripts 中。它们被称为：

- **对于 PPP-2.1.2**
  - ppp-on
  - ppp-off
- **对于 PPP-2.2.2**
  - ppp-off
  - ppp-on
  - ppp-on-dialer

现在，如果你正在使用 PPP 2.1.2，我强烈建议你删除示例文件。这些文件存在潜在问题——别告诉我它们运行良好——我之前也使用过它们很久（并且在这个 HOWTO 的第一个版本中推荐过它们）！

为了 PPP 2.1.2 用户的利益，这里提供了来自 PPP 2.2 发行版中更好的模板版本。我建议复制并使用这些脚本，而不是旧的 PPP-2.1.2 脚本。

## ppp-on 脚本

这是实际启动连接的一对脚本中的第一个。

```bash
#!/bin/sh
#
# Script to initiate a PPP connection. This is the first part of the
# pair of scripts. This is not a secure pair of scripts as the codes
# are visible with the 'ps' command. However, it is simple.
#
# These are the parameters. Change as needed.
TELEPHONE=555-1212    # The telephone number for the connection
ACCOUNT=george        # The account name for Iogon (as in 'George
                     # Burns')
PASSWORD=gracie       # The password for this account (and 'Gracie
                     # Allen')
LOCAL_IP=0.0.0.0      # Local IP address if known. Dynamic = 0.0.0.0
REMOTE_IP=0.0.0.0     # Remote IP address if desired. Normally 0.0.0.0
NETMASK=255.255.255.0  # The proper netmask if needed
#
# Export them so that they will be available to 'ppp-on-dialer'
export TELEPHONE ACCOUNT PASSWORD
#
# This is the location of the script which dials the phone and logs
# in. Please use the absolute file name as the $PATH variable is not
# used on the connect option. (To do so on a 'root' account would be
# a security hole so don't ask.)
#
DIALER_SCRIPT=/etc/ppp/ppp-on-dialer
#
# Initiate the connection
#
exec /usr/sbin/pppd debug /dev/ttySx 38400 \\
    $LOCAL_IP:$REMOTE_IP \\
    connect $DIALER_SCRIPT
```

这是 ppp-on-dialer 脚本：

```bash
#!/bin/sh
#
# This is part 2 of the ppp-on script. It will perform the
# connection protocol for the desired connection.
#
/usr/sbin/chat -v
    TIMEOUT     3
    ABORT       '\nBUSY\r'
    ABORT       '\nNO ANSWER\r'
    ABORT       '\nrINGING\r\n\nrRINGING\r'
    ABORT       '\r'
    '\rAT'
    'OK-\+c0:'  'ATH0'
    TIMEOUT     30
    OK          'ATDT$TELEPHONE'
    CONNECT     ''
    login:--     $ACCOUNT
    asword:--    $PASSWORD
```

对于 PPP-2.2，ppp-off 脚本看起来像这样：

```bash
#!/bin/sh
#####################################################################
#
# Determine the device to be terminated.
if [ "$1" = "" ]; then
    DEVICE=ppp0
else
    DEVICE=$1
fi
#####################################################################
#
# If the ppp0 pid file is present then the program is running.
# Stop it.
if [ -r /var/run/$DEVICE.pid ]; then
	kill -INT `cat /var/run/$DEVICE.pid`
# If the kill did not work then there is no process running for
# this pid. It may also mean that the lock file will be left. You
# may wish to delete the lock file at the same time.
	if [ ! "$?" = "0" ]; then
		rm -f /var/run/$DEVICE.pid
		echo "ERROR: Removed stale pid file"
		exit 1
	fi
fi
# Success. Let pppd clean up its own junk.
	echo "PPP link to $DEVICE terminated."
	exit 0
fi
# The ppp process is not running for ppp0
echo "ERROR: PPP link is not active on $DEVICE"
exit 1
```

## 编辑提供的 PPP 启动脚本

由于新脚本分为两部分，我们将依次编辑它们。

### ppp-on 脚本

你需要编辑脚本以反映你在 ISP 的*用户名*、你在 ISP 的*密码*以及你 ISP 的电话号码。

诸如 TELEPHONE= 这样的每一行实际上都设置了 shell 变量，其中包含“=”右边的信息（当然不包括注释）。因此，编辑这些行中的每一行，使其适用于你的 ISP 和连接。

此外，由于你在 */etc/ppp/options* 文件中设置 IP 号（如果需要），请*删除*说明如下的一行：

`LOCAL_IP=$REMOTE_IP \`

此外，确保 shell 变量 *DIALERSCRIPT* 指向你实际要使用的拨号脚本的完整路径和名称。因此，*如果*你移动或重命名了该脚本，请确保在 ppp-on 脚本中正确编辑此行！

