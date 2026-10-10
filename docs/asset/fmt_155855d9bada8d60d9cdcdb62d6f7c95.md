
```
9:       printf("Directory %s\n", file);

10:

11:     return 0;

12: }

13:

14:  int main(int argc, char *argv[])

15: {

16:     if (argc < 2) return 1;

17:

18:     ftw(argv[1], fnencheck, 1);

19:

20:     return 0;

21: }
```

本节探索的最后一种枚举技术称为通配符（globbing）。`glob` API 函数允许你指定一个表示要返回文件的正则表达式。结果存储在 `glob` 缓冲区中，当函数执行完成时可以对其进行枚举。列表 19.6 提供了一个 `glob` API 函数的示例。第一个参数是模式（在本例中为以 `.o` 或 `.n` 结尾的文件）。第二个参数是一个或多个标志（例如，`GLOB_APPEND` 用于将新的 `glob` 附加到之前的调用上）。第三个参数是一个错误处理函数，当尝试打开目录但失败时会调用该函数。结果存储在 `glob` 缓冲区中（这涉及到内存的内部分配）。因此，当你不再需要此缓冲区时，必须使用 `globfree` 释放它。

这个简单的程序（列表 19.6）结果是打印出当前目录下所有以 `.c` 或 `.h` 结尾的文件。

# 列表 19.6 演示 glob API 函数（位于 CD-ROM 的 ./../software/ch19/globtest.c）

```c
1:   #include <stdio.h>
2:   #include <glob.h>

4:   int main() {
5:     {
6:       glob_t globbuf;
7:       int err, i;

9:       err = glob("*.*.[ch]", NULL, 0, &globbuf);

11:      if (err == 0) {

13:          for (i = 0; i < globbuf.gl_pathc; i++) {

15:              printf("%s\n", globbuf.gl_pathv[i]);

17:          }
18:      }
19:      globfree(&globbuf);

21:    }

23:    return 0;
  }
```

Linux（GNU C 库）为枚举子目录提供了多种选项，无论你想查看所有文件、基于正则表达式的文件，还是通过回调方式对每个文件进行操作。

# 使用 notify 进行文件事件通知

## 2.6 内核的新功能之一是提供了对文件系统事件通知的支持

这种新机制被称为 `inify`，指的是它提供了对 inode 事件的通知。这种功能已用于多种应用程序，最引人注目的是 Beagle 搜索工具。Beagle 使用 `inify` 自动通知文件系统的更改以进行索引。另一种方法是定期扫描文件系统以检查更改，这是非常低效的。

`ify` 的趣味之处在于它使用基于文件的机制来提供文件系统事件的通知。例如，当请求监控时，事件将通过文件描述符提供给用户空间应用程序。`notify` API 封装了这些机制的系统调用。现在是时候详细查看此功能了。

# 通知进程

`notify` 的基本流程是首先提供一个监控点。这可以是一个文件，也可以是一个目录。如果提供了一个目录（可能是整个文件系统），那么该目录的所有元素都是事件监控的候选。在定义了观察点后，你可以从文件描述符读取内容以接收事件。

# notify 事件

事件（其结构在列表 19.7 中）提供了事件类型（掩码）、受影响的文件名（如果适用）以及其他元素。

# 列表 19.7 notify_event 结构

```c
struct notify_event {
    int wd;
    uint32_t mask;      /* 观察掩码。 */
    uint32_t cookie;    /* 用于同步两个事件的 cookie。 */
    uint32_t len;       /* 名的长度（包含 NUL）。 */
    char name __flexarr; /* 名。 */
};
```

列表 19.7 中的 `mask` 字段是事件标记，指示了已执行（并正在通知）的操作类型。当前事件的列表见表 19.2。

# 表格 19.2 当前版本中 notify 支持的事件

| 事件名称 | 数值 | 描述 |
|---|---|---|
| IN_ACCESS | 0x00000001 | 文件被访问。 |
| IN_MODIFY | 0x00000002 | 文件被修改。 |
| IN_ATTRIB | 0x00000004 | 属性已更改。 |
| IN_CLOSE_WRITE | 0x00000008 | 文件以写入方式关闭。 |
| IN_CLOSE_NONWRITE | 0x00000010 | 文件以非写入方式关闭。 |
| IN_CLOSE | 0x00000018 | 文件已关闭。 |
| IN_OPEN | 0x00000020 | 文件被打开。 |
| IN_CREATE | 0x00000040 | 文件被创建。 |
| IN_DELETE | 0x00000080 | 文件被删除。 |
| IN_DELETE_SELF | 0x000000C0 | 观察点被删除。 |
| IN_MOVE_SELF | 0x00000100 | 观察点被移动。 |
| IN_UNMOUNT | 0x00000200 | 包含文件系统已卸载。 |
| IN_OVERFLOW | 0x00000400 | 事件队列溢出。 |
| IN_ISDIR | 0x00000800 | 事件指向目录。 |
| IN_ALL_EVENTS | 0x00000FFF | 所有事件 |

# 基于 notify 的应用程序

现在是时候查看一个注册事件的简单应用程序了。首先，`ify_init` 返回文件描述符。主函数见列表 19.8。

# 列表 19.8 主函数（位于 CD-ROM 的 /software/ch19/globtest.c）

```c
1:   #include <stdio.h>
2:   #include <glob.h>

4:   int main() {
5:     {
6:       glob_t globbuf;
7:       int err, i;

9:       err = glob("*.*.[ch]", NULL, 0, &globbuf);

11:      if (err == 0) {

13:          for (i = 0; i < globbuf.gl_pathc; i++) {

15:              printf("%s\n", globbuf.gl_pathv[i]);

17:          }
18:      }
19:      globfree(&globbuf);

21:    }

23:    return 0;
  }
```

# 列表 19.9 注册事件（位于 CD-ROM 的 /software/ch19/globtest.c）

```c
1: int register_watch(int ifd, char *dir)
2: {
3:     int err;

5:     err = inify_add_watch(fd, dir, IN_ALL_EVENTS);

7:     return err;
}
```

## 372 GNU/Linux 应用编程

```c
28:    i += sizeof(struct inotify_event) + ievent->len;

29:

30:    }

31:

32:    }

33:

34:

35:    return 0;
}
```

最后一个函数 `emit_event`（列表 19.11 所示）解析结构并将信息输出到标准输出。首先，你检查是否提供了字符串，如果是，则先输出它。此名称指的是受影响的文件名（目录或普通文件）。然后，你测试每个事件标记以查看哪些标记存在，然后将其输出到标准输出。

# 列表 19.11 解析并输出事件结构（位于 CD-ROM 的 /software/ch19/emitdiratch.c 上）

```c
1:  void emit_event(struct inotify_event *ievent)
2:  {
3:    if (ievent->len) printf("[%s", ievent->name);

5:    if (ievent->mask & IN_ACCESS) printf("Accessed\n");
```
