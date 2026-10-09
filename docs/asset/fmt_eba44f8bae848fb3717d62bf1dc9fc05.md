
`st_dev` 字段包含文件所在硬件设备的主设备和次设备号。设备号在第 6 章中进行了讨论。主设备号左移 8 位；次设备号占用低位。`st_ino` 字段包含该文件的 `inode` 号（节点号）。这在文件系统中定位该文件。

## 附录 B 低层 I/O

如果你对符号链接进行调用，`stat` 会跟随该链接，你可以获取链接所指向的文件信息，而不是链接本身的信息。这意味着对于 `stat` 的结果，`S_ISNK` 永远为假。如果你不想跟随符号链接，请使用 `lstat` 函数；该函数获取链接本身的信息，而不是链接的目标。如果你对非符号链接的文件调用 `lstat`，其效果等同于 `stat`。对断开的链接（指向不存在或不可访问目标的链接）进行调用会导致错误，而对这种链接调用 `lstat` 则不会。

如果你已经有一个文件描述符作为第一个参数进行读或写操作，请调用 `fstat` 而不是 `stat`。列表 B.6 展示了一个函数，它分配一个足够容纳文件内容的缓冲区，然后将其读入。该函数使用 `fstat` 来确定需要分配的缓冲区大小，并检查该文件确实是一个普通文件。

### 列表 B.6 (read_file.c) 将文件读入缓冲区

```c
#include <fcntl.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
```

```c
/* 将内容读入新分配的缓冲区。

缓冲存的大小存储在 LENGTH 中。返回缓冲区，

调用者必须释放它。如果 FILENAME 不对应于

普通文件，则返回 NULL。 */

char* read_file(const char* filename, size_t* length)

{

    int fd;

    struct stat file_info;

    char* buffer;

    /* 打开文件。 */

    fd = open(filename, O_RDONLY);

    /* 获取文件信息。 */

    fstat(fd, &file_info);

    *length = file_info.st_size;

    /* 确保文件是一个普通文件。 */

    if (!S_ISREG(file_info.st_mode)) {

        /* 如果不是，则放弃。 */

        close(fd);

        return NULL;

    }

    /* 分配一个足够容纳文件内容的缓冲区。 */

    buffer = (char*) malloc(length);

    /* 将文件读入缓冲区。 */

    read(fd, buffer, length);

    /* 完成工作。 */

    close(fd);

    return buffer;

}
```

## B.3 向量读写

`write` 调用接受的参数是指向数据缓冲区起始位置指针以及该缓冲区的长度。它将连续的内存区域写入文件描述符。`writev` 调用允许你在单次操作中写入多个不连续的内存区域，这比多次调用 `write` 效率更高。

### 列表 B.7 (write-args.c) 使用 writev 将参数列表写入文件

```c
#include <fcntl.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <sys/uio.h>
#include <unistd.h>

int main (int argc, char * argv[])
{
    int fd;

    struct iovec *vec;

    struct iovec *vec_next;

    int i;

    /* 我们需要一个包含换行符的'buffer'。使用
       普通的字符变量来实现。 */

    char newline = '\n';

    /* 第一个命令行参数是输出文件名。 */

    char * filename = argv[1];

    /* 跳过参数列表的前两个元素。元素
       0 是程序的名称，元素 1 是输出
       文件名。 */

    argc = 2;

    argv = 2;

    /* 分配一个 iovec 元素数组。参数列表中的
       每个元素我们需要两个，一个用于文本本身，
       一个用于换行符。 */

    vec = (struct iovec *) malloc(2 * argc * sizeof(struct iovec));

    /* 遍历参数列表，构建 iovec 条目。 */

    vec_next = vec;

    for (i = 0; i < argc; i++) {
        /* 第一个元素是参数本身的文本。 */

        vec_next->iov_base = argv[i];

        vec_next->iov_len = strlen(argv[i]);

        ++vec_next;

        /* 第二个元素是单个换行符。struct iovec
           数组中的多个元素指向同一内存区域           是允许的。 */

        vec_next->iov_base = &newline;

        vec_next->iov_len = 1;

        ++vec_next;
    }

    /* 将参数写入文件。 */

    fd = open(filename, O_WRONLY | O_CREAT);

    writev(fd, vec, 2 * argc);

    free(vec);

    close(fd);

    return 0;
}
```

## B.4 与标准C库 I/O 函数的关系

这里是运行 `write-args` 的示例。

```
% ./write-args outputfile "first arg" "second arg" "third arg"
% cat outputfile
first arg
second arg
third arg
```

Linux 提供了一个相应的函数 `readv`，它可以在单次操作中将数据读取到多个不连续的内存区域。与 `writev` 类似，一个 `iovec` 元素数组指定了将从文件描述符读取数据的内存区域。

我们之前提到过，标准 C 库 I/O 函数是在这些低级 I/O 函数之上实现的。有时，结合文件描述符使用标准库函数是困难的，或者在标准库的 `FILE*` 流上使用低级 I/O 函数也很困难。GNU/Linux 允许你同时完成这两者。

如果你使用 `fopen` 打开了一个文件，可以使用 `fileno` 函数获取底层的文件描述符。该函数接受一个 `FILE*` 参数并返回文件描述符。例如，为了使用标准库的 `open` 调用打开文件但使用 `writev` 写入，你可以使用以下代码：

```c
FILE* stream = fopen (filename, "w");

int file_descriptor = fileno (stream);

write (file_descriptor, vector, vector_length);
```

注意 `stream` 和 `file_descriptor` 对应于同一个打开的文件。如果你调用了这一行，你可能无法再向 `file_descriptor` 写入：

```c
close (stream);
```

同样，如果你调用了这一行，你可能无法再向 `stream` 写入：

```c
close (file_descriptor);
```

要进行反向操作，即从文件描述符到流，请使用 `fdopen` 函数。它会构造一个与文件描述符对应的 `FILE*` 流指针。`fdopen` 函数接受一个文件描述符参数和一个指定创建流的模式的字符串参数。模式参数的语法与 `fopen` 的第二个参数相同，并且必须与文件描述符兼容。例如，为读文件描述符指定模式 `r`，或为写文件描述符指定模式 `w`。

与 `fclose` 一样，流和文件描述符指向同一个打开的文件，因此如果你关闭了其中一个，可能就无法再使用另一个。

## B.5 其他文件操作

一些其他对文件和目录的操作也很有用：

- `getcwd` 获取当前工作目录。它接受两个参数：一个 `char` 缓冲区和缓冲区长度。它将当前工作目录的路径拷贝到缓冲区中。
- `chdir` 将当前工作目录更改为参数提供的路径。
- `mkdir` 创建新目录。它的第一个参数是新目录的路径。第二个参数是用于新文件的访问权限。权限的解释与 `open` 调用的第三个参数相同，并会被进程的 `umask` 修改。
- `rmdir` 删除目录。它的参数是目录的路径。
- `unlink` 删除文件。它的参数是文件的路径。此调用也可用于删除其他文件系统对象，例如命名管道（"FIFOs"）或设备（见第 6 章）。实际上，`unlink` 并不一定删除文件的内容。正如其名所示，它将文件从包含它的目录中取消链接。该文件不再列在目录中，但如果有任何进程持有该文件的打开文件描述符，文件的内容就不会从磁盘中移除。因此，如果一个进程打开一个文件进行读写，然后第二个进程 `unlink` 了该文件并创建一个同名的新文件，第一个进程将看到文件的旧内容而不是新内容（除非它关闭文件并重新打开）。
- `rename` 重命名或移动文件。它的两个参数是文件的旧路径和新路径。如果路径在不同的目录中，`rename` 会移动文件，只要它们都在同一个文件系统上。你也可以使用 `rename` 移动目录或其他文件系统对象。

## B.6 读取目录内容

GNU/Linux 提供了读取目录内容的函数。虽然这些与本附录描述的低级 I/O 函数没有直接关系，但我们仍然在这里展示了它们，因为它们在应用程序中经常有用。

要读取目录内容，请遵循以下步骤：

1. 调用 `opendir`，传递要检查的目录路径。`opendir` 返回一个 `DIR*` 句柄，你用它访问目录内容。如果发生错误，调用返回 `NULL`。
2. 重复调用 `readdir`，传递从 `opendir` 获取的 `DIR*` 句柄。每次调用 `readdir` 时，它都会返回一个指向下一个目录条目的 `struct dirent` 实例的指针。当到达目录末尾时，`readdir` 返回 `NULL`。从 `readdir` 获取的 `struct dirent` 有一个字段 `d_name`，它包含目录条目的名称。
3. 调用 `closedir` 并传递 `DIR*` 句柄，结束目录列表操作。

如果你在程序中使用这些函数，请包含 `<sys/types.h>` 和 `<dirent.h>`。注意，如果你需要按特定顺序排列目录内容，必须自己进行排序。

列表 B.8 中的程序打印目录内容。可以在命令行指定目录，但如果没有指定，程序将使用当前目录。对于目录中的每个条目，它会显示类型和路径。

### 列表 B.8 打印列表

```c
#include <assert.h>
#include <dirent.h>
#include <stdio.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>

/* 返回描述文件类型的字符串 */

const char* get_type(const char* path) {
    struct stat st;
    stat(path, &st);
    if (S_ISLNK(st.st_mode))
        return "symbolic link";
    else if (S_ISDIR(st.st_mode))
        return "directory";
    else if (S_ISCHR(st.st_mode))
        return "character device";
    else if (S_ISBLK(st.st_mode))
        return "block device";
    else if (S_ISFIFO(st.st_mode))
        return "fifo";
    else if (S_ISSOCK(st.st_mode))
        return "socket";
    else if (S_ISREG(st.st_mode))
        return "regular file";
    else
        return "unknown";
}

int main(int argc, char *argv[]) {
    char *dir_path;
    DIR *dir;
    struct dirent *entry;
    char entry_path[PATH_MAX];
    size_t path_len = 2;

    /* 在命令行上指定了目录，使用它 */
    if (argc >= 2) {
        dir_path = argv[1];
    } else {
        /* 否则，使用当前目录 */
        dir_path = ".";
    }

    /* 将目录路径拷贝到 entry_path */
    strncpy(entry_path, dir_path, sizeof(entry_path));
    path_len = strlen(entry_path);

    /* 如果路径不以斜杠结尾，添加一个 */
    if (entry_path[path_len-1] != '/') {
        entry_path[path_len] = '/';
        entry_path[path_len+1] = '\0';
    }
    path_len++;

    /* 开始对指定的目录列表 */
    dir = opendir(dir_path);

    /* 遍历所有目录条目 */
    while ((entry = readdir(dir)) != NULL) {
        /* 通过拼接名称构建条目的路径 */
        strncpy(entry_path + path_len, entry->d_name, sizeof(entry_path) - path_len);

        /* 确定条目的类型 */
        const char *type = get_type(entry_path);

        /* 打印条目的类型和路径 */
        printf("%-18s: %s\n", type, entry_path);
    }

    /* 全部完成 */
    closedir(dir);

    return 0;
}
```

这里列出 `/dev` 目录的前几行输出。（你的输出可能略有不同。）

```
% ./listdir /dev

total 124

drwxr-xr-x 7 root root 36864 Feb 1 15:14 .

drwxr-xr-x 22 root root 4096 Oct 11 16:39 ..

crw-rw-rw- 1 root root - Dec 10 01:31:3 log

crw-rw-rw- 1 root root 1, 3 May 1998 null

-rw-rw--x 1 root root 26689 Mar 2 2000 MAKEDEV

prw------- 1 root root 0 Dec 11 18:37 initctl

crw-rw-rw- 1 root root 10, 175 Feb 3 2000 agpgart

...
```

`ls` 输出中每行的第一个字符表示条目的类型。

## 信号列表

表 C.1 列出了你最可能遇到或使用的 Linux 信号。请注意，某些信号具有多种解释，具体取决于它们发生的位置。

此处列出的信号名称被定义为预处理器宏。要在你的程序中使用它们，请包含 `<usr/include/sys/signal.h>`，该文件是 `<signal.h>` 的一部分。

要获取 Linux 信号的完整列表（包括每个信号的简要描述以及信号传递时的默认行为），请通过以下命令查看第 7 节的帮助页：

```
% man 7 signal
```
