
```c
fpos_t file_pos;
...
/* 获取目标位置 */
fgetpos( fin, &file_pos );
...
rewind( fin );
/* 返回到目标位置 */
fsetpos( fin, &file_pos );
```

# 168 GNU/Linux 应用程序编程

建议使用 `fgetpos` 和 `fsetpos` API 代替 `ftell` 和 `seek` 方法。因为 `ftell` 和 `seek` 方法没有抽象机制的细节，`fgetpos` 和 `fsetpos` 函数在未来较可能被废弃。

## 基础 API

`open`、`read` 和 `write` 函数也可以用于文件 I/O。虽然 API 略有不同，但本节还查看了如何通过 `fdopen` 在文件模式和流模式之间切换。

> 这些函数被称为基础 API，因为它们是标准 I/O 库构建的平台。

`open` 函数允许你打开或创建一个新文件。提供了两种变体，其 API 如下：

```c
int open(const char *pathname, int flags);
int open(const char *pathname, int flags, mode_t mode);
```

`pathname` 参数定义了要打开或创建的文件（带路径，例如 `temp.txt` 或 `/tmp/file.txt`）。`flags` 参数是 `O_RDONLY`、`O_WRONLY` 或 `O_RDWR` 之一。根据 `open` 用的需要，表 11.3 所示的一个或多个标志也可能通过按或（位或操作）组合。

表 11.3 `open` 函数的附加标志

| 标志 | 描述 |
| --- | --- |
| `O_CREAT` | 如果文件不存在则创建该文件。 |
| `O_EXCL` | 与 `O_CREAT` 使用，如果文件已存在则返回错误；否则创建文件。 |
| `O_NOCTTY` | 如果文件描述符指向 TTY 设备，此进程将不会成为控制终端。 |
| `O_TRUNC` | 截断文件（如果存在）并将长度重置为零，允许写入权限。 |
| `O_APPEND` | 在每次写入之前，将文件指针重新定位到文件末尾。 |
| `O_NONBLOCK` | 以非阻塞模式打开文件。对文件的操作不会阻塞（如读、写等）。 |
| `O_SYNC` | `write` 函数将被阻塞，直到数据写入物理设备。 |
| `O_NOFOLLOW` | 失败跟踪符号链接。 |
| `O_DIRECTORY` | 如果正在打开的文件不是目录，则打开失败。 |
| `O_DIRECT` | 尝试通过直接对用户空间缓冲区进行 I/O 来尽量减少缓存影响（与 `O_SYNC` 一样同步同步）。 |
| `O_ASYNC` | 当文件描述符的输入或输出可用数据时请求发送信号。 |
| `O_LARGEFILE` | 在 32 位系统上请求打开大文件系统，其大小无法用 32 位表示。 |

第二个实例的第三个参数是模式。该模式定义了创建文件时使用的权限（仅当带有 `O_CREAT` 标志时）。表 11.4 列出了可以按或组合的可能符号常量。

# 表 11.4 `open` 系统调用的模式参数

| 常量 | 用途 |
|---|---|
| `S_IRWXU` | 用户具有读/写/执行权限。 |
| `S_IREAD` | 用户具有读取权限。 |
| `S_IWITE` | 用户具有写入权限。 |
| `S_IEXEC` | 用户具有执行权限。 |
| `S_IRWXG` | 组具有读/写/执行权限。 |
| `S_IRGRP` | 组具有读取权限。 |
| `S_IWGRP` | 组具有写入权限。 |
| `S_IXGRP` | 组具有执行权限。 |
| `S_IRXO` | 其他人具有读取权限。 |
| `S_IWOTH` | 其他人具有写入权限。 |
| `S_IROTH` | 其他人具有读取权限。 |
| `S_IXOTH` | 其他人具有执行权限。 |

# 第11章 GNU/Linux 中的文件处理 169
