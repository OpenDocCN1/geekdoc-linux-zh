
POSIX 线程 API 在《Programming with POSIX Threads》（[Butenof, 1996]）中有详尽的描述。

《Linux and Unix Philosophy》（[Gancarz, 2003]）是对 Linux 和 UNIX 系统上应用设计哲学的简要介绍。

许多书籍提供了阅读和修改 Linux 内核源码的介绍，包括《Linux Kernel Development》（[Love, 2010]）和《Understanding the Linux Kernel》（[Bovet & Cesetti, 2005]）。

关于 UNIX 内核的更多通用背景，《The Design of the Unix Operating System》（[Bach, 1986]）仍然具有很可读性，并包含了与 Linux 相关的材料。《UNIX Internals: The New Frontiers》（[Vahalia, 1996]）综述了现代 UNIX 实现的内核内部原理。

对于编写 Linux 设备驱动程序，核心参考书籍是《Linux Device Drivers》（Corbet et al., 2005）。

《Operating Systems: Design and Implementation》（[Tanenbaum & Woodhull, 2006]）描述了使用 Minix 实现的操作系统。（另见 `http://www.minix.org/`）

## 现有程序的源码

查看现有应用程序的源代码可以为如何使用特定的系统调用和库函数提供良好的示例。对于使用 RPM 包管理器的 Linux 发行版，我们可以按照以下方法找到包含特定程序（如 `ls`）的包：

```
$ ls -ls

/bin/ls

$ rpm -qf /bin/ls

coreutils-5.075
```

相应的源码包将具有与上述类似的名称，后缀为 `.src.ls`。该包将位于发行版的安装媒体上，或者可以从发行者的网站下载。一旦获取该包，我们可以使用 `rpm` 命令进行安装，然后检查源码，源码通常放置在 `/usr/src/` 下的某个目录下。

在使用 Debian 包管理器的系统上，过程类似。我们可以使用以下命令确定创建程序的包（在本例中为 `ls` 程序）：

```
$ dpkg -S /bin/ls

coreutils: debian
```

## Linux 文档项目

Linux 文档项目（`http://www.ldp.org/`）提供免费的 Linux 文档，包括关于各种系统管理和编程主题的 HOWTO 指南和 FAQ（常见问题与解答）。该网站还提供了更多主题的电子书。

## GNU 项目

GNU 项目（`http://www.gnu.org/`）提供了大量的软件源码和相关文档。

## 新闻组

Usenet 新闻组通常是特定编程问题的良好来源。以下新闻组特别关注：

- comp.unix.programmer 处理一般的 UNIX 编程问题。
- comp.os.linux.development 专门处理与 Linux 应用开发相关的问题。
- comp.os.linux.system 是 Linux 系统开发新闻组，重点关注修改内核以及开发设备驱动和可加载模块的问题。
- comp.programming.threads 讨论线程编程，特别是 POSIX 线程。
- comp.protocols.tcp-ip 讨论 TCP/IP 网络协议族。

许多 Usenet 新闻组的 FAQ 可以在 `http://www.faqs.org/` 找到。

在向新闻组发布问题之前，请检查该组的 FAQ（通常在组内定期发布），并尝试通过网络搜索找到问题的解决方案。`http://groups.google.com/` 网站提供了基于浏览器的界面用于搜索旧的 Usenet 帖子。

## Linux 内核邮件列表

Linux 内核邮件列表（LKML）是 Linux 内核开发人员主要的广播通信媒介。它提供了内核开发动态的信息，并是提交内核报告和补丁的论坛。（LKML 并不是系统编程问题的论坛。）要订阅 LKML，请向 `majondomo@vger.kernel.org` 发送邮件，内容仅为单行：

`subscribe linux-kernel`

关于列表服务器工作原理的信息，请发送包含以下内容的邮件到 `majondomo@vger.kernel.org`：

# 第 9 章

9-1. 在考虑以下内容时，请记住有效用户 ID（effective user ID）的变化始终会改变文件系统用户 ID。

- a) `real=2000, effective=2000, saved=2000, file-system=2000`
- b) `real=1000, effective=2000, saved=2000, file-system=2000`
- c) `real=1000, effective=2000, saved=0, file-system=2000`
- d) `real=1000, effective=0, saved=0, file-system=2000`
- e) `real=1000, effective=2000, saved=3000, file-system=2000`

9-2. 严格来说，这种进程是非特权的。然而，非特进程可以调用 `setuid()`、`setreuid()`、`seteid()` 或 `setresuid()` 将有效用户 ID 设置为与其真实 ID 或保存用户 ID（saved-user-ID）相同的值。因此，该进程可以使用这些调用中的一个来重新获得特权。

9-4. 下面的代码展示了每个系统的步骤。

```c
e = getuid(); /* 保存有效用户 ID 的初始值 */

setuid(getuid()); /* 挂起特权 */

setreuid(e); /* 恢复特权 */

/* 无法通过 setuid() 永久放弃 set-user-ID 身份 */

seteid(getuid()); /* 挂起特权 */

seteid(e); /* 恢复特权 */

/* 无法通过 setuid() 永久放弃 set-user-ID 身份 */

setresuid(-1, getuid(), -1); /* 临时放弃特权 */

setresuid(-1, e, -1); /* 恢复特权 */

setresuid(getuid(), getuid(), getuid()); /* 永久放弃特权 */
```

9-5. `setuid()` 外，上一个练习的答案相同，只是我们将变量 `e` 的值替换为 0。对于 `setuid()`，以下情况成立：

- (a) 无法通过 `setuid()` 挂起并恢复特权
  `setuid(getuid());`
- (b) 永久放弃特权

# 第 10 章

10-1. 最大 32 位无符号整数的值为 4,294,967,295。除以每秒 100 次时钟周期，这对应于略多 497 天。除以 100 万（`CLOCKS_PER_SEC`），这对应于 71 分钟 35 秒。

# 第 12 章

12-1. 本书源码发行版的 `sysinfo/profs_user_exe.c` 文件中提供了解决方案。

# 第 13 章

13-3. 一系列语句确保了写入 `stdio` 缓冲区的数据被刷新到磁盘。`fflush()` 将 `fp` 的 `stdio` 缓冲区刷新到内核缓冲区缓存中。随后的 `fsync()` 提供的参数是文件描述符 `fp`；因此，该调用刷新了文件描述符对应的（刚刚填充的）内核缓冲区。

13-4. 当标准输出发送到终端时，它是行缓冲的，因此 `printf` 的输出会立即出现，紧接着是 `write()` 的输出。当标准输出发送到磁盘文件时，它是块缓冲的。因此，`printf()` 的输出保留在 `stdio` 缓冲区中，只有在程序退出时（即在 `write()` 调用之后）才会被刷新。包含本练习代码的完整程序可在源码发行版的 `linebuff/mix23_linebuff.c` 文件找到。

# 第 15 章

15-2. `stat()` 系统调用不会更改任何文件时间戳，因为它只是从文件 i 节点（i-node）获取信息（并且没有最后的 i 节点访问时间戳）。

15-4. GNU C 库提供了这样的函数，名为 `euidaccess()`，位于库源文件 `sys/posix/euidaccess.c` 中。

15-5. 为了实现这一点，我们使用了两次 `umask()` 调用，如下：

```c
mode_t currMask;

currMask = umask(0);      /* 获取当前 umask，将 umask 设置为 0 */
```
