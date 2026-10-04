
# HELP history

displays the command history

## 浏览 Windows 网络

与从 Windows 轻松浏览网络相比，使用 `smtree` 和 `smclient` 浏览 Windows 要笨得多；GNOME 提供了一个更易用的替代方案。在 Nautilus 中，在位置栏输入 `smb://` 即可浏览网络上的 Windows 共享。

Nautilus 使用虚拟文件系统插件，这些插件是桌面环境的一部分，而不是原生 Linux 系统的部分。因此，只有 GNOME 应用可以打开远程共享上的文件；普通的 Linux 程序则不能。例如，`edit` 可以打开远程共享上的文件，而 `OpenOffice`、`mplayer` 和 `xedit` 则不能。

## 挂载 Windows 共享

`mount` 工具（第 572 页）配合 `-t cifs` 选项可以将 Windows 共享挂载为类似于 Linux 目录层次结构。有关 CIFS 协议的更多信息请参阅第 1029 页。当你挂载 Windows 共享时，你可以向共享上的文件写入；你不能使用 `smbclient` 向共享上的文件写入。

挂载 Windows 共享的 `mount` 命令语法如下（你必须以 root 权限运行此命令）：

```
mount -t cifs //host/share dir
```

其中 `host` 是该系统的名称，`share` 是你想要挂载的 Windows 共享名称，`dir` 是你挂载共享的 Linux 目录的绝对路径（挂载点）。

以下命令在 root 权限下运行时，会将上例中的共享挂载到 `/share` 目录上：

```
$ sudo mount -t cifs //jam/d/share -o username=sam
Password:
$ ls /share
Linux RECYCLER audit laptop.data
PSFONTS Volume Information data oldfonts
```

你可以省略 `username` 参数并提供空密码来挂载来用户可见的共享。在使用类型为 `cifs` 的文件系统时，使用 `uid`、`file_mode` 和 `dir_mode` 选项来建立挂载文件的所有权和权限。

```
$ sudo mount -t cifs //jam/d/share -o username=sam,uid=sam,file_mode=0644,dir_mode=0755
```

权限必须以以 0 开头的八进制数表示。更多信息请参阅 `mount.cifs` man 页面。

## 故障排除

Samba 提供了两个可以帮助排除连接故障的工具：`testparm` 检查 `/etc/samba/smb.conf` 的语法并显示其内容；`smbstatus` 显示打开的 Samba 连接报告。

以下步骤可以帮助你在无法让 Samba 工作时缩小问题范围。

1. 重启 Samba 守护进程。确保输出的最后一行以 `OK` 结尾。

```
$ sudo /etc/init.d/samba restart         [ OK ]
  Stopping Samba daemons...                [ OK ]
  Starting Samba daemons...                [ OK ]
```

2. 运行 `testparm` 以确认 `smb.conf` 文件语法是否正确：

```
$ testparm
Load smb config files from /etc/samba/smb.conf
Processing section "[printers]"
Processing section "[print$]"
Processing section "[pr1$]"
Loaded services file OK.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions
```

若你遗漏了 `smb.conf` 中的某个关键字，将得到如下错误：

```
$ testparm
Load smb config files from /etc/samba/smb.conf
Unknown parameter: "workgroup"
```

3. 检查防火墙是否阻止了 Samba。

4. 使用 `ping`（第 375 页）确保 Samba 正常。

5. 在 Windows 提示符下，使用 `net view` 查看 Samba 共享。

6. 在 Windows 提示符下，使用 `net use` 挂载共享：

```
C:>net use
 \dog
```

7. 在 Windows 提示符下，尝试映射共享作为驱动器：

```
C:>map
```

8. 在 Samba 服务器上，使用 `-B` 选项查询服务器。

9. 从 Samba 服务器上，使用 `smclient -L` 参数生成服务器提供的共享列表：

```
$ smclient -L
Password: (do not enter a password)
Anonymous login successful
Domain=[MGS] OS=[Unix] Server=[3.24]
```
