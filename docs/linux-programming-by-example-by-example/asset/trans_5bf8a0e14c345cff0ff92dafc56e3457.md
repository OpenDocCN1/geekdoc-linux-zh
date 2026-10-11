
/* 关闭文件并退出 */
close(fdsr c);
close(fdnull);
close(fdtmp);

exit(EXIT_SUCCESS);}

该程序打开了三个文件，一个用于读取，两个用于写入。文件 /tmp/foo.bar 相对不那么有趣，但请注意，该程序打开设备文件 /dev/null，就好像它是一个普通文件一样。因此，你应该能够看到，你可以将大多数设备作为文件来处理。适用于普通文件的标准文件处理语义同样适用于设备和其他特殊文件。该程序的另一个特点是，在写入磁盘文件 /tmp/foo.bar 时，它只写入 numbytes 个字符，这防止了空字节被写入文件末尾。在到达文件结尾前的最后一次读取可能不会读满 10 个字节，但写入操作会按照指示写入相应数量的字节。通过仅写入 numbytes，该程序不会在文件末尾追加额外的字符。

## 定位文件指针

如果你希望从文件中的随机位置进行读写，你必须能够确定文件指针的当前位置，并能够将指针定位到特定位置。lseek 调用就是为此目的而设计的工具。它在 <unistd.h> 中的原型如下：

```c
int lseek(int fd, off_t offset, int whence);
```

lseek 根据 whence 的值，将打开在文件描述符 fd 上的文件的文件指针定位到 offset 位置。whence 可以是以下三个常量之一：

- SEEK_SET 将指针设置到文件中的 offset 字节处。
- SEEK_CUR 将指针的位置设置为相对于当前指针位置的文件中的 offset 字节处，offset 可以是负数。
- SEEK_END 将位置设置为距文件末尾 offset 字节处。

在成功时，lseek 返回新的指针位置；出错时返回 off_t 类型的 -1，并相应地设置 errno。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_172_0.png)

## 示例

此示例在将光标定位到文件中的各个位置后，从输入文件中读取 10 个字节。

```c
/*
 * seek.c - 使用 lseek
 */
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

int main(void)
{
  char ftmp[] = "tmpXXXXXX";
  char buf[10];
  int i, infd, outfd;

  /* 打开输入文件 */
  if((infd = open("devices.txt", O_RDONLY)) < 0) {
    perror("open devices.txt");
    exit(EXIT_FAILURE);
  }
  /* 创建用于输出的临时文件 */
  if((outfd = mkstemp(ftmp)) <0) {
    perror("mkstemp");
    exit(EXIT_FAILURE);
  }
  fprintf(stdout, "Output file is %s\n", ftmp);

  /* 设置文件中的初始位置 */
  lseek(infd, 100, SEEK_SET);
  /*
  * 将每 100 字节中的前 10 个字节
  * 复制到输出文件
  */
  for(i = 0; i < 10; ++i) {
    read(infd, buf, 10);
    write(outfd, buf, 10);
    lseek(infd, 90, SEEK_CUR); /* 向前跳转 90 字节 */
  }
  close (infd);
  close (outfd);
  exit (EXIT_SUCCESS);
}
```

输入文件 devices.txt 包含在本书网站本章的源代码目录中。为了避免硬编码输出文件名，该程序使用 mkstemp 调用在当前目录中打开一个具有唯一名称的文件。在将文件指针设置在文件中的第 100 字节处之后，程序然后读取 10 个字节，将它们写入输出文件，然后再向前搜索 90 个字节。输出文件的名称每次运行时会不同。一次测试运行产生了以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_174_0.png)

**输出**

```
$ ./seek
output file is ttmpjtQXQN
$ cat ttmpjtQXQN
sed: Augusnumbers an included om
ftp://fteX versionunix Files/linux-stanly.        Alloc in the puributed wi
```

**截断文件**

显然，要延长文件，你只需要向其中写入更多数据或 lseek 越过末尾。那么，你如何截断文件呢？当然，使用 truncate 或 ftruncate 调用。它们在 <unistd.h> 中声明，原型如下：

```
int truncate (const char *pathname, off_t length);
int ftruncate (int fd, off_t length);
```

这两个调用都将它们的文件（pathname 或 fd）缩短到 length 长度，成功时返回 0。请记住，许多文件 I/O 系统调用有两种形式，一种接受标准的空终止字符串（truncate），另一种以 f_ 为前缀，接受文件描述符而不是路径名（ftruncate）。如果发生错误，它们返回 -1 并设置 errno。如果你使用 ftruncate，文件必须以写入模式打开。

为什么你想使用这些调用之一来缩短文件？一个典型的原因是删除文件末尾不需要保留的数据，同时保留文件的其余部分。将文件截断到所需长度比创建新文件、从旧文件中读取想要的数据、将其写入新文件，然后删除旧文件要简单得多。单一的 truncate 或 ftruncate 调用取代了至少四个调用：一个 open、一个 read、一个 write 和一个 unlink。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_175_0.png)

### 示例

接下来的 `trunc` 程序是一个缩短文件的实用工具。它期望在命令行上依次传入要缩短的文件名和新长度。

```c
/*
 * trunc.c - 将命名文件缩短到指定长度：
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>

int main(int argc, char **argv)
{
    long len;

    if (argc != 3)
        exit(EXIT_FAILURE);
    len = (long) strtol(argv[2], NULL, 10);
    if (truncate(argv[1], len)) {
        perror ("truncate");
        exit(EXIT_FAILURE);
    }

    exit(EXIT_SUCCESS);
}
```

在当前目录下对 `test.txt` 运行此程序产生了以下结果：

![](img/be588b36b489136ce784030a08a1d3d4_175_1.png)

**输出**

```
$ ls -l test.txt
-rw-r--r-- 1 kwall users 56561 Jul 24 15:56 test.txt
$ trunc test.txt 2000
$ ls -l test.txt
-rw-r--r-- 1 kwall users 2000 Jul 24 15:58 test.txt
```

在确认传入了两个参数后，`trunc` 使用 `strtol` 将传入的长度参数从字符串转换为 long 型。然后它立即使用传入的文件名和请求的长度调用 `truncate`。如果 `truncate` 调用失败，程序打印错误消息并退出。如果成功，程序安静退出，向操作系统返回零。

虽然功能上可行，但 `trunc` 程序还不够健壮，因为它假设收到的参数是有效的。生产质量的程序应该确认命中的文件存在，并且传入的文件名是有效的文件名。为了简洁起见，忽略了这些元素。

## 获取文件信息

现在，你可以打开、关闭、读取、写入和截断文件了。然而，你可以获取关于文件的许多有趣信息，正如 `stat (1)` 命令所示：

![](img/be588b36b489136ce784030a08a1d3d4_176_0.png)

### 输出

```
$ stat trunc.c

File: "trunc.c"

Size: 420
Filetype: Regular File

Mode: (0644/-rw-r--r--)

Uid: (500/kwall)

Gid: (100/users)

Device: 3,2

Inode: 534555

Links: 1

Access: Sat Jul 24 16:02:50 1999(00000.00:15:56)

Modify: Sat Jul 24 16:04:29 1999(00000.00:14:17)

Change: Sat Jul 24 16:04:29 1999(00000.00:14:17)
```

`stat` 命令从文件的信息节点（称为 inode）中读取信息，并将其显示给用户。虽然它们的细节超出了本书的范围，但*inode* 是内核为文件系统中的每个文件维护的数据结构。除了其他内容，它们包含诸如文件名称、大小、所有权、最后修改、访问和更改日期、类型以及指向它的符号链接数量等信息。示例中的 `stat` 列出了所有这些详细信息。

获取此信息有三种方法：`stat`、`lstat` 和 `fstat`。要使用它们，必须在代码中包含 `<sys/stat.h>` 和 `<unistd.h>`。它们的原型如下：

```c
int stat(const char *filename, struct stat *buf);

int fstat(int fd, struct stat *buf);

int lstat(const char *filename, struct stat *buf);
```

所有的 `stat` 函数都会用指定由 `filename` 或文件描述符 `fd` 的文件的信息来填充 `buf`。成功时，它们返回 `0`；如果发生错误，它们返回 `-1` 并设置 `errno`。它们之间唯一的实际区别在于 `lstat` 不跟随符号链接，而 `stat` 和 `fstat` 会跟随。`stat` 结构的定义如下：

