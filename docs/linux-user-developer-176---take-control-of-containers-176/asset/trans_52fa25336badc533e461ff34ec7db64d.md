
## 05 测试 OpenVPN 连接

当 OpenVPN 服务运行起来后，在终端中打开一个新标签页，或者启动一个新的 SSH 服务，并运行命令 `ifconfig` 来列出你的网络接口。通常，VPN 连接会显示为 `tun0`。

![](img/6866071e033820549b214c239744aaa0_76_0.png)

你可以使用以下命令检查你的表观位置：

```
curl --interface tun0 freegeoip.net/json/
```

接下来，确保每次登录时 OpenVPN 服务都会自动启动。然后运行

```
sudo nano /etc/default/openvpn
```

并移除 “`#AUTOSTART=`all`” 这一行开头的 `#`。

## 06 安装先决条件

现在我们将安装设置无线接入点（Wireless AP）所需的必要软件。通过运行以下内容来完成：

![](img/6866071e033820549b214c239744aaa0_76_1.png)

```
sudo apt-get install dnsmasq hostapd
```

接下来，运行

```
sudo nano /etc/dhcpd.conf
```

将这些行添加到文件的底部：

```
interface wlan0
static ip_address=172.24.1.1/24
```

按 Ctrl+X，Y 然后回车以保存并退出。

![](img/6866071e033820549b214c239744aaa0_76_2.png)

## 07 设置静态 IP

使用以下命令打开你的网络接口配置文件：

```
sudo nano /etc/network/interfaces
```

将 “`iface wlan0 inet static`” 这一行更改为 “`iface wlan0 inet manual`”。按回车键开始新的一行，然后粘贴以下内容：

```
address  172.24.1.1
netmask   255.255.255.0
network   172.24.1.0
broadcast 172.24.1.255
```

在 “wpa-conf” 开头的行前加一个 “#”。以与之前相同的方式保存并退出。

使用以下命令重启 dhcpcd 服务：

```
sudo service dhcpcd restart
```

## 08 配置接入点

运行

```
sudo nano /etc/hostapd/hostapd.conf
```

![](img/6866071e033820549b214c239744aaa0_76_3.png)

并粘贴以下内容：

```
interface=wlan0
driver=nl80211
ssid=PiVPN
hw_mode=g
channel=1
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_passphrase=raspberry231
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

你可以自由地将网络名称从 ‘PiVPN’ 更改为对你有意义的名称。同样，将密码 ‘raspberry231’ 更改为更安全的密码。

接下来运行

```
sudo nano /etc/default/hostapd
```

找到以 `#DAEMON_CONF=`“`”` 开头的行，并将其更改为 DAEMON_CONF=`“`/etc/hostapd/hostapd.conf`”`。注意必须移除该行开头的 “#”。

![](img/6866071e033820549b214c239744aaa0_76_4.png)

## 09 配置 dnsmasq

使用以下命令移动旧的 dnsmasq 配置文件：

```
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
```

然后运行以下命令创建一个新文件：

```
sudo nano /etc/dnsmasq.conf
```

粘贴以下文本：

```
interface=wlan0
listen-address=172.24.1.1
bind-interfaces
server=8.8.8.8
domain-needed
bogus-priv
dhcp-range=172.24.1.50,172.24.1.150,12h
```

请注意，我们暂时使用 Google 的 DNS 服务器（8.8.8.8）；如果你愿意可以更改此设置，然后保存并退出。

运行

```
sudo nano /etc/sysctl.conf
```

## 自动登录

如果你的 VPN 需要用户名和密码，你可以保存这些信息，以便 OpenVPN 自动连接。首先运行

```
sudo nano auth.txt
```

在第一行输入用户名，在第二行输入你的密码。保存并退出。接下来编辑你的 OpenVPN 配置文件，例如：

```
sudo nano /etc/openvpn/vpn2.conf
```

向下滚动到包含文本 “`auth-user-pass`” 的行，留一个空格并输入路径 auth.txt，例如：

```
auth-user-pass /home/pi/auth.txt
```

再次保存并退出。

找到以 “net.ipv4_ip_forward=1” 开头的行，移除开头的 “#”。现在重启树莓派。

## 10 设置 IPv4 转发

为了进行下一步，你需要单独运行以下每条命令：

```
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i tun0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
```

接下来，运行

```
sudo nano /etc/rc.local
```

将以下内容粘贴在 “exit 0” 行的正上方：

```
iptables-restore < /etc/iptables.ipv4.nat
/usr/sbin/hostapd /etc/hostapd/hostapd.conf
```

## 11 测试接入点

运行以下命令：

```
sudo update-rc.d hostapd enable
sudo update-rc.d dnsmasq enable
```

重启树莓派。此时你需要第二个设备来检查是否可以访问无线接入点。在你的网络菜单中搜索它，并输入你之前创建的密码。如果你忘记了，请在树莓派上运行

```
sudo nano /etc/hostapd/hostapd.conf
```

以再次查看。连接成功后，访问 www.whatsmyipaddress.com 以检查你是否位于 VPN 之后。

## 12 修复 DNS 泄漏

某些 VPN 提供商使用自己的 DNS 服务器。其他 VPN 提供商则不那么谨慎。访问 https://www.dnsleaktest.com/ 并点击 Extended Test（扩展测试）以检查你是否安全。如果任何 DNS 服务器与你的常规 ISP（互联网服务提供商）匹配，你的连接就不完全安全。

为了解决这个问题，编辑你的 VPN 配置文件，例如：

```
sudo nano /etc/openvpn/vpn2.conf
```

并在 “ca” 上方立即添加这些行：

```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf
```

保存并退出，然后重启你的树莓派。再次检查 DNS 泄漏网站。如果这未能解决问题，请尝试使用另一个 VPN 提供商。

运行以下命令以保护连接：

```
sudo iptables -A INPUT -i tun0 -m conntrack --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A INPUT -i tun0 -j DROP
```

确保保存你的更改，以便它们在重启时生效：

```
sudo sh -c “iptables-save > /etc/iptables.ipv4.nat”
```

## 13 阻止未经请求的连接

由于你的树莓派位于你的计算机和互联网之间，它可能会被其他设备访问。使用以下命令阻止来自其他设备的未经请求的传入连接。

## 14 将所有流量路由通过 OpenVPN

当你最初启动树莓派时，某些应用程序可能会尝试直接连接到互联网，这可能会损害你的匿名性。

为了将所有网络流量通过 VPN 传输，你需要编辑 /etc/openvpn 中的配置文件，例如运行：

```
sudo nano /etc/openvpn/vpn2.conf
```

确保 “redirect-gateway” 这一行读取为 “redirect-gateway def1”。DNS 查询也将通过 VPN 路由，因此请确保你的提供商支持此功能。

## 15 设置防火墙

尽管你之前可能已经配置了 iptables 以防止未经请求的传入连接，但为了安全起见，考虑使用以下命令安装 ufw（简易防火墙）：

```
sudo apt-get install ufw
```

运行

```
sudo ufw enable
```

以启用它，然后使用以下命令打开默认的 OpenVPN 端口 1194：

```
sudo ufw allow 1194
```

你可能还想启用端口 22 以允许通过 SSH 连接。请记住，这不会更改路由器上哪些端口是打开或关闭的。

![](img/6866071e033820549b214c239744aaa0_78_0.png)

电子前哨基金会（Electronic Frontier Foundation，EFF）是捍卫数字世界公民自由的主要非营利组织。EFF 成立于 1990 年，通过影响力诉讼、政策分析、草根行动主义和技术开发，支持用户隐私、言论自由和创新。我们致力于确保随着技术使用的增长，权利和自由得到增强和保护。

## EFF.ORG

## 电子前哨基金会

保护电子边境上的权利并促进自由

# 用于树莓派的 Anaconda

Python 是树莓派的首选语言，并且 Raspbian 仓库中有许多可用的软件包。Berrycconda 帮助你超越这些模块。

![](img/6866071e033820549b214c239744aaa0_79_0.png)

Joey Bernard 是一位真正的文艺复兴式人物，他在制作家具、帮助研究人员解决科学计算问题和编写 Android 应用之间分配时间。

## 为什么选择 Python？

它是树莓派的官方语言。在 python.org/doc 阅读文档。

Python 一直是树莓派项目的语言之选。这有几个原因，但我们不会在此深入探讨历史。由于这一决定，Raspbian 软件包仓库中有许多 Python 模块作为软件包可用。你可以放心，这些软件包已编译以在 ARM 处理器上运行，并且已经过测试，因此可以安全使用。但并非所有 Python 模块都以此方式可用。对于缺失的模块，其意图是你可以使用 pip 自己在树莓派上安装它们。虽然这对于某些模块运行良好，但你最终会遇到那些需要调试才能确定为何在 ARM 处理器上未正确工作的模块。调试这类问题所投入的工作量确实应该由很多人分担，幸运的是它确实如此。对于 Python 程序员来说，有一个非常棒的 Python 模块分发版，即 Anaconda 项目。Anaconda 项目还有一个社区部分，称为 Berrycconda，它已被移植到树莓派上。该项目的官方网站位于 github.com/jihelmus/berrycconda。本文将介绍在树莓派上安装并准备使用它的步骤，以便我们可以继续在未来文章中查看 Python 编程中可用的功能。

> “Anaconda 中的主要实用工具是 conda 打包系统”

第一步是下载并安装 Berrycconda 系统的核心。在下载页面上，有适用于 armh6l（树莓派 1 或 Zero）和 armv7l（树莓派 2 或 3）的安装文件。还有适用于 Python 2.X 或 Python 3.X 的不同版本的安装程序。这涵盖了你特定项目可能需要的所有选项。安装程序实际上是一个 shell 脚本，所以你只需要使脚本可执行，然后运行它。例如，我们可以使用以下命令在树莓派 1 上安装 Python 3.x 版本：

```
wget https://github.com/jihelmus/berrycconda/releases/download/v1.0.0/Berrycconda-1.0.0-Linux-armv6l.sh
chmod +x Berrycconda-1.0.0-Linux-armv6l.sh
./Berrycconda-1.0.0-Linux-armv6l.sh
```

默认情况下，这将在你的主目录中的 berrycconda3 目录下安装 Anaconda 环境的基础。如果你希望将其放在其他位置，可以在安装期间更改此安装目录。安装程序还会询问你是否希望将二进制文件的路径添加到你的 PATH 环境变量中。这通常是个好主意。请记住退出当前 shell 并重新登录，以便获取新的路径。或者，手动 source 初始化文件以设置它。

Anaconda 中的主要实用工具是 conda 打包系统。Conda 提供了一个功能非常全面的包管理系统，用于处理 Python 模块及可能需要的所有各种依赖项。在 conda.io/docs 网站上有一个非常好的文档网站，涵盖了所有可用的选项和功能。你首先想要做的是保持当前系统的最新状态。你可以使用以下命令更新单个软件包：

```
conda update package-name
```

此命令将访问互联网并确定给定软件包的新版本是否存在，如果找到，它会询问你是否真的想执行更新。如果你只想查看将执行的操作，可以使用命令行选项 --dry-run 来显示将运行的命令。如果你只想保持整个系统更新，可以使用以下命令来处理更新所有内容：

```
conda update --all
```

要安装新软件包，你首先需要找出哪些已经打包并可用。由于这是社区努力，选择会随时间变化。因此，在尝试安装某些软件包之前应进行检查。你可以使用以下命令进行搜索：

```
conda search some_text
```

这将对软件包标题进行正则表达式搜索，查找给定文本，并返回任何可用的列表。然而有时，你可能会返回一个相当大的列表。如果发生这种情况，你可以使用许多其他 UNIX 实用程序中常用的正则表达式选项进行更精细的搜索。如果你已经知道软件包名称，可以使用 -f 选项强制搜索仅返回与你提供的文本完全匹配的结果。如果要查询的软件包已安装在你的树莓派上，其已安装版本的旁边会有一个星号。当你准备好安装你正在搜索的软件包时，可以使用以下命令：

```
conda install ipython
```

这将在默认情况下在 Berrycconda 环境中安装 ipython 软件包的最新版本。它还将安装任何缺失的依赖项，并更新任何过时的依赖项。虽然在线文档很出色，但 conda 内部也有可用的帮助页面。如果你需要一般帮助，可以使用 help 命令获取。对于某些特定 conda 命令的帮助，你可以使用类似以下的命令：

```
conda install --help
```

这对于所有详细信息都非常有用
