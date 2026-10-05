

# CIFS 实现

所以，从管理员的角度来看，如果你想从几台 UNIX 服务器共享文件，你应该怎么做？是在你所有的 Windows 客户端上安装 NFS 客户端吗？还是在你的几台 UNIX 服务器上安装 CIFS 服务端？哪种方式的行政开销最少？虽然可能有些站点会选择以 NFS 为标准（这样做效果很好），但我会在 UNIX 服务器上安装某种 CIFS。一旦你这样做了，UNIX 系统就可以通过 NFS 访问其数据，而基于 Windows 的客户端则可以通过其原生文件共享协议 CIFS 访问相同的数据。与另一种方法相比，你的安装量更少，需要管理的服务器也更少。UNIX 系统由于其优秀的内存模型，可以轻松适应多个协议栈。在 CIFS 的情况下，它们只需要适应传输层以上层的功能：会话层、表示层和应用层。

## 12.3 CIFS 实现

CIFS 基于 SMB 协议，后者首次出现在 1987 年的 Microsoft Lan Manager 中。一年后，它出现在 IBM 的 OS/2 LAN Server 中。1992 年，SMB 成为一个开放标准，并随着 Windows for Workgroups、Windows 95、Windows 98 和 Windows NT 网络系统的陆续进入市场而成为它们的一部分。1994 年，微软将 SMB 服务端代码提供给了 AT&T；后者将代码移植到 UNIX 并提供给 UNIX 厂商。该产品被称为 Advanced Server for UNIX (ASU)，它被包括惠尔-派德（HP）和数字设备公司（DEC）在内的各种用户进行了修改和重命名。1996 年，微软将 SMB 的名称更改为 CIFS——这两个术语经常通用——并将其规范作为互联网草案（Internet-Draft）提交给互联网工程任务组（IETF）。

开源运动产生了名为 Samba 的免费软件，这是一种为 UNIX 系统设计的 CIFS 产品。Samba 的起源也可以追溯到 1991 年，当时 Andrew Triddell 的项目，他当时澳大利亚国立大学计算机科学实验室的一名研究生。目前，该免费软件由一个名为 Samba Team 的小小组领导，适用于所有 UNIX 实现。由于它是开源软件，因此其许可证遵循 GNU 通用公共许可证（GPL）（有关 GNU 的信息请参见第 1 章）。

2000 年，惠尔-派德生产了一款新产品 CIFS/9000，它在 HP-UX 11 上实现了 CIFS 服务端和 CIFS 客户端。CIFS/9000 服务端基于 Samba 2.0.6 版本，为 CIFS 客户端提供文件打印服务，包括 Windows 95、98、NT、2000 以及运行 CIFS/9000 客户端软件的 HP-UX 机器。CIFS/9000 客户端允许 HP-UX 用户从 CIFS 文件服务器挂载 UNIX 文件共享，包括运行 CIFS/9000 服务端的 Windows 和 HP-UX 机器。CIFS/9000 客户端还提供了一个可选的可插认证模块（PAM），用于实现 Windows NT LAN（NTLM）认证协议。在 HP-UX 环境中安装并配置 PAM 后，PAM NTLM 允许 HP-UX 用户通过 Windows 身份验证。

## 12.4 Windows 2000 域中的 CIFS/9000 服务

为了说明如何连接 HP-UX 系统与 Windows 2000 系统，我们现在描述一种使用 CIFS/9000 的配置。鉴于该产品与 Samba 之间密切的关系，通过这一概述将得出许多结果。通过这种方式，你可以推断在其他 UNIX 衍生系统中使用 CIFS 需要执行的操作。

### 12.4.1 愿景

如果你有一个 Windows 2000 域并想向该域引入一个 CIFS/9000 服务端，那么让 Windows 2000 域控制器对资源请求进行身份验证是合理的。这样做的主要目的是为了避免维护两个独立的密码数据库。客户端请求 CIFS/9000 资源，CIFS/9000 服务端将认证传递给域控制器。正如我们在第 11 章中通过 NFS 所看到的，用户账户名称匹配是有帮助的；否则，你必须为不同的账户名创建一个用户映射文件。

因此，站点配置用户使其 UNIX 账户名与 Windows 账户名匹配是常见的做法。然而，尽管认证发生在一个位置——即域控制器——你仍然维护着两个独立的数据库：一个用于 UNIX，一个用于 Windows 2000。如果你在 UNIX 环境中添加一个用户，就必须在 Windows 2000 域中添加一个相应的用户。但是，如果你在域控制器上运行 Server for NIS 呢？那样，你就可以通过 Active Directory Users and Computers 在一个位置为两个环境创建新账户。（有关 Server for NIS 的描述请参见第 10 章“Windows Services for UNIX”）。通过将 CIFS/9000（配置为使用域安全）与 Server for NIS 结合，你可以有效地统一你的 HP-UX 和 Windows 2000 用户数据库。让我们看看如何实现。

### 12.4.1.1 配置 CIFS/9000 服务端

设置 CIFS/9000 服务端的完整说明见惠尔-派德的文档《Installing and Administering the CIFS/9000 server》。该文档主要描述了 HP 对 Samba 所做的增强，并引导读者参考由 Robert Eckstein、David Collier 和 Peter Kelley 编写的另一本书《Using Samba》，以获取有关具体的get信息。由于该产品与 Samba 的关系密切，通过这一概述将得出许多结果。通过这种方式，你可以推断在其他 UNIX 衍生系统中使用 CIFS 需要执行的操作。

- 1. 安装 CIFS/9000 服务端的参考《Installing and Administering the CIFS/9000 server》。
- 2. 在配置 smb.conf 之前，创建一个名为 smbnull 的虚拟用户，参考《Installing and Administering the CIFS/9000 server》。
- 3. 在 smb.conf 的 global 节中将 guest account 设置为 smbnull（该文件位于 `/etc/opt/samba` 目录）。
- 4. 修改 smb.conf 以支持以下功能：ACL 支持、区分大小写、打印服务和国际化。
- 5. 在启动 Samba 守护进程之前，在 Active Directory Users and Computers 中选择你的域，然后选择 New→Computer。填写必要信息，勾选 Allow-Windows 2000 computers 使用此账户，然后点击 OK。[img/1c1e7552b53cca8883c6954] 图 12-1 将 CIFS/9000 服务端添加到 Windows 2000 域。
- 6. 然后，在 CIFS/9000 服务端上执行 smbpasswd 命令。例如：

```
smbpasswd -j book.local -r w2kserv
```
将 Windows 2000 域名作为 -j 的参数，将域控制器的名称作为 -r 的参数。此命令将创建一个系统密码并存储在 `/var/opt/samba/private` 目录下，文件名格式如下：domain_name.server_name.mac。在我的示例中，名称为 BOOK.LOCAL.HPUX1.mac。（Mac 扩展表示这是一个账户。）
- 7. 编辑你的 smb.conf 文件并指定以下变量：

- security = domain
- netbios name = server_netbios_name
- workgroup = domain_name
- password server = domain_controller_name(s)
- encrypt passwords = yes

例如，我的 smb.conf 包含了这些变量的条目，以及另外两个：

```
[global]
workgroup = BOOK.LOCAL
netbios name = HPUX1
security = DOMAIN
encrypt passwords = Yes
password server = w2kserv
username map = /var/opt/samba/usermap
guest account = smbnull
read only = No
case sensitive = yes
```

正如所示，我指定 `/var/opt/samba/usermap` 文件来包含两个操作系统之间不同用户账户的映射。在我的测试环境中，所有的用户账户名称都匹配，除了 root 和 administrator 之外。因此，在该文件中，我只有一个条目：

```
root = administrator
```

同时也为 guest账户和区分大小写指定 smbnull。

- 启动 Samba 守护进程 smbd 和 nmbd。在 CIFS/9000 中，你通过执行以下命令来实现：

```
# /opt/samba/bin/startsmb
```
