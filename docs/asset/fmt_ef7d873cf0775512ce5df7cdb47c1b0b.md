
如果你使用域级安全功能，可以使用 Windows 2000/NT 的信任域功能。例如，假设你在名为 `ADMIN` 的 Windows 2000/NT 域中有一个名为 `myuser` 的用户，而你的 Samba 服务器属于一个名为 `ENGR` 的域。如果这两个域的主域控制器（PDC）已建立信任关系，那么来自 `ADMIN` 的 `myuser` 应该能够访问你 `ENGR` 域全局部分（global section） Samba 服务器。你可以通过设置 `/etc/samba/smb.conf` 文件中的以下参数来实现此点。

```
allow trusted domain = yes
```

当设置此参数时，来自信任域的用户可以访问 Samba 服务器——尽管他们仍然需要在 Samba 服务器上拥有 Linux 用户账户。请在 `/etc/samba/smb.conf` 文件的全局部分添加以下参数：

```
add user script = /usr/sbin/useradd -u musers
delete user script = /usr/sbin/userdel -u
```

配置好这些参数后，当来自信任域的用户首次尝试访问（另一个域的）S 服务器时，Samba 会执行域级安全措施。它会请求所属域的主域控制器（PDC）来验证用户。由于你已经与用户所在的域建立了信任关系，Samba 服务器的 PDC 就可以验证该用户。Samba 服务器将创建一个 Linux 用户账户并允许该用户访问请求的资源。

> 当 `allow trusted domain` 参数设置为 `no` 时，信任关系将被忽略。

![](img/177ab5b774eeb101e12de61f8616d71a_499_0.png)

## 通过网络接口控制 Samba 访问

你可以告诉 Samba 监听 Linux 系统的一个或多个网络接口。假设你正在一个有两个网络接口 `eth0` (`192.168.2.10`) 和 `eth1` (`192.168.3.10`) 的系统上运行 Samba，并希望将 Samba 服务限制在 `eth0` 上。在这种情况下，请在 `/etc/samba/smb.conf` 文件的全局部分定义以下参数。

```
interfaces = 192.168.2.10/24 127.0.0.1
bind interfaces = yes
```

第一个参数 `interfaces` 定义了 Samba 监听的网络接口列表。`192.168.1.10/24` 网络绑定到 `eth0` `{192.168.1.10}` 接口，因此被添加到接口列表中。添加 `127.0.0.1` 接口是因为它是本地回环接口，并用于 `smbpasswd` 连接到本地 Samba 服务器。下一个参数 `bind interfaces only` 设置为 `yes`，告诉 Samba 服务器仅监听 `interfaces` 参数中列出的接口。

![](img/177ab5b774eeb101e12de61f8616d71a_500_0.png)

你可以在 `interfaces` 参数中使用如 `eth0` 和 `eth1` 等接口设备名称。

## 通过主机名或 IP 地址控制 Samba 访问

你可以让 Samba 服务器允许允许主机访问其资源。例如，以下配置限制了其他主机的访问：

```
hosts deny = ALL
hosts allow = 192.168.1.0/24 127.0.0.1
```

在前面的行中，对 Samba 的访问限制如下：

- 第一个参数禁止所有主机的访问。
- 第二个参数开放了以下访问：
  - `192.168.1.0` 网络中的主机。
  - 本地主机 (`127.0.0.1`)。

如果你使用 IP 网络作为 `hosts allow` 参数的值，你也可以排除某些 IP 地址。例如，以下行允许 `192.168.1.0/24` 网络中的所有主机访问 Samba 服务器，但 `192.168.1.100` 除外：

```
hosts deny = ALL
hosts allow = 192.168.1.0/24 EXCEPT 192.168.1.100
```

你可以使用主机名代替 IP 地址。例如，以下配置允许网络中的三台计算机访问：

```
hosts deny = ALL
hosts allow = kabirspc, lancespc, stevespc
```

# 第 19 章：Samba 和 NFS 服务器安全 479

## 使用 pam_smb 通过 Windows NT 服务器验证所有用户

通常情况下，Linux 是大多数组织中的新成员；如果你有一个使用 Windows 2000/NT 机器进行验证的 Windows 2000/NT 网络，通常将 Linux 用户验证委托给 Windows 2000/NT 服务器会更容易管理。Samba 配合 `pam_smb` 可以使用 Windows 2000/NT 用户（或作为 PDC 的 Linux 版 Samba 服务器）来验证想要通过 Telnet 或 SSH 登录你的 Linux 系统的用户。

## 获取 PAM_SMB

你可以从位于 `ftp://ftp.samba.pub/samba/pam_smb` 的 FTP 站点下载 `pam_smb` 源码。

## 安装和配置 PAM_SMB

要安装并配置 `pam_smb`，请执行以下操作：

1. `su root`。
2. 使用 `tar xvzf pam_smb.tar.gz` 命令在目录中提取 `pam_smb` 分发包。切换到新创建的 `pam_smb` 目录。
3. 运行 `./config` 准备源码分发。将 `pamsmbd` 守护进程运行在默认位置 (`/usr/local/sbin`) 以外，运行 `--bindir=/path/to/sbin`，其中 `/path/to/sbin` 是你想保留守护程序的路径。可以使用 `--disable-password` 选项禁用密码。
4. 运行 `make` 命令。使用 `cp pam_smb_auth.so /lib/security` 命令将文件复制。
5. 如下所示修改 `/etc/pam.d/system-auth` 文件：

```
#PAM-
# 此文件是自动生成的。
# 下次运行 authconfig 时用户更改会被覆盖。
auth      sufficient      /lib/security/pam_smb_auth.so
auth     sufficient      /lib/security/pam_unix.so nullok md5
auth      required        /lib/security/pam_deny.so
account   sufficient      /lib/security/pam_unix.so
account   required        /lib/security/pam_deny.so
password  required        /lib/security/pam_crypt.so retry=3
password sufficient      /lib/security/pam_unix.so nullok use_authtok md5
password required        /lib/security/pam_deny.so
session required        /lib/security/pam_limits.so
session required        /lib/security/pam_unix.so
```

6. 配置文件存储在 `/etc/pam_smb.conf` 中，由三行组成：
   - 第一行用于验证的 NT 域名。
   - 第二行为主域控制器名称。
   - 第三行是辅助域控制器名称。

![](img/177ab5b774eeb101e12de61f8616d71a_502_0.png)

这些不需要是 NT 服务器——只需能够在域中验证的机器即可。例如，列表 19-1 显示了 `/etc/pam_smb.conf` 的示例版本。这里第一行 `KINET` 是域名，第二行 `PDCSRV` 是主域控制器，最后一行 `BDCSRV` 是辅助域控制器。

列表 19-1：`/etc/pam_smb.conf` 的示例版本

```
KINET
PDCSRV
BDCSRV
```

7. 如果你将 `pamsmbd` 安装在 `/usr/local/sbin` 目录，请在 `/etc/rc.d/rc.local` 文件中添加以下行，以便系统启动时自动启动守护程序：

```
/usr/local/sbin/pamsmbd
```

8. 运行 `/usr/local/sbin/pamsmbd` 命令首次启动守护程序。

你的 Linux 系统使用 `/etc/pam_smb.conf` 中指定的 Windows 域控制器进行用户验证。在列表 19-1 所示的示例文件中，验证过程使用 `KINET` 域中的 `PDCSRV` 机器。如果 `PDCSRV` 宕机，则使用 `BDCSRV`。
