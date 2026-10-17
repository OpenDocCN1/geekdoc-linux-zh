
```c
for (i = 1; i < NR_TASKS; i++) if (task[i])

inode->i_op = &proc_root_inode_operations;

return;

/* * if(ino == PROC_ROOT_INO) /*

} /* proc_read_inode() */
```

`proc_root_inode_operations` 结构只提供了两个函数：以 `proc_readroot()` 函数形式实现的组件 `readdir`，以及以 `proc_lookuproot()` 函数形式实现的组件 `lookup`。这两个函数都使用 `root_dir[]` 表操作，该表包含了根目录的固定条目。

```c
static struct proc_dir_entry root_dir[] = ( ({ PROC_ROOT_INO

#ifdef CONFIG_PROFILE

{ PROC_PROFILE, 7, "profile" }, #endif ;
```

各个结构包含 inode 号、文件名的长度和文件名本身。当读取根目录时，`proc_readout()` 函数相应地返回 `root_dir[]` 字段中给出的条目，以及每个运行中进程的条目。然而，这些条目只有在调用 `proc_readout()` 时才会被生成。

比 `proc_readout()` 更趣的函数是 `proc_lookuproot()`，它通过引用目录的 inode 和其中包含的文件名确定文件的 inode。在这个过程中，inode 号的生成方式使得它们之后可以唯一地标识已打开的文件。

```c
static int proc_lookuproot(struct inode * dir, const char * name, int len,

    struct inode ** result) {

    unsigned int pid, c;

    int i, ino;
```

首先检查打开的文件，判断它是否来自 `root_dir[]` 表。

```c
i = NR_ROOT_DIRENTRY;

while (i-- > 0 && !proc_match(len,name,root_dir+i)) /* */;

if (i >= 0) {
```

如果是，则可以直接从表中读取 inode 号。在这种情况下，inode `PROC_SELF` 代表目录并被当前进程的编码形式替换：

```c
if (ino == 7) /* self modifying inode ... */ ino = (current-pid <<

16) + 2;
```

否则，尝试将名称转换为数字，解释为进程号。接着检查是否存在匹配的进程；如果没有，则返回错误。如果存在，则将进程号存储在变量 `ino` 中。

```c
{
  pid = string_to_integer(name);
  for (i = 0; i < NR_TASKS; i++)
    if (task[i] && task[i]->pid == pid) break;
  if (!pid || i >= NR_TASKS) {
    iput(dir);
    return -ENOENT;
  }
  ino = (pid << 16) + 2;
}
```

现在再次调用 `iget` 生成 inode。该函数反而使用相关的 inode 号调用 `proc_read_inode()`。

```c
if ((*result = iget(dir->i_sb, ino))) {
  iput(dir);
  return -ENOENT;
}

return 0;

} /* proc_lookuproot() */
```

如果请求的 inode 是目录，该函数最终返回一个 inode，其 inode 操作在 `inode_operations` 结构中给出。然而，该结构只包含描述目录的 `readdir` 和 `lookup`。这涵盖了 Proc 文件系统的目录表示，留下了如何创建普通文件的问题。通过 `proc_read_inode()` 函数，为普通文件分配了 `inode_operations`。然而，这里实现的是读取文件的 `array_read()` 函数。如果进程想要读取 `/proc/uptime` 文件，它通过调用 `get_free_page()` 分配空页并将其传递给 `get_uptime()` 函数。后者通过在缓冲区中输入所需的值来生成文件内容，如下：

```c
static int get_uptime(char * buffer) {
    unsigned long uptime;
    unsigned long idle;
    utime = utime + task[0]->stime;
    if (HZ != 100)
        return snprintf(buffer, "%u.%2lu %u.%2lu", uptime / HZ,
            ((utime % HZ) * 100) / HZ, idle / HZ,
            (((idle % HZ) * 100) / HZ) % 100);
    else
        return snprintf(buffer, "%u.%2lu %u.%2lu", uptime / HZ,
            utime, idle);
}
#endif
```
