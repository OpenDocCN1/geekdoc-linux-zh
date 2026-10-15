
创建一个名为 `tty1` 的 `/dev` 条目。这是一个主号为 4、次号为 65 的字符设备。这里没有引用设备。我们通过 `mknod` 只是在文件系统中创建了一个条目。

### 底层 I/O API

离设备驱动程序最近的用户空间系统函数集被称为“底层 I/O”。对于本章处理的设备类型，I/O 可能是最有用的。对于通用文件传输，“流” I/O 包更有意义。图 6-2 显示了底层 I/O API 的基本元素。

- `OPEN`。在调用进程和文件设备之间建立连接；`path` 是要打开的目录条目；`flags` 是指定访问模式的位集标志，且必须包含以下之一：
  - `O_RDONLY` 以读模式打开。
  - `O_WRONLY` 以写模式打开。
  - `O_RDWR` 以读写模式打开。
  此外，`flags` 可能包含以下模式的一个或多个：
  - `O_APPEND` 将写入的数据放在文件末尾。
  - `O_TRUNC` 将文件长度置为零；丢弃现有内容。
  - `O_CREAT` 如果需要则创建文件。需要调用带有三个参数的函数，其中 `mode` 是初始权限。

如果 `OPEN` 成功，它将返回一个表示“文件描述符”的非负整数。该值随后被用于所有后续 I/O 操作，以识别这一特定的连接。

- `READ` 和 `WRITE`。这些函数在进程与文件或设备之间传输数据；`file` 是 `OPEN` 返回的文件描述符；`buf` 是指向要传输数据的指针，`count` 是 `buf` 以字节为单位的大小。如果返回值为非负，则它是实际传输的字节数，可能小于 `count`。

- `CLOSE`。当进程完成某个特定设备或文件时，它关闭连接，这会使文件描述符失效并释放供其他进程/文件连接使用的任何资源。关闭任何不需要的是一个良好的习惯，因为可用的文件描述符数量通常是有限的：

### 用于嵌入式和实时应用的 Linux

- `IOCTL`：这是处理特定设备特性的“逃生口”。例如，串口具有波特率，并可能连接了调制解调器。控制这些功能的方式是特定于设备的。因此，每个设备驱动程序都可以为 `IOCTL` 函数建立自己的协议。

```c
int open (const char *path, int flags);

int open (const char *path, int flags, mode_t mode);

size_t read (int filedes, void *buf, size_t count);

size_t write (int filedes, void *buf, size_t count);

int close (int filedes);

int ioctl (int filedes, int cmd, ...);
```
