
以下是 /etc/mnttab 文件的示例：

```
more /etc/mnttab
/dev/dsk/c0t0d0s0   /   ufs   rw,intr,largefiles,onerror=panic,suid,dev=2200000   985708256
/dev/dsk/c0t0d0s3   /usr  ufs   rw,intr,largefiles,onerror=panic,suid,dev=2200003   985708257
/proc   /proc proc dev=2dc0000   985708254
fd   /dev/fd fd   rw,suid,dev=2e80000   985708258
mnttab /etc/mnttab mnttfs dev=2f80000   985708260
/dev/dsk/c0t0d0s4   /var  ufs   rw,intr,largefiles,onerror=panic,suid,dev=2200004   985708260
swap   /var/run   tmpfs dev=1   985708260
swap   /tmp   tmpfs dev=2   985708263
/dev/dsk/c0t0d0s6   /data ufs   rw,intr,largefiles,onerror=panic,suid,dev=2200006   985708263
/dev/dsk/c0t0d0s5   /opt  ufs   rw,intr,largefiles,onerror=panic,suid,dev=2200005   985708263
/dev/dsk/c0t0d0s7   /export/home   ufs   rw,intr,largefiles,onerror=panic,suid,dev=2200007   985708263
-hosts /net   autofs indirect,nosuid,ignore,nobrowse,dev=3040001   985708269
auto_home /home autofs indirect,ignore,nobrowse,dev=3040002   985708269
-xfn /xfn autofs indirect,ignore,dev=3040003   985708269
```

在 Solaris 的早期版本中，/etc/mnttab 文件是一个文本文件。作为文本文件的缺点是它可能与已挂载文件系统的实际状态不同步，或者可以被手动编辑。在 Solaris 8 中，该文件是一个 mnttfs 文件系统，它直接从内核提供有关本地主机上已挂载文件系统的只读信息。

## 卸载文件系统

卸载文件系统时，使用 umount 命令：

```
umount <mount-point>
```

<mount-point> 是你要卸载的文件系统的名称。这可以是文件系统所挂载的目录名，也可以是文件系统的设备名称路径。例如，要卸载 /home2 文件系统，输入以下内容：

```
umount /home2
```

或者，你可以指定文件系统的设备名称路径：

```
umount /dev/dsk/c0t0d0s0
```

卸载文件系统会将其从文件系统挂载点移除，并从 /etc/mnttab 中删除条目。某些文件系统管理任务无法在已挂载的文件系统上执行，例如 labelit、fsck 和 tunefs。如果存在以下三种情况之一，你应该卸载文件系统：

- 文件系统不再需要或已被包含更新软件的文件系统取代。
- 你需要使用 fsck 命令检查和修复文件系统。
- 你计划进行完整备份。

> NOTE
文件系统会在系统关机过程中自动卸载。

## fuser 命令

在卸载文件系统之前，你必须以管理员（root）身份登录，并且文件系统不能忙。如果用户位于文件系统中的目录中或程序在该文件系统中打开了文件，则认为文件系统忙。你可以通过切换到不同文件系统中的目录或注销系统来使文件系统可供卸载。如果有某物导致文件系统忙，你可以使用表 7.7 中描述的 fuser 命令列出所有访问文件系统的进程，并在必要时停止它们。

> NOTE
卸载文件系统前请务必通知用户。

fuser 的语法如下：

/usr/sbin/fuser [options] <file>|<filesystem>

将 <file> 替换为你要检查的文件名，或将 <filesystem> 替换为你要检查的文件系统名称。

### 表 7.7

### fuser 命令

| Option | Description |
| --- | --- |
| -c | 报告文件系统挂载点上的文件以及该已挂载文件系统内的任何文件。 |
| -f | 打印指定文件的报告，但不打印已挂载文件系统内的文件。 |
| -k | 向每个进程发送 SIGKILL 信号。由于此选项为每个进程生成 kill，因此 kill 消息可能不会立即显示。 |
| -u | 在进程 ID 后用括号显示用户登录名。 |

以下示例使用 fuser 命令查找 /home2 为何忙：

```
fuser -u /home2
```

系统显示使用此文件系统的每个进程和用户登录名：

/home2:      8448c(root)    8396c(root)

以下命令通过向每个进程发送 SIGKILL 来停止所有使用 /home2 文件系统的进程。不要在未先警告用户的情况下使用它。

```
fuser -c -k /home2
```

使用 fuser 命令如上所述是卸载文件系统前确定谁在使用文件系统的首选方法。Solaris 8 中新增的另一种不太理想的方法是使用带有 -f 选项的 umount 命令卸载文件系统，如下所示：

```
umount -f /home2
```

-f 选项将强制卸载文件系统。使用此选项可能导致数据丢失，因为在文件系统卸载后，打开的文件和访问文件的程序会返回错误（EIO）。-f 选项应仅作为最后手段使用。

## 卷管理器

卷管理器（不要与第 18 章“名称服务”中描述的企业卷管理器混淆），与 vold 守护进程一起，是管理可移动媒体（如 CD-ROM 和软盘驱动器）的机制。挂载和卸载文件系统需要 root 权限。如何让用户在不作为管理员（root）的情况下插入、挂载和卸载 CD-ROM 和软盘？在文件系统已挂载且你移除介质后，挂载会发生什么？通常，当在挂载时断开磁盘驱动器时，系统开始显示错误和消息。如果在挂载时移除软盘或 CD-ROM 也会发生同样的情况。

卷管理器及其 vold 守护进程提供了克服这些问题的帮助。vold 守护进程通过自动挂载来简化磁盘和 CD 的使用。卷管理器提供三大主要好处：

- 通过自动挂载软盘和 CD，卷管理器简化了它们的使用。
- 卷管理器允许用户在无需以 root 登录的情况下访问软盘和 CD。
- 卷管理器允许管理员（root）让网络上的其他系统自动访问用户插入到你的系统中的任何软盘和 CD。

首先，让我们来看系统管理员需要管理的两个设备：软盘驱动器和 CD-ROM。卷管理器通过 /vol/dev 目录提供对这两个设备的访问。此外，卷管理器通过各种目录创建指向软盘和 CD-ROM 设备的链接，如表 7.8 所示。

### 表 7.8

### 卷管理器目录和链接

| Link | Description |
|---|---|
| /vol/dev/diskette0 | 提供对软盘驱动器 0 中介质的块设备访问的目录 |
| /vol/dev/rdiskette0 | 提供对软盘驱动器 0 中介质的字符设备访问的目录 |
| /vol/dev/aliases/floppy0 | 指向软盘驱动器 0 中介质的字符设备的符号链接 |
| /dev/rdiskette | 提供对主软盘驱动器（通常为驱动器 0）中介质的字符设备访问的目录 |
| /vol/dev/aliases/cdrom0 | 提供对主 CD-ROM 驱动器中介质的字符设备访问的目录 |
| /vol/dev/dsk/ | 提供对 CD-ROM 缓冲或块设备的访问的目录 |
| /vol/dev/rdsk/ | 提供对 CD-ROM 字符或原始设备访问的目录 |
| /cdrom/cdrom0 | 指向 CD-ROM 驱动器 0 中介质的缓冲设备的符号链接 |
| /floppy/floppy0 | 指向软盘驱动器 0 中介质的缓冲设备的符号链接 |

vold 守护进程在可识别文件系统的可移动媒体插入设备时自动挂载 CD-ROM 和文件系统。当插入 CD 时，vold 会自动将 CD-ROM 文件系统挂载到刚才描述的 /vol/dev 目录中。然而，对于软盘，软盘的文件系统在发出 volcheck 命令之前不会自动挂载。volcheck 命令指示 vold 检查每个设备并确定是否已将新媒体插入驱动器。对于软盘，不要让 vold 不断轮询磁盘驱动器，如同对 CD 所做的那样，因为软盘驱动器存在硬件限制。对软盘媒体的持续轮询会导致软盘驱动器产生机械动作并导致驱动器过早磨损。

vold 守护进程是卷管理器背后的主力。它由 /etc/init.d/volmgt 脚本自动启动。vold 在启动时读取 /etc/vold.conf 配置文件。vold.conf 文件包含 vold 使用的卷管理器配置信息。
