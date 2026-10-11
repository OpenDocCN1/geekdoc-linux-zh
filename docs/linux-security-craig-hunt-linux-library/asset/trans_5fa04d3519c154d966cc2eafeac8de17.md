
**注意** 如果您的远程 SMB 服务器是 Windows NT 服务器，则域模式访问控制总是优于服务器模式，因为服务器模式在客户端-服务器连接期间会占用 Windows NT 服务器上的一个许可证。另一方面，域模式认证在认证完成后立即释放连接（以及 Windows NT 许可证实例）。这一点非常重要，因为微软的授权策略围绕并发服务器连接。

## 其他访问控制功能

除了上述四种访问控制方法外，您还可以选择利用本地 NT 域和一个受信任的第二 NT 域之间的信任关系。截至 Samba 2.0.4，可以使用 `smb.conf` 指令 `allow trusted domain = yes` 来获取来自 NT 域控制器的认证，尽管该控制器不是您域的主控制器，但它受您的 PDC 信任。

Samba 访问控制功能集的另一项新近添加的功能是 `add user script` 指令。在 `user` 和 `domain` 访问控制模式下都可以使用此指令，以便在用户/密码被密码服务器认证但用户在本地不存在时自动添加用户。例如，您可能希望 Samba 使用以下 `smb.conf` 指令在本地自动添加用户：

```text
add user script = sudo /usr/sbin/useradd %u
```

相反，可以指定 `delete user script` 指令来删除本地存在但在 PDC 上不再有效的用户。此用法的示例如下：

```text
delete user script = sudo /usr/sbin/userdel %u
```

虽然以这种方式添加和删除本地用户可能很方便，但我敦促您谨慎实施，因为这允许在用于常规 Linux 服务器认证的 `/etc/passwd` 或 `/etc/shadow` 文件中无人值守地创建和删除用户。

## [homes] 指令

允许所有 Linux 服务器用户访问其主目录的一种常见方法是 `smb.conf` 文件中的特殊 `[homes]` 指令。请考虑以下示例：

```text
[homes]
comment = Home Directories
browseable = no
writable = yes
```

该指令指定 `/etc/passwd` 中的任何用户可以通过将其 SMB 客户端指向 `\\server\\username` 来访问其主目录。这并不总是理想的，因为此文件包含诸如 root、operator、uucp 和 bin 等系统相关账户。为确保这些用户不被授予访问权限，请使用 `invalid users` 指令来排除这些用户名，如下例所示：

```text
[global]
   invalid users = root, operator, uucp, bin
```

### Samba 通信的隐私性

Samba 使用 TCP/IP 层来传输从客户端到服务器的 NetBIOS 流量。这允许您通过互联网共享驱动器，这是一种方便但通常不安全的做法，因为文件内容可能会暴露给潜在的窃听者。如果您打算在公共（不受信任）网络（如互联网）上交换 SMB 流量，您的安全策略需要包含一项条款，以确保此类流量的隐私性和认证。

通过使用前一节中描述的用于传输 SWAT 流量的常用 OpenSSL 实现，可以保护 SMB 流量的内容。由于 Windows SMB 客户端不直接支持 SSL，您必须在本地（受信任）网络的边缘设置一个代理 SSL 站点，该站点加密流量并代表客户端将其转发到目标 SSL 启用的 Samba 服务器。此过程如图 8.5 所示。

**图 8.5** 使用 SSL 保护 Samba

![](img/3258bbaf790525f8c4eb25fabff7844a_248_0.png)

图中显示了两个企业站点（站点 A 和站点 B），它们通过接入路由器连接到互联网。在站点 A 的接入路由器后面，设置了一台 Linux 服务器作为 SSL 代理。站点 A 局域网中的一台典型 Windows SMB 客户端将其 SMB 请求指向本地 SSL 代理，然后该代理在 OpenSSL 隧道内将连接中继到站点 B 内部的 Samba 服务器。站点 B 的服务器也以加密响应进行回复，而站点 A 的 SSL 代理则将其明文中继回 Windows 客户端。这确保了 SMB 流量受到保护，至少是在通过公共互联网传输时。但请注意，SMB 流量在站点 A 的本地网络内是明文传输的。

**为 Samba-SSL 创建证书颁发机构** 设置任何 SSL 应用的第一步是创建一个证书颁发机构 (CA)，以颁发用于两个端点相互认证所需的数字证书。首先，确保您的系统上安装了 OpenSSL：

```text
[ramon]$ rpm -q openssl
openssl-0.9.5a-14
```

然后，您需要使用以下命令为 CA 创建一个新的目录。首先创建将存储 Samba CA 的目录：

```text
[ramon]$ sudo mkdir /etc/samba/CA
[ramon]$ cd /etc/samba/CA
```

此 CA 签发的每个证书都将包含一个序列号。通过在文件 `/etc/samba/CA/serial` 中添加文本 "01"，您正在初始化 CA 将用于分配序列号的文件：

```text
[ramon]$ sudo echo "01" > serial
```

`index.txt` 文件用于 CA 维护证书数据库，必须简单地创建为空：

```text
[ramon]$ sudo cp /dev/null index.txt
```

接下来，您需要创建一个适合您需求的适当的 OpenSSL 配置文件。首先将原始 `/usr/share/ssl/openssl.cnf` 文件复制到 `/etc/samba/CA` 目录：

```text
[ramon]$ sudo cp /usr/share/ssl/openssl.cnf openssl.cnf
```

现在，编辑新创建的 `openssl.cnf` 文件以包含这些新设置：

```text
dir             = /etc/samba/CA                  # Where everything is kept
new_certs_dir   = $dir                            # default place for new certs.
certificate     = $dir/ca-cert.pem                # The CA certificate
private_key     = $dir/ca-key.pem                 # The private key
```

注意，您只是将默认基础 CA 目录更改为您之前为 Samba 创建的目录（`/etc/samba/CA`）。您还定义了 CA 的证书和密钥将分别驻留在 `/etc/samba/CA/ca-cert.pem` 和 `/etc/samba/CA/ca-key.pem` 中。

![](img/3258bbaf790525f8c4eb25fabff7844a_249_0.png)

![](img/3258bbaf790525f8c4eb25fabff7844a_249_1.png)

接下来，发出 `openssl` 命令以生成 CA 的私钥 (`ca-key.pem`) 及其 X.509 证书 (`ca-cert.pem`)：

```bash
[ramon]$ sudo openssl req -new -x509 -keyout ca-key.pem -out ca-cert.pem -days 365 -config openssl.cnf
```

现在您可以为 Samba 服务器本身创建一个新的证书，并使用 CA 的私钥对其进行签名。输入以下命令：

```bash
[ramon]$ sudo openssl req -nodes -new -x509 -keyout server-key.pem -out newreq.pem -days 365 -config openssl.cnf
[ramon]$ sudo openssl x509 -x509toreq -in newreq.pem -signkey server-key.pem -out tmp.pem
[ramon]$ sudo openssl ca -config openssl.cnf -policy policy_anything -out server-cert.pem -infiles tmp.pem
```

第一条命令为 Samba 服务器创建私钥 (`server-key.pem`) 和证书签名请求 (`newreq.pem`)。第二条和第三条命令获取证书签名请求并使用 CA 的私钥对证书进行签名。生成的 Samba 证书文件保存为 `server-cert.pem` 文件。

您还需要为客户端（SSL 代理）创建一个证书，因为客户端和服务器都需要相互认证。使用以下命令创建此证书：

```bash
[ramon]$ sudo openssl req -nodes -new -x509 -keyout proxy-key.pem -out newreq.pem -days 365 -config openssl.cnf
[ramon]$ sudo openssl x509 -x509toreq -in newreq.pem -signkey proxy-key.pem -out tmp.pem
[ramon]$ sudo openssl ca -config openssl.cnf -policy policy_anything -out proxy-cert.pem -infiles tmp.pem
```

现在您拥有了名为 `proxy-cert.pem` 和 `server-cert.pem` 的客户端和服务器证书，以及相应的私钥文件 `proxy-key.pem` 和 `server-key.pem`。请注意，您需要将 `proxy-cert.pem` 和 `proxy-key.pem` 文件复制到代理机器上。关于这些文件的放置，您将在本章后面的“下载和安装 SSL 代理”部分中了解更多内容。

恭喜！您现在已经完成了通过 SSL 传输 SMB 请求所需的 OpenSSL 配置。接下来，您需要通过输入 `/etc/samba/smb.conf` 文件中的适当指令来告知 Samba 此配置的存在。这是下一节的主题。

**配置 Samba 以支持 SSL** 表 8.1 列出了使 Samba 支持 SSL 所需的指令的语法及其含义。

