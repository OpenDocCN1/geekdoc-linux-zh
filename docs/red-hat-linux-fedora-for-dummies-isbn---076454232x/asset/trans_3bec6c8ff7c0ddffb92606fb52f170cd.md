

## 第16章：创建基础Linux网络服务

![](img/8c094d1b36276212c03d10d898508a6e_240_0.png)

Samba最初由澳大利亚的Andrew Tridgell设计和编写。Samba迅速在全球范围内变得流行，以至于少数几人无法应付。因此，启动了Samba项目以处理这一现象。你可以在www.samba.org找到关于Samba的更多信息。

按照以下步骤来——嗯，安装、配置和使用——Samba：

- 1. **以root身份登录并插入本书随附的DVD-ROM。**

- 2. **打开一个终端仿真器窗口并输入以下命令：**

```
rpm -ivh /mnt/cdrom/RedHat/PPMS/samba-client*
```

Samba服务器由两个守护进程组成：smbd 和 nmbd。在任何人都能访问你的Samba服务器之前，你必须启动这两个守护进程。

- 3. **输入以下命令以启动守护进程：**

```
/etc/init.d/smb start
```

你可以通过用 stop 选项替换 start 选项来停止守护进程。你可以使用 restart 选项重启Samba服务器：

```
/etc/init.d/smb restart
```

- 4. **通过创建以下软链接使用 chkconfig 实用程序来自动化Samba守护进程的启动：**

以下命令告诉Linux在级别3（非图形界面）和级别5（运行图形X服务器）自动启动Samba；无论你的Linux计算机以图形模式还是非图形模式启动，Samba都会启动：

```
chkconfig --level 35 smb on
```

Samba默认配置为使用其自己的密码文件。你必须使用 mksmbpasswd.sh 脚本创建密码文件。

- 5. **使用 smbpasswd 程序创建Samba用户账户和密码。**

-a 选项告诉脚本将用户账户添加到 smbpaswd 文件：

```
smbpasswd -a paul
```

系统会提示你两次输入密码。

- 6. 这是终极测试：**运行以下命令来查看你的主目录（在本例中，它是Paul的主目录）：**

```
smbclient //localhost/paul -U paul
```

- 7. **输入你在第6步中输入的密码，你将获得访问Paul主目录的权限，其外观应类似于以下内容：**

```
added interface ip=192.168.1.1 bcast=192.168.1.255
                   nmask=255.255.255.0
Password:
Domain=[MYGROUP] OS=[Unix]  Server=[Samba 3.0]
smb: \>
```

- 8. **在** `smb: \>` **提示符下输入 help，你将看到所有可用的命令。**

例如，输入 **dir**，你将看到主目录中的所有文件。

- 9. **你可以在Linux计算机上挂载Samba文件系统。输入以下命令以将你登录的同一台计算机上的主目录 (/home/paul) 挂载起来：**

```
mount -t smbfs -o username=paul //localhost/paul /mnt
```

此示例不需要你有网络即可工作，并将你的主目录挂载在 /mnt 挂载点上。你可以通过指定远程机器名称来挂载另一台Linux计算机上的Samba共享。例如，如果你登录到计算机 Cancun，而Samba服务器运行在 Veracruz 上，请输入此行：

```
mount -t smbfs -o username=paul //veracruz/paul /mnt
```

你的主目录现在已挂载在 /mnt 目录上。这很好！现在你可以使用你的Linux计算机向网络上的其他部分提供文件和目录。

### 使用SWAT配置Samba

呼叫SWAT小组！（抱歉，这不得不这么写。）**SWAT** 是 Samba Web Administration Tool（Samba Web管理工具）的缩写，用于图形化配置Samba。SWAT帮助你配置Samba服务器的所有方面，还可以启动、停止并查看Samba的状态。

你必须配置 `inetd.d` 守护进程以启动SWAT。这些步骤展示了如何设置 `xinetd.d` 以运行SWAT：

- 1. 以root身份登录到你的Samba服务器并打开一个终端仿真器窗口（参见第4章）。

- 2. 插入随附的DVD-ROM并通过输入以下命令安装SWAT包：

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/samba-swat*
```

- 3. 编辑 `/etc/xinetd.d/swat` 文件并将最后一行从 `disable=yes` 更改为 `disable=no`。

- 4. 重启 xinetd.d。

```
/etc/init.d/xinetd restart
```

- 5. 在你的Samba服务器上启动Mozilla，并在URL窗口中输入此地址：

```
localhost:901
```

SWAT启动并提示你输入用户名和密码。SWAT通过 `/etc/xinetd.d/swat` 文件配置为使用root用户和密码。

- 6. 在 User Name 提示符下输入 root，在 Password 提示符下输入root用户的密码。

Mozilla显示SWAT配置系统，如图16-2所示。
你现在可以使用SWAT配置Samba的任何方面。这些步骤描述了如何使用Samba导出你的DVD-ROM/CD-ROM驱动器：
Samba默认配置为导出用户的主目录和它所在服务器上的打印机，因此基础部分已经涵盖。向你的局域网用户提供一个良好的Samba共享是你 DVD-ROM/CD-ROM 驱动器。

- 7. 点击 Shares 按钮。

Shares 窗口打开。

- 8. 在 Create Share 按钮旁边的文本框中输入 cdrom，然后点击 Create Share 按钮；单词 `cdrom` 是任意的但具有描述性。

新的 `cdrom` 共享的配置窗口打开。

- 9. 如图16-3所示，在 Path 文本框中输入 `/mnt/cdrom`。

可选地，你可以输入注释来描述你要导出的内容。

- 10. 点击 Commit Changes 按钮，新的共享将被保存到 `/etc/samba/smb.conf` 文件。

这些更改也会立即生效，因为每次向Samba服务器发出共享请求时，都会生成一个新的 `smbd` 守护进程。你现在可以从局域网上的任何机器（包括服务器）挂载这个新的Samba共享。

- 11. 创建一个新的目录来挂载Samba共享（名称是任意的）：
```
mkdir /samba
```

- 12. 重启 Samba 守护进程。
```
/etc/init.d/smb restart
```

- 13. 尝试通过从服务器输入以下命令来挂载共享：
```
mount -t smbfs -o username=paul //cancun/cdrom /samba
```

![](img/8c094d1b36276212c03d10d898508a6e_243_0.png)

**图 16-2：**
SWAT 配置系统。

![](img/8c094d1b36276212c03d10d898508a6e_244_0.png)

- 14. **输入你的密码，共享将被挂载在 /samba 目录上。**

请注意，当你将一个文件系统挂载到现有文件系统之上时，只有新挂载的文件系统可见。在这种情况下，你将CD-ROM挂载在 /mnt 上，这覆盖了初始的CD-ROM挂载。

### 构建打印服务器

Linux可以在不使用Samba的情况下向其他Linux（和Unix）计算机共享打印机；你可以选择Unix Style打印队列来创建Linux打印服务器。但是，Windows不懂Unix，而使用Samba使得所有Linux、Unix和Windows计算机都能使用Linux打印服务器。

为了让你的Linux计算机作为整个网络的打印服务器，你完成以下步骤：

- 1. **将打印机连接到Linux计算机。**
- 2. **配置Linux打印服务器以使用打印机。**
- 3. **配置Linux客户端通过服务器打印。**

以下各节描述了如何完成这些步骤，以便你私有网络上的每台计算机都可以通过你的Linux打印服务器进行打印。

#### 将打印机连接到你的Linux计算机

在创建打印服务器时，你可以选择两种类型的打印机：

- ✓ **网络打印机：** 可以直接连接到局域网的打印机是网络打印机。它们拥有自己的以太网（以及未来的无线）NIC。网络打印机分为那些可以充当自身打印服务器（也称为*打印暂存器*）的打印机和那些需要连接到打印服务器的打印机。

- ✓ **非网络打印机：** 传统打印机必须通过打印机（并行）端口或通用串行总线（USB）端口连接到计算机。

非网络打印机比网络打印机多，因为成本更低。传统打印机比网络打印机灵活性低，因为它们必须连接到计算机；而网络打印机可以放置在存在网络连接的任何地方。

本节描述如何使用非网络计算机，因为它们非常常见。过程很简单：你通过USB或并行端口将打印机连接到Linux打印服务器。连接后，可以配置Linux计算机将打印作业发送到打印机。

使用并行端口不需要配置Linux操作系统。然而，USB连接需要Linux加载USB内核模块（在Windows术语中本质上是驱动程序）。加载内核模块应该是自动的。但是，如果你遇到问题，你可以手动加载模块：

