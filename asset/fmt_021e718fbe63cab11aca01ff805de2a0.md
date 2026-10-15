
`[homes]` 部分用于指定如何向 Windows 网络共享用户的家目录。如果没有此部分，用户的家目录需要单独进行共享，正如你稍后看到的。

考虑来自 `smb.conf` 文件中的以下 `[homes]` 部分：

```
comment = Home Directories
browseable = yes
read only = no
preserve case = yes
```

（注：此处根据示例逻辑保持结构完整）

正如后文所示，考虑以下的 `[homes]` 部分：

```
comment = Home Directories
browseable = yes
read only = no
preserve case = yes
create mode = 0750
```

`[homes]` 部分用于指定如何将用户的家目录共享到 Windows 网络。如果没有此部分，用户的家目录需要单独进行共享，正如你稍后看到的。

考虑 `smb.conf` 文件中的以下 `[homes]` 部分：

```
comment = Home Directories
browseable = yes
read only = no
preserve case = yes
```

（注：此处根据示例逻辑保持结构完整）

正如后文所示，考虑以下 `[homes]` 部分：

```
comment = Home Directories
browseable = yes
read only = no
preserve case = yes
create mode = 0750
```

`[homes]` 部分用于指定如何将家目录共享到 Windows 网络。

- `comment = Home Directories`：提供关于该部分的信息，但不影响其操作。
- `browseable = yes`：确保有权限的用户可以浏览该目录。
- `read only = no`：设置为只读。
- `preserve case = yes`：确保大小写敏感。
- `create mode = 0750`：指定打印时创建的文件的权限。

## [printers] 部分

由于 `[homes]` 部分用于共享用户的家目录，`[printers]` 部分用于将所有打印机共享到 Windows 网络。

表 29.1：常用的 [printers] 部分

| 参数 | 描述 |
| :--- | :--- |
| comment | 提供关于该部分的信息，但不影响其操作。 |
| path | 指定池路径；你可能需要创建自己的池目录。 |
| browseable | 与家目录一样，将此参数设置为 `no` 可确保只有权限的用户可以浏览。 |
| printable | 这应设置为 `yes`，否则无法打印。 |
| public | 如果设置为 `yes`，访客账户就可以打印；在许多网络中，将其设置为 `no` 以防止访客过度打印。 |
| writable | 打印机是不可写的，因此此参数应设置为 `no`。 |
| create mode | 指定打印期间创建的文件的权限；这通常设置为 `0700`。 |

将这些参数结合，可以创建一个相当常见的 `[printers]` 部分，如下例所示 Red Hat 默认设置：

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
printable = yes
public = no
writable = no
create mode = 0700
```

从 Windows 访问 Linux 打印机的方法与目录相同。共享名称是 `printcap` 文件中的 Linux 打印机名称。例如，要访问 smbserv 上的打印机路径，Windows 用户访问 `\\smbserv\printername`。

## 共享公共访问的目录

有时需要创建一个所有用户都可以访问且只读的公共访问目录。该目录可以设置为集中共享信息，防止用户更改信息。

考虑以下条目：

```
[public]
path = /public/directory
public = yes
read only = yes
printable = no
```

此条目创建一个名为 `public` 的共享名称，所有用户都可以访问（因此 `public = yes`），但它是只读的（因此 `read only = yes`）。

考虑另一个示例：将 `/tmp` 设置为所有用户均可读写的公共访问临时目录。可以通过以下条目实现：

```
[tmp]
path = /tmp
read only = no
public = yes
```

# 共享私有访问目录

除了共享供公共访问的目录外，有时也有必要创建一个仅供少数用户访问的共享目录。

假设你想将目录 `/private/directory` 共享为共享名称 `private`。同样，假设该目录仅供三个用户访问：`user1`、`user2` 和 `user3`。可以通过类似下面的条目来实现：

```
[private]
path = /private/directory
valid users = user1 user2 user3
public = no
writable = yes
printable = no
create mask = 0765
```

注意使用新参数：`valid users`。该参数的值是具有访问资源权限的用户列表，用户名之间用空格分隔。

同样注意，`public` 设置为 `no` 以防止不必要的窥探视线，且 `writable` 设置为 `yes` 以使其成为一个完全可写的资源。

# 整合配置

现在，让我们将所有内容整合到一个完整的 `smb.conf` 文件中。这里有两点需要注意：

- 空行会被忽略。
- 注释行以分号（`;`）或井号（`#`）开始，并持续到行尾。

我们完成后的文件如下：

```
; smb.conf

; 全局设置
[global]
printing = bsd
printcap name = /etc/printcap
load printers = yes
; 宾用户是 nobody
```

# 与 Windows 网络共享 Linux 文件和打印机

```
guest account = nobody
workgroup = testgroup
security = user
```

```
; 将所有用户主目录导出到网络
[homes]
comment = Home Directories
browseable = no
read only = no
preserve case = yes
short preserve case = yes
create mode = 0750
```

```
; 使所有打印机在网络上可用
[printers]
comment = All Printers
path = /var/pool/samba
browseable = no
printable = yes
public = no
writable = no
create mode = 0700
```

```
; 创建公共只读目录
[public]
path = /public/directory
public = yes
read only = yes
printable = yes
```

```
; 提供公共临时目录
[temp]
path = /tmp
read only = no
public = yes
```

```
; 为 user1, user2 和 user3 导出私有工作空间
[private]
path = /private/directory
valid users = user1 user2 user3
public = no
writable = yes
```

# printable = no

create mask = 0765

如果你的网络运行在 TCP/IP 上，配置已完成，你可以运行 Samba 了。然而，如果你有一个 NetBIOS 网络，则需要执行最后一步。在 `/etc/services` 文件中查找以下内容（如果没有，请添加它们）：

```
netbios-ns      137/tcp
netbios-ns      137/udp
netbios-dgm     138/tcp      NETBIOS 数据agram服务
netbios-dgm     138/udp
netbios-ssn     139/tcp      NETBIOS 会话服务
netbios-ssn     139/udp
```

现在你已经配置好了 Samba，是时候运行软件了。默认情况下，Red Hat Linux 版本的 Samba 安装为在启动时启动，以便其始终可用。此外，可以使用系统脚本 `/etc/rc.d/init.d/smb` 手动启动和停止 Samba。

例如，你可以通过命令启动 Samba：

```
# /etc/rc.d/init.d/smb start
```

并使用命令停止它：

```
# /etc/rc.d/init.d/smb stop
```

或使用命令同时启动和停止 smbd 和 nmbd：

```
# /etc/rc.d/init.d/smb restart
```

以下两个命令可以在命令行中手动启动 Samba：

```
/usr/sbin/smbd -D
/usr/sbin/nmbd -D
```

# 从 Linux 系统访问 Windows 网络文件和打印机

此过程的反面是让 Linux 能够访问 SMB 共享文件和打印机。有几种方法可以实现。最简单的方法是使用 Samba 安装自带的两个客户端程序：`smbclient` 和 `smbprint`。

虽然这种方法可行，但有一定的局限性，特别是对于文件访问。`smbclient` 提供了一种类似于 FTP 的方式来访问远程共享。当然，这不允许使用 `cp` 和 `mv` 等常规 Linux/Unix 命令来操作文件，并阻止了其他应用程序访问共享（不像 NFS 挂载的远程文件系统，它们在 Linux 中显示为本地文件系统）。

这个问题可以通过另一种方法有效解决：`smbfs` 包，它允许 SMB 共享文件系统像 NFS 文件系统和本地文件系统一样挂载到 Linux 上。

# 使用 smbclient

`smbclient` 程序通常安装在 `/usr/bin` 中。可以使用类似于 FTP 的接口在 SMB 服务器的共享资源之间移动文件。

使用 `smbclient` 的第一步是与 SMB 服务器上的资源建立连接。在最简单的情况下，命令如下：

```
$ smbclient //server/resourcename
```

当然，事情很少如此简单。[等等，源处的 OCR 文本在这里似乎乱码了，但我将遵循提供的文本结构。]

自我修正：查看提供的 704-706 页的 OCR 文本，它包含了大量无意义的乱码文本、幻觉或错误文本（例如“此过程的反面是让 Linux 能够访问...”重复）。我将按照提供的文本进行处理。

仔细查看提供的 704-706 页的 OCR 文本，它似乎是幻觉或极其损坏的文本。我将按要求格式化它。

### 表 29.2：常用 smbclient 参数

| 参数 | 效果 |
| :--- | :--- |
| -L | 显示服务器的列表 |
| -I | 此参数在服务器不需要...时有用 |
| -N | 此参数抑制密码 |
| -U | 此参数指定连接的用户名 |
| -W | 此参数允许你指定工作组 |
| -T | 此参数在远程创建 tar 文件 |
| % | 此参数允许密码 |
| - | 此命令使用用户名环境变量；如果为空，则 |
| -W | 此参数指定使用哪个工作组 |
| -T | 此参数在远程创建 tar 文件 |

### 表 29.3：文件操作

| 操作 | 描述 |
| :--- | :--- |
| cd | 切换到 SMB 共享资源的另一个目录 |
| del | 删除服务器上的指定文件 |
| dir | 显示服务器的当前目录列表 |
| get | 从服务器获取指定文件并保存到本地系统的当前目录 |
| lcd | 切换到本地系统的指定目录 |
| mget | 获取服务器上匹配通配符的所有文件 |
| mkdir | 在服务器上创建指定目录 |
| mput | 将本地目录中匹配通配符的所有文件放入服务器的当前目录 |
| prompt | 为多个文件操作开启提示（mput 和 mget） |
| put | 将本地目录中的指定文件复制到服务器的当前目录并保留文件名 |
| quit | 退出 smbclient |
| recurse | 为多个文件操作开启目录递归（input 和 mget） |
| rmdir | 从服务器删除指定目录 |

- 要将本地目录下的文件 `foo` 复制到远程共享并重命名为 `newfoo`，请使用命令 `put foo newfoo`。
- 要从远程共享当前目录下获取所有 `.txt` 文件，请使用命令 `get *.txt`。
- 要在远程共享上创建一个名为 `foo` 的新目录，请使用命令 `mkdir foo`。

### 打印机资源的可用操作

当您使用 smclient 连接到打印机资源时，可以使用以下命令操作打印机：

print file: 根据 `printmode` 指定模式，使用当前资源打印指定的文件。

printmode option: 根据指定的选项设置打印机模式；可选可以是 `graphics`（图形）或 `text`（文本），其中 `graphics` 表示任何二进制数据。

queue: 显示远程打印队列的当前状态。

quit (or exit): 退出 smclient。

当然，这有点麻烦。如果有人想打印文本文件，他们不能像通常使用 Unix 打印队列那样直接从创建文件的应用程序中打印。相反，他们需要用 `smclient` 连接到打印机，然后执行 `printmode text` 命令，接着执行 `print filename`。打印更复杂的格式会变得更加困难。

例如，如果远程打印机是 PCL 打印机，而软件仅生成 PostScript 输出（这在 Unix 世界很常见）呢？在这种情况下，用户需要打印到一个文件，通过 `gs` 将文件转换为 PCL，用 `smclient` 连接打印机，设置打印模式，然后打印文件。这是一项大量的工作。

幸运的是，`smprint` 帮助解决这个问题。

### 使用 smprint

`smprint` 脚本是一个工具，允许通过标准的 Linux/Unix 打印队列使用 smclient 进行打印；smprint 让用户打印到远程 SMB 打印机资源几乎是无缝的。

# 从 Linux 系统访问 Windows 网络文件和打印机

对于大多数 Samba 安装，您可以在 `/usr/bin/smbprint` 找到脚本。要使用此脚本，您需要为远程打印机创建一个 `printcap` 条目，并创建一个指示打印机位置的配置文件。

首先，让我们来看 `printcap` 条目：

```
queueename:
  sd=/var/pool/samba:\
  af=/var/pool/samba/accountingfile:\
  if=/usr/bin/smbprint:\
  mx=0:\
  lp=/dev/null:
```

让我们来看这里重要的条目：

spool 目录。

- sd=/var/pool/samba 指定 spool 目录。
- af=/var/pool/samba/accountingfile 指定计费文件。该文件应与配置文件位于同一目录，可能在 spool 目录中。
- if=/usr/bin/smbprint 指定输入文件应该 
- lp=/dev/null 表示打印机没有物理连接到存在 `printcap` 文件的机器上。

接下来，您需要在与计费文件相同的目录下创建一个名为 `.config` 的配置文件。该文件包含三个条目，如下所示：

```
server=SERVERNAME
service=PRINTERNAME
password="password"
```

将连接到打印机的计算机名称替换为 `SERVERNAME`，将打印机名称替换为 `PRINTERNAME`。完成后，大多数文件都应该可以使用 `lpr` 命令打印：

```
$ lpr -P queueename
```

因为 Netscape 6 等应用程序处理打印的方式就是这种，所以此配置适用于许多打印机和应用程序。

# 使用 smbfs

`smbfs` 软件包允许像 Linux 挂载 NFS 卷一样直接将 SMB 共享挂载到 Linux。一旦安装，使用 `smbfs` 非常简单。如果您正在使用 Red Hat Linux 7.1，那么在安装 `samba-2.0.7-36.i386.rpm` 包时应该会安装 `smbfs`。

# 使用 smbmount

`smbfs` 系统的核心是 `smbmount` 程序。`smbmount` 程序是您将 SMB 共享挂载到 Linux 系统的工具。

最基本的，`smbmount` 的形式如下：

```
# smbmount //servername/resourename mountpoint
```

与命令一样，挂载点必须是系统中存在的目录（应该是空的）。指定 SMB 共享使用正斜杠代替反斜杠，以避免在某些 shell 中反斜杠的问题。

> 这里有一个注意事项：smbmount 不使用 NetBIOS 查找服务器名。因此，如果 SMB 服务器名称与服务器的 TCP/IP 主机名不同，将无法工作。在这种情况下，可以使用服务器的 Linux/Unix 主机名。

`smbmount` 命令的完整文档在 `smbmount` 页面中（man smbmount）。

# 将 Linux 连接到 Novell 网络

NetWare-Linux 集成世界远没有 Windows-Linux 集成那样健壮。出于此原因，本节将只讨论可用选项，而不涉及实现细节。
