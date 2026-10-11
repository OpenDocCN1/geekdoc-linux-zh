

曾用于在 Linux 上创建文件共享服务器。Samba 项目提供客户端工具来访问服务器，既可以访问文件也可以访问打印机。2003 年发布的版本 3 能够作为成员加入 **Active Directory**。新版本 Samba（4.x）支持最新的 SMB 协议，并包含协议提供的现代功能。这些功能的一些示例如下：

- NetBIOS over TCP/IP
- WINS 服务器（也称为 NetBIOS 名称服务器）
- 安全账户管理器
- 本地安全机构
- NTLM（NT 局域网管理器）

*图 10.7* 展示了 Samba 架构的示意图：

![](img/863afa537de4eed7deb11978bfbfa90e_313_0.png)

*图 10.7：Samba 架构示意图。来源：Samba*

## Samba 服务器

**Samba 服务器**，名为 **smbd**，向 Windows 客户端提供文件共享和打印服务。该服务器包含在 **samba** 软件包中，在 APT 和 RPM 软件仓库中名称相同。配置该服务的主要文件是 */etc/samba/smb.conf*，其中包含全局配置参数以及共享（目录和打印机）的定义。Ubuntu 系统中的默认配置如下所示：

```ini
[global]
    workgroup = WORKGROUP
    server string = %h server (Samba, Ubuntu)
    log file = /var/log/samba/log.%m
    max log size = 1000
    logging = file
    panic action = /usr/share/samba/panic-action %d
    server role = standalone server
    obey pam restrictions = yes
    unix password sync = yes
    passwd program = /usr/bin/passwd %u
    passwd chat = *Enter\new\s*\password:* %\n\n
    *Retype\snew\s*\password:* %\n\n
    *password\supdated\ssuccessfully* .
    pam password change = yes
    map to guest = bad user
    usershare allow guests = yes
[printers]
    comment = All Printers
    browseable = no
    path = /var/spool/samba
    printable = yes
    guest ok = no
    read only = yes
    create mask = 0700
[print$]
    comment = Printer Drivers
    path = /var/lib/samba/printers
    browseable = yes
    read only = yes
    guest ok = no
```

在全局配置中，工作组名称定义为 WORKGROUP，并定义了日志目录 /var/log/samba/，以及其他与用户相关的选项。配置了两个默认共享，`printers` 和 `print$`，但来宾用户无法访问它们。要定义新的共享，应在文件 `smb.conf` 中添加一个新部分，例如，将目录 `/storage` 共享给用户以便写入，将 `/public` 共享为只读：

```ini
[storage]
    comment = storage directory
    path = /storage
    browseable = Yes
    read only = No
[public]
    comment = Public directory
    path = /public
    browseable = Yes
    read only = Yes
```

修改文件 `smb.conf` 后，可以使用命令 `testparm` 来确保语法和选项有效。如果文件内容正确，它将在屏幕上显示内容。然而，如果发现任何问题，它会报告位置，如图 10.8 所示：

```text
root@ubuntu:~# testparm -v /etc/samba/smb.conf
Load smb config files from /etc/samba/smb.conf
Error loading services.
```

*图 10.8：命令 testparm 的输出示例*

Samba 套件还提供名为 `smbcontrol` 的命令，该命令向 `smbd` 发送消息。通常使用该命令的参数 `reload-config` 来重新加载配置，或使用参数 `shutdown` 来停止服务。例如，命令 `smbcontrol smbd reload-config` 会向服务 `smbd` 发送消息以重新加载配置文件内容。

Samba 提供命令 `smbpasswd` 来管理访问该服务的用户和密码。用户将映射到本地用户，这意味着分配给本地用户的用户 ID 和组 ID 将用于访问客户端请求的目录。命令 **smbpasswd** 具有选项 **-a**，用于向允许访问系统的 Samba 用户添加新用户，如*图 10.9*所示：

```text
root@ubuntu:~# smbpasswd -a agonzalez
New SMB password:
Retype new SMB password:
```

*图 10.9：命令 smbpasswd 的输出示例*

用户存储在目录 `/var/lib/samba/private/` 中的私有数据库中。Samba 提供命令 **pdbedit**，使用选项 **-L** 列出数据库中的用户，使用选项 **-v** 获取关于用户的详细信息。*图 10.10* 显示了这两个选项的使用情况：

```text
root@ubuntu:~# pdbedit -L
agonzalez:1000:agonzalez
root@ubuntu:~# pdbedit -L -v
------------------
Unix username:    agonzalez
NT username:    
Account Flags:    [U          ]
User SID:    S-1-5-21-1583416681-3049946014-381383256-1001
Primary Group SID:    S-1-5-21-1583416681-3049946014-381383256-513
Full Name:    agonzalez
Home Directory:    \\UBUNTU\agonzalez
HomeDir Drive:    
Login Script:    
Profile Path:    \\UBUNTU\agonzalez\profile
Domain:    UBUNTU
Account desc:    
Workstations:    
Munged dial:    
Logon time:    0
Logoff time:    Wed, 06 Feb 2036 15:06:39 UTC
Kickoff time:    Wed, 06 Feb 2036 15:06:39 UTC
Password last set:    Sat, 10 Sep 2022 21:53:01 UTC
Password can change:    Sat, 10 Sep 2022 21:53:01 UTC
Password must change:    never
Last bad password    :    0
Bad password count :    0
Logon hours    :    FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
```

*图 10.10：命令 pdbedit 的输出示例*

可以配置 Samba 服务器使用不同的认证源，例如 **轻量级目录访问协议**（LDAP）。Samba 还可以作为 **Active Directory 域控制器**运行，提供 DNS 服务和 **Kerberos** 认证。本书仅涵盖作为文件共享的 Samba。

## Samba 客户端

Samba 软件套件包含不同的命令，用于作为 SMB 协议的客户端。最常用的命令是 **smbclient**，它是 RPM 软件仓库中软件包 **samba-client** 和 DEB 软件仓库中软件包 **smbclient** 的一部分。该命令用于连接 SMB 服务以访问资源。除非使用选项 **-L**（**--list**），否则该命令以交互模式工作。*图 10.11* 和 *10.12* 显示了语法和不同的用法：

- 列出服务器 192.168.122.43 的共享资源，如*图 10.11*所示：

```text
[root@rhel ~]# smbclient -L //192.168.122.43/ -U agonzalez
Password for [SMB\ agonzalez]:
Sharename    Type    Comment
---------    ----    -------
print$       Disk    Printer Drivers
storage      Disk    Storage directory
public       Disk    Public directory
IPC$         IPC     IPC Service (ubuntu server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
```

*图 10.11：命令 smbclient 的使用示例*

- 交互式访问 Samba 服务器并列出 *storage* 目录的内容，如*图 10.12*所示：

```text
[root@rhel ~]# smbclient //192.168.122.43/storage/ -U agonzalez%Start123
Try "help" to get a list of possible commands.
smb: \> dir
       D    0 Sat Sep 10 21:17:56 2022
       D    0 Sat Sep 10 22:43:09 2022
       N    0 Sat Sep 10 21:17:56 2022  newfile
   11758760 blocks of size 1024. 5635424 blocks available
```

*图 10.12：命令 smbclient 的使用示例*

可以使用 **mount** 命令在 Linux 系统中挂载远程 *SMB* 资源。当类型为 **cifs**（或 **smb3**）时，**mount** 命令会将请求重定向到命令 `mount.cifs`。命令 `mount.cifs` 是名为 **cifs-utils** 的软件包的一部分。一些常用选项如下：

- **username (或 user)**：指定连接服务器使用的用户名。
- **password (或 pass)**：指定用户名对应的密码。
- **domain (或 dom 或 workgroup)**：指定用户的域（工作组）。
- **credentials (或 cred)**：指定包含用于向服务器认证的用户名和密码的文件。也可以指定域。
- **ro**：以只读方式挂载。
- **rw**：以读写方式挂载。
- **sec**：使用的安全模式；某些选项为 *krb5*、*krb5i*、*ntlm* 和 *ntlmv2*。
- **vers**：指定协议版本。

*图 10.13* 展示了挂载之前共享资源的示例，指定用户名和密码作为选项。命令 **mount** 的输出用于列出默认选项：

```text
[root@rhel ~]# mount -t cifs -o rw,username=agonzalez,password=Start123 \
> //192.168.122.43/storage/ /exported
[root@rhel ~]# mount |grep "/exported"
//192.168.122.43/storage/ on /exported type cifs (rw,relatime,vers=3.1.1,cache=strict,username=agonzalez,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.122.43,file_mode=0755,dir_mode=0755,soft,nounix,serverino,mapposix,rsize=4194304,wsize=4194304,bsize=1048576,echo_interval=60,actimeo=1)
```

*图 10.13：命令 mount 的使用示例*

建议使用选项 **credentials (或 cred)** 来指定一个受保护的文件，其中包含用户名和密码。该文件的一个示例如下：

```text
username=agonzalez
password=Start123
```

### FTP 服务器和客户端

**文件传输协议（FTP）** 是一种历史悠久的协议，最早于 1971 年发布。它主要用于向最终用户共享文件。如今，FTP 的流行度较低，主要用于公开分发软件。该

