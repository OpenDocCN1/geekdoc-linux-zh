
我们已经在本章中讨论了第 1 到 8 项，因此请参考相关章节进行设置。

## 安装 `vpn-server` 和 `vpn-client`

我们的 VPN 连接需要两个程序：`vpn-client` 通过 `Stunnel` 向服务器启动 `PPP` 连接，而 `vpn-server` 启动一个守护进程来运行它自己的 `pppd` 副本。你可以从我们的网页 `http://www.buildinglinuxvpn.net/` 下载这些文件。我们将按照如下方式在客户端和服务器的 `sslvpn` 主目录中安装这些文件：

```
falcons-client# mkdir /opt/ssl-vpn/bin; chmod 755 /opt/ssl-vpn/bin
falcons-client# cp vpn-client /opt/ssl-vpn/bin; chmod 755 /opt/ssl-vpn/bin*

bears-server# mkdir /opt/ssl-vpn/bin; chmod 755 /opt/ssl-vpn/bin
bears-server# cp vpn-server /opt/ssl-vpn/bin; chmod 755 /opt/ssl-vpn/bin/*
```

我们以 `root` 身份安装这些程序，因为妥协 `sslvpn` 账户将无法更改文件。

`vpn-client` 和 `vpn-server` 程序分别位于列表 4.1 和 4.2 中。与其手动输入它们，你应该从我们的网页获取它们，因为我们会在网上维护这些程序的最新版本。

### 列表 4.1 `vpn-client` 程序。

```bash
#!/bin/sh -x

# 将此更改为你的
# SSL VPN 安装目录的相应位置
SSL_VPN_DIR=/opt/ssl-vpn

### 从这里开始不应有任何更改。

vpn_config() {
  vpn_network=$1

  # 获取全局变量
  $SSL_VPN_DIR/etc/ssl-vpn.conf

  # 获取 VPN 特定的变量
  VPN_ETC=$SSL_VPN_DIR/etc/$vpn_network
  $VPN_ETC/config || exit 0
}

run_as_ssvpn() {
  whoami=$WHOAMI
  case $whoami in
    root)
      exec su $SSL_VPN_USER -c "$0"; exit 0;;
    $SSL_VPN_USER)
      echo "# 必须作为 $SSL_VPN_USER 运行" >&2
      exit 1;;
    *)
  esac
}

if [ ! -z "$LINKNAME" -a $# -eq 0 ]; then
  # 我们作为 pppd 的 ip-up 脚本被调用
  vpn_config $LINKNAME

  # 配置我们的新路由
  # 不需要 sudo -- 我们是以 root 身份运行的
  # $IPREMOTE 由 pppd 为我们设置
  [ "$server_network" ] && $ROUTE add -net $server_network gw $IPREMOTE
  exit 0
elif [ "$1" = "stop" ]; then
  # 我们停止 VPN
  -u $SSL_VPN_USER -c "$0 stop"
  exit 0
else
  echo "Usage: $0 start|stop" >&2
  exit 1
fi
```

### 列表 4.2 `vpn-server` 程序。

```bash
#!/bin/sh -x

### 将此更改为你安装此软件的任何位置
SSL_VPN_DIR=/opt/ssl-vpn

### 好的，从这里开始不再需要任何更改。
```

# 第 4 章 使用 SSL/TLS 和 PPP 构建 VPN

```bash
run_as_sslvpn () {
  whoami=$WHOAMI
  pwd=pwd
  case "$whoami" in
    root) exec su $SSL_VPN_USER -c "$pwd"; "$@";
      exit 0;;
    $SSL_VPN_USER) echo "$0 Must be run as $SSL_VPN_USER" >&2;
      exit 1;;
  esac
}
```

## Determine 我们应该如何行为：

```bash
if [ "$LINKNAME" ]; then
  # 我们被 pppd 作为 ip-up 脚本调用
  vpn_config $LINKNAME

  # 配置我们的新路由
  # 不需要 sudo -- 我们是从 pppd 以 root 身份运行的
  # IPREMOTE 由 pppd 为我们设置
  [ "$client_network" ] && $ROUTE add -net $client_network $IPREMOTE

  exit 0
elif [ "$1" = "pppd" ]; then
  # 我们从 shell 以 SSL_VPN_USER 身份调用 'vpn-server pppd1'
  vpn_config $2
```

```bash
### 通用 pppd 参数
PPPD_ARGS="updatetch linkname $vpn_network \
  remotename $vpn_network-client user $vpn_network-server \
  name $vpn_network-server $server $pppd_args"

if [ "$server_require_pap" = "yes" ]; then
  PPPD_ARGS="require-pap $PPPD_ARGS"
elif [ "$server_require_chap" = "yes" ]; then
  PPPD_ARGS="require-chap $PPPD_ARGS"
else
  PPPD_ARGS="noauth $PPPD_ARGS"
fi
```

```bash
# 我们被 -- 启动的 pppd 调用
$SUDO PPPPD $PPPD_ARGS $server_ppp_ip:$client_ppp_ip
exit 0
```

elif [ '$1' = 'stop' ]; then

### 我们以 init.d 风格被调用

```bash
[ "$2" ] && vpn_config "$2" \
| vpn_config basename $0 | sed 's/^/[SK][0-9][0-9]//'
```

```bash
### 杀死 pppd进程和隧道进程
kill -9 -1 $PIDDIR/pppd.$vpn_network.pid 2>/dev/null
kill -cat $PIDDIR/stunnel.$vpn_network.pid 2>/dev/null
exit 0;
```

elif [ '$1' = 'start' ]; then

### 我们以 init.d 风格被调用

```bash
[ "$2" ] && vpn_config "$2" \
| vpn_config basename $0 | sed -e 's/^/[SK][0-9][0-9]//'
```

```bash
run_as_sslvpn "$0" # 确保我们不是 root 等等
```

elif [ $# -eq 1 ]; then

### 参数是 vpn 名称 - 启动它

```bash
vpn_config $1
run_as_sslvpn "$0"
```

else

echo "Usage: $0 {vpn_name|start|stop}" >&2

exit 1

fi

# 好，我们已经设置好了变量，现在该执行

# 真正的工作了，取决于我们是如何被用的

```bash
$STUNNEL -p VPN_ETC/server.pem -N $vpn_network \
-P $PIDDIR/stunnel.$vpn_network.pid \
-d $server_tunnel_port $stunnel $stunnel_debug $server_stunnel_args \
```

```bash
exit 0;
```

## 在 `/etc/init.d` 中链接 `vpn-{server,client}`

用于启动和停止系统服务的脚本位于 `/etc/init.d` 目录。（在某些 Linux 发行版中，特别是早期的 Red Hat 系统，它们被保留在 `/etc/rc.d/` 中）。这些脚本通常从 `/etc/rc.x` 目录之一链接，以决定服务应该在哪个运行级别（runlevel）激活。

我们的脚本设计为直接作为启动/停止脚本之一运行，因此我们只需要对它们进行链接即可。假设我们想让名为 `vpn1` 的 VPN 在运行级别 2 启动时运行。我们创建了以下软符号链接：

```bash
bears-server# ln -s /opt/ssl-vpn/bin/vpn-server /etc/rc2.d/S99vpn1
bears-server# ln -s /opt/ssl-vpn/bin/vpn-server /etc/init.d/vpn1
```

```bash
falcons-client# ln -s /opt/ssl-vpn/bin/vpn-client /etc/rc2.d/S99vpn1
falcons-client# ln -s /opt/ssl-vpn/bin/vpn-client /etc/init.d/vpn1
```

这些命令设置了我们的 VPN 在运行级别 2 开始时作为最后一个程序启动。你可以将 99 修改为适合系统的数字。我们还会创建一个通用的 init.d 条目以方便使用。

## 配置 `ip-up` 运行我们的 VPN 脚本

当 PPP 连接建立时，我们展示了如何创建 `ip-up` 将使用的软链接，以调用我们的 `vpn-server` 或 `vpn-client` 程序设置路由。

详情参见第 3 章中的“配置 ip-up 运行我们的 VPN 脚本”部分。如果你只是想捕获它，以下是某些发行版的相应命令：

Slackware:

```bash
falcons-client# ln -s /opt/ssl-vpn/bin/vpn-client /etc/ppp/ip-up
bears-server# ln -s /opt/ssl-vpn/bin/vpn-server /etc/ppp/ip-up
```

Debian:

```bash
falcons-client# ln -s /opt/ssl-vpn/bin/vpn-client /etc/ppp/ip-up.d/vpn-client
bears-server# ln -s /opt/ssl-vpn/bin/vpn-server /etc/ppp/ip-up.d/vpn-server
```

Red Hat:

```bash
falcons-client# ln -s /opt/ssl-vpn/bin/vpn-client /etc/ppp/ip-up.local
bears-server# ln -s /opt/ssl-vpn/bin/vpn-server /etc/ppp/ip-up.local
```

### 创建全局配置文件

`vpn-client` 和 `vpn-server` 脚本都会读取 `/opt/ssl-vpn/etc/vpn.conf` 文件。该文件位于我们的系统中。按如下方式为客户端和服务器安装：

```bash
root# mkdir /opt/ssl-vpn/etc; chmod 755 /opt/ssl-vpn/etc
root# cp vpn.conf /opt/ssl-vpn/etc
root# chmod 644 /opt/ssl-vpn/etc/vpn.conf
```

此文件包含可能需要的外部程序的路径：

```bash
# 程序的位置。对于你的系统这些可能是正确的，但你应该验证一下。
su=/bin/su
sudo=/usr/bin/sudo
pppd=/bin/pppd
route=/bin/route
stunnel=/bin/stunnel
```

它还包含变量 `SSL_VPN_USER`。将其设置为为在客户端上运行 `vpn-client` 脚本的用户，在我们的示例中：

```bash
SSL_VPN_USER=sslvpn
```

client 程序最初将验证它是否以正确的用户运行，并在 `pppd` 参数中使用该值：

```bash
sudo -u pppd $stunnel
```

再次，这是因为 `pppd` 通过 `sudo` 以 `root` 身份运行，但我们希望 `pppd` 命令以 `SSL_VPN_USER` 身份运行。明白了吗？

## 创建 VPN 特定配置文件

我们的 `vpn-server` 和 `vpn-client` 程序被编写为能够建立任意数量 VPN 连接。这些命令通过检查程序名称和参数来确定应该创建哪个 VPN。如果指定了两个参数（如 `vpn-server start vpn1`），第二个参数就是 VPN 名称。通过 `/etc/init.d/vpn1` 或 `/etc/rc.X/S99vpn1` 符号链接调用，将使用程序名称，去掉任何 `S##`（或 `K##`），得到 VPN 名称 `vpn1`。也就是说，脚本尽可能直观地判断你的需求。

一旦确定了 VPN 名称，它将从 `/opt/ssl-vpn/etc/vpn_name/config` 获取配置变量。

因此，对于名为 `vpn1` 的 VPN，我们将创建 `/opt/ssl-vpn/etc/vpn1/config`。配置文件中的每个变量都以 `server_` 或 `client_` 开头，这意味着你可以创建一个包含所有值的文件并在系统之间共享，而无需担心冲突。表 4.2 显示的变量最重要的。

## 表 4.2 配置文件变量

| 变量 | 使用者 | 示例 | 说明 |

| :--- | :--- | :--- | :--- |

| client_network | server | 192.168.1.0/24 | VPN 客户端上的网络。VPN 客户端用 add 命令建立到远程网络的路由。如果未设置，假设客户端是主机、网关，不添加路由。 |

| server_network | client | 192.168.2.0/24 | VPN 服务器上的网络。VPN 客户端用 add 命令建立到远程网络的路由。如果未设置，假设服务器是主机、网关，不添加路由。 |

| server_ppp_ip | server | 192.168.254.254 | PPP 链路端 VPN 服务器的 IP 地址。确保此地址不在任何一台机器可用的网络中。 |

| client_ppp_ip | server | 192.168.254.253 | PPP 链路端 VPN 客户端的 IP 地址。确保此地址不在任何一台机器可用的网络中。 |

| server_stunnel port | both | 9871 | Stunnel 应该在服务器上绑定的端口，客户端应该连接到该端口。 |

| 可选变量 | | | |

| client_debug | client | yes | 向 pppd 参数添加 debug 选项，向 pppd 参数添加 -D7，并启用 set -x 以逐条命令输出 vpn-client 脚本。 |

| server_debug | server | yes | 与服务器端的 client_debug 相同。 |

| client_stunnel_args | client | -u sslvpn | 客户端额外的 Stunnel 参数。 |

## VPN 脚本 129

| 变量 | 使用位置 | 示例 | 解释 |

| --- | --- | --- | --- |

| server_stunnel_args | 客户端 | -C DES-CBC3-SHA | 服务器的额外 Stunnel 参数。 |

| client_pppd_args | 客户端 | usepeerdns | 此 VPN 的 pppd 额外命令行参数。 |

| server_pppd_args | 服务器 | proxyarp | 此 VPN 的 pppp 额外命令行参数。 |

| client_require_pap | 客户端 | yes | VPN 要求服务器进行 PAP 认证。yes 以外的任何值等同于 no。 |

| server_require_pap | 服务器 | yes | VPN 服务器要求客户端进行 PAP 认证。yes 以外的任何值等同于 no。 |

| client_require_chap | 客户端 | yes | 与 client_require_pap 相同但适用于 CHAP 协议。 |

| server_require_chap | 服务器 | yes | 与 server_require_chap 相同但适用于 CHAP 协议。 |

示例配置如下：

```
# VPN1 配置文件
# /opt/ssl-vpn/etc/vpn1

### 双方连接的网络，适用于
### 'route' 命令
client_network=192.168.2.0/24
server_network=192.168.1.0/24

### 我们需要调试信息吗？
client_debug="yes"
server_debug="yes"

# 为你需要的每个 VPN 选择不同的 IP。
server_ppp_ip=192.168.254.254
client_ppp_ip=192.168.254.253

# 我们需要 PPP 认证吗？
client_require_pap="no"
server_require_pap="no"
client_require_chap="yes"
server_require_chap="yes"
```

# 第 4 章 使用 SSL/TLS 和 PPP 构建 VPN

### 启动和停止 VPN

要手动启动 VPN，你可以只需运行以下命令：
