
```c
/*
 * process --- do something with the file, in this case,
 *             send it to stdout (fd 1).
 *             Returns 0 if all OK, 1 otherwise.
 */

int
process(char *file)
{
    int fd;
    size_t rcount, wcount;
    char buffer[BUFSIZ];
    int errors = 0;

    if (strcmp(file, "-") == 0)
        fd = 0;
    else if ((fd = open(file, O_RDONLY)) < 0) {
        fprintf(stderr, "%s: %s: cannot open for reading: %s\n",
                myname, file, strerror(errno));
        return 1;
    }
```

缓冲区 `buffer`（第 47 行）的大小为 `BUFSIZ`；`<stdio.h>` 将该常量定义为 I/O 的“最优”块大小。虽然 `BUFSIZ` 的值在不同系统中有所不同，但使用此常量的代码是干净且可移植的。

该例程的核心是以下循环，它反复读取数据，直到遇到文件末尾或错误为止：

```c
while ((rcount = read(fd, buffer, sizeof buffer)) > 0) {
    wcount = write(1, buffer, rcount);
    if (wcount != rcount) {
        fprintf(stderr, "%s: write error: %s\n",
                myname, file, strerror(errno));
        errors++;
        break;
    }
}
```

第 45 行中的 `rcount` 和 `wcount` 变量的类型为 `ssize_t`，即“有符号的 size_t”，这使得它们能够存储负值。请注意，传递给 `write()` 的计数值是 `read()` 的返回值（第 59 行）。虽然我们希望能够读取固定大小为 `BUFSIZ` 的块，但文件本身的大小不太可能是 `BUFSIZ` 字节的整数倍。当从文件中读取最后一个较小的字节块时，返回值指示 `buffer` 中有多少字节接收了新数据。只有这些字节应复制到标准输出，而不是整个缓冲区。

第 60 行的测试 `wcount != rcount` 是检查写入错误的正确方法；如果只有部分（而非全部）数据被写入，那么 `wcount` 将是正数但小于 `rcount`。

最后，`process()` 检查读取错误（第 68–72 行），然后尝试关闭文件。在（不太可能的）`close()` 失败（第 75 行）的情况下，它会打印一条错误消息。在这个程序中避免关闭标准输入并非严格必要，但在编写更大的程序时，养成这种习惯是有益的，以防其他代码希望对其进行某种操作或子程序继承它。最后一行语句（第 82 行）如果有错误则返回 1，否则返回 0。

```c
if (rcount < 0) {
    fprintf(stderr, "%s: %s: read error: %s\n",
            myname, file, strerror(errno));
    errors++;
}
if (fd != 0) {
    if (close(fd) < 0) {
        fprintf(stderr, "%s: %s: close error: %s\n",
                myname, file, strerror(errno));
        errors++;
    }
}
return (errors != 0);
}
```

`ch04-cat` 对每个系统调用都进行了错误检查。虽然这很繁琐，但它提供了健壮性（或至少是清晰度）：当出现问题时，`ch04-cat` 会打印一条尽可能具体的错误消息。`errno` 和 `strerror()` 的组合使这变得轻而易举。这就是 `ch04-cat` 的全部内容，只有 88 行代码！

总之，有几点需要理解关于 Unix I/O：

- **I/O 是非解释性的。**

  I/O 系统调用仅仅移动字节。它们不对数据进行任何解释；所有的解释工作都由用户级程序负责。这使得读取和写入二进制结构与读取和写入文本行一样容易（实际上更容易，尽管使用二进制数据会引入可移植性问题）。

- **I/O 是灵活的。**

  你可以一次读取或写入任意数量的字节。你甚至可以一次读取和写入一个字节，尽管对于大量数据来说，这样做的成本比以大块方式操作要高。

- **I/O 是简单的。**

  三值返回机制（负数表示错误，零表示文件结束，正数表示计数）使编程变得直接且显而易见。

- **I/O 可能是部分完成的。**

  `read()` 和 `write()` 都可能传输比请求少字节数。应用程序代码（即你的代码）必须始终意识到这一点。

#### 4.4.4 示例：Unix cat

正如承诺的那样，这里是 V7 版本的 cat。[^1] 它首先检查选项。V7 版本的 cat 接受一个选项 `-u`，用于执行无缓冲输出。

基本设计与上面所示的类似；它遍历由命令行参数指定的文件，逐个字符读取每个文件，并将字符发送到标准输出。与我们的版本不同，它使用了 `<stdio.h>` 的功能。在很多方面，使用标准 I/O 库的代码更容易阅读和编写，因为所有缓冲问题都由库隐藏了。
