
```text
# truss -t kaio,lwp_create aio /junkfile
kaio(5, 0xFFFFFFFF, 0xFFFFFFFF, 0x0EEBF510, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0x00000000, 0, 0xE6FF64) = 2
kaio(AIOREAD, 3, 0xFFFFFFFF, 1024, 0, 0xEFFFF590) Err#48 ENOTSUP
lwp_create(0xEFFFFDA8, 0, 0xE6FF64) = 3
lwp_create(0x00000000, 0, 0x00000000) = 278369456
lwp_create(0xEFFFFDA8, 0, 0xE6FF64) = 4
lwp_create(0x00000000, 0, 0x00000000) = 5278406320
lwp_create(0xEFFFFDA8, 0, 0xE6F64) = 5
lwp_create(0x00000000, 0, 0x00000000) = 6278443184
lwp_create(0xEFFFFDA8, 0, 0xE6FDD44) = 6
lwp_create(0x00000000, 0, 0x00000000) = 627848048
lwp_create(0xEFFFFDA8, 0, 0xE6F62F44) = 7
lwp_create(0x00000000, 0, 0x00000000) = 278516912
lwp_create(0xEFFFFDA8, 0, 0xE6F59F44) = 8
lwp_create(0x00000000, 0, 0x00000000) = -278553776
lwp_create(0xEFFFFDA8, 0, 0xE6F50F44) = 927859640
lwp_create(0xEFFFFDA8, 0, 0xE6F47F44) = 10
lwp_create(0x00000000, 0, 0x00000000) = 1278627504
lwp_create(0xEFFFFDA8, 0, 0xE6F00F44) = 11
lwp_create(0x00000000, 0, 0x00000000) = -278664368
kaio(AIOWAIT, 0x00000000) = Err#22 EINVAL
kaio(AIOWAIT, 0x00000000) = Err#22 EINVAL
kaio(AIONOTIFY, 17506) = 0
aio succeeded
```

在此示例中，我们读取的是文件系统中的一个文件。跟踪结果显示，我们的示例通过一个 `kaio` 系统调用进入内核，创建了几个 LWP，并尝试通过 `kaio` 机制执行异步 I/O。第二个 `kaio` 调用以 `ENOTSUP`（不支持）错误失败，系统随后回退到库实现，导致在 I/O 完成前创建了一堆线程（LWP）。请注意，程序输出的最后一行 `aio succeeded` 表明 `aioread(3)` 确实成功了——只是我们没有使用 `kaio` 机制来完成它。

很明显，用户线程实现会导致更多的线程/LWP 创建和管理，从而增加开销、降低效率。那么，为什么 Solaris 环境会为单个异步 I/O 请求创建 11 个 LWP？答案与异步 I/O 库的初始化有关。

第一次调用 `aioread(3)` 或 `aiowrite(3)` 时，会调用异步 I/O 库的初始化例程，并创建多个工作线程来执行异步 I/O。系统只是在准备处理多个异步 I/O，因此创建了四个读 LWP 和四个写 LWP，外加一个用于文件同步的线程。这正好解释了上面你看到的九次成功的 `lwp_create` 调用。如果你在测试程序中加入第二个 `aioread(3)` 或 `aiowrite(3)`，并使用 `truss(1)` 命令重新运行，就不会看到第二个异步 I/O 对应的所有这些 `lwp_create` 调用。库会使用初始化期间创建的工作线程来处理后续的异步 I/O 请求（当然，为了跟上传入的异步 I/O 请求负载，它也会创建更多工作线程）。

虽然预先创建工作线程池有助于为用户线程异步 I/O 机制提供更好的可扩展性，但与内核异步 I/O 相比，它仍然涉及更多开销和更长的代码路径。

## 11.5 内存映射文件 I/O

到目前为止所讨论的文件 I/O 都是通过 `read`、`write` 和 `lseek` 系统调用完成的，这些调用代表进程执行 I/O，并将数据复制到进程的地址空间或从进程的地址空间复制出来。I/O 先在内核缓冲区中进行，然后再复制到进程地址空间或从进程地址空间复制出来，如图 11.3 所示。

![](img/220ae4af07df2fe8e5be69d27f885d1b_550_0.png)

图 11.3 *使用 `read(2)` 读取文件*

![](img/220ae4af07df2fe8e5be69d27f885d1b_551_0.png)

图 11.4 *内存映射文件 I/O*

`mmap(2)` 系统调用的函数定义如下所示。

```c
void *mmap(void *addr, size_t len, int prot, int flags, int filedes, off_t off);
```

**头文件** `<sys/mman.h>`

调用 `mmap` 系统调用时，需要传入一个打开的文件句柄、被映射文件的偏移量和长度、映射在进程地址空间中的地址和长度、一个选项标志，以及一个保护类型，用于指明该映射应使用的内存保护，如下所示。

```c
if ((addr = mmap64((caddr_t)0, length, PROT_READ,
        MAP_SHARED, fd, offset)) == NULL) {
        perror("mmap failed");
        exit(1);
}
```

操作系统使用内存映射函数将可执行文件和共享库映射到进程的地址空间中。可以使用 `mmap(1)` 命令列出进程的映射。

```text
# /usr/proc/bin/mmap 25888

25888:   /bin/ksh
00010000    192K read/exec          /usr/bin/ksh
0004E000      8K read/write/exec     /usr/bin/ksh
00050000     40K read/write/exec     [ heap ]
FF180000    656K read/exec          /usr/lib/libc.so.1
FF232000     32K read/write/exec     /usr/lib/libc.so.1
FF280000    512K read/exec          /usr/lib/libnsl.so.1
FF3E0000     40K read/exec          /usr/lib/libnsl.so.1
FF318000     32K read/write/exec     [ anon ]
FF330000     16K read/exec          /usr/platform/sun4u/lib/libc_psr.so.1
FF340000     16K read/exec          /usr/lib/libmp.so.2
FF352000      8K read/write/exec     /usr/lib/libmp.so.2
FF370000     32K read/exec          /usr/lib/libsocket.so.1
FF390000     16K read/write/exec     /usr/lib/libsocket.so.1
FF390000      8K read/exec          /usr/lib/libdl.so.1
FF3A0000      8K read/write/exec     /usr/lib/ld.so.1
FF3B0000    120K read/exec          /usr/lib/ld.so.1
FF3CD000      8K read/write/exec     [ stack ]
FF3CE000     16K read/write/exec     [ stack ]
total      1760K
```

`mmap` 命令向我们显示每个段的大小和保护，并在可能的情况下显示映射到进程中的文件名。在此示例中，我们可以看到二进制文件(`/usr/bin/ksh`)以及映射到 Korn shell 中的库。

### 11.5.1 映射选项

某些标志允许向 `mmap` 传递不同的选项，以控制文件映射到进程地址空间的方式（参见表 11-7）。这些选项通过 `flags` 参数传入。

**表 11-7. _来自 `<sys/mman.h>` 的 Solaris 7 `mmap` 标志_**

| 类型 | 描述 |

| --- | --- |

| `MAP_FIXED` | 在提供的地址处进行映射。 |
