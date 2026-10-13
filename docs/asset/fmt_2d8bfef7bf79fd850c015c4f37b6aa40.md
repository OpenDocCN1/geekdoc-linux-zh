
例如，假设我的 NFS 服务器名为 `terry.muhlenberg`，导出的目录是 `/musicfiles`，我想将导出的目录挂载到文件系统的 `/mnt/temp` 下。我会使用任何文本编辑器在 `/etc/fstab` 文件的最后一行添加以下内容：

```
terry.muhlenberg.edu:/musicfiles /mnt/temp rsize=8192,wsize=8192
```

前一个示例中的选项指定了以字节为单位的读写大小。默认值为 1024 字节，但将大小增加到 8192 会极大提高系统性能。在挂载 NFS 共享指定的许多选项中，这两个是最常见的。你可以通过阅读 `nfs` 手页查看可用选项的完整列表，你可以在终端提示符下输入以下命令访问：

```
mount nfs
```

# 使用 Samba 连接到 Windows PC

## 本章内容

- 安装 Samba
- 配置 Samba
- 创建 Samba 用户
- 启动 Samba 服务器
- 连接到 Samba 服务器
- 连接到 Samba 客户端

通过使用 Samba 程序，你可以模拟 Windows 文件共享协议，并将你的 Red Hat 网络连接到 Windows 网络以共享文件和打印机。在本章中，我将展示如何安装和配置 Samba 以将 Red Hat Linux 网络连接到微软网络。

在本章中，我们将 Red Hat Enterprise Linux PC 称为 Samba 服务器，将 Windows PC 称为 Samba 客户端。

## 安装 Samba

在使用 Samba 连接到 Windows 计算机之前，必须先在 Linux PC 上安装它。所有当前版本的 Red Hat Enterprise Linux 都包含 Samba，但在系统安装期间可能尚未安装。即使已经安装，你也应该始终检查最新版本，以了解最新发布是否修复了某些问题，并在必要时进行安装。要查看系统是否安装了 Samba，请在终端窗口输入以下内容：

```
rpm -q samba
```

如果未安装 Samba，命令将返回说明 Samba 未安装的输出。如果已安装 Samba，`rpm` 查询将返回系统中安装的 Samba 版本。最新版本的 Samba（截至编写本文时为 3.0）可以在 Samba 网站（www.samba.org）获取。要安装 Samba，请按照以下步骤操作：

1. 下载 `samba-3.0.tar.gz` 文件。
2. 使用以下命令提取文件：`tar -xf samba-3.0.tar.gz`。
3. 进入提取出的文件目录（通常为 src），然后输入 `./configure`。
4. 按回车并等待命令提示符出现。
5. 在命令提示符下输入 `make`。
6. 在命令提示符下输入 `make install`。

## 配置 Samba

在使用 Samba 连接你的 Windows PC 之前，必须对其进行配置。可用于配置 Samba 的图形界面程序只是在后台更改配置文件的前端。直接编辑配置文件要快且简单得多。Samba 配置文件位于 `/etc/samba` 目录，分为若干部分，称为“共享”（shares），我在列表 9-1 中以括号标题的形式显示这些名称。列表 9-1 显示我在学校使用的一台计算机的 `sm.conf` 文件。

### 第 9 章：使用 Samba 连接到 Windows PC

### 列表 9-1：Samba 配置

```
# 这是主 Samba 配置文件。你应该阅读 smb.conf(5) 手页以理解此处列出的选项。
# Samba 拥有大量的配置选项（可能太多了！）本示例中未显示大部分。
# 任何以 :（冒号）或 #（井号）开头的行都是注释并会被忽略。在本示例中，
# 使用 # 作为注释，使用 : 作为可能启用的配置部分。
# 注意：每当你修改此文件时，都应该运行 "testparm" 命令
# 以检查是否存在任何语法错误。
#============================= 全局设置 =
[global]
log file = /var/log/samba/sm.log
smb password file = /etc/smpasswd
load printers = yes
passwd chat = *NewPassword* *n*Retype*new*password* *n
*password:*H)authentication*tokens*updated*successfully*
socket options = TCP_NODAY SO_RCVBUF=8192 SO_SNDBUF=8192
obey path restrictions = yes
encrypt password = yes
passwd program = /usr/bin/passwd %u
dns proxy = no
netbios = rhl
writeable = yes
server string = Samba Server
printing = lprng
path = /
default = homes
unix password sync = Yes
workgroup = Tardis
printcap name = /etc/printcap
security = user
max log size = 50
pam password change = yes
[homes]
comment = Home Directories
browse = yes
writeable = yes
create mode = 0664
directory mode = 0775
max connections = 1
[printers]
browable = yes
printable = yes
path = /var/spool/samba
comment = All Printers
```

### 全局 (Global)

`smb.conf` 文件的第一部分是全局部分。全局部分包含适用于整个服务器的设置，以及可以应用于其他共享的默认设置。全局部分包含按如下格式的选项和值列表：

```
option = value
```
