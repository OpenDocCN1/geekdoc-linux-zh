
## Samba 配置文件示例

```
remote browse sync = 192.168.0.255

remote announce = 192.168.0.255/LNB SOFTWARE

name resolve order = 1lmhosts bcast

dns proxy = no

ununix password sync = no

[homes]

comment = Home Directories

browseable = no

writable = yes

[printers]

comment = All Printers

path = /var/spool/samba

browseable = no

guest ok = no

writable = no

printable = yes

[tmp]

comment = Temporary file space

path = /tmp

read only = no

public = yes

[public]

comment = Public Stuff

path = /home/public

browseable = yes

public = yes

guest ok = yes

writable = yes

printable = no

available = yes

guest only = no

user = naba
```

将用户从 `naba` 改为你的用户名。同时，确保配置文件中提到的所有目录都存在。例如，使用命令 `mkdir /home/public` 创建 `/home/public` 目录。

编辑 Samba 配置文件后，添加 `/etc/samba/smbusers` 文件。以下是我的系统中 `/etc/samba/smbusers` 文件的内容：

```
@Unix_name = SMB_name1 SMB_name2 ...

root = administrator admin

body = guest pcsmgbuest

adm = naba
```

修改 `/etc/samba/smb.conf` 文件后，输入以下命令来验证它是否加载了文件：

```
testparm
```

> 如果命令显示它已加载文件，那么你已经准备就绪了。

使用以下命令启动 SMB 服务：

```
service smb start
```

要在系统重启时自动启动 SMB 服务，请输入以下命令：

```
chkconfig --level 3
```

## 从 Windows 访问 Samba 服务器

你可以从一个 Windows 系统访问 Linux 上的 Samba 服务器。在 Windows 98 上双击“网络”图标。在 Windows XP 上，选择“开始 > 网络”，然后点击“计算机”。你应该能够通过双击图标查看共享文件夹。例如，你会看到 `tmp` 和 `public` 文件夹。你可以打开这些文件夹进行深入探索。![](img/3b3329dddbc9c0857ad4f2ef1c0db305_589.png)

## 使用 smclient 访问 Windows 资源

你可以使用 `smclient` 程序访问局域网 Windows 系统上的共享目录和打印机，并确保你的 Linux 服务器工作正常。一种快速方法是使用 `smclient -L` 命令查看资源列表。这是我在 Linux 服务器上运行 `smclient` 时得到的输出：

```
smclient -L LNB200

Password: (press Enter)

Anonymous login

Domain[LNB SOFTWARE] OS[Unix] Server[3.0.11]
```

| Sharename | Type | Comment |
|---|---|---|
| tmp | Disk | Temporary file space |
| public | Disk | Public Stuff |
| IPC$ | IPC | IPC Service (Samba Server) |
| ADMIN$ | IPC | IPC Service (Samba Server) |

Anonymous login
Domain[LNB SOFTWARE] OS[Unix] Server[3.0.11]

| Server | Comment |
|---|---|
| LNB200 | Samba-Samba Server |
| NABA-4400 | Workgroup |
| LNB SOFTWARE | Master |

`smclient -L` 的输出显示了局域网上其他 Windows 服务器的名称。如果你周围有其他服务器，可以使用 `smclient` 查看它们的服务。这是我在 Windows 98 上查看共享资源时得到的输出：

```
smclient //naba-dell-4400/access naba mypassword

Domain[NABA_DELL-4400] OS[Windows 5.1] Server=

smb: dir ~

DR 0 Min Dec 20 10:52:57 2004

DR 0 Min Dec 20 10:52:57 2004

Ashley D 0 Mar 7 02:07:28 2004

botball.ppt A 832000 Sun May 16 14:08:13 2014

desktop.ini ARC Tue 9 16:52:44 2004

DSC332.JPG A 379772 Fri Sep 17 23:00:52 2004

... D 0 Jan 6 19:54:54 2005

34153 blocks of size 2097152. 6130 blocks available
```

```
smb: > quit
```

要查看 `smclient` 命令列表，在提示符处输入 `help`。表 19-2 是常用 `smclient` 命令的要概述。为了熟悉 `smclient`，请尝试尽可能多的命令。

## 表 19-2：常用的 smclient 命令

| Command | Description |
| --- | --- |
| ! | 执行 shell 命令（记住你在 Linux 上运行 smclient） |
| ? cmd | 显示命令列表或特定命令的帮助 |
| cancel id | 取消由 ID 标识的打印作业 |
| cd dir | 切换目录 |
| del file | 删除文件 |
| dir file | 显示目录列表 |
| exit | 退出 Windows 服务器 |
| get rfile lfile | 将远程文件 (rfile) 复制到本地文件 (lfile) |
| help cmd | 提供命令帮助（或命令列表） |
| lcd newdir | 切换本地目录（在 Linux PC 上） |
| lowercase | 在执行 `get` 命令时切换文件名自动小写转换 |
| ls files | 列出服务器上的文件 |
| mask name | 对所有文件操作应用掩码（如 `*.`） |
| md dirname | 在服务器上创建目录 |

你可以不仅仅用 `smclient` 程序查看资源；还可以用它访问 Windows 服务器上的磁盘或将文件发送到 Windows 打印机。`smclient` 程序类似于 FTP——你连接到 Windows 服务器并使用命令提取发送文件到打印机。

以下示例显示了如何使用 `smclient` 访问你的 Windows PC 磁盘并查看其目录：

```
smclient //naba-dell-4400/access naba mypassword

Domain[NABA_DELL-4400] OS[Windows 5.1] Server=

smb: dir ~

DR 0 Min Dec 20 10:52:57 2004

DR 0 Min Dec 20 10:52:57 2004

Ashley D 0 Mar 7 02:07:28 2004

botball.ppt A 832000 Sun May 16 14:08:13 2014

desktop.ini ARC Tue 9 16:52:44 2004

DSC332.JPG A 379772 Fri Sep 17 23:00:52 2004

... D 0 Jan 6 19:54:54 2005
```

# 第三部分：Linux 网络化

| 表 19-2（续） |

| 命令 | 描述 |

| --- | --- |

| mget name | 获取具有匹配名称的文件（如 *.doc） |

| mkdir dirname | 创建目录 |

| mput name | 将文件从 Linux PC 复制到服务器 |

| newer file | 仅比指定文件更新的文件 |

| print name | 打印打印名称 |

| printmode mode | 设置打印模式（模式必须是文本或图形） |
