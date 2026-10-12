
### 10.2.2. `testpar` 命令输出示例

`[root@RHEL4b]# testpar -v |`

```
Load smb config files from /etc/samba/smbd.conf

Processing section "[pub]"

Processing section "[global]"

Loaded services OK.

Server role: ROLE_STANDONE

Press enter to see dump of service definitions
```

```
[global]

dos charset = CP85
unix charset = UTF-8
display charset = LOCALE
workgroup = WORK

realm =
netbios name =
netbios scope =
server string = Samba 3.0.2
```

Samba 3.0.x 中的 `smb` 参数大约有 350 个默认值。在 Samba 3.5.x 中，这个数字增加到了近 400 个。

### 10.2.3. `testpar -s`

Samba 守护一直在检查 `smb.conf` 文件，因此保留此文件是一个良好的习惯。但记录你的 Samba 配置并显式设置具有默认值的选项也是一种良好的习惯。`testpar -s` 选项允许你同时完成这两点。它将输出尽可能小的配置，同时保留你的设置。其思想是将你的 Samba 配置放在另一个文件（如 `smb.conf`）中，并让 `testpar` 为你解析。下面显示了设置了 `workgroup` 为 `WORKGROUP` 的第一个 `smb.conf` 文件。

```
@root@RHEL4b samba)# cat smb.conf.full

[global]

workgroup = WORKGROUP

# is a demo of documented smb.conf

# These two lines are removed by testpar -s

server string = Public Server
```

接下来，我们使用 `-s` 选项执行并将标准输出重定向到真实的 `smb.conf` 文件。

```
@root@RHEL4b samba)# testpar -s smb.conf.full > smb.conf

Load smb config files from smb.conf.full

Processing section "[firstshare]"

Loaded services file OK.

[firstshare]

path = /srv/samba/public

[root@RHEL4b samba)# cat smb.conf

[global]

server string = Public Server

[firstshare]

path = /srv/samba/public

[root@RHEL4b samba)#
```

下面是最终结果。那两个注释和默认选项不再存在了。

## 10.3. /usr/bin/smbclient

### 10.3.1. `smbclient` 查看 Samba

通过 `smbclient`，你可以从 SMB 服务器浏览并共享信息。它将显示你所有的共享、工作组以及主浏览器（Master Browser）的名称。添加 `-N` 选项是为了避免输入空密码。`-L` 选项后跟着要检查的主机名称。

```
root@RHEL4b init.d# smbclient -NL rhel4b

Anonymous login successful

Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]
```

| Sharename | Type | Comment |
| --- | --- | --- |
| firstshare | Disk | |
| IPC$ | IPC | IPC Service (Public Test Server) |
| ADMIN$ | IPC | IPC Service (Public Test Server) |
| Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]| | |

| Server | Comment |
| ------ | ----- |
| RHEL4B | Public Test Server WINXP |
| ------ | ---- |
| Workgroup | Master |
| ------ | ---- |
| WORKGROUP | WINXP |

### 10.3.2. `smbclient` 匿名

下面的截图是 Microsoft Windows Server 2003 sp2 上的 `net view` 命令。它显示了 Red Enterprise Linux 5.3 和一台 Ubuntu 9.04 Samba 服务器（都使用了极简的 `smbd.conf`）是如何对附近的微软计算机可见的。

![](img/1d499a6177836f6f088a9e2a53e11a14_153_0.png)

### 10.3.3. `smbclient` 认证

下面的截图使用 `smbclient` 显示关于匿名 Samba 的信息。

```
root@RHEL4b smclient -L 127.0

Anonymous login successful

Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]
```

| Sharename | Type | Comment |
| --- | --- | --- |
| firstshare | Disk | |
| IPC$ | IPC | IPC Service (Public Test Server) |
| ADMIN$ | IPC | IPC Service (Public Test Server) |
| Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]| |

| Server | Comment |
| ------ | ----- |
| RHEL4B | Public Test Server WINXP |
| ------ | ---- |
| Workgroup | Master |
| ------ | ---- |
| WORKGROUP | WINXP |

### 10.3.4. `smbclient` 使用凭据

Windows xp 和 2003 不接受匿名访问（`NT_STATUS_DENIED`）。此示例显示了如何为 `smbclient` 提供凭据。

```
[paul@RHEL5] smbclient -L target -U administrator
```

| Sharename | Type | Comment |
| --- | --- | --- |
| C$ | Disk | Default share |

```
paul@laika:- $ smbtree

Password:

WORKGROUP

\W2000

\W2000\firstshare

\W2000\C$ Default share

\W2000\ADMIN$ Remote Admin

\W2000\IPC$ Remote IPC

PEGAS55

\WINXP

cli_rpc_pipe_open: nt_name_create failed on pipe \srvpc to machine WINXP.

Error was NT_STATUS_ACCESS_DENIED

RHEL4B Pegasus Domain Member Server

\RHEL4B\ADMIN$ IPC Service (Pegasus Domain Member Server)

\RHEL4B\IPC$ IPC Service (Pegasus Domain Member Server)

\RHEL4B\domainata Active Directory users only

HM2003

cli_rpc_pipe_open: nt_name_create failed on pipe \srvpc to machine HM2003.

Error was NT_STATUS_ACCESS_DENIED

paul@laika:- $
```

上一页幻灯片提供了为什么我们无法在 winxp 和 w2003 电脑上看到共享信息的有用原因。让我们在我们的 RHEL 服务器上尝试 `smbtree`，但这次使用管理员凭据（所有电脑上的凭据都是相同的）。

```
[paul@RHELab -]$ smbtree -Uadministrator%Stargatel

WORKGROUP

\W2000

PEG

\WINXP

\WINXP\C$ Default share
```
