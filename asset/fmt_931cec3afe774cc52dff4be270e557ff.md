
```
1829         int ptoc[2], ctop[2];
1830         int pid;
1831         int save_errno;

1835
1836     if (pipe(ptoc) < 0)    /* 设置 errno，由调用者进行诊断 */
1837             return FALSE;
1838
1839     if (pipe(ctop) < 0) {
1840             save_errno = errno;
1841             close(ptoc[0]);
1842             close(ptoc[1]);
1843             errno = save_errno;
1844             return FALSE;
1845     }
```

第一步是创建两个管道。`ptoc` 是“父进程到子进程”，`ctop` 是“子进程到父进程”。在阅读代码时请记住，索引 `0` 是读端，索引 `1` 是写端。

第 1836–1837 行创建了第一个管道 `ptoc`。第 1839–1845 行创建第二个管道，如果失败则关闭第一个。这很重要。未能关闭已打开但未使用的管道会导致文件描述符泄漏。像内存一样，文件描述符是有限的资源，一旦用尽，它们就消失了¹⁴。打开的文件也是如此：确保你的所有错误处理代码在发生故障时关闭任何不再需要的打开文件或管道。

`save_errno` 保存了由 `pipe()` 设置的 `errno` 值，以防 `close()` 可能会失败（第 1840 行）。`errno` 在第 1843 行恢复。

> ¹⁴ 显然，你可以关闭它们。但如果你不知道它们是打开的，那么它们的丢失就和通过内存泄漏丢失内存一样同样有效。

## 示例：`gawk` 中的双向管道

```
1906 if ((pid = fork()) < 0) {
1907     save_errno = errno;
1908     close(ptoc[0]); close(ptoc[1]);
1909     close(ctop[0]); close(ctop[1]);
1910     errno = save_errno;
1911     return FALSE;
1912 }
```

第 1906–1912 行派生子进程，这次如果 `fork()` 失败则关闭两个管道。在这里保存并恢复了原始 `errno` 值，以便后续生成诊断。

```
1914 if (pid == 0) { /* 子进程 */
1915     if (close(1) == -1)
1916         fatal("close of stdout in child failed (%s)",
1917             strerror(errno));
1918     if (dup(ctop[1]) != 1)
1919         fatal("moving pipe to stdin child failed: %s)",
1920             strerror(errno);
1921     if (close(0) == -1)
1922         fatal("close of stdin in child failed (%s)",
1923             strerror(errno);
1924     if (dup(ptoc[0]) != 0)
1925         fatal("moving pipe to stdin child failed: %s)",
1926             if (close(ptoc[0]) == -1 || close(ctop[1]) == -1)
1927                 fatal("close of pipe failed (%s)", strerror(errno));
1928     /* stderr 不会被 dup 到子进程的 stdout */
1929     execcl("/bin/sh", "sh", "-c", str, NULL);
1930     exit(errno == ENOENT ? 127 : 126);
1931 }
```

第 1914–1931 行处理子进程的代码，在每一步都带有适当的错误检查和消息。第 1915 行关闭标准输出。第 1918 行将父到子管道的读端复制到 `0`。如果这成功了，子进程的标准输入和第 1923 行（第 1920 行复制标准输入）现在已就绪，并连接到父进程。

第 1925–1926 行关闭了四个原始文件描述符，因为它们不再被需要。第 1928 行提醒我们标准错误保持在原位。这是最佳决定，因为用户将看到来自协进程的错误。必须捕获标准错误的 `awk` 程序在命令中使用 `'2>&1'` 符号将协进程的标准错误重定向到单独的文件。

最后，第 1929–1930 行尝试在 `shell` 上运行 `execcl()`，并在该时适当地退出。

```
1934      /* 父进程 */
1935      rp->pid = pid;
1936      rp->iop = iop_alloc(ctop[0], str, NULL);
1937      if (rp->iop == NULL) {
1938          (void) close(ctop[0]);
1939          (void) close(ctop[1]);
1940          (void) close(ptoc[0]);
1941          (void) close(ptoc[1]);
1942          (void) kill(pid, SIGKILL);
1943      return FALSE;
1944
```

父进程的第一步是管理来自协进程的输入。`rp` 指针指向 `struct redirect`，它维护一个持有子进程 `PID` 的字段、一个用于输出的 `FILE *` 以及一个名为 `iop` 的 `IOBUF`。`IOBUF` 是用于输入的内部结构。它保留了文件描述符的副本。第 1935 行保存进程 ID。第 1936 行为给定的文件描述符字符串分配一个新的 `IOBUF`。这里的第三个参数为 `NULL`，允许在必要时使用预分配的 `IOBUF`。如果分配失败，第 1937–1942 行通过关闭管道并向子进程发送信号来清理。`kill()` 函数在第 10.6 节“发送信号：`kill()` 和 `killpg()`”中有描述。

```
1946      rp->fp = fdopen(ptoc[1], "w");
1947      if (rp->fp == NULL) {
1948          iop_close(rp->iop);
1949          rp->pid = NULL;
1950          (void) close(ctop[0]);
1951          (void) close(ctop[1]);
1952          (void) close(ptoc[0]);
1953          (void) close(ptoc[1]);
1954          (void) kill(pid, SIGKILL);
1955      return FALSE;
1957      }
```

第 1946–1957 行是类似的。它们通过 `fdopen()` 设置了父进程到子进程的输出，并保存了父子管道的 `FILE *` 这种。如果失败，第 1947–1957 行采取相同的操作：关闭管道描述符并向子进程发送信号。从这里开始，父到子管道的读端和子到父管道的读端分别保留在较大的结构中：分别为 `FILE *` 和 `IOBUF`。它们由关闭这些结构的常规程序关闭。然而，还有两个任务：

```
os_close_on_exec(ctop[0], str, "pipe", "from");
os_close_on_exec(ptoc[1], str, "from");
(void) close(ptoc[0]);
(void) close(ctop[1]);
return TRUE;
```
