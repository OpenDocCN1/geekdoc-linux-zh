
- 更改用户对目录所拥有的权限
- 限制目录在一天中的可访问时间段

可能性几乎是无限的。各个部分中设置的任何参数都会覆盖 [global] 部分中设置的参数。以下内容为 [programs] 部分添加了一些限制：

```
[programs]
path = /usr/local/programs
writeable = true
valid users = ahudson
browseable = yes
create mode = 0700
```

valid users 条目将用户 ID 限制为仅限 ahudson。由于存在 browseable = yes 条目，所有其他用户都可以浏览该目录，但只有 ahudson 可以写入该目录。ahudson 在该目录中创建的任何文件都会赋予 ahudson 完全权限，但其他任何人都无法访问该文件。这与使用 chmod 命令设置权限完全相同。同样，选项非常多，因此在创建各个部分时，你可以尽情发挥创造力。

## 使用 [global] 部分设置全局 Samba 行为

[global] 部分设置了一些参数，用于为所有 Samba 建立配置设置。如果某个参数没有在其他部分中专门设置，Samba 将使用 [global] 部分中的默认设置。[global] 部分还设置 Samba 的常规安全配置。[global] 部分是唯一不需要方括号名称的部分。

Samba 会假定在第一个未标记为 [global] 的方括号部分之前的所有内容都属于全局配置。（在 /etc/samba/smb.conf 中使用方括号标题可以使配置文件更易读。）接下来的部分将讨论用于共享目录和打印机的常见 Samba 设置。然后你会看到如何测试 Samba 配置。

## 使用 [homes] 部分共享主目录

（请参阅本章后面的“使用 SWAT 配置 Samba”一节）。完整的路径设置如下：

```
/home/%u/share
```

此设置指定每个用户目录下名为 share 的目录是共享的 Samba 目录。相应的手动 smb.conf 设置（用于提供单独的“主目录”）如下所示：

```
[homes]
    comment = Home Directories
    path = /home/%u/share
    valid users = %S
    read only = No
    create mask = 0664
    directory mask = 0775
    browseable = No
```

如果你有一个默认的 [homes] 部分，该共享在用户的网上邻居中会以该用户的名字显示。当用户连接时，Samba 会扫描 smb.conf 中现有的各个部分，查找用户主目录的特定实例。如果没有找到，Samba 会在 /etc/passwd 中查找用户名。如果提供了正确的用户名和密码，/etc/passwd 中列出的主目录就会作为该用户的主目录共享出来。通常，[homes] 部分如下所示（browseable = no 条目可防止其他用户浏览你的主目录，是一种良好的安全实践）：

```
[homes]
browseable = no
writable = yes
```

此示例共享了主目录，并使其对用户可写。下面是为每个用户指定单独的 Windows 主目录的方法：

```
[homes]
browseable = no
writable = yes
path = /path/to/windows/directories
```

## 通过编辑 [printers] 部分共享打印机

[printers] 部分的工作方式与 [homes] 部分非常相似，但它定义的是供网络上使用的共享打印机。如果该部分存在，用户就可以访问 Ubuntu /etc/printcap 文件中列出的任何打印机。

与 [homes] 部分一样，当收到打印请求时，会扫描所有部分以查找打印机。如果没有找到共享（只要命名谨慎，除非你为特定打印机创建了部分，否则不应该找到），则会扫描 /etc/printcap 文件以获取打印机名称，随后使用该名称发送打印请求。

为了正常进行打印，你必须在 Ubuntu 计算机上正确设置打印服务。一个典型的 [printers] 部分如下所示：

```
[printers]
comment = Ubuntu Printers
browseable = no
printable = yes
path = /var/spool/samba
```

/var/spool/samba 是仅用于 Samba 打印而设置的假脱机路径。

## 使用 testparm 命令测试 Samba

创建好 /etc/samba/smb.conf 文件后，你可以使用 testparm 命令检查其正确性。该命令会解析你的 /etc/samba/smb.conf 文件并检查是否存在语法错误。如果没有发现错误，你的配置文件很可能会正常工作。但该命令并不保证文件中指定的服务一定有效。它只是确保文件编写正确。

与所有配置文件一样，如果要在现有可用的文件上修改，最稳妥的做法是先将可用的文件复制到另一个位置，再修改那个副本。然后，你可以使用 testparm 实用程序检查该文件。命令语法如下：

```
# testparm /path/to/smb.conf.back-up
Load smb config files from smb.conf.back-up
Processing section "[homes]"
Processing section "[printers]"
Loaded services file OK.
```

该输出表明 Samba 配置文件正确，并且只要你的 Ubuntu 机器上所有服务都正常运行，Samba 就应该能正常工作。现在，将旧的 smb.conf 文件复制到一个新位置，将新文件放到原位置，然后使用 /etc/init.d/samba restart 命令重启 Samba。你的新配置或修改后的 Samba 配置现在应该已经生效。

## 启动 smbd 守护进程

既然 smb.conf 文件已正确配置，现在可以启动 Samba 服务器守护进程。这可以通过 /usr/sbin/smbd 命令完成，该命令（不带选项）会使用所有默认设置启动 Samba 服务器。在此命令中，你最常更改的选项是 smb.conf 文件的位置；如果你不想使用默认位置 /etc/samba/smb.conf，可以更改此选项。-s 选项允许你更改 Samba 使用的 smb.conf 文件；此选项也可用于测试新的 smb.conf 文件是否确实有效。另一个有用的选项是 -l 选项，它指定 Samba 用于存储信息的日志文件。

要从命令行启动、停止或重启 Samba，请使用 /etc/init.d/samba 脚本并附上相应的关键字，例如 start，如下所示：

```
$ sudo /etc/init.d/samba start
```

