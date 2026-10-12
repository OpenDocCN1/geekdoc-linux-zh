
，并使用命令 `/etc/init.d/smb restart` 重启 Samba。您新建或修改的 Samba 配置现在应该已经生效。

## 启动 smbd 守护进程

既然您的 smb.conf 文件已正确配置，您就可以启动 Samba 服务器守护进程。可以使用 `/usr/sbin/smbd` 命令来完成此操作，该命令（不带选项）将以所有默认设置启动 Samba 服务器。在此命令中，您最常更改的选项是 smb.conf 文件的位置；如果您不想使用默认位置 `/etc/smb/smb.conf`，就需要更改此选项。`-s` 选项允许您更改 Samba 使用的 smb.conf 文件；该选项对于测试新的 smb.conf 文件是否确实有效也很有用。另一个有用的选项是 `-l` 选项，它指定 Samba 用于存储信息的日志文件。

要从命令行启动、停止或重启 Samba，请使用 service 命令；system-config-services 客户端；或者使用带有适当关键字（例如 start）的 `/etc/rc.d/init.d/smb` 脚本，如下所示：

```
# /etc/rc.d/init.d/smb start
```

## 使用 smbstatus 命令

smbstatus 命令报告当前 Samba 连接的状态。其语法为

```
/usr/bin/smbstatus [options]
```

部分可用选项如表 21.2 所示。

**表 21.2** smbstatus 选项

| 选项 | 结果 |
| :--- | :--- |
| -b | 简要输出。 |
| -d | 详细输出。 |
| -s /path/to/config | 如果启动时使用的配置文件不是标准文件，则使用此项。 |
| -u username | 显示特定用户连接的状态。 |
| -p | 列出当前的 smb 进程。这在脚本中可能很有用。 |

## 使用 smbclient 命令连接

smbclient 命令允许其他 Linux 主机上的用户访问您的 smb 共享。您无法在主机上挂载该共享，但可以像使用 FTP 客户端一样使用它。smbclient 命令可以使用多个选项。最常使用的是 `-I`，后跟您要连接的计算机的 IP 地址。smbclient 命令运行时不需要 root 权限：

```
smbclient -I 10.10.10.20 -U username%password
```

这将给出以下提示符：

```
smb: <current directory on share>
```

从这里开始，命令与标准的 Unix/Linux FTP 命令几乎完全相同。请注意，您可以在 smbclient 命令行中省略密码。此时系统会提示您输入 Samba 共享密码。

## 挂载 Samba 共享

有两种方法可以将 Samba 共享挂载到您的 Linux 主机。挂载共享与挂载可用的介质分区或远程 NFS 目录相同，不同之处在于 Samba 共享是通过 SMB 访问的。（参见第 37 章“管理文件系统”了解如何挂载分区。）第一种方法使用标准的 Linux mount 命令：

```
mount -t smbfs //10.10.10.20/homes /mount/point -o username=jkennedy,dmask=777,fmask=777
```

> **注意**  
> 如果您的名称服务正在运行，或者主机在 /etc/hosts 文件中，可以用主机名代替 IP 地址。

此命令将 jkennedy 的主目录挂载到您的主机上，并赋予所有用户对该挂载的完整权限。这些权限等同于 chmod 命令上的权限。

第二种方法使用 smbmount 命令产生相同的结果，如下所示：

```
# smbmount //10.10.10.20/homes /mount/point -o username=jkennedy,dmask=777,fmask=777
```

若要取消挂载共享，请使用标准的

```
# umount /mount/point
```

这些挂载命令也可用于将真正的 Windows 客户端共享挂载到您的 Fedora 主机。使用 Samba，您可以配置服务器以提供 Windows 可以提供的任何服务，而且除了您之外，没有人会知道这一点。

## 使用 SWAT 配置 Samba

Samba 开发团队通过 Samba Web Administration Tool (SWAT) 让管理 Samba 变得轻而易举。SWAT 是一个基于 Web 的配置和维护界面，它尽可能接近点对点的 Samba 环境。本节提供了一个简单的示例，说明如何使用 SWAT 设置对用户主目录的 SMB 访问以及如何共享目录。

在开始使用 SWAT 之前，您需要执行几个步骤。首先，确保已安装 Samba 和 samba-swat RPM 软件包。然后，通过编辑 `/etc/xinetd.d/swat` 文件来启用系统的 SWAT 访问权限，将以下行更改为：

```
disable = yes
```

将单词 yes 改为 no，如下所示：

```
disable = no
```

保存文件，然后使用 system-config-services 客户端或 `/etc/rc.d/init.d` 下的 xinetd shell 脚本重启 xinetd 守护进程，如下所示：

```
# /etc/rc.d/init.d/xinetd restart
```

接下来，启动一个 X 会话，启动 Mozilla Web 浏览器，并浏览到 `http://localhost:901` 统一资源定位符 (URL)。您将看到登录提示。输入 root 用户名和密码，然后单击 OK 按钮。屏幕会清除，您将看到 SWAT 主页，如图 21.2 所示。

> **提示**
>
> 您还可以使用 Red Hat 的 system-config-samba 客户端来配置 Samba。从 X 终端窗口的命令行启动该客户端，或选择“系统设置”、“Samba 服务器”菜单项（如图 21.9 稍后所示）。

## sample_database

## phonebook

| last_name | first_name | phone |
|---|---|---|
| Doe | John | 555-555-1212 |
| Doe | Jane | 555-555-1212 |
| Palmer | John | 555-123-4567 |
| Johnson | Richard | 555-111-4321 |

## cd_collection

| id | title | artist | year | rating |
|---|---|---|---|---|
| 1 | Mind Bomb | The The | 1989 | 4 |
| 2 | For All You've Done | Hillsong | 2004 | |
| 3 | Trouser Jazz | Mr Scuff | 2002 | 5 |
| 4 | Natural Elements | Acoustic Alchemy | 1988 | 3 |
| 5 | Combat Rock | The Clash | 1982 | 4 |
| 6 | Life for Rent | Dida | 2003 | |
| 7 | Aidermus 4 | Karl Jenkins | 2000 | 5 |
| 8 | The Two Towers | Howard Shore | 2002 | 5 |

![](img/774d40fd20903495c5cd00e2efad3f33_629_0.png)

首先，单击 SWAT 主页上的 GLOBALS 图标。您将看到一个与图 21.3 中显示的类似的页面。窗口中有很多选项，但您只需在安全选项部分的 Hosts Allow 字段中输入一个或多个 IP 地址或子网地址（例如 `192.168.2.` — 请注意末尾的句点，这允许所有主机访问；在此示例中，是在 `192.168.2` 子网上），就可以快速为来自您局域网 (LAN) 的主机设置访问权限。如果您需要有关如何格式化条目的帮助，请单击字段左侧的 Help 链接。此时将出现一个新网页，显示相关信息。

完成后，单击 Commit Changes 按钮以保存全局访问设置。下一步是创建一个 Samba 用户并设置该用户的密码。单击主 SWAT 页面上的 PASSWORD 图标（参见图 21.2）。此时将打开服务器密码管理页面，如图 21.4 所示。在 User Name 字段中输入新的用户名；然后在 New Password 和 Re-type New Password 字段中输入密码。

> **注意**
> 您需要提供一个现有系统用户的用户名，但用于 Samba 访问的密码无需与现有用户的密码匹配。

完成后，单击 Add New User 按钮。SWAT 随后创建用户名和密码，并显示已添加用户 *username*（其中 *username* 是您输入的名称）。如果 Samba (smb) 服务器正在运行，新的 Samba 用户现在应该能够从任何允许的主机访问主目录。

![](img/774d40fd20903495c5cd00e2efad3f33_630_0.png)

**图 21.3** 配置 Samba 以允许从您局域网中的特定主机或子网访问。

![](img/774d40fd20903495c5cd00e2efad3f33_631_0.png)

**图 21.4** 在 SWAT 密码页面中输入 Samba 用户名和密码。

例如，如果您在一台名为 shuttle2 的主机上设置了 Samba，该主机上有一个名为 spice 的用户，则该用户可以从任何远程主机（如果 GLOBALS 设置允许）访问 shuttle2 上的主目录，或许可以使用 smbclient 命令，如下所示：

```
$ smbclient //shuttle2/spice -U spice
added interface ip=192.168.2.68 bcast=192.168.2.255 nmask=255.255.255.0
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.5]
smb: \> pwd
Current directory is \\shuttle2\spice\
smb: \> quit
```

单击 Status 图标（如图 21.2 或 21.4 所示）以查看 Samba 状态，或启动、停止或重启服务器。您可以使用生成的网页上的各种按钮来控制服务器并查看定期或连续的状态更新。

您还可以使用 SWAT 共享 Linux 目录。首先，单击主 Samba 页面顶部工具栏中的 Shares 图标（参见图 21.2）。在 Create Shares 字段中输入共享名称，然后单击 Create Shares 按钮。SWAT 页面将在对话框中显示详细的配置信息，如图 21.5 所示，为新 Samba 共享提供详细的配置访问权限。

