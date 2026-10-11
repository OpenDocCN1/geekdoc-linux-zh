
## 5.5.3 utime：设置访问时间和修改时间

```c
struct utimbuf {
    time_t actime; /* access time */
    time_t modtime; /* modification time */
};
```

如果调用成功，返回 0；否则，返回 -1。如果 `buf` 为 `NULL`，则系统会将访问时间和修改时间都设置为当前时间。

若要只更改其中一个时间而保持另一个不变，请使用 `struct stat` 中的原始值。例如：

```c
/* 为简洁起见，省略了错误检查 */
struct stat sbuf;
struct utimbuf ut;
time_t now;

time(&now); /* 获取当前时间，参见下一章 */
stat("/some/file", &sbuf); /* 填充 sbuf */
ut.actime = sbuf.st_atime; /* 保持访问时间不变 */

ut.modtime = now - (24 * 60 * 60); /* 将修改时间设置为 24 小时前 */

utime("/some/file", &ut); /* 设置这些值 */
```

关于 `now`，你可能会问：“为什么有人想要更改文件的访问时间和修改时间呢？” 这是一个好问题。

要回答这个问题，请考虑创建备份归档的程序，例如 `tar` 或 `cpio`。这些程序必须读取文件内容才能将其归档。当然，读取文件会更改文件的访问时间。

然而，该文件可能已经 10 年没有被人类读取过。执行 `ls -lu`（显示访问时间，而不是默认的修改时间）的用户应该看到该文件最后一次被读取是在 10 年前。因此，备份程序应保存原始的访问时间和修改时间，读取文件以进行归档，然后使用 `utime()` 恢复原始时间。

同样，考虑归档程序从归档中恢复文件的情况。归档存储了文件原始的访问时间和修改时间。然而，当从归档中提取文件并作为磁盘上的新副本创建时，新文件的访问时间和修改时间将是当前的日期和时间。

但是，如果新创建的文件看起来与归档中的原始文件年龄相同会更有用。因此，归档程序需要能够将访问时间和修改时间设置为归档中存储的值。

> **注意** 在新代码中，你可能希望使用 `utimes()` 调用（注意名称中的 s），该调用在本书第 14.3.2 节“微秒文件时间：utimes()”，第 545 页中有描述。

### 5.5.3.1 模拟 utime (file, NULL)

一些较旧的系统在 `utime()` 的第二个参数为 `NULL` 时，不会将访问时间和修改时间设置为当前时间。然而，如果更高层的代码（如 GNU `touch`）可以依赖单一的标准化接口，它将更简单、更直接。

因此，GNU Coreutils 库包含一个替代 `utime()` 的函数来处理这种情况，然后由更高层的代码调用。这体现了我们在第 1.5 节“重新审视可移植性”，第 19 页中描述的“为工作选择最佳接口”的设计原则。

替代函数位于 Coreutils 发行版中的 `lib/utime.c` 文件。以下是 Coreutils 5.0 中的版本。行号相对于文件开头：

```c
24 #include <sys/types.h>
25 
26 #ifdef HAVE_UTIME_H
27 # include <utime.h>
28 #endif
29 
30 #include "full-write.h"
31 #include "safe-read.h"
32 
33 /* Some systems (even some that do have <utime.h>) don't declare this
34 structure anywhere.  */
35 #ifdef HAVE_STRUCT_UTIMBUF
36 struct utimbuf
37 {
38 long actime;
39 long modtime;
40 };
41 #endif
42 
43 /* Emulate utime (file, NULL) for systems (like 4.3BSD) that do not
44 interpret it to set the access and modification times of FILE to
45 the current time. Return 0 if successful, -1 if not.  */
46 
47   static int
48   utime_null (const char *file)
49   {
50    #if HAVE_UTIMES_NULL
51      return utimes (file, 0);
52    #else
53      int fd;
54      char c;
55      int status = 0;
56      struct stat sb;
57
58      fd = open (file, O_RDWR);
59      if (fd < 0
60        || fstat (fd, &sb) < 0
61        || safe_read (fd, &c, sizeof c) == SAFE_READ_ERROR
62        || lseek (fd, (off_t) 0, SEEK_SET) < 0
63        || full_write (fd, &c, sizeof c) != sizeof c
64      /* Maybe do this -- it's necessary on SunOS4.1.3 with some combination
65         of patches, but that system doesn't use this code: it has utimes.
66        || fsync (fd) < 0
67      */
68        || (st.st_size == 0 && ftruncate (fd, st.st_size) < 0)
69      || close (fd) < 0)
70        status = -1;
71      return status;
72    #endif
73   }
74
75   int
76   rpl_utime (const char *file, const struct utimbuf *times)
77   {
78     if (times)
79       return utime (file, times);
80
81     return utime_null (file);
82   }
```

第 33–41 行定义了 `struct utimbuf`；正如注释所说，一些系统没有声明该结构体。`utime_null()` 函数执行实际工作。如果 `utimes()` 系统调用可用，则使用它。（`utimes()` 是一个类似但更高级的系统调用，在第 14.3.2 节“微秒文件时间：utimes()”，第 545 页中有介绍。它也允许第二个参数为 `NULL`，意味着使用当前时间。）

在必须手动更新时间戳的情况下，代码通过首先从文件读取一个字节，然后将其写回来进行更新。（原始的 Unix `touch` 就是这样工作的。）操作如下：

- 1. 打开文件，第 58 行。
- 2. 对文件调用 `stat()`，第 60 行。
- 3. 读取一个字节，第 61 行。就我们的目的而言，`safe_read()` 类似于 `read()`；它在第 10.4.4 节“可重启的系统调用”，第 357 页中有解释。
- 4. 使用 `lseek()`  seek 回文件开头，第 62 行。这样做是为了将刚刚读取的字节写回其原位置。
- 5. 写回该字节，第 63 行。`full_write()` 类似于 `write()`；它也在第 10.4.4 节“可重启的系统调用”，第 357 页中有介绍。
- 6. 如果文件大小为零，使用 `ftruncate()` 将其设置为零大小（第 68 行）。这不会改变文件内容，但具有更新访问时间和修改时间的副作用。（`ftruncate()` 在第 4.8 节“设置文件长度”，第 114 页中描述过。）
- 7. 关闭文件，第 69 行。

这些步骤都在一个长的连续测试链中完成，位于 `if` 内部。测试设置得使任何操作失败时，`utime_null()` 返回 -1，就像常规系统调用一样。`errno` 由系统自动设置，供更高层代码使用。

`rpl_utime()` 函数（第 75–82 行）是“替代版 `utime()`”。如果第二个参数不是 `NULL`，则调用真正的 `utime()`。否则，它调用 `utime_null()`。

### 5.5.4 使用 `fchown()` 和 `fchmod()` 进行安全操作

原始的 Unix 系统只有 `chown()` 和 `chmod()` 系统调用。然而，在高负载系统上，这些系统调用容易受到竞态条件的影响，攻击者可以借此安排用不同的文件替换正在更改所有权或权限的文件。

然而，一旦文件被打开，竞态条件就不再是一个问题。程序可以使用 `stat()` 在路径名上获取文件的信息。如果信息符合预期，那么在文件打开后，可以使用 `fstat()` 验证文件是否相同（通过比较“之前”和“之后”的 `struct stat` 结构体中的 `st_dev` 和 `st_ino` 字段）。

一旦程序确认文件是相同的，就可以使用 `fchown()` 或 `fchmod()` 更改所有权或权限。

这些系统调用以及 `lchown()` 都是相对较新的；[11] 较旧的 Unix 系统不会拥有它们，尽管现代的、符合 POSIX 标准的系统拥有它们。

没有对应的 `futime()` 或 `lutime()` 函数。对于 `futime()` 的情况，这（显然）是因为文件时间戳不像所有权和权限那样对系统安全至关重要。没有 `lutime()`，因为对于符号链接，时间戳是不相关的。

## 5.6 摘要

- 用户看到的文件和目录层次结构是一棵以 / 为根的逻辑树。它由一个或多个存储分区组成，每个分区包含一个文件系统。在一个文件系统中，inode 存储关于文件的信息（元数据），包括文件数据块的位置。

- 目录建立文件名和 inode 之间的关联。概念上，目录内容只是 (inode, 名称) 对的序列。文件的每个目录项称为（硬）链接，文件可以有很多链接。硬链接，因为它们仅通过 inode 号工作，必须都在同一个文件系统中。符号（软）链接是指向文件或目录的指针，基于文件名而非 inode 号工作，因此不受限于必须在同一文件系统中。

- 使用 `link()` 创建硬链接，使用 `symlink()` 创建符号链接，使用 `unlink()` 移除链接，使用 `rename()` 重命名文件（可能移动到另一个目录）。文件的数据块不会回收，直到链接计数变为零并且文件最后一个打开的文件描述符被关闭。

- 使用 `mkdir()` 创建目录，使用 `rmdir()` 移除目录；目录在移除前必须是空的（除了 ‘.’ 和 ‘..’ 外没有任何内容）。GNU/Linux 版本的 ISO C `remove()` 函数会根据需要调用 `unlink()` 或 `rmdir()`。

- 使用 `opendir()`、`readdir()`、`rewinddir()` 和 `closedir()` 函数处理目录。`struct dirent` 包含 inode 号以及文件的名称。最大可移植性的代码仅使用 `d_name` 成员中的文件名。用于保存和恢复的

