
![](img/c99d6f526a5f9fa62f2c34daada85ad7_288_0.png)

**图 7.24** SSH/PPP 服务器架构。

在图 7.24 所示的架构中，SSH 服务器同时也是 PPP 服务器，它是一个运行 OpenSSH 的 Linux RedHat 8.0 服务器。此外，示例中的客户端是一台普通的 RedHat 8.0 客户机，未安装或运行任何服务。防火墙无需进行特殊更改，只需添加一条允许连接到 SSH/PPP 服务器 22 端口的规则即可。一旦 SSH/PPP 客户端建立该连接，它将在内部网络中获得一个 VPN 连接。

## 服务器上的 PPP 守护进程

首先，您必须确保 SSH 服务器上的 PPP 守护进程（pppd）已加载并正常工作。如果您使用的是 Linux RedHat 8.0 或更高版本，PPP 守护进程应该可以开箱即用。要确认这一点，请在服务器上输入以下命令：

```bash
# cd /usr/sbin
# pppd
```

如果在服务器上看到类似以下的内容，说明 PPP 守护进程运行正常。PPP 守护进程会向屏幕输出一些终端用户无法阅读的信息，但这实际上证实了 PPP 守护进程正在正确运行。以下内容仅为 PPP 守护进程输出的节选：

```text
4)#&k1!!) 4)*k& )) )%&k"--1L\()*(*@e"~ )#_1!!) 4)*k& )) )%&k"--1L\()*(*@e"~ )#_1!!) 4)*k& )) )%&k"--1L\()*(*@e"~ )#_1!!) 4)*k& )) )%&k"--1L\()*(*@e"~ )#_1!!) 4)*k& )) )%&k"--1L\()*(*@e"~ )#_1!!)
```

## VPN 用户和 Sudo

接下来，您必须配置一个用户来运行 pppd 服务。许多用户选择创建一个除了 root 之外的单独用户账户（例如 vpnmonkey）来执行 PPP 守护进程。使用 sudo 可以确保远程 VPN 用户不会拥有对 PPP/SSH 服务器的完全 root 访问权限，从而避免降低远程访问方案的安全态势。如果您也采取这种方式，请确保通过编辑 sudoers 文件允许 vpnmonkey 账户执行 pppd 服务。此外，请确保已为 vpnmonkey 账户设置了适当的公钥认证要求，如第 4 章所述。不过，为了快速回顾，请确保 vpnmonkey 账户的公钥文件（identity.pub）位于 SSH/PPP 服务器的授权密钥文件中（/home/vpnmonkey/.ssh/authorized_keys）。此外，请编辑 SSH/PPP 服务器上的 sudoers 文件（/etc/sudoers），并允许 vpnmonkey 启动 PPP 守护进程。服务器上 sudoers 文件的内容应如下所示：

```text
Cmnd_Alias VPN=/usr/sbin/pppd

vpnmonkey  ALL=NOPASSWD: VPN
```

为了验证 su 和 sudo 是否正常工作并正确配置，请在服务器上输入以下命令：

```bash
# su vpnmonkey

# sudo /usr/sbin/pppd noauth
```

如果在 sudo 下运行正常，您应该在服务器上看到以下内容，这是 PPP 守护进程向屏幕输出的一些终端用户无法阅读的信息，但实际证实了 PPP 守护进程正在正确运行。以下内容仅为 PPP 守护进程输出的节选：

```text
* #~}~}{ }  } } } }~{}*) }* }* )*)*) { } } } #~!}~) }*} ) } }  }*}~}*) { )"e~" } #~_}~}! ) }~ }~ }~}*) {"~~}" ) ***) { ) } #~_}~}! ) } } { ) #~{}*~}*) { }* }* )*)*) { } } } } }~{}*) }* }* }* }*)*) { } } } } } #~!}~) }*} ) } }  }*}~}*) {"e"~" } #~!}~}! ) } } { } }*}~}*) { } "e"~" } #~!}~) }
```

## 客户端脚本

接下来，您必须在 VPN 客户端上配置一个脚本，以便使用 SSH 进行 PPP 连接。该脚本最初由 www.linuxorg.org 的创作者创建。

在编辑脚本之前，您必须定义根据架构需要自定义的变量。根据图 7.24，您的服务器主机名将为 ssh.ppp.server.com，服务器用户名将为 vpnmonkey，服务器 IP 地址将为 11.30.11.21，客户端 IP 地址将为 72.12.8.15。需要修改的具体条目是 SERVER_HOSTNAME、SERVER_USERNAME、SERVER_IFIPADDR 和 CLIENT_IFIPADDR。

既然已经建立了这些变量，您就可以在脚本中使用这些变量，如下面的脚本中**粗体**部分所示：

```bash
#!/bin/sh
# /usr/local/bin/vpn-pppssh
#
# This script initiates a ppp-ssh vpn connection.
# see the VPN PPP-SSH HOWTO on http://www.linuxdoc.org for more
# information.
#
# revision history:
# 1.6 11-Nov-1996 miguels@cistron.nl
# 1.7 20-Dec-1999 bart@jukie.net
# 2.0 16-May-2001 bronson@trestle.com
#
# You will need to change these variables...
#
# The host name or IP address of the SSH server that we are
# sending the connection request to:
SERVER_HOSTNAME=ssh.ppp.server.com

# The username on the VPN server that will run the tunnel.
# For security reasons, this should NOT be root. (Any user
# that can use PPP can initiate the connection on the client)
SERVER_USERNAME=vpnmonkey

# The VPN network interface on the server should use this address:
SERVER_IFIPADDR=11.30.11.21

# ...and on the client, this address:
CLIENT_IFIPADDR=72.12.8.15

# This tells ssh to use unprivileged high ports, even though it's
# running as root. This way, you don't have to punch custom holes
# through your firewall.
LOCAL_SSH_OPTS="-P"

#
# The rest of this file should not need to be changed.
#

PATH=/usr/local/sbin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/bin/X11/:
#
# required commands...
#

PPPD=/usr/sbin/pppd
SSH=/usr/bin/ssh

if ! test -f $PPPD ; then echo "can't find $PPPD"; exit 3; fi
if ! test -f $SSH ; then echo "can't find $SSH"; exit 4; fi

case "$1" in
start)
	# echo -n "Starting vpn to $SERVER_HOSTNAME: "
	$($PPPD) udetach noauth passive pty "$($SSH) $LOCAL_SSH_OPTS)
	$(SERVER_HOSTNAME) -l $(SERVER_USERNAME) -o Batchmode=yes sudo $(PPPD)
	nodetach notary noauth" ipparam vpn $(CLIENT_lFIPADDR):$(SERVER_IFIPADDR)
	# echo "connected."
	;;

stop)
	# echo -n "Stopping vpn to $SERVER_HOSTNAME: "
	PID=$(ps ax | grep "$($SSH) $(LOCAL_SSH_OPTS) $(SERVER_HOSTNAME) -
	l$(SERVER_USERNAME) -o" | grep -v ' passive ' | grep -v 'grep ' | awk
	' (print $1)')
	if [ "$(PID)" != "" ]; then
	kill $PID
	echo "disconnected."
	else
	echo "Failed to find PID for the connection"
	fi
	;;

config)
	echo "SERVER_HOSTNAME=$SERVER_HOSTNAME"
	echo "SERVER_USERNAME=$SERVER_USERNAME"
	echo "SERVER_IFIPADDR=$SERVER_IFIPADDR"
	echo "CLIENT_IFIPADDR=$CLIENT_IFIPADDR"
	;;

*)
	echo "Usage: vpn (start|stop|config)"
	exit 1
	;;
esac

exit 0
```

将该脚本保存为 wee-pee-en，或者您喜欢的任何名称，并将其设置为可执行（chmod a+x wee-pee-en）。脚本变为可执行后，在客户端输入以下命令，使用 wee-pee-en 脚本并通过可信的 VPN 连接访问 SSH/VPN 服务器：

```bash
# wee-pee-en start
```

如果一切顺利，您应该在客户端看到以下内容：

```text
Using interface ppp1
Connect: ppp1 <--> /dev/pts/1
local IP address 11.30.11.21
remote IP address 72.12.8.15
```

要禁用 VPN，请在客户端输入以下内容：

```bash
# wee-pee-en stop
```

就是这样！该场景允许任何人通过加密的 SSH 连接使用 PPP 来在互联网上创建安全的 VPN 会话。

## 摘要

使用上一章讨论的一些基本技术，结合本章描述的一些先进技术，使我们能够将 SSH 作为一个完整的远程访问解决方案来使用，该解决方案可以支持流行的远程访问需求，如电子邮件、文件传输和管理。虽然这些远程访问需求的具体配置略有不同，但端口转发的基本原理适用于每一项。

端口转发是 SSH 的一个强大且非常有用的功能，其重要性几乎掩盖了它提供的终端访问功能。事实上，当前网络中部署的许多 SSH 解决方案更多地是出于其端口转发能力，而非远程终端访问能力而被部署。此外，SSH 的灵活性使其可以从 NAT 网络和非 NAT 网络中两者使用，这使得它成为一种非常有吸引力的远程访问解决方案，可以在任何类型的网络环境中支持终端用户安全性，无论是酒店客房、家庭办公室、客户现场、数据中心，还是当地咖啡馆的无线网络。

将其他应用程序（如 Outlook Express、Netscape Messenger 和 Eudora）与 SSH 结合使用，使 SSH 能够缓解并解决其他实体中的安全问题。除了保护其他应用程序外，SSH 与现有、必需或标准协议（如 SMB 和 NFSAllow）一起使用，使其能够轻松与现有网络互操作，且对网络几乎没有影响

