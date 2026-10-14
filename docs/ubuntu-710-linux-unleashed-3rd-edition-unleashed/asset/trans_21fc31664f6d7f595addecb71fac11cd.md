

## 使用 [homes] 节共享主目录

[homes] 节为各用户共享 Ubuntu 主目录。当用户的 Windows 计算机连接到保存主目录的 Linux 服务器时，该主目录会自动共享出去。使用默认配置的一个问题是，用户会看到所有配置文件（如 .profile 以及文件名中以句点开头的其他文件），而这些文件在通过 Linux 登录时通常不会看到。一种快速避免此问题的方法是在 [homes] 节中包含一个 path 选项。要使用此解决方案，每个需要 Samba 共享其主目录的用户都需要一个单独的“主目录”来充当其 Windows 主目录。

例如，这个伪主目录可以是 Ubuntu 系统上每个用户主目录中名为 share 的目录。在使用 SWAT 时，你可以通过为默认 homes 共享指定路径时使用 %u 选项来指定 path 选项（参见本章后面的“使用 SWAT 配置 Samba”一节）。完整的路径设置如下：

```
/home/%u/share
```

此设置指定每个用户目录下名为 share 的目录为共享的 Samba 目录。相应的手动 smb.conf 设置（用于提供单独的“主目录”）如下所示：

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

如果你有一个默认的 [homes] 节，该共享会以用户名形式出现在用户的“网上邻居”中。当用户连接时，Samba 会扫描 smb.conf 中现有的节，以查找该用户主目录的特定实例。如果没有找到，Samba 会在 /etc/passwd 中查找用户名。如果提供的用户名和密码正确，则 /etc/passwd 中列出的主目录会被共享为用户的 Windows 主目录。通常，[homes] 节如下所示（browseable = no 条目可防止其他用户浏览你的主目录，是一种良好的安全做法）：

```
[homes]
browseable = no
writable = yes
```

此示例共享主目录，并使其对用户可写。下面是如何为每个用户指定单独的 Windows 主目录：

```
[homes]
browseable = no
writable = yes
path = /path/to/windows/directories
```

## 通过编辑 [printers] 节共享打印机

[printers] 节的工作方式与 [homes] 节非常相似，但它定义的是在网络上使用的共享打印机。如果该节存在，用户就可以访问 Ubuntu /etc/printcap 文件中列出的任何打印机。

与 [homes] 节一样，当收到打印请求时，会扫描所有节以查找打印机。如果没有找到共享（只要仔细命名，除非你为特定打印机创建了节，否则不应找到），则会扫描 /etc/printcap 文件以查找打印机名称，然后使用该名称发送打印请求。

为了正常打印，你必须在 Ubuntu 计算机上正确设置打印服务。典型的 [printers] 节如下所示：

```
[printers]
comment = Ubuntu Printers
browseable = no
printable = yes
path = /var/spool/samba
```

/var/spool/samba 是专门为 Samba 打印设置的假脱机路径。

## 使用 testparm 命令测试 Samba

创建 /etc/smb.conf 文件后，你可以使用 testparm 命令检查其正确性。该命令会解析你的 /etc/smb.conf 文件并检查是否存在语法错误。如果没有发现错误，你的配置文件很可能会正常工作。但并不能保证文件中指定的服务一定能正常工作。它只是确保文件编写正确。

与所有配置文件一样，如果你要修改现有且可用的文件，最稳妥的做法是先将该可用文件复制到其他位置，然后再修改副本。之后，你可以使用 testparm 工具检查该文件。命令语法如下：

```
$ sudo testparm /path/to/smb.conf.back-up
Load smb config files from smb.conf.back-up
Processing section "[homes]"
Processing section "[printers]"
Loaded services file OK.
```

此输出表明 Samba 配置文件正确无误，并且只要所有服务在 Ubuntu 机器上正常运行，Samba 就应该正常工作。现在，将旧的 smb.conf 文件复制到新位置，把新文件放到原位置，然后使用命令 /etc/init.d/smb restart 重新启动 Samba。你新的或修改后的 Samba 配置现在应该已生效。

