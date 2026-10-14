

```
public = no
read only = yes
printable = yes
```

本节定义了一个打印机共享，只有用户ID为 frank、melanie 和 nick 的用户才能从网络访问。因为 printable 参数已启用，所以他们无需对 /home/frank/spool 目录具有写权限即可从共享打印机打印。

## 创建 Samba 服务器

现在你已经了解了 smb.conf 配置文件的不同部分，让我们尝试在网络上搭建一个可用的服务器。要使 Samba 服务器准备就绪，需要做三件事：

- ♦ 编辑 smb.conf 配置文件。
- ♦ 将 Samba 用户密码添加到系统中。
- ♦ 重启 Samba 软件。

以下各节将逐步介绍这些过程。

## 编辑 smb.conf 文件

你首先需要为网络配置 Samba 服务器。按照以下步骤启动服务器：

- 1. 在文本编辑器中打开 smb.conf 文件。如果你使用的是控制台上的 Ubuntu 服务器安装，则需要使用命令行编辑器，例如 vim。你可以使用命令 sudo vim /etc/samba/smb.conf 用 vim 编辑器打开文件
- 2. 将 workgroup 设置为现有工作组或新工作组。workgroup 行定义要加入的 Windows 网络工作组：workgroup = WORKGROUP
- 如果你在现有的 Windows 网络上使用 Ubuntu 服务器，在此处输入工作组名称可使服务器出现在网络邻居浏览列表中，以便客户端无需知道其名称即可连接。
- 3. 删除 interfaces 行的注释以启用来自其他网络设备的连接。默认设置应为 interfaces 127.0.0.1/8 eth0
- 在命令行使用 ifconfig 命令确保定义的以太网端口（eth0）也在服务器上处于活动状态。
- 4. 删除 security 行的注释以启用用户级安全性。这允许你将 Samba 服务器作为网络上的独立服务器运行，并在 Ubuntu 服务器上管理自己的用户帐户。
- 5. 删除 [homes] 部分的注释。[homes] 部分使用了三行：[homes] comment = Home Directories browseable = no

如果你想允许用户浏览到其主文件夹，请将 browseable 设置更改为 yes。

- 6. 删除 read only 行的注释，并将设置更改为 no。这允许你的用户向其主文件夹写入文件：
```
read only = no
```

- 7. 删除 valid users 行的注释。此设置限制用户只能连接到自己的主文件夹：
```
valid users = %S
```

- 8. 删除 CUPS 服务器条目的 printing 和 printcap name 行的注释。这使你的 Samba 服务器能够共享在 CUPS 服务器中定义的任何打印机：
```
printing = cups
printcap name = cups
```

- 9. 保存新的 smb.conf 文件并退出编辑器。

现在 Samba 服务器配置已为你的网络环境设置好。下一步是为你的用户创建 Samba 帐户密码。

## 定义 Samba 密码

Ubuntu 中默认的 Samba 配置使用 Ubuntu 用户帐户系统来跟踪 Samba 配置中的用户。但是，此设置存在一个问题。当用户尝试使用其 userID 连接到 Samba 服务器时，Windows 服务器和客户端会使用加密方案传递密码。Samba 必须知道加密后的密码才能验证用户登录请求。

为此，Samba 软件维护了一个单独的密码文件，其中包含由 Windows 加密算法加密的用户密码。你必须将 Samba 用户密码与 Ubuntu 密码分开设置才能使其工作。

用于加密 Samba 密码的工具称为 smbpasswd。你必须使用 smbpasswd 程序为将要访问 Samba 服务器的每个 Ubuntu 用户帐户定义密码。要首次定义用户帐户密码，必须使用 -a 参数：

```
rich@testbox:~$ sudo smbpasswd -a test
New SMB password:
Retype new SMB password:
Added user test.
rich@testbox:~$
```

这为新用户帐户创建了 Samba 密码。如果需要更改帐户密码，则不需要 -a 参数：

```
rich@testbox:~$ sudo smbpasswd test
New SMB password:
Retype new SMB password:
rich@testbox:~$
```

你需要为所有希望通过网络作为 Windows 共享驱动器连接到其主文件夹的 Ubuntu 用户执行此操作。

