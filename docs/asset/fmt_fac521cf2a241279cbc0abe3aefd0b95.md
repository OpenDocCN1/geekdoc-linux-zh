
# 41

`parseCommandLine(argc, argv)`

`int argc;`

`char *argv[];`

/* * 解析命令行参数 */

```c
int i;
{
  for (i = 1; i < argc; i++)
  {
    if(argv[i][0] == '-')
      processOptions(argv[i]);
    else if (fileName == NULL)
      fileName= argv[i];
    else
      usageError (); /* 发生错误 */
  }
  standardInput = (fileName == NULL);
}
```

/********************************************************************************/

`processOptions(char* str)`

{
  `char* str;`
  /* 解析选项 */
  `int j;`
  for (j= 1; str[j] != NULL; j++)
  {
    switch(str[j]) /* 根据命令行标志进行切换 */
    {
      case 'c':
        charOption = TRUE;
        break;
      default:
        usageError ();
        break;
    }
  }
}

/********************************************************************************/

`usageError ()`

{
  `fprintf(stderr, "Usage: reverse -c [filename]\n");`
  `exit (/* EXIT_FAILURE */ 1);`
}

# 442 第 13 章 系统编程

```c
/************************************************************************/
`pass1 ()`

/* 对文件进行第一次扫描 */

{
    `int tmpfd, charsRead, charsWritten;`
    `char buffer [BUFFER_SIZE];`

    if (standardInput) /* 从标准输入读取 */
    {
        fd = STDIN;
        sprintf(tmpName, ".rev%d", getpid()); /* 随机名称 */
        /* 创建临时文件来存储输入的拷贝 */
        tmpfd = open (tmpName, O_CREAT | O_RDWR, 0600);
        if (tmpfd == -1) fatalError ();
    }
else /* 打开命名文件读取 */
{
    fd = open (fileName, O_RDONLY);
    if (fd == -1) fatalError ();
}

lineStart[0] = 0; /* 第一行的偏移量 */

while (TRUE) /* 读取所有输入 */
{
    /* 填充缓冲区 */
    charsRead = read (fd, buffer, BUFFER_SIZE);
    if (charsRead == 0) break; /* 结束 */
    if (charsRead == -1) fatalError (); /* 错误 */
    tracklines(buffer, charsRead); /* 处理行 */
    /* 如果从标准输入读取，则拷贝到临时文件 */
    if (standardInput)
    {
        charsWritten = write (tmpfd, buffer, charsRead);
        if (charsWritten != charsRead) fatalError ();
    }
}

    /* 存储尾行的偏移量，如果存在 */
    lineStart[lineCount + 1] = fileOffset;
    /* 如果从标准输入读取，为第二遍扫描准备 fd */
    if (standardInput) fd = tmpfd;
}
```

```c
`trackLines (buffer, charsRead)`

{
  `char* buffer;`
  `int charsRead;`

  /* 在缓冲区中存储每行的偏移量 */
{
  `int i;`
  for (i = 0; i < charsRead; i++)
  {
    ++fileOffset; /* 更新当前位置 */
    if (buffer[i] == '\n') lineStart[++lineCount] = fileOffset;
  }
}
```

/**************************************************/

`int pass2()`

/* 再次扫描输入文件，反向显示行 */

{
  `int i;`
  for (i = lineCount - 1; i >= 0; i--)
    processLine(i);
  close(fd); /* 关闭文件 */
  if (standardInput) unlink(tmpName); /* 删除文件 */
}

/**************************************************/

`int processLine (i)`

{
  `int i;`
  `int charsRead;`
  `char buffer[BUFFER_SIZE];`

  /* 读取指定行 */
  lseek(fd, lineStart[i], SEEK_SET);
  charsRead = read(fd, buffer, BUFFER_SIZE);
  buffer[charsRead] = '\0';

  /* 反序打印字符 */
  for (i = charsRead - 1; i >= 0; i--)
    putchar(buffer[i]);
  putchar('\n');
}
# 444 第 13 章 系统编程

## 打开文件：`open ()`

`open()` 允许你打开或创建一个文件进行读取或写入，一个路径。`reverse -c [filename]` 选项通过执行 `open()` 来设置各种标志：

- 如果 `reverse` 从标准输入读取，将创建一个具有所有者读写权限的临时文件（0600）。在第一遍扫描期间，文件描述符 `fd` 为零。
- 如果 `reverse` 读取命名文件，将以只读模式打开文件。在第二遍扫描中使用 `fd`。

每个操作都使用 `open()` 系统调用；详情见图 13.10。

`系统调用：int open(char* fileName, int mode, permissions)`

`open()` 允许你打开或创建一个文件进行读取或写入，一个绝对或相对路径。`mode` 是读写标志或某些杂项标志的位或，`permissions` 是仅在创建文件时提供的权限标志值，通常使用第 2 章描述的进制编码。`permissions` 值受进程 `umask` 值的影响（见第 4 章）。预定义的读写和杂项标志定义在 `/usr/include/fcntl.h` 中。读写标志如下：

| 标志 | 含义 |
| :--- | :--- |
