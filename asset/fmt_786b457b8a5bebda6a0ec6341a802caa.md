
```
# This is an automounter map and it has the following format
# key [ -mount-options-separated-by-comma ] location
# Details may be found in autofs(5) manpage
cd                 -fstype=iso9660,ro,nosuid,nodev :/dev/cdrom
# The following entries are samples to pique your imagination
#linux             -ro,soft,intr              ftp.example.org:/pub/linux
#boot              -fstype=ext2              :/dev/hda1
#floppy            -fstype=auto              :/dev/fd0
#1floppy           -fstype=ext2              :/dev/fd0
#e2floppy          -fstype=ext2              :/dev/fd0
#jaz               -fstype=ext2              :/dev/sdc1
#removable         -fstype=ext2              :/dev/hdd
```

要启动 `autofs`，以 `root` 身份在终端窗口中输入 `rcautofs start` 命令；`rcautofs status` 列出已配置和活动的挂载点，如以下示例所示：

```
da10:~ # rcautofs status
Checking for service autofs:
running
Configured Mount Points:
------------------------
/usr/sbin/automount /misc file /etc/auto.misc

Active Mount Points:
--------------------
/usr/sbin/automount /misc file /etc/auto.misc
```

使用之前的配置，`automounter` 在启动时会创建 `/misc` 目录。起初该目录为空，但如果你输入 `ls /misc/cd`，你会看到 CD-ROM 驱动器的内容，因为它已自动挂载：

```
da4:~ # ls /misc
da4:~ # ls /misc/cd
ARCHIVES.gz content.key COPYRIGHT.de
...
da4:~ # ls /misc
cd
da4:~ #
```

一段时间后（默认为五分钟），`/misc/cd` 会自动卸载，`/misc` 又看起来为空。

`automounter` 也可以用于主目录。相应的 `/etc/auto.home` 可能如下所示（由于 NFS 是默认值，在这种情况下包含它并不是真正必要的）：

```
tux      -fstype=nfs   da2:/home/tux
geeko    -fstype=nfs   da3:/home/geeko
```

当 `tux` 现在登录时，他在 `da2` 上的主目录 `/home/tux` 会挂载到此机器上的 `/home`。当 `geeko` 登录时，他的主目录会从 `da3` 挂载。

为了避免为每个用户输入一行，`automounter` 也支持通配符，如以下示例所示：

```
*   -fstype=nfs   da2:/home/&
```

当有人尝试访问 `automounter` 运行的计算机上的 `/home/whatever` 时，`automounter` 将尝试从 `da2` 将 `/home/whatever` 挂载到 `/home`。

当与集中式用户管理（如 NIS 或 LDAP）结合使用时，使用 `automounter` 非常有用。

## OpenLDAP 和 Automounter

`automounter` 通常从 `/etc/auto.master` 文件及其引用的文件读取信息。然而，当需要对许多客户端进行更改时，使用客户端上的文件很麻烦，因为所有客户端上的文件都必须修改。

如果信息保存在 LDAP 目录中，则信息只需在一个地方更新。客户端在下次连接目录时（例如用户在桌面上登录时）会获得新信息。

当在 YaST LDAP 客户端对话框（图 13-3）中选择 Start Automounter 时，`/etc/nsswitch.conf` 文件会被更改，以便以 `automount` 开头的行看起来如下：

```
...
automount: files nis ldap
...
```

这意味着 `automount` 信息按以下顺序搜索：首先检查文件（`/etc/auto.*`）中的 `autofs` 配置，然后检查 NIS，最后检查 LDAP。为了避免可能的混淆，你应该删除任何 `/etc/auto.*` 文件，因为它们可能与 LDAP 目录中存储的配置冲突。

`automounter` 查询 LDAP 目录以获取 `automount` 信息。所需模式文件已包含在 SUSE Linux Enterprise Server 10 上使用的 OpenLDAP 服务器包中。`automount` 信息包含在 SUSE Linux Enterprise Server 10 上的 `/etc/openldap/schema/rfc2307bis.schema` 文件中。

原本在 `/etc/auto.*` 文件中可用的信息现在必须存在于 LDAP 目录中。在下面的示例 LDIF 文件中，创建了一个 Services 组织单元来保存 `automounter` 所需的信息：

```
# Organizational Unit "Services"
dn: ou=Services,dc=digitalairlines,dc=com
objectclass: top
objectclass: organizationalUnit
ou: Services
```

然后可以使用以下 LDIF 文件创建 `auto.master` 和 `auto.home` 的条目：

```
# auto.master
dn: nisMapName=auto.master,ou=Services,dc=digitalairlines,dc=com
objectClass: top
objectClass: nisMap
nismapname: auto.master

dn: cn=/home,nisMapName=auto.master,ou=Services,
dc=digitalairlines,dc=com
nismapname: auto.master
objectclass: top
objectclass: nisObject
nismapentry: ldap:10.0.0.254:nismapname=auto.home,ou=Services,
dc=digitalairlines,dc=com
cn: /home

# auto.home
dn: nisMapName=auto.home,ou=Services,dc=digitalairlines,dc=com
objectclass: top
objectclass: nisMap
nismapname: auto.home

dn: cn=/,nisMapName=auto.home,ou=Services,
dc=digitalairlines,dc=com
objectclass: nisObject
cn: /
nismapentry: 10.0.0.254:/home/&
nismapname: auto.home
```

假设上述 LDIF 信息包含在 `/root/automount.ldif` 文件中，可以使用以下命令将文件中的信息添加到 LDAP 目录：

```
da4:~ # ldapadd -x -D "cn=Administrator,dc=digitalairlines,dc=com" -W -f /root/automount.ldif -c
```

在输入 LDAP 目录的 `root` 密码后，信息将被添加到目录中。

![](img/9129877170834ca9d5fdac5319bf5f12_487_0.png)

## 练习 13-2：将 SLED 10 集成到 LDAP 环境中

在本练习中，你将把 SUSE Linux Enterprise Desktop 10 集成到 LDAP 环境中进行身份验证并激活 `automounter`。

### 完成本练习的详细步骤

要将 SUSE Linux Enterprise Desktop 10 集成到 LDAP 环境中，请执行以下操作：

+   1. 启动 YaST 并选择 Network Services > LDAP Client。

+   2. 在 LDAP 客户端配置对话框中，选择或输入以下内容：

+      - *用户身份验证*—Use LDAP
