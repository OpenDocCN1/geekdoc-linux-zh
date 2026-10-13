
`users::100:games`

`group::-2`

`test::500:test1,test2`

| 用户名 | 密码 |
| :--- | :--- |
| test1 | test1pass |
| test2 | test1pass |

此网络上不存在域名服务器（DNS）或 Windows 网络名称服务（WINS）服务器，所有 PC 都有当前的 hosts 和 lmhosts，可以正确识别网络中的所有主机。每台服务器都连接了一台打印机（两种情况下都是惠普 DeskJet 500），且两者都有针对特定命名用户的共享，以及针对用户组和匿名用户的共享。`LINUXSERVER` 的 `smb.conf` 文件见列表 6.2。

## 列表 6.2 来自 LINUXSERVER 的 smb.conf 文件。

```
# Global parameters

workgroup = SAMBABOOK

netbios name = LINUXSERVER

server string = Samba Server

security = USER

printers = BSD

[homes]

comment = Home Directories

path = %H

writeable = yes

valid users = %S

[printers]

comment = All Printers

path = /var/spool/samba

print ok = Yes

browseable = yes

[groupshare]

comment = Group Share

path = /home/group

writeable = yes

valid users = @test
```

`/home/group` 目录的权限为 `test` 组设置为 `rwx--`，这意味着该目录不是全局可读的，`test` 组的所有成员可以读取文件、列出目录内容、创建文件和目录并进入该共享中的其他目录。`/home/group` 目录包含以下文件结构：

```
/home/group
/test1work
/test2work
/jointwork
```
