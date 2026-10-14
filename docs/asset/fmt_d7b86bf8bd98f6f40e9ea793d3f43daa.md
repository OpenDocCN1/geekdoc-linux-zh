
`#include <sys/mount.h>`

`int umount2(const char *target, int flags);`

成功时返回 0，出错时返回 -1

此 `flags` 位标志掩码参数由以下一个或多个值通过位或（OR）操作组合而成：

- `MNT_DETACH`（自 Linux 2.4.11 起）
执行懒卸载（lazy unmount）。挂载点被标记，使得没有进程可以对其进行新的访问，但正在使用它的进程继续使用。当所有进程停止使用该挂载时，文件系统实际上会被卸载。

- `MNT_EXPIRE`（自 Linux 2.6.8 起）
将挂载点标记为过期。如果执行指定此标志的初始 `umount2()` 调用且挂载点未繁忙，则调用将以错误 `EAGAIN` 失败，但挂载点会被标记为过期。（如果挂载点繁忙，则调用将以错误 `BUSY` 失败，且挂载点不会标记为过期。）只要后续没有进程使用它，挂载点将保持过期状态。第二次指定 `MNT_EXPIRE` 的 `umount2()` 调用将卸载一段时间未使用的文件系统。此标志不能与 `MNT_DETACH` 或 `MNT_FORCE` 同时指定。

- `MNT_FORCE`
即使设备正忙也强制卸载（仅限 NFS 挂载）。使用此选项可能导致数据丢失。

- `MOUNT_NOFOLLOW`（自 Linux 2.6.34 起）
如果目标是符号链接，则不对进行解引用。此标志设计用于某些特定的用户-ID-root 程序，这些程序允许非特权用户执行卸载，以避免当目标是被更改指向不同位置的符号链接时可能发生的安全问题。

## 14.9 高级挂载特性

我们将查看在挂载文件系统时可以使用的一些更高级的特性。我们将通过使用 `mount(8)` 命令演示大部分这些特性的用法。通过调用 `mount(2)` 的程序调用，同样可以实现相同的效果。

### 14.9.1 在多个挂载点上挂载文件系统

在 2.4 之前的内核版本中，文件系统只能挂载在一个挂载点上。从内核 2.4 开始，一个文件系统可以挂载到文件系统内的多个位置。由于每个挂载点都显示相同的子树，通过一个挂载点所做的更改在其他挂载点上也是可见的，如下 shell 会话所示：

```bash
$ su

Password:

# mkdir /testfs

# mkdir /demo

# mount /dev/sda12 /testfs

# mount /dev/sda12 /demo

# mount | grep sda12

/dev/sda12 on /testfs type ext3 (rw)

/dev/sda12 on /demo type ext3 (rw)

# touch /testfs/myfile

# ls -l myfile
```

> 需要权限来使用 `mount(8)`
> 创建两个目录作为挂载点
> 在一个挂载点上挂载文件系统
> 在第二个挂载点上挂载文件系统
> 验证设置
> 通过第一个挂载点进行更改
> 在第二个挂载点查看文件

`ls` 命令的输出显示通过第一个挂载点 (`/testfs`) 做的更改在第二个挂载点 (`/demo`) 上是可见的。我们在第 14.9.4 节中将介绍为什么在多个点上挂载文件系统是有用的示例。这是因为设备可以挂载到多个点，而在 Linux 2.4 及更高版本中，`umount()` 系统调用无法接受设备作为参数。

### 14.9.2 在同一挂载点上堆叠多个点

在 2.4 之前的内核版本中，挂载点只能使用一次。从内核 2.4 开始，Linux 允许在单个挂载点上堆叠多个点。每个新挂载都会隐藏该挂载点之前可见的子树。当栈顶部的挂载被卸载时，之前隐藏的挂载将再次可见，如下 shell 会话所示：

```bash
$ su

Password:

# mount /dev/sda12 /testfs

# touch /testfs/myfile

# mount /dev/sda13 /testfs

# mount | grep testfs

/dev/sda12 on /testfs type ext3 (rw)

/dev/sda13 on /testfs type reiserfs (rw)
```

> 需要权限来使用 `mount(8)`
> 在 `/testfs` 创建第一个挂载点
> 在子树中文件
> 在 `/testfs` 上堆叠第二个挂载
> 验证设置

```bash
# touch /testfs/newfile

# ls /testfs

newfile

# umount /testfs

# mount | grep testfs

/dev/sda12 on /testfs type ext3 (rw)

/dev/sda13 on /testfs type reiserfs (rw)
```

> 在子树中创建文件
> 在子树中查看文件
> 从栈中弹出一个挂载
> 现在 `/testfs` 上只有一个挂载
> 之前的挂载现在可见了

挂载堆叠的一种用途是在繁忙的现有挂载点上堆叠新挂载。处理已打开的文件符且工作目录在该内的进程将继续操作，但对挂载点进行新访问的进程将使用新挂载。结合 `MNT_DETACH`，这可以在无需重启的情况下平滑迁移文件系统。我们将在第 14.10 节讨论 `tmpfs`。

### 14.9.3 基于挂载的标志

在内核 2.4 中，文件系统和挂载点之间是一一对应的。由于这种关系在 Linux 2.4 之后不再成立，14.8 节中讨论的某些挂载标志可以基于每次挂载进行设置。这些标志包括 `MS_NOTIME`（自 Linux 2.6 起）、`MS_NODEV`、`MS_NODIRTIME`（自 Linux 2.6 起）、`MS_NOEXEC`、`MS_NOSUID`、`MS_RDONLY`（自 Linux 2.6 起）以及 `MS_RELATIME`。以下 shell 会话演示了 `MS_NOEXEC` 标志：

```bash
$ su

Password:

# mount /dev/sda12 /testfs

# mount -o noexec /dev/sda12 /demo

# cat /proc/mounts | grep sda12

/dev/sda12 on /testfs ext3 rw,noexec 0

/dev/sda12 on /demo ext3 rw 0

# cp /bin/echo /testfs

/testfs/echo "something is well done"

# /demo/echo "something is well done"

bash: /demo/echo: Permission denied
```

### 14.9.4 绑定挂载 (Bind Mounts)

从内核 2.4 开始，Linux 允许创建绑定挂载。绑定挂载（使用 `mount()` 的 `MS_BIND` 标志）允许目录或文件挂载到文件系统层次结构中的其他位置。这导致目录或文件在两个位置都是可见的。绑定挂载有点类似于硬链接，但有两个方面不同：

- 绑定挂载可以跨越文件系统挂载点（甚至是 chroot 监狱）。
- 可以为目录创建绑定挂载。

我们可以使用 `mount(8)` 的 `--bind` 选项从 shell 创建绑定挂载，如下例所示。在第一个示例中，我们在另一个位置绑定了一个目录，并显示在一个目录中创建的文件在另一个位置也是可见的：

> 需要权限来使用 `mount(8)`

```bash
$ su
Password:
# pwd /testfs
# mkdir d1
# touch d1/x
# mkdir d2
# mount --bind d1 d2
# ls d2
x
# touch d2/y
# ls d1
x y
```

> 在另一个位置绑定目录
> 在目录中创建文件
> 创建 d1 将被绑定的挂载点
> 创建挂载：通过 d2 可看到 d1
> 验证我们是否通过 d2 看到 d1 的内容
> 在目录中创建第二个文件
> 验证此更改通过 d1 可见

在第二个示例中，我们在另一个位置绑定了一个挂载，并演示文件挂载的更改通过另一个挂载是可见的：

```bash
# cat f1
Chance is always powerful. Your hook is always cast.
# touch f2
# mount --bind f1 f2
# mount | grep 'd1\|f1'
/testfs/d1 on /testfs/d2 type (rw,bind)
/testfs/f1 on /testfs/f2 type (rw,bind)
# cat >> f2
In the pool you let expect it, will be a fish.
# cat f1
Chance is always powerful. Let your hook be always cast. In the pool you let expect it, will be a fish.
# rm f2
rm: not unlink 'f2': Device or resource busy
# umount f2
# rm f2
```
