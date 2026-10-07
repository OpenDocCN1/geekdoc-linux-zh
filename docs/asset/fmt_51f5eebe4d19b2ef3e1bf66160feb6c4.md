
然后，我们执行了在两个目录中产生事件的命令。我们首先使用 `cat(1)` 创建一个文件：

```
$ cat > dir1/aaa

Read 64 bytes from inotify fd

wd = 1; mask = IN_CREATE

name = aaa

wd = 1; mask = IN_OPEN

name = aaa
```

上述后台程序产生的输出显示 `read()` 获取了一个包含两个事件的缓冲区。我们继续向文件中输入一些内容，并输入终端的*文件结束符*（end-of-file）：

```
Hello world

Read 32 bytes from inotify fd

wd = 1; mask = IN_MODIFY

name = aaa
```

```
Type ControlD

Read 32 bytes from inotify fd

wd = 1; mask = IN_CLOSE_WRITE

name = aaa
```

我们将文件重命名到另一个被监控的目录。这导致了两个事件，一个是文件移出的目录（监控描述符 1），另一个是目标目录（监控描述符 2）：

```
$ mv dir1/aaa dir2/bbb

Read 64 bytes from inotify fd

wd = 1; cookie = 548; mask = IN_MOVED_FROM

name = aaa

wd = 2; cookie = 548; mask = IN_MOVED_TO

name = bbb
```

这两个事件共享相同的 `cookie` 值，允许应用程序将它们关联起来。
当我们在一个被监控的目录创建创建一个子目录时，生成的事件中的掩码包含 `IN_ISDIR` 位，表示事件的主体是一个目录：

```
$ mkdir dir2/ddd

Read 32 bytes from inotify

wd = 1; mask = IN_CREATE_IN_ISDIR

name = ddd
```

此时，值得重复的是，inotify 监控不是递归的。如果应用程序想要监控新创建的子目录中的事件，那么它需要再次调用 `inotify_add_watch()` 并指定该子目录的路径。
我们删除了其中一个被监控的目录：

```
$ rmdir dir2

Read 32 bytes from inotify

wd = 1; mask = IN_DELETE_SELF

IN_IGNORED
```
