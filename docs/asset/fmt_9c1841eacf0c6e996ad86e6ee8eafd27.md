
# Samba 安装与配置

## 9.3 安装 Samba

如果需要，应该更改 `PATH` 环境变量以包含二进制文件路径。
`samba` 必须手动启动，例如 `smbd -D`。

一些实用的 Samba 二进制文件有：

- `smbd` - SMB / CIFS 守护进程 [samba]
- `nmbd` - NetBIOS 服务器守护进程 [samba]
- `smbpasswd` - Samba 密码工具 [samba-common]
- `net` - 管理 Samba 的多用途工具 [samba-common]
- `smbclient` - 基于 Linux 的 Samba 客户端 [smbclient]
- `testparm` - 测试 Samba 配置文件是否正确 [samba-common]
- `nmblookup` - 将 NetBIOS 名称解析为 IP 地址 [samba-common]

假设 Linux 发行版提供了这些二进制文件，可以通过执行命令 `apt-get install samba smbclient samba-doc` 来完成。
我们也可以通过以下方式启动 samba：`/etc/init.d/samba start`

## 9.3.1 配置 Samba 服务器

主配置是 `smb.conf`。二进制文件期望在 `/etc/samba/smb.conf` 找到此文件。Samba 在 `/var/lib/samba/` 中维护配置，并在 `/var/cache/samba/` 中维护其他缓存配置。默认 Samba 日志 `log.smbd` 和 `log.nmb` 位于 `/var/log/samba/`。Samba 还必须维护一个名为 `smbpasswd` 的文件，存储有关 SMB 用户账户及其密码的信息。

有一个基于浏览器的工具 SWAT（Samba Web 管理工具），人们可以在网络上使用它连接并监控 Samba。从本地浏览器，可以通过输入启动它：`http://localhost:901`。

Debian 提供的 `smb.conf` 文件有六部分：

- `[global]` - 包含许多与网络相关的子部分，例如域/工作组名称、WINS、某些打印设置、验证、日志和计费等。
- `[homes]` - 用于共享用户主目录
- `[netlog]` - 默认被注释，用于将服务器配置为域控制器
- `[printers]` - 用于本地连接打印机的打印共享
- `[print$]` - 用于设置 Windows 打印机驱动程序的共享
- `[cdrom]` - 默认注释，用于可选共享服务器的 CD-ROM 驱动器

每个部分都有一组遵循以下格式的语句：

```
选项 = 值
```

这些语句通常是每个部分所特有的（即：必须将正确的设置放在正确的部分）。

### 全局配置最小选项

| 选项 | 类型 | 说明 |
| :--- | :--- | :--- |
| `workgroup` | M,s | Samba 服务器将加入的工作组或域 |
| `netbios name` | O,s | 服务器在网络上的显示名称 |
| `server string` | O,s | Samba 服务器的描述 |
| `security` | O,m | Samba 服务器将承担的角色——可以是 `user`（当启用域控制器时使用）、`share`（仅启用按共享层级的访问控制和身份验证）、`domain`（从域控制器或服务器获取身份验证信息） |
| `encrypt passwords` | M,b | 客户端发送的密码是否应该加密 |
| `passdb backend` | M,s | 使用什么类型的数据库来获取用户账户 |
| `printing` | O,m | 使用的打印系统 |
| `log level` | O,s | 日志信息的详细程度 |
| `preferred master` | M,b | 服务器是否将成为工作组的主浏览器？ |
| `local master` | M,b | `nmbd` 是否尝试成为工作组的本地主？ |
| `domain master` | M,b | 是否为主域控制器？ |
| `domain logons` | M,b | 是否启用域登录？ |
| `logon home` | M,s | 登录主共享的网络路径 |

### Samba 全局配置示例

```
[global]
workgroup = NRCFOSS
netbios name = laptop
server string = Samba Test Server
security = user
encrypt passwords = yes
passdb backend = smbpasswd;/etc/samba/samba
printing = cups
log level = 1
preferred master = yes
local master = yes
domain master = yes
domain logons = yes
logon home = \\laptop\homes
logon drive = x:
```

## 9.3.2 配置 Samba 共享

Samba 共享部分可用于编写导出 Linux 文件/目录并使其在其他机器上可用。基本的 Samba 共享选项有：

- `comment` - 共享内容的描述
- `path` - 被共享目录的绝对路径
- `read only` - 共享是只读还是读写
- `guest ok` - 是否允许未身份验证的用户查看共享
- `browseable` - 在“浏览”Samba 服务器时是否显示该共享
- `valid users` - 允许查看此共享的用户列表
- `force user` - 代替执行目录操作的用户
- `read list` - 对共享数据具有只读访问权限的用户；这通常与 `force user` 选项配合使用。如果给出了此选项，将使用基于文件系统的访问控制
- `write list` - 对共享数据具有完全写权限的用户

### Samba 共享示例

```
[mydata]
comment = MyData Share
path = /mydata
read only = no
guest ok = no
browseable = yes

[homes]
comment = %U 的主目录
path = /home/%U
read only = no
guest ok = no
browseable = no
force user = %U
```

### 另一个 Samba 共享示例

```
[test]
comment = Force User 的测试共享
path = /usr/local/test
read only = no
guest ok = yes
browseable = yes
force user = admin
read list = useroneertwo admin
write list = useroneerthree admin
valid users = useroneertwo userthree admin
```

## 9.3.4 管理 Samba 用户

Samba 只能根据存储在自身数据库中的密码对用户进行验证；它无法根据 Linux `passwd` 文件验证用户。然而，在 Linux 系统用户和 Samba 用户之间建立映射是必要的——对于每个 Samba 用户，都应该存在一个同名的有效系统用户；否则 Samba 将无法查找该用户。在最简单的情况下，Samba 可以将其账户存储在 `smbpasswd` 文件中。可以使用 `smbpasswd` 工具操作 `smbpasswd` 文件。

- 添加用户：`smbpasswd -a <username>`
- 更改用户密码：`smbpasswd <username>`
- 删除用户：`smbpasswd -x <username>`
- 输入 `smbpasswd` 查看帮助

## 9.3.3 Samba 客户端

要测试 Samba 身份验证和配置，运行 `smbclient`：

```
smbclient \\<machine>\\<share-name> -U<username>
```

### 从 Windows 测试 Samba

- 以本地用户登录
- 打开“网络邻居”并浏览整个网络
- 找到 Linux 机器上设置的感兴趣的“工作组”并点击它
- 在工作区域，选择机器并测试访问性
- 将提示密码，如果验证通过，将显示在 Samba 中定义的共享
- 在服务器上尝试一些操作，以验证访问控制是否正确

## 9.4 NFS 简介

NFS 是一种主要用于 Linux/Unix 世界的文件共享协议。对于用户或应用程序来说，NFS 是完全透明的——用户或应用程序访问磁盘或 NFS 文件的方式没有变化。NFS 通常在 UDP 上实现；它依赖 RPC 来执行大部分功能。

安装完成后，将出现以下消息：

```
nfs-server
```

`/etc/exports` 文件中有内容。如果该文件中没有行，NFS 服务器将不会启动。

`/etc/exports` 文件遵循格式：

```
/directory-to-share client(permissions,sync-type)
```

注意 `client` 与权限/同步值之间没有空格。可以使用以下方式指定 `client`：

- 可解析的主机名（即 `/etc/hosts` 文件中有 client 的记录，或使用 DNS 设置局域网服务器）
- client 的 IP 地址
- 网络或子网（带有子网掩码），指定网络上的所有 client
- 带有通配符 `*` 的内部域名，指定域内的所有计算机

在各种权限中，最常用的三个是：

- `ro` - 只读（如果没有指定则是默认值）
- `rw` - 读写
- `no_access` - 禁止访问

继承意味着如果授予了某个目录的权限，这些权限将“向下”传递到其所有子目录。如果需要授予目录权限，但不授予部分或所有子目录，则需要在 `/etc/exports` 文件中为每个子目录添加记录并指定 `no_access`。

同步类型可以是 `sync` 或 `async`。通常建议使用 `sync`，因为它经常刷新写入到磁盘。如果没有选择选项，当 NFS 服务器启动时将会有消息提示默认使用 `sync` 操作。如果 NFS 服务器启动时出现消息 `<hostname> no address`，通常意味着 `/etc/exports` 文件中指定的主机无法解析。

例如：

```
/export/docs 172.16.0.0/255.255.0.0(ro,sync)
```

这将为 172.16.0.0 网络上的所有用户提供对共享目录的只读访问。

## 9.5 NFS 配置与测试

如果网络上存在第二台 Linux 或 Unix 系统，可以使用它来测试 NFS。为此，需要在 Debian 服务器上执行以下操作：

- 按照如下内容编辑 `/etc/exports` 文件：
- 确保在 Debian 操作系统安装期间创建了一个用户账户。该用户的家目录即为要指定的共享目录。
- 为客户端输入另一个 Linux 或 Unix 系统的主机名。
- 指定 `rw`（读写）权限和 `sync`（同步）操作。
- 保存后退出编辑器。
- 如果必要，编辑 Debian 服务器上的 `/etc/hosts` 文件，使其包含第二台 Linux 或 Unix 系统的主机名和 IP 地址。
- 如果必要，按顺序输入以下命令启动 NFS 服务进程：

```
/etc/init.d/nfs-common start
/etc/init.d/nfs-kernel-server start
```

(`nfs-common` 脚本之所以这样命名，是因为它在 Linux 和 Unix 客户端及服务器上都会运行。)

- 进入第二台 Linux 或 Unix 系统，并尝试挂载 Debian 服务器上的共享目录。此操作步骤取决于第二个系统上的 Linux 发行版或 Unix 类型。如果第二个 Linux 或 Unix 发行版也是 Debian 系统，请执行以下操作：
- 确保 Debian 服务器（我们假设其名为 "sarge"）在第二个系统的 `/etc/hosts` 文件中
- 输入以下命令以启用客户端 NFS，创建本地“挂载点”，并将远程服务器的共享挂载到本地挂载点：

```
/etc/init.d/nfs-common start
mkdir /mnt/private
mount share:/home/bates /mnt/private
```

当然，必须将 `bates` 替换为操作系统安装期间在服务器上创建的用户账户名。
注意上述 `mount` 命令的语法：

```
server-name:/path-to-share-on-server /path-to-local-mount-point
```

结果，可以通过进入本地系统上的挂载点来访问服务器上的远程共享目录，例如：

```
cd /mnt/private
```

要卸载共享，可以使用如下所示的本地挂载点：

```
umount /mnt/private
```
