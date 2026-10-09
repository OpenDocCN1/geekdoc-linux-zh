

7. 将目录更改为 `arch/i386/boot`。如果硬件架构是 Intel，则需要替换 `i386`，并且可能还需要参考内核使用说明文档来编译和安装你的内核版本。我假设大多数读者的系统是基于 i386 的，并以此继续说明。

8. 将 `bzImage` 复制到 `/boot/vmlinuz-2.4.1`，并编辑 `/etc/lilo.conf` 文件以包含新的配置，如下所示：
```text
image=/boot/vmlinuz-2.4.1
label=linux3
read-only
root=/dev/hda1
```

9. 运行 `/sbin/lilo` 命令重新配置 `lilo` 并重启系统。在 `lilo` 提示符下输入 `linux3` 以启动新内核。如果遇到问题，你应该能够重启到标准的 Linux 内核，这应该是默认选项。

10. 启动新内核后，你就准备好使用 ramfs 了。使用 `mkdir /ramdrive` 命令创建一个名为 `ramdrive` 的目录。

11. 现在使用 `mount -t ramfs none /ramdrive` 命令挂载 ramfs 文件系统。

一切就绪；你现在可以像往常一样向 `/ramdrive` 写入文件了。

> **注意**
>
> 请预先知悉，当系统重启或你卸载文件系统时，所有内容将丢失。这就是为什么它应该用作高速访问的临时空间。此外，请注意，由于 ramfs 实际上并不是一个块设备，诸如 `df` 和 `du` 等程序无法看到它。你可以通过运行 `cat /proc/mounts` 命令并找到如下条目来验证你确实正在使用 RAM：
> ```text
> none /ram ramfs rw 0 0
> ```

> **提示**
>
> 在挂载文件系统时，你可以使用 `-o` 选项来指定选项，就像挂载基于常规磁盘的文件系统一样。例如，要将 ramfs 文件系统挂载为只读，你可以使用 `-o ro` 选项。你還可以指定特殊选项，例如 `maxsize=n`，其中 `n` 是为 RAM 中文件系统分配的千字节数；`maxfiles=n`，其中 `n` 是文件系统允许的文件总数；以及 `maxnodes=n`，其中 `n` 是 inode 的最大数量（默认为 `0` = 无限制）。

# 利用基于 RAM 的文件系统

如果你运行 Web 服务器，基于 RAM 的文件系统将有多种用途。网站上的常见图片和文件，只要不是太大（不超过几 KB），都可以保存在 ramfs 文件系统中。你可以编写一个简单的 shell 脚本，在每次重启时从原始位置复制内容。列表 23-4 是一个执行此操作的简单脚本。

## 列表 23-4: _make_ramfs.sh_

```sh
#!/bin/sh
#
# Simply script to create a ramfs file system
# on $MOUNTPONT (which must exists).
#
# It copies files from $ORIG_DIR to $MOUNTPONT
# and changes ownership of $MOUNTPONT to
# $USER and $GROUP
#
# Change values for these variables to suit
# your needs.

MOUNTPONT=/ram
ORIG_DIR=/www/commonfiles

USER=httd
GROUP=httpd

MOUNTCMD=/bin/mount
CHOWN=/bin/chown
CP=/bin/cp

echo -n "Creating ramfs file system in $MOUNTPONT ":
$MOUNTCMD -t ramfs none $MOUNTPONT
echo "done."

echo -n "Copying $ORIG_DIR to $MOUNTPONT ... ":
$CP -r $ORIG_DIR $MOUNTPONT
echo "done."

echo -n "Changing ownership to $USER:$GROUP for $MOUNTPONT ...":
$CHOWN -R $USER:$GROUP $MOUNTPONT
echo "done."
```

要在系统上使用该脚本，请执行以下操作：

- 1. 在 `/usr/local/scripts` 目录中创建 `make_ramfs.sh`。如果没有该目录，请创建 `/usr/local/scripts` 目录。
- 2. 编辑 `/etc/rc.d/rc.local` 文件并在其中追加以下行：
  `/usr/local/scripts/make_ramfs.sh`
- 3. 使用 `mkdir ram` 命令创建一个名为 `ram` 的目录。如果你想将加载到 RAM 中的文件保存在 `/www/commonfiles` 以外的任何位置，请修改脚本中 `ORIG_DIR` 变量的值。例如，如果你的文件位于 `/www/mydomain/htdocs/common` 目录中，请将此变量设置为指向该目录。
- 4. 如果你使用除 `httpd` 以外的用户名或组来运行 Web 服务器，则相应地修改 `USER` 和 `GROUP` 变量的值。例如，如果你以 `nobody`（用户和组）运行 Apache，则设置 `USER=nobody` 和 `GROUP=nobody`。
- 5. 如果你正在使用 Apache Web 服务器，请在 `httpd.conf` 文件中创建一个别名，如下所示：

```text
Alias /commonfiles/ "/ram/commonfiles/"
```

每当 Apache Web 服务器需要访问 `/commonfiles/*` 时，它将使用 RAM 中的版本，这应该比存储在原始位置的文件快得多。请记住，基于 RAM 的版本会在你重启或卸载文件系统时消失。因此，除非你同时也将内容复制回基于磁盘的目录，否则永远不要更新那里的任何内容。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_701_0.png)

如果你使用类似 `mount -t ramfs none /ram` 的命令挂载了 `ramfs` 文件系统并将内容复制进去，之后重新运行相同的挂载命令，则重新运行该命令会清除内容并重新挂载 `ramfs`。`/proc/mounts` 文件显示同一个挂载点有多个条目，这会导致卸载设备时出现问题。如果你必须重新获得内存以作他用，则必须重启。希望此问题很快能得到解决。

# 创建可靠的后端网络

典型的 Web 网络由一组 Web 服务器、代理服务器、应用服务器、数据库服务器等组成。在大多数情况下，只有 Web 服务器和代理服务器（如果有）需要位于 Web 网络的前端。图 23-3 显示了一个具有前端和后端网络的 Web 网络示例。

每个 Web 服务器节点有两个网络接口。一个接口连接到前端网络 `207.185.233.0/24`，另一个接口连接到后端网络 `192.168.1.0/24`。前端网络由 Web 服务器和负载平衡硬件组成；后端网络由 Web 服务器、应用服务器和数据库服务器组成。

当请求到达活动（主）负载均衡器时，将执行以下一系列操作：

- 负载均衡器确定处理请求的最佳 Web 服务器，并将请求传递给相应的 Web 服务器。
- Web 服务器决定请求是否需要额外资源。例如，如果请求是在应用服务器上运行应用程序，Web 服务器将选择合适的应用服务器和/或数据库服务器，并执行完成请求所需的任务。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_702_0.png)

**图 23-3：** 具有前端和后端网络的 Web 网络

应用服务器和数据库服务器不需要通过 Web 直接访问，因为只有前端网络中的 Web 服务器才与它们联系。这确保了良好的安全性，因此，对于连接到 Web 网络的所有后端网络，使用不可路由的 192.168.x.x 网络地址是一个好主意。

然而，大型 Web 网络要求对应用服务器和数据库服务器也进行负载平衡，否则应用或数据库的使用将成为非常繁忙站点的重大瓶颈。图 23-4 显示了一个高度平衡的 Web 网络，它对前端和后端网络都使用了负载平衡硬件。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_703_0.png)

**图 23-4：** 具有前端和后端负载均衡器的 Web 网络

# 加强你的 Web 网络

黑客发现 Web 网络或构成 Internet 服务的任何节点集群都是攻击的理想目标。这是因为如果他们能够入侵计算机网络，该网络就可以用作攻击其他系统的跳板。基本上，安全防护薄弱但连接良好（高带宽）的 Web 网络为黑客提供了攻击他人的巨大资源。这可能导致 Web 网络管理员面临严重问题。因此，至关重要的是，你必须采取所有可能的预防措施来降低被攻击的风险。有关如何保护 Web 服务器的详细信息，请参见第 18 章。本节提供了适合 Web 网络以及单服务器系统的其他安全相关信息。

