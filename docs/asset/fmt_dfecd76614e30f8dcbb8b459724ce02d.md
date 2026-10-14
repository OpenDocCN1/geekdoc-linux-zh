
```
$ mount

/dev/sda6 on / type ext4 (rw)

proc on /proc type proc (rw)

sysfs on /sys type sysfs (rw)

devpts on /dev/pts type devs (rw,mode=0620,gid=5)

/dev/sda8 on /home type ext3 (rw,acml,user_xattr)

/dev/sda1 on /windows/C type vfat (rw,noexec,nosuid,nodev)

/dev/sda9 on /home/mtk/test type reiserfs (rw)
```

图 14-4 显示了执行上述 `mount` 命令的系统的部分目录和文件结构。该图显示了挂载点如何映射目录层次结构。

![](img/f77eaa15a5bf88efd4fac6bc0be0e69d_298_0.png)

图 14-4: 显示文件系统挂载点的示例目录层次结构

## 14.8 挂载与卸载文件系统

`mount()` 和 `unmount()` 系统调用允许特权（`CAP_SYS_ADMIN`）进程挂载和卸载文件系统。大多数 UNIX 实现提供了这些系统调版本。然而，它们并没有被 SUSv3 标准化，其操作在不同的 UNIX 实现和文件系统之间存在差异。

在查看这些系统调用之前，了解包含当前已挂载或可挂载文件系统信息的三个文件是有用的：

- 可以从 Linux 特有的 `/proc/mounts` 虚拟文件读取当前挂载的文件系统列表，它是内核数据结构的接口，因此它始终包含关于挂载文件系统的准确信息。

随着前面提到的进程级命名空间的出现，每个进程现在都有一个 `/proc/PID/mounts` 文件，列出构成其挂载命名空间的挂载点，而 `/proc/mounts` 只是指向 `/proc/self/mounts` 的符号链接。

- `mount(8)` 和 `umount(8)` 命令会自动维护文件 `/etc/mtab`，它包含的信息与 `/proc/mounts` 类似但稍为详细。特别是 `/etc/mtab` 包含了传递给 `mount(8)` 的文件系统特定选项，这些选项在 `/proc/mounts` 中并不显示。然而，由于 `mount()` 和 `unmount()` 系统调用不会更新 `/etc/mtab`，如果应用程序挂载或卸载设备未能更新它，该文件可能是不准确的。

- `/etc/fstab` 文件由管理员手动维护，包含了系统中可用文件系统的描述，并供系统使用。这里是 `/proc/mounts` 中的一行示例：

```
/dev/sda9 / ext3 rw 0 0
```

这一行包含六字段：
1. 设备名称。
2. 挂载点。
3. 系统类型。
4. 挂载标志。在上面的示例中 `rw` 表示读写。
5. 用于 `dump` 的数字。
6. 用于检查的数字。

### 14.8.1 挂载文件系统：mount()

`mount()` 系统调用将 `source` 设备上的文件系统挂载到 `target` 指定的目录（挂载点）下。

```c
#include <sys/mount.h>

int mount(const char *source, const char *target, const char *fstype,
        unsigned long mountflags, const void *data);
```
成功返回 `0`，错误返回 `-1`
