
NFS 使用用户数据报协议（UDP）进行无连接的信息传输。这使其能够从网络故障的影响。一旦服务器恢复可用，数据传输将从中断的地方继续。对于像 TCP 这样有连接的协议，网络故障意味着服务也随失败。自创建以来，NFS 已被修改为同时使用 UDP 和 TCP 协议。

## 安装并运行 NFS

必须安装三个组件才能使 NFS 服务器正常工作：

- `Portmap`——它作为基础系统的一部分默认安装，并包含在 `netbase` 软件包中。`/usr/sbin/portmap` 脚本在系统启动时通过 `/etc/init.d/mountfs` 脚本作为守护进程启动，该脚本在启动时运行以挂载任何远程文件系统。portmapper 在服务编号可用端口号之间进行翻译。
- `rpc.mountd`——此守护进程在启动时由 `/etc/init.d/nfs-kernel-server` 脚本启动，仅处理挂载请求。它验证请求客户端是否有权访问系统以及请求的文件系统，并向客户端传递请求文件系统的句柄。
- `rpc.nfsd`——此守护进程同样在启动时由 `/etc/init.d/nfs-kernel-server` 脚本启动。建立连接后，此守护进程处理客户端和服务器之间的信息传输。

至少，你需要为 NFS 客户端安装 `netbase` 和 `nfs-common` 软件包。服务还需要 `nfs-kernel-server` 软件包。一旦安装了这些软件包，它们会在系统启动时自动作为守护进程运行。

> 注意：为了提高安全性，请将 `portmap` 添加到 `hosts.allow` 和 `hosts.deny` 文件中以限制访问。portmapper 守护进程使用这些文件来控制其使用的访问。有关安全性的更多信息，请参见第19章。

## 第24章 - 文件服务器

当 `portmapper` 运行时，你可以使用 `rpcinfo` 查询它以列出注册的程序。使用 `-p` 选项将结果输出到屏幕上，如下：

```
rpcinfo -p debian
```

| program vers proto port |
|---|---|---|---|
| 100000 2 tcp 111 portmapper |
| 100000 2 udp 111 portmapper |
| 100024 1 udp 757 status |

（此处省略了重复的表格内容，翻译逻辑保持一致）

在此文件中，为两个主机授予了 root 权限。这两个主机都可以读取和写入 NFS 服务器的整个文件系统，但只有其中一个拥有 root 权限。下一行赋予了所有以 dev 开头并 `.my.domain` 结尾的主机对 `/code` 文件系统的读/写权限。文件的第三行赋予了所有以 `my.domain` 结尾域名的用户只读权限；然而，`@trusted` NIS 组的成员具有读/写权限。第四行允许仅匹配特定 IP 地址的一台主机具有写权限。它强制所有访问都以特定用户的身份进行，无论客户端上的实际用户是谁。文件中的两行赋予了所有人对 `/pub` 文件系统的只读权限，但排除了所有人对 `/pub/private` 子目录的访问。

## 自动挂载 NFS 共享

在企业环境中，许多计算机（如果不是全部）将连接到 NFS 共享以存储公共文件、配置和数据。为了立即访问这些共享而无需等待控制台挂载它们，需要将共享设置为启动时自动挂载。对于本地文件系统，共享的 NFS 文件系统需要添加到 `/etc/fstab` 直接中。

与本地系统一样，远程 NFS 共享具有某些选项用于指定连接参数。这些选项列在表 24-2 中，并不是强制性的，但为共享卷提供了更大的灵活性和控制。

### 表 24-2

在 `/etc/fstab` 中挂载 NFS 共享的设置

| 设置 | 说明 |
| --- | --- |
| `rsize=nnnn` | 指定通过网络读取的 `nnn` 字节数。默认值为 1,024；然而，设置为 8,192 时吞吐量会提高。将此设置更改为错误的数字会对性能产生不利影响。 |
| `wsize=nnnn` | 指定通过网络写入的 `nnn` 字节数。默认大小为 1,024。备注见 `rsize`。 |
| `Hard` | 设置到 NFS 服务器的连接。如果服务器宕机或连接丢失，任何使用此选项连接的进程都将挂起，直到服务器恢复可用，此时进程将像什么都没发生过一样继续。 |
| `Soft` | 如果 NFS 服务器宕机或丢失连接，允许进程超时。使用 `timeout` 设置超时持续时间。 |
| `retrans=nnnn` | 设置在进程终止（软连接情况下）或向控制台发布消息（“服务器未响应”）之前的次要事务超时次数，由 `nn` 表示。 |

### 表 24-2（续）

| 设置 | 说明 |
| --- | --- |
| `Intr` | 允许在等待 NFS 服务器的响应时中断或杀死硬连接。 |
| `timeo-nn` | 设置在 RPC 超时发生后、下一次尝试之前等待的秒数，由 `nn` 表示。与软连接（`soft`）设置配合使用。 |
| `Bg` | 如果第一次尝试挂载文件系统失败，则在后台重试挂载。这使得其他文件系统的挂载过程可以继续。 |
| `Fg` | 如果第一次尝试挂载文件系统失败，则在前台重试挂载。将此项用于在继续操作之前必须挂载的文件系统，例如 `/usr`。 |
| `Rw` | 将文件系统设置为可读写。 |
| `Ro` | 将文件系统设置为只读。 |

最初，你的 `/etc/fstab` 文件可能只包含原始配置的本地文件系统。该文件可能如下：

```
# /etc/fstab
# /etc/fstab: 静态文件系统信息。
# <file system> <mount point> <type> <dump> <pass>
/dev/hd1 / ext2 defaults,errors=remount-ro 1 1
/dev/hd2 none swap sw 0 0
/dev/hdal /win_c vfat defaults,user.ro 0 0
proc /proc proc 0 0
/dev/fd0 /floppy auto defaults,user.noauto 0 0
/dev/cdrom /cdrom iso9660 defaults,ro,user.noauto 0 0
```

要添加 NFS 共享，请使用 `vi` 等文本编辑器编辑此文件。按照以下格式为其添加一行：

```
server:/share nfs options 0 0
```

`server` 是主机的名称，后面紧跟远程主机上的共享 NFS 卷。这些信息来自 `/etc/exports` 文件。接下来是本地挂载点，你可以将其设置为任何想要的内容。NFS 指定该文件系统使用 NFS 连接。选项可以在表 24-2 中。这里使用的每个选项必须用逗号（`,`）隔开，且没有空格。最后两个零表示在启动时不 `dump` 内容或执行文件系统检查 (`fsck`)。

## 以下是添加 NFS 共享后的 /etc/fstab 文件示例：

```
more /etc/fstab
# /etc/fstab: 静态文件系统信息。
# <file system> <mount point> <type> <options> <dump> <pass>
/dev/hdb1               ext2    defaults,errors-remount-ro 0 1
/dev/hdb2               none    swapped  sw                             0 0
debian:/remote          nfs     fg,ro,hard,intr                  0 0
proj/home/projects      nfs     bg,rw,soft                     0 0
/dev/hda1               _c vfat    defaults,user,ro             0 0
proc                    proc    defaults                         0 0
/dev/fd0                floppy  defaults,user,noauto         0 0
/dev/cdrom              iso9660  defaults,ro,user,noauto      0 0
```

现在，建立了两个远程挂载。第一个连接到主机 `debian`，并且因为 `fg` 选项允许继续。下一个为共享 `projects` 打开了命令区域。这些数据存储在主机 `proj` 上。为了让 NFS 共享成功挂载，其挂载目录必须存在。在本地文件系统上创建挂载点，请使用 `mkdir`：

```
mkdir /mnt/point
```

将路径 `/mnt/point` 更改为你想让远程文件系统挂载的地方。

## 手动挂载 NFS 文件系统

挂载 NFS 文件系统不需要在 `/etc/fstab` 文件中有条目。这些文件系统可以从命令行挂载：

```
mount server:/remote/share /usr/share
```
