
使用证书和私钥，你可以创建一个安全环境，允许多个客户端通过互联网访问你的私有网络。以下步骤在 Fedora 系统上执行，但该系统不一定与你用于 VPN 服务器的系统相同。尽管如此，整个过程都在 OpenVPN 服务器上运行。

要开始设置公钥基础设施，以 root 身份打开终端并执行以下操作：

### 1. 复制示例配置文件

```
# cp -r /usr/share/openvpn/easy-rsa/ /etc/openvpn/
# cd /etc/openvpn/easy-rsa-2.0
```

### 2. 选择变量

编辑 `vars` 文件（在本示例中，`vars` 位于 `/etc/openvpn/easy-rsa/2.0`）。由于你是从此配置目录操作，大多数默认值都可以生效。但是，你至少需要设置放置在证书中的键值。将引号中的示例替换为你自己的值：

```
export KEY_COUNTRY="US"
export KEY_PROVINCE="WI"
export KEY_CITY="Madison"
export KEY_ORG="Madisonburg-LUG"
export KEY_EMAIL="chris@linuxuxtoys.net"
```

在 `vars` 文件中，你可以更改诸如默认密钥大小（1024）和证书有效期（3650 天）等变量。

### 3. 设置变量

将 `vars` 文件中的变量导出到当前 shell，以便稍后运行的命令可以使用：

```
./vars
```

### 4. 准备创建新密钥

如果你的 `KEY_DIR` 中有任何密钥（可能在当前目录下命名为 `keys/`），此命令将删除它们并在该目录下创建 `index.txt` 和序列文件：

```
./clean-all
```

接下来你将创建服务器证书和密钥。

### 5. 构建根权威证书和密钥

运行以下脚本，该脚本将使用 `pktool` 命令创建一个 1024 位 RSA 私钥：

```
# ./build-ca
Generating a 1024 bit RSA private key
+++++++
writing new private key to 'ca.key'
```

`Country Name (2 letter code) [US]:n`

`State or Province Name (full name) [WI]:n`

`Locality Name (eg, city) [Madison]:n`

`Organization Name (eg. company) [Reedsburg-LUG]:n`

`Organizational Unit Name (eg, section) []:`

`Common Name (eg, your name or server's hostname) [Reedsburg-LUG CA]:n`

`Email Address [chris@huxotus.net].`

你在 `keys` 目录下有两个新文件。`ca.key` 文件持有私钥，`ca.crt` 文件持有根据你的 `KEYS` 值生成的证书。

### 6. 为 SSL/TLS 创建参数

输入命令以构建 SSL/TLS 连接所需的服务器端 Diffie-Hellman 参数：

```
# ./build-dh
Generating DH parameters, 1024 bit long safe prime, generator
This is going to take a long time
+++++
```

这会在 `keys` 目录下创建一个名为 `dh1024.pem` 的文件。

### 7. 创建服务器密钥和证书

运行以下命令在 OpenVPN 服务器上所需的密钥和证书，将 `server1` 替换为你的服务器的主机名或其他标识性名称：

```
# ./build-key-server server1
Generating a 1024 bit RSA private key
+++++++
+++++++
writing new private key to 'server.key'

A challenge password []: chrypassw77
An optional company name []:
Using configuration from /etc/openvpn/rsa/2.0/openssl.cnf
.
```

`Sign the certificate? [y/n]:y`

`1 out of 1 certificate requests received, commit? [y/n] y`

`Write out database with 1 new entries`

`Data Base Updated`

该命令仅在 `keys` 目录下生成 `server.crt`、`server.csr` 和 `server.key` 文件。`server.key` 文件必须保密！接下来你需要为每个想要连接到 OpenVPN 的客户端创建证书和密钥。

### 8. 创建客户端证书和密钥

对于每个想要使用 OpenVPN 服务器的客户端，运行 `build-key`（或 `build-key-pass`）脚本。这里是为名为 `client01` 和 `client02` 的两个客户端运行 `build-key` 脚本的示例：

```
./build-key client01

A challenge password [:]: my67chvyB
Sign the certificate? [y/n] y
1 out of 1 certificate requests, commit? [y/n] y
./build-key client02
```

在为每个客户端运行 `build-key` 后，你将在 `keys` 目录下为每个客户端拥有一个 `crt` (`client01.crt`)、`csr` (`client01.csr`) 和 `key` (`client01.key`) 文件。下一步是确保每个文件都传输到相应的计算机上。

在本示例中，你将密钥复制到我们称为 `client01` 的 Fedora 客户端机器上的 `/etc/openvpn/keys/` 目录。（请参阅本章稍后的“创建 OpenVPN 客户端配置”部分。）

## 创建 OpenVPN 服务器配置

在服务器上启动 OpenVPN 服务之前，你需要在 `/etc/openvpn` 目录中创建一个 `server.conf` 文件。你可以通过复制 `server.conf` 文件并编辑它来完成。这里有一个你可以使用的示例：

```
# cd /usr/doc/openvpn-2.1/sample-config-files
# cp server.conf /etc/openvpn/
```

以 root 身份，使用任何文本编辑器编辑 `server.conf` 文件。这是一个多客户端路由（而非桥接）服务器的示例。密钥的位置应与你之前在服务器密钥部分创建的位置匹配。此示例中省略了许多注释，你应该阅读 `server.conf` 文件中的注释来指导你的配置。

```
port 1194
proto udp
dev tun

ca /etc/openvpn/easy-rsa/2.0/keys/ca.crt
cert /etc/openvpn/easy-rsa/2.0/keys/server.cert
```

```
key /etc/openvpn/easy-rsa/2.0/keys/server.key  # 此文件应保持保密
dh /etc/openvpn/easy-rsa/2.0/keys/dh1024.pem
```

```
server 10.8.0.0 255.255.255.0

keepalive 10 120
comp-lzo
persist-key
persist-tun

status openvpn-status.log
```

在此配置中，OpenVPN 服务器监听在端口 `1194` 上，使用 UDP 协议，作为路由 VPN 服务器（`dev tun`）。你可以使用不同的端口号使服务更具隐蔽性，但客户端也必须使用该端口。OpenVPN 客户端通过此 VPN 连接可以访问的私有网络位于 `10.8.0.0` 子网（由 `10.8.0.0 255.255.255.0` 标识）。配置文件完成后，你可以通过输入以下命令在服务器上启动 OpenVPN 服务：

```
# service openvpn start
```

让你的 OpenVPN 服务器准备好接受连接的最后一步是打开防火墙以接受端口 `1194` 的连接，并允许系统将数据包路由到你的私有子网。在示例中，我们使用 IP 地址从 `10.8.0.1` 到 `10.8.0.254` 的私有子网。详情见第 14 章的“防火墙”部分。

## 创建 OpenVPN 客户端配置

要配置 OpenVPN 客户端连接到服务器，你需要将密钥文件复制到客户端，创建客户端配置文件并启动服务。以下是你如何从服务器复制密钥的示例：
