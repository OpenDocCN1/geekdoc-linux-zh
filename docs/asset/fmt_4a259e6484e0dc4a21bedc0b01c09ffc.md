
```c
        stats[entryIndex].thisCycle = TRUE; /* 更新状态数组 */

}

/*****************************************************************/

findEntry(fileName)

char* fileName;

/* 定位状态数组中命名文件的索引 * */

{

    int i;

    for (i = 0; i < MAX_FILES; i++)

        if (stats[i].lastCycle &&

          strcmp(stats[i].fileName, fileName) == 0)

            return (i);

    return (NOT_FOUND);

}

/*****************************************************************/

addEntry(fileName, statBuf)

char* fileName;

struct stat* statBuf;

/* 向状态数组中添加新条目 */

{

    int index;

    index = nextFree(); /* 查找下一个空闲条目 */

    if (index == NOT_FOUND)

        return (NOT_FOUND); /* 无剩余空间 */

    strcpy(stats[index].fileName, fileName); /* 添加文件名 */

    stats[index].status = *statBuf; /* 添加状态信息 */

    printf("ADDED"); /* 通知标准输出 */

    printEntry(index); /* 显示状态信息 */

    return(index);

}

/*****************************************************************/

nextFree ()

/* 返回状态数组中的下一个空闲索引 */

{

    int i = 0;

    for (i = 0; i < MAX_FILES; i++)

        if (!stats[i].lastCycle && !stats[i].thisCycle)

            return (i);

    return (NOT_FOUND);

}

/*****************************************************************/

updateEntry(index, statBuf)

int index;

struct stat* statBuf;

/* 如果文件被修改，则显示信息 */

{

    if (stats[index].status.st_mtime != statBuf->st_mtime)

    {

        stats[index].status = *statBuf; /* 存储 stat 信息 */

        printf("CHANGED"); /* 通知标准输出 */

        printEntry(index);

    }

}

/*****************************************************************/

printEntry(index)

int index;

/* 显示状态数组的一个条目 */

{

    printf("%s", stats[index].fileName);

    printStat(&stats[index].status);

}

/*****************************************************************/

printStat(statBuf)

struct stat* statBuf;

/* 显示状态缓冲区 */

{

    printf("size %lu bytes, time = %s", statBuf->st_size,

           ctime(localtime(&statBuf->st_mtime)));

}

/*****************************************************************/

fatalError ()

{

    perror("monitor: ");

    exit (/* EXIT_FAILURE */ 1);

}
```

## 12.3.14 获取文件信息：`stat()`

`monitor` 通过调用 `stat()` 获取其文件信息（图 12–18）。

### 系统调用：`int stat (const char* name, struct stat* buf)`

```c
int lstat (const char* name, struct stat* buf)
int stat (int fd, struct stat* buf)
```

`stat()` 填充缓冲区。`stat` 结构定义在 `/usr/include/stat.h`。`lstat()` 返回关于符号链接的信息而非其引用的文件。`stat()` 的功能与 `stat()` 相同，只是它将要状态的文件描述符作为第一个参数。`stat` 结构包含以下成员：

| 名称 | 含义 |
|--- |--- |
| `st_dev` | 设备号 |
| `st_ino` | 节点号 (inode) |
| `st_mode` | 权限标志 |
| `st_nlink` | 硬链接数 |
| `st_uid` | 用户 ID |
| `st_gid` | 组 ID |
| `st_size` | 文件大小 |
| `st_atime` | 上次访问时间 |
| `st_mtime` | 最后修改时间 |
| `st_ctime` | 最后状态更改时间 |

在 `/usr/include/stat.h` 中定义了一些预定义宏，这些宏以 `st_mode` 为参数，并对以下文件类型返回真（1）：

| 宏 | 对于以下文件类型返回真 |
|--- |--- |
| `S_ISDIR` | 目录 |
| `S_ISCHR` | 字符设备特殊设备 |
| `S_ISBLK` | 块设备特殊设备 |
| `S_ISREG` | 普通文件 |
| `S_ISFIFO` | 管道 (pipe) |

时间字段使用标准 库的 `asctime()` 和 `localtime()` 子程序进行解码。

`stat()` 和 `fstat()` 成功时返回 0，否则返回 -1。

图 12–18 `stat()` 系统调用描述。

## 12.3.16 杂项文件管理系统调用

下面是对后续杂项文件管理系统用的简要描述（图 12-20）。

| 名称 | 功能 |
| --- | --- |
| `chown` | 更改文件的所有者和或组。 |
| `chmod` | 更改文件的权限设置。 |
| `dup` | 复制文件描述符。 |
| `dup2` | 与 `dup` 类似。 |
| `fchown` | 功能与 `chown` 相同。 |
| `fchmod` | 功能与 `chmod` 相同。 |
| `fcntl` | 访问各种文件特性。 |
| `truncate` | 功能与 `truncate` 相同。 |
| `ioctl` | 控制设备。 |
| `link` | 创建硬链接。 |
| `mknod` | 创建特殊文件。 |
| `sync` | 调度所有文件缓冲区写入磁盘。 |
| `truncate` | 截断文件。 |

**图 12–20** Linux 文件管理系统调用。

## 12.3.17 更改文件的所有者和/或组：`chown()`

`chown()` 更改文件的所有者和/或组（图 12–21）。

```
System call: int chown (const char* fileName, uid_t ownerId, gid_t groupId)
int chown (const char* fileName, uid_t ownerId, gid_t groupId)
int fchown (int fd, uid_t ownerId, gid_t groupId)
```
