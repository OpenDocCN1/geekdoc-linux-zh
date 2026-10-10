
## 设置互联网连接

3. **选择变量** — 编辑 vars 文件。在本示例中，vars 文件位于 `/etc/openvpn/easy-rsa/2.0`。只要您在此配置目录中操作，大多数默认值都能正常工作。但是，您至少需要设置放置在证书中的键值。请将引号中的示例替换为您自己的值：

```
export KEY_COUNTRY="US"  
export KEY_PROVINCE="WI"  
export KEY_CITY="Madison"  
export KEY_ORG="Reedensburg-LUG"  
export KEY_EMAIL="chris@linuxtoys.net"
```

在 vars 文件中，您还可以更改诸如默认密钥大小（1024）和证书到期天数（3,650 天）等值。

4. **设置变量** — 将 vars 文件中的变量导出到当前 shell，以便您稍后运行的命令可以使用它们。

```
# source ./vars
```

5. **准备创建新密钥** — 如果您的 KEY_DIR 中有任何密钥（在当前目录中通常命名为 `keys/`），此命令将删除它们，并在该目录中创建 index.txt 和 serial 文件：

```
# ./clean-all
```

接下来，您将创建服务器证书和密钥。

6. **构建根证书颁发机构证书和密钥** — 运行以下命令，进而使用 `openssl` 命令创建一个 1,024 位 RSA 私有密钥：

```
# ./build-ca
Generating a 1024 bit RSA private key
...
++++
writing new private key to `ca.key`
...
Country Name (2 letter code) [US]:
State or Province Name (full name) [WI]:
Locality Name (eg, city) [Madison]:
Organization Name (eg, company) [Reedensburg-LUG]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) [Reedensburg-LUG CA]:
Email Address [chris@linuxtoys.net]:
```

keys 目录中应该有两个新文件。ca.key 文件保存私有密钥，ca.crt 文件保存从您的 KEY$ 值生成的新证书。

## 第四部分 网络

7. **创建 SSL/TLS 参数** — 输入以下命令以构建 SSL/TLS 连接所需的服务器端 Diffie-Hellman 参数：

```
# ./build-dh
Generating DH parameters, 1024 bit long safe prime, generator 2
This is going to take a long time
......*......*..................*....*...........
This creates a file named *dh1024.pem* in the keys directory.
```

8. **创建服务器密钥和证书** — 运行以下命令以创建 OpenVPN 服务器所需的密钥和证书，将 *server1* 替换为您的服务器主机名或其他用于标识它的通用名称：

```
# ./build-key-server server1
Generating a 1024 bit RSA private key
..++++++
.................+++++
writing new private key to 'server.key'
.
.
A challenge password []: chzypassw77
An optional company name []:
Using configuration from /etc/openvpn/easy-rsa/2.0/openssl.cnf
.
.
Sign the certificate? [y/n] Y
1 out of 1 certificate requests certified, commit? [y/n] y
Write out database with 1 new entries
Data Base Updated
```

刚才运行的命令会在 keys 目录中生成 *server.crt*、*server.csr* 和 *server.key* 文件。服务器密钥文件必须保密！

接下来，您需要为希望连接到您的 OpenVPN 服务器的每个客户端创建客户端证书和密钥。

9. **创建客户端证书和密钥** — 为每个希望使用 OpenVPN 服务器的客户端运行 *build-key*（或 *build-key-pass*）脚本。以下是为两个命名为 *client01* 和 *client02* 的客户端运行 *build-key* 脚本的示例：

```
# ./build-key client01
.
.
A challenge password []: my67ChvyB8
Sign the certificate? [y/n] y
1 out of 1 certificate requests certified, commit? [y/n]  y
   # ./build-key client02
```

当您为每个客户端运行 build-key 后，keys 目录中将为每个客户端拥有 crt（client01.crt）、csr（client01.csr）和 key（client01.key）文件。下一步是确保将这些密钥传输到相应的计算机。

在本示例中，我们将密钥复制到名为 client01 的 CentOS 客户端机器上的 /etc/openvpn/keys/ 目录中。（请参见本章后面的“创建 OpenVPN 客户端配置”部分。）

## 创建 OpenVPN 服务器配置

在服务器上启动 OpenVPN 服务之前，您需要创建 /etc/openvpn 目录中的 server.conf 文件。您可以通过复制示例 server.conf 文件并对其进行编辑来实现。以下是一个可用的示例：

```
# cd /usr/share/doc/openvpn-2.0.9/sample-config-files
# cp server.conf /etc/openvpn/
```

作为 root 用户，使用任何文本编辑器打开 server.conf 文件。这是一个进行路由（而非网桥）的多客户端服务器的示例。密钥文件的位置应与您在之前的密钥服务器部分中创建的位置匹配。本示例省略了许多注释，但您应该阅读 server.conf 文件中的注释以指导您的配置。

```
port 1194
proto udp
dev tun

ca /etc/openvpn/easy-rsa/2.0/keys/ca.crt
cert /etc/openvpn/easy-rsa/2.0/keys/server.crt
key /etc/openvpn/easy-rsa/2.0/keys/server.key       # This file should be kept secret
dh /etc/openvpn/easy-rsa/2.0/keys/dh1024.pem

server 10.8.0.0 255.255.255.0

keepalive 10 120
comp-lzo

persist-key
persist-tun

status openvpn-status.log
verb 3
```

在此配置中，OpenVPN 服务器监听端口 1194，使用 UDP 协议，作为路由 VPN 服务器（dev tun）。您可以使用不同的端口号使服务更隐蔽，但客户端也必须使用该端口号。OpenVPN 客户端可以通过此 VPN 连接访问的私有网络位于 10.8.0 子网（由 10.8.0.0 255.255.255.0 标识）上。完成配置文件后，您可以通过输入以下内容在服务器上启动 OpenVPN 服务：

```
# service openvpn start
```

为使您的 OpenVPN 服务器准备好接受连接，您需要采取的最后一个步骤是打开防火墙以接受端口 1194 上的连接，并允许您的系统将数据包路由到私有子网。在本示例中，我们使用了 IP 地址范围为 10.8.0.1 到 10.8.0.254 的私有子网。有关详细信息，请参见第 13 章的“防火墙”部分。

## 创建 OpenVPN 客户端配置

要配置 OpenVPN 客户端以连接到您刚刚配置的 OpenVPN 服务器，您需要将密钥文件复制到客户端，创建客户端配置文件，并启动服务。以下是如何从服务器复制密钥的示例：

```
# cd /etc/openvpn
# mkdir keys
# scp root@server1:/etc/openvpn/easy-rsa/2.0/keys/ca.crt keys
# scp root@server1:/etc/openvpn/easy-rsa/2.0/keys/client01.crt keys
# scp root@server1:/etc/openvpn/easy-rsa/2.0/keys/client01.key keys
```

将客户端配置文件复制到您的 /etc/openvpn 目录，并适当进行编辑。例如，输入以下内容：

```
# cd /usr/share/doc/openvpn-2.0.9/sample-config-files
# cp client.conf /etc/openvpn/
```

以下是一个编辑后的客户端 conf 文件示例：

```
client
dev tun
proto udp
ns-cert-type server
remote example.com 1194
resolv-retry infinite

nobind

persist-key
persist-tun

ca /etc/openvpn/keys/ca.crt
cert /etc/openvpn/keys/client01.crt
key /etc/openvpn/keys/client01.key

comp-lzo
verb 3
```

要测试您的 VPN 客户端配置是否有效，请输入以下内容：

```
# openvpn --config client.conf
```

此命令输出的信息将帮助您调试连接到 OpenVPN 服务器时遇到的任何问题。如果使用图形用户界面（GUI）启动您的 OpenVPN 客户端，请务必确定客户端配置文件和密钥的位置。

## 将 Linux 配置为代理服务器

您已设置了一个 LAN（局域网），且您的 Linux 计算机同时具有到 LAN 的连接和到 Internet 的连接。一种在不设置路由的情况下为 LAN 上的计算机提供 Web 浏览服务的方式是将 Linux 配置为代理服务器。

CentOS 附带 Squid 代理缓存服务器软件包。在基本配置中，您可以快速让软件运行起来。然而，该软件包功能丰富，可以根据您的需求进行适应。您可以控制哪些主机可以访问代理服务、内存如何用于缓存数据、如何记录日志以及各种其他功能。以下是 Squid 提供的基本代理服务：

- **HTTP** — 允许超文本传输协议（HTTP）代理服务是使用 Squid 的主要原因。这使得客户端计算机能够通过浏览器（通过您的 Linux 计算机）访问 Internet 上的网页。换句话说，HTTP 代理服务将查找并返回类似于 `www.ab.com` 的地址的内容。
- **FTP** — 这代表文件传输协议（FTP）代理服务。当您为客户端启用 HTTP 时，浏览器会自动启用匿名 FTP（例如，`ftp://ftp.ab.com`）。
- **Gopher** — Gopher 协议代理服务是组织 Internet 上文档和搜索的早期机制之一。它比 Web 早了十多年。现在已经没有人使用 Gopher 了；然而，当为客户端启用 HTTP 时，它会自动获得支持。

