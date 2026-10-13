
- `192.168.1.0` 网络中的主机。
- 本地主机 (`127.0.0.1`)。

如果你将 IP 网络作为 `hosts allow` 参数的值，你也可以排除某些 IP 地址。例如，以下行允许 `192.168.1.0/24` 网络中的所有主机访问 Samba 服务器，排除 `192.168.1.100`：

`hosts deny = ALL`

`hosts allow = 192.168.1.0/24 EXCEPT 192.168.1.100`

你可以使用主机名代替 IP 地址。例如，以下内容允许网络中的三台计算机访问：

`hosts deny = ALL`

`hosts allow = kabirsp, lancespc, stevespc`

# 第十九章：Samba 和 NFS 服务器安全

## 使用 pam_smb 通过 Windows 服务器验证所有用户

通常，Linux 是大多数组织中的新成员；如果你有一个 Windows 2000/NT 网络，其中 Windows 2000/NT 机器用于身份验证，那么如果可以将 Linux 用户验证委托给 Windows 2000/NT 服务器，通常管理会更简单。Samba 配合 `pam_smb` 可以使用 Windows 2000/NT 服务器（或作为 PDC 的 Linux Samba 服务器）来验证通过 Telnet 或 SSH 登录你的 Linux 系统的用户。

## 获取 PAM_SMB

你可以从 `ftp://ftp.samba.org/pub/samba/pam_smb` 站点下载 `pam_smb` 源码。

## 安装和配置 PAM_SMB

要安装并配置 `pam_smb` 模块，请执行以下操作：

1. `su root`。
2. 使用 `tar xvzf pam_smb.tar.gz` 命令在目录中提取 `pam_smb`。将当前目录切换到新创建的 `pam_smb` 目录。
3. 运行 `./configure` 提供源码。要将 `pammsbd` 守护放在默认位置 (`/usr/local/sbin`) 之外，运行 `./configure --sbindir=/path/to/path/to/pam/to/pam_smb`，即你想保留守护二进制文件的路径。要禁用加密密码，可以在运行配置脚本时使用 `--disable-encrypt-pass` 选项。
4. 运行 `make` 命令。使用 `cp pam_smb_auth.so /lib/security` 命令将 `pam_smb_auth.so` 文件复制到 `/lib/security`。
5. 如下所示修改 `/etc/pam.d/system-auth` 文件：

```
#PAM-1.0
# 此文件自动生成。
# 用户更改在下次运行 authconfig 时会被删除。
auth sufficient /lib/security/pam_smb_auth.so
#auth sufficient /lib/security/pam_unix.so likenullock md5
auth required /lib/security/pam_deny.so
account sufficient /lib/security/pam_unix.so
account required /lib/security/pam_deny.so
password required /lib/security/pam_unix.so
session required /lib/security/pam_deny.so
```

`/etc/samba/smb.conf` 文件限制了 `SSL` 连接到 `192.168.1.0/24` 网络。

- `hosts allowsign` 允许主机名、IP 地址、IP/掩码的某些主机或 IP 地址。例如，`hosts allowsign 192.168.1.10/24` 允许所有客户端通过 SSL 通信。
- 3. 使用 `certdir /usr/local/ssl/certs` 参数指向存放证书颁发（CA）证书的目录。你应该为服务器信任的每个 CA 准备一个文件，文件名必须是 CA 的区分名称。
- 4. 使用 `certfile /usr/local/ssl/certs/trustedAs.pem` 指向包含所有服务器证书的文件。如果你使用了上一个示例所示的 `certdir` 参数，则不需要此参数。
- 如果你只有一个 CA 证书，请使用此参数代替 `certdir`。
- 5. 使用 `servercert /usr/local/ssl/certs/samba.pem` 指向服务器证书。
- 使用 `serverkey /usr/local/ssl/private/samba.pem` 指向服务器的私钥。
- 使用 `clientcert /usr/local/ssl/certs/smclient.pem` 参数指向客户端使用的证书。
- 6. 使用 `clientkey /usr/local/ssl/private/smclient.pem` 参数指向私钥文件。
- 7. 使用 `requireclient yes` 参数，服务器拒绝没有有效客户端证书的连接。当客户端提交证书时，服务器将通过指定的 `certfile` 目录或指定的证书来验证证书。
- 8. 使用 `smb` 时如果需要服务器证书，请使用 `requireserver yes` 参数。

一旦你为 SSL 配置了 `/etc/samba/smb.conf` 文件，就可以运行支持 SSL 的 Samba。

## 使用 SSL 运行 Samba

运行支持 SSL 的 Samba 与运行不支持 SSL 的版本没有区别。但是如果你在创建私钥时使用了密码，系统会提示你输入密码。

1. 如果你使用了加密（带密码）的私钥，则要求不要通过 `/etc/rc.d/Sxx` 符号链接（xx 是数字）自动启动 Samba。它不会启动并等待密码。
2. 如果你必须对私钥使用密码，请删除符号链接 `/etc/rc.d/Sxx` 并始终手动启动 Samba 服务器。
3. 如果你创建一个未加密的私钥，可以像往常一样启动 Samba 服务器。手动启动服务器请运行 `/etc/rc.d/init.d/smb` 命令。

Samba 会正常启动。如果私钥是加密的，守护进程在进入后台之前会询问私钥密码。如果你从 `inetd` 启动 `smbd`，这将不起。因此，如果你从 `inetd` 运行 `smbd`，则不要加密你的私钥。

NFS 服务器广泛用于文件服务器。在本节中，我将讨论与 NFS 服务器有关的安全问题。

## 为导出目录授予只读访问

要允许从你的 NFS 服务器向客户端导出的任何目录或文件系统的只读访问，你可以像示例所示使用 `ro` 选项：

```
/apps devpc.nitec.com(ro)
```

在这里，`devpc.nitec.com` 客户端系统对 `/apps` 目录具有只读访问权限。我建议使用 `ro` 导出存储应用程序二进制文件的目录。

## 禁用特定目录的访问

当你导出整个文件系统或目录时，导出目录下的子目录可以使用相同的访问选项访问。然而，这并不总是所需要的。你可能希望允许访问 `/pub` 目录，但不允许 `/pub/staff-only` 目录。在这种情况下，如下使用 `noaccess` 选项：

```
/pub ??nitec.com (ro)
/pub/staff-only ??nitec.com (noaccess)
```

在这里，所有 `??nitec.com`（?? 是任意字符）对 `/pub` 目录都有只读访问权限，但由于下一行的 `noaccess` 选项，无法访问 `/pub/staff-only` 目录。

## NFS 服务器与客户端之间的用户映射

设置 NFS 服务器后，很快出现的问题就是保持 NFS 服务器与客户端之间的用户映射。例如，假设你正在导出一个目录 `/www`，它分别由用户 `webguru` 和组 `webdev` 所有。能够挂载此目录的 NFS 客户端必须拥有名为 `webguru` 的用户或 `webdev` 组以获取权限。特别是，NFS 服务器默认强制执行 root。

## 使用 NOSUID 和 NOEXEC 选项

你可以使用 `nosuid` 选项禁用从 NFS 运行 set-UID 程序。

例如，你可以在 `/etc/exports` 文件中写入如下的一行：

`/www www.nitecom.com(rw, root_squash, nosuid)`

在这里，`/www` 目录可以在 `www.nitecom.com` 上挂载。`www.nitecom.com` 上的用户可以读写 `/www` 下的文件和目录，但不能从中运行 set-UID 程序。

你也可以通过在选项列表中添加 `noexec` 选项来完全禁止在挂载的文件系统上执行文件。

## 使用加密文件系统
