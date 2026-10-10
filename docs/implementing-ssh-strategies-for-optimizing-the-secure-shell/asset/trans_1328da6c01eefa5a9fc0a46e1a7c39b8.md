

## 网络设置

sshd2_config 文件中的网络部分应如下所示：

```
    Port                        443
    ListenAddress               0.0.0.0
    RequireReverseMapping        no
    ResolveClientHostName        yes
    MaxBroadcastsPerSecond       0
    NoDelay                      yes
    KeepAlive                    yes
```

SSH 配置图形用户界面中的网络部分应如图 2.3 所示。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_82_0.png)

**图 2.3** SSH 服务器配置工具中的网络屏幕。

表 2.19 描述了 SSH 服务器可用的网络选项。

### 表 2.19 网络部分的选项（Windows）

| 选项 | 描述 |
| :--- | :--- |
| Port | 设置 SSH 监听的端口号。默认端口为 22；然而，监听多个端口（包括 80、443 或 8080 等非常规端口）可能更优，因为商务旅行者可能无法在 22 端口建立出站连接，而 80 或 443 端口通常是可访问的。若要监听多个端口，请添加以下行：<br>`Port 22`<br>`Port 80`<br>`Port 443`<br>`Port 8080` |
| ListenAddress | 设置 SSH 守护进程监听的 IP 地址。默认为 0.0.0.0，这将启用所有接口上的 SSH 服务。如果存在 SSH 不应监听的接口（例如防火墙的外部接口），请移除 0.0.0.0 并添加相应的 IP 地址。若要仅监听特定接口，请添加以下行：<br>`ListenAddress 172.16.1.1,192.168.0.1`<br>`ListenAddress 10.0.0.1` |
| RequireReverseMapping | 启用（yes）或禁用（no）DNS 查找必须成功的设置，以便与 AllowHost 和 DenyHost 条目配合使用。如果启用且 DNS 查找失败，请求将被拒绝。如果禁用且 DNS 查找失败，系统将检查 AllowHosts 和 DenyHosts 中的 IP 地址。 |
| ResolveClientHostname（仅限 sshd_config 文件） | 启用（yes）或禁用（no）服务器通过 DNS 解析客户端 IP 地址的功能。 |
| MaxBroadcastPerSecond（仅限 sshd_config 文件） | 指定服务器每秒应处理的 UDP 广播数量。默认值为零，表示不处理任何广播。 |
| NoDelay | 启用（yes）或禁用（no）TCP_NODELAY 套接字选项。 |
| KeepAlive | 启用（yes）或禁用（no）SSH 服务器向 SSH 客户端发送 KeepAlive 数据包的功能。该值有助于防止会话挂起，通过判断对端的客户端是否仍在运行且未崩溃或蓝屏来实现。 |

## 加密设置

sshd2_config 文件中的加密部分应如下所示：

```
		Ciphers		AnyStdCipher
		MACs		AnyStdMac
		RekeyIntervalSeconds	0
		RandomSeedFile	"server_random_seed"
```

SSH 配置图形用户界面中的加密部分应如图 2.4 所示。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_84_0.png)

**图 2.4** SSH 服务器配置工具中的加密屏幕。

表 2.20 描述了 SSH 服务器可用的加密选项。

### 表 2.20 加密部分的选项（Windows）

| 选项 | 描述 |
| :--- | :--- |
| Ciphers | 列出用于加密会话的密文类型。支持三重 DES（3DES）、Blowfish、ArCFour、Twofish、CAST – 128 和 DES。可以设置更多全局选项，如 Any、Anystd、anycipher 和 anystdcipher。Any 和 anystd 允许使用标准密码；anycipher 允许任何密文；anystdcipher 允许在 IETF SSH 草案中列出的任何密码；设置为 none 则不提供密码。 |
| MACs | 消息认证码（MAC）是一种哈希算法，用于验证数据传输前后的完整性。支持的算法包括 SHA1、MD5、SHA1-96 和 MD5-96。也可以设置多个 MAC。 |
| RekeyIntervalSeconds | 指定再次执行密钥交换流程前的时间间隔。默认值为 3600 秒，即一小时。将该值设置为零即可禁用密钥交换流程。 |
| RandomSeedFile | 指定随机种子文件的位置。此文件用于为 SSH 服务器生成随机数。 |

## 用户设置

sshd2_config 文件中的用户部分应如下所示：

```
LoginGraceTime				600
PermitEmptyPasswords	no
UserConfigDirectory		"%D\_ssh2"
AuthorizationFile		"authorization"
PrivateWindowStation	yes
```

SSH 配置图形用户界面中的用户身份验证部分应如图 2.5 所示。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_86_0.png)

**图 2.5** SSH 服务器配置工具中的用户身份验证屏幕。

此外，用户身份验证-密码部分应如图 2.6 所示。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_86_1.png)

**图 2.6** SSH 服务器配置工具中的用户身份验证-密码屏幕。

最后，用户身份验证-公钥部分应如图 2.7 所示。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_87_0.png)

**图 2.7** SSH 服务器配置工具中的用户身份验证-公钥屏幕。

表 2.21 描述了 SSH 服务器可用的用户身份验证选项。

### 表 2.21 用户身份验证部分的选项（Windows）

| 选项 | 描述 |
| :--- | :--- |
| LoginGraceTime | 用户发起身份验证请求后完成登录流程允许的时间（以秒为单位）。取值范围从零（无限制）到 600 秒。 |
| PermitEmptyPasswords | 允许（yes）或拒绝（no）用户使用空密码。在大多数情况下，此项应设置为 no。 |
| UserConfigDirectory（sshd_config 文件） | 指定用户特定配置数据（如密钥和标识文件）的位置。默认为用户主目录中的 .ssh2 文件夹，例如 /home/<username>/.ssh2 或 Documents and Settings\<username>\.ssh2（%D 是用户主目录；%U 是用户登录名）。可以指定多个位置用于配置数据。 |
| 用户密钥目录（GUI） | 指定授权文件的位置，该文件通常命名为 authorization，位于 SSH 服务器上的用户主目录中。SSH 服务器使用此文件来指示在身份验证过程中哪些公钥是被授权接受的。例如，如果用户有两个用于身份验证的公钥，如 id_dsa_2048_a.pub 和 id_rsa_2048_a.pub，则授权文件的内容将如下所示：<br>`Key     id_dsa_2048_a.pub`<br>`Key     id_rsa_2048_a.pub`<br>注意：授权文件中列出的公钥也需要位于用户主目录中，详见第 4 章。 |
| PrivateWindowStation（仅限 sshd2_config 文件） | 启用（yes）或禁用（no）任何创建的终端处于完全私有窗口或非私有窗口的状态。 |

## 服务器公钥配置

sshd2_config 文件中的服务器公钥配置部分应如下所示：

```
#     HostKeyFile                hostkey
#     PublicHostKeyFile          hostkey.pub
```

SSH 配置图形用户界面中的标识部分应如图 2.8 所示。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_89_0.png)

**图 2.8** SSH 服务器配置工具中的标识屏幕。

表 2.22 描述了 SSH 服务器可用的服务器公钥选项。

### 表 2.22 服务器公钥配置部分的选项（Windows）

| 选项 | 描述 |
| :--- | :--- |
| HostKeyFile | 指定私钥主机密钥文件的位置。默认位置在本地文件系统的 /etc/sshd2 目录中。 |
| PublicHostKeyFile | 指定公钥主机密钥文件的位置。默认为 hostkey.pub，位于本地文件系统中。 |

## 服务器证书配置

sshd2_config 文件中的服务器证书配置部分应如下所示：

```
#        HostKeyFile          " "
#        HostCertificateFile " "
#        Pki                " "
#        MapFile            " "
#        LDAPServers
#        Socks5Server
#        PkiDisableCRLs     no
```

表 2.23 描述了 SSH 服务器可用的服务器证书选项。

### 表 2.23 服务器证书配置部分的选项（Windows）

| 选项 | 描述 |
| :--- | :--- |
| HostKeyFile | 指定私钥主机密钥文件的位置。默认为 hostkey，位于本地文件系统中。 |
| HostCertificateFile | 指定证书文件的位置。 |
| Pki | 启用（yes）或禁用（no）使用证书进行用户身份验证。 |

