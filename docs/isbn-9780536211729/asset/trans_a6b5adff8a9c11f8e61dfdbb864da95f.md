

auth.* |/usr/local/etc/syslog_auth

（你也可以选择用其他方式处理其中一些日志，例如发送电子邮件到你的账户，甚至发送到另一台系统上。在一次成功的入侵破解中，你所有的“绊索”都会被禁用，但如果将它们设置在所有入口附近，以便在系统被攻破之前获得“警告”，你仍然会收到警告，并且希望能及时阻止攻击者）。

原始日志消息看起来像这样：

```
Nov 24 13:13:18 cavu su[426]: - tty2 bob-root
```

以下脚本可以很好地处理这种情况。（它可以由任何 shell 调用）。

```
#!/bin/csh -f
loop:
read x

echo "$x" | grep -q ': invalid password'
if ($status == 0) then
necho "$x"
| sed "s/...........: \([^]*\).*: invalid password for /BAD PW:\1/"
| Mail 1234567@skytel.com
endif

echo "$x" | grep -q 'su[.:* - -'
if ($status == 0) then
necho "$x"
| sed -e "s/^.*........: \([^]*\).*: - /BAD SU:\1/\ "
| Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
endif

goto loop
```

这将生成以下页面，其中 "-" 被更改为 "->" 以指示 bob 试图获得比其他用户更高的权限。让所有这些页面非常容易理解是很重要的，因为你可能在凌晨 3 点从熟睡中被叫醒，此时你的精神状态可能并不处于最佳。

```
BAD SU:cavu:ttty2 bob-warren
```

在此脚本中，你还安排了向你的家庭和工作系统接收电子邮件。真正谨慎的人不希望留下任何家庭系统地址的证据，以免攻击者利用它来扩大其攻击范围。一种解决方案是将此电子邮件发送到第三个应该非常安全的系统，该系统然后将电子邮件转发到你的家庭系统。有许多公共 re-mailer（中继邮件服务）可以使用。

### 呼叫 telnet 和 rsh 使用情况

你可以通过以下添加内容来向脚本添加部分功能，当某人发起 telnet 会话时（无论登录是否成功）呼叫你自己。对于来自 cia.com 或 cavu 的 telnet 会话，你不会收到呼叫，因为你是信任这些系统的。注意，这处理的是 TCP Wrappers 允许的 telnet 连接。TCP Wrappers 是一个用于阻挡攻击者的绝佳工具，其用法在本章和第 109 页的“TCP Wrappers”部分中有介绍。

```
set y=echo "$x" | sed -e 's/.*' -e 's/.*//'
echo "$x" | grep -q 'telnet\[.*: connect from '
if ("$status == 0) then
  if ("$y" = "cia.com") goto pasttelnet
  if ("$y" = "cavu.com") goto pasttelnet
  echo "$x" \
  | sed -e "s/^...::\([^^]*).*: /telnet\:1;"
  | Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
endif
```

下一个示例将在 TCP Wrappers 不允许的情况下尝试 telnet 时生成呼叫。这将被视为一次被挫败的破解尝试！

```
echo "$x" | grep -q 'telnet\[.*: refused connect from '
if ("$status == 0) then
  echo "$x" \
  | sed -e "s/^...::\([^^]*).*: /refused connect from/telnet\:1;REFUSED /"
  | refused connect from //"
  | Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
```

rsh 程序非常流行，因为它允许你轻松地向远程系统发出命令。如果某人破解了 joe@cia.com 并且 joe@cia.com 有权限向 nsa.com 上的 bob 账户发出 rsh 命令（通过在 nsa.com 上的 ~joe/.rhosts 中列出 cia.com），那么他们也就“拥有”了 joe@nsa.com 的权限。
相比之下，ssh 命令更受青睐，因为它是安全的。作为替代方案（但不如 ssh 安全），你可以使用 TCP Wrappers 来限制哪些系统可以使用 rsh 向你的系统发出命令。无论如何，如果你允许使用 rsh，你希望在它被使用时收到呼叫（或电子邮件），可以通过以下添加内容来实现：

```
echo "$x" | grep -q 'rsh\[.*: .*cmd='
if ("$status == 0) then
  echo "$x" \
  | sed -e "s/^...::\([^^]*\)\[]:*: /rsh\:1;"
  | Mail 1234567@skytel.com bob@homesys.com bob@pentacorp.com
```

你将收到的电子邮件或呼叫看起来像这样：

```
rsh:cavu:root@cracker.com as root: cmd='chown root /bin/csh;
chmod 4777 /bin/csh'
```

## 8.10 使用 Arpwatch 捕获 ARP 和 MAC 攻击

在任何基于以太网的局域网（LAN）中，在最低层级上，数据包的目标是通过机器的以太网卡地址（更常见的术语是媒体访问控制（MAC）地址）来指定的。当系统想要向特定 IP 地址发送数据包时，它会发出一个地址解析协议（ARP）请求，例如说“谁是 IP 10.0.0.27”。如果每个人都公平行事且配置正确，目标系统会回应说“是我，我的 MAC 地址是 00:87:72:23:7F:AA”。源系统会将数据包发送到 MAC 地址 00:87:72:23:7F:AA。该协议设计于 20 多年前，当时现代互联网尚不存在，没有人担心安全，只有经验丰富的系统管理员才有权限管理局域网上的系统。

现在，任何人都可以将笔记本电脑接入网络并响应 ARP 请求，从而彻底攻击网络。一旦网络规模扩展到 10 台左右系统以上，管理就变得不平凡了。即使是善意用户也可能无意中使用了冲突的 IP 地址，忘记将笔记本电脑的 IP 地址更改为组织正确的地址，等等。

> 许多网络使用动态主机配置协议（DHCP）或 ZeroConf 自动分配 IP 地址，但使用这些程序并不能完全防止 IP 冲突。DHCP 服务器可能导致重复 IP 地址的许多情况，最常见的是系统管理员错误。然而，如果租约文件损坏或被删除，可能会发出重复的 DHCP 租约。

解决意外和故意问题的最佳方案是使用 Arpwatch 监控 ARP 流量。这个开源程序由美国政府的 Lawrence Berkeley 实验室开发，适用于 Linux 和 UNIX。2002 年春天，我对它进行了主要增强，以更好地跟踪拥有多个子网的大型敌对网络中的问题。这个增强版可以在 CD-ROM 上找到，或者通过电子邮件向 book@verysecurelinux.com 请求获取。

在进一步讨论之前，我需要引入“bogon”（bo'gon）这个术语。如果一个数据包的 IP 地址与其所在子网不匹配，则称为 bogon。

要在你的系统上安装增强版的 Arpwatch，请挂载 CD-ROM 并从 tarball 构建：

```
cp /mnt/cdrom/book/arpackwatch.bob.tar.gz
zcat arpackwatch.bob.tar.gz | tar -xovf-
cd arpackwatch-bob
./configure
make
make install
make install-man
man arpackwatch
```

接下来，添加类似于以下命令到 /etc/rc.d/local 文件，以便它在重启时自动启动：

```
# "-O"          增强功能，抑制 Apple 0.0.0.0 的无意义行为
# "-m foo"      增强功能，将邮件发送给 foo 而不是 root
# "-w from"      增强功能，指定发件人地址（包含哪个办公室）
# "-u MAC"      增强功能，指定上游路由器的 MAC 地址
               以避免在 bogon 检测中产生误报
echo "Starting arpackwatch on each Ethernet interface"
ARPACKET=/usr/local/sbin/arpackwatch
ARPARGS="-O -m sysadmin@pentacorp.com"
# 指定上游路由器的 MAC 地址（如果有）
ARPUPS="-u 00:07:4C:92:76:68"
killall arpackwatch
$ARPARGS -f /var/log/eth0 -i eth0 -w "arpackwatch" (NYC:eth0) " \
  $ARPUPS
$ARPARGS -f /var/log/eth1 -i eth1 -w "arpackwatch" (NYC:eth1) " \
  $ARPUPS
$ARPARGS -f /var/log/eth2 -i eth2 -w "arpackwatch" (NYC:eth2) " \
  $ARPUPS
```

最后，初始化其人类可读的数据库并首次启动它：

```
cd /var/log
touch eth0 eth1 eth2
chmod 600 eth0 eth1 eth2
/etc/rc.d/local
```

这个防火墙在 eth1 上有一个内部网络，在 eth2 上有一个 DMZ。-w 标志的参数将显示为“发件人”地址，例如“arpackwatch”，并指示哪台防火墙生成了消息以及数据包源自哪个网卡。每个运行的 Arpackwatch 进程都会构建一个内存数据库

