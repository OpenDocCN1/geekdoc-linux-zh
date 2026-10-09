

## 3.6 实现 `ls` 命令

if (cleanup)
    (void)get_cwd(true);
else {
    ec_null( cwd = get_cwd(false) )
    printf("\n%s:\n", cwd);
}
return true;
EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END

稍后我们将看到整体清理代码中会调用 `print_cwd(true)`。

现在让我们跳回主函数的顶层，看看一切是如何初始化的，以及列表显示是如何开始的：

```
#define USAGE "Usage: aupls [-Rd] [dir]\n"
static long total_entries = 0, total_dirs = 0;
int main(int argc, char *argv[])
{
    struct travser_info ti = {0};
    int c, status = EXIT_FAILURE;
    bool stat_only = false;
    ti.ti_fcn = show_stat;
    while ((c = getopt(argc, argv, "dR")) != -1)
        switch(c) {
            case 'd':
                stat_only = true;
                break;
            case 'R':
                ti.ti_recursive = true;
                break;
            default:
                fprintf(stderr, USAGE);
                EC_CLEANUP
        }
    switch (argc - optind) {
        case 0:
            ti.ti_name = ".";
            break;
        case 1:
            ti.ti_name = argv[optind];
            break;
        default:
            fprintf(stderr, USAGE);
            EC_CLEANUP
        }
    ec_false( do_entry(&ti, stat_only) )
    printf("\nTotal entries: %ld; directories = %ld\n", total_entries, total_dirs);
    status = EXIT_SUCCESS;
    EC_CLEANUP
    EC_CLEANUP_BGN
    print_cwd(true);
    exit(status);
    EC_CLEANUP_END
}
```

两个全局变量 `total_entries` 和 `total_dirs` 用于保持总体计数，我们发现将这些显示在结尾很有意思；稍后我们会看到它们在哪里被递增。

`getopt` 是一个标准库函数（属于 POSIX/SUS，而不是标准 C）。它的第三个参数是允许使用的选项字母列表。当选项处理完毕后，它将全局变量 `optind` 设置为下一个待处理参数的索引，在我们的示例中，这是一个可选的路径名。如果没有给出，则假设为当前目录。

真正的工作由 `do_entry` 完成，它看起来是这样的：

```
static bool do_entry(struct traverse_info *p, bool stat_only)
{
    bool is_dir;

    ec_negil( lstat(p->ti_name, &p->ti_stat) )
    is_dir = S_ISDIR(p->ti_stat.st_mode);
    if (stat_only || !is_dir) {
        total_entries++;
        if (is_dir)
            total_dirs++;
        ec_false( (p->ti_fcn)(p, SHOW_INFO) )
    }
    else if (is_dir)
        ec_false( do_dir(p) )
    return true;

    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}
```

`do_entry` 有两种使用方式：如果 `stat_only` 参数为真，或者当前条目不是目录，它会递增全局计数器，然后在 `SHOW_INFO` 模式下调用回调函数。这在指定了 `-d` 参数、在 `aupls` 命令行上指定了非目录项，或在目录列表的第一遍（Pass 1）期间完成。否则，对于目录，它会调用包含 `readdir` 循环以处理目录条目的函数 `do_dir`：

```
static bool do_dir(struct traverse_info *p)
{
    DIR *sp = NULL;
    struct dirent *dp;
    int dirfd = -1;
    bool result = false;

    ec_neg1( dirfd = open(".", O_RDONLY) )
    if ( (sp = opendir(p->ti_name)) == NULL || chdir(p->ti_name) == -1) {
        if (errno == EACCES) {
            fprintf(stderr, "%s: Permission denied.\n", p->ti_name);
            result = true;
            EC_CLEANUP
        }
        EC_FAIL
    }
    if (p->ti_recursive)
        ec_false( (p->ti_fcn)(p, SHOW_PATH) )
    while (errno = 0, (dp = readdir(sp)) != NULL) {
        if ( strcmp(dp->d_name, ".") == 0 ||
             strcmp(dp->d_name, "..") == 0 )
            continue;
        p->ti_name = dp->d_name;
        ec_false( do_entry(p, true) )
    }
    if (errno != 0)
        syserr_print("Reading directory (Pass 1)");
    if (p->ti_recursive) {
        rewinddir(sp);
        while (errno = 0, (dp = readdir(sp)) != NULL) {
            if ( strcmp(dp->d_name, ".") == 0 ||
                 strcmp(dp->d_name, "..") == 0 )
                continue;
            p->ti_name = dp->d_name;
            ec_false( do_entry(p, false) )
        }
        if (errno != 0)
            syserr_print("Reading directory (Pass 2)");
    }
    result = true;
    EC_CLEANUP
    EC_CLEANUP_BGN
    if (dirfd != -1) {
        (void)fchdir(dirfd);
        (void)close(dirfd);
    }
    if (sp != NULL)
        (void)closedir(sp);
    return result;
    EC_CLEANUP_END
}
```

`do_dir` 是递归发生的地方。它打开指向当前目录的 `dirfd`，以便在清理时可以恢复。然后它使用 `opendir` 打开目录并切换到该目录，以便相对于父目录处理条目。由于目录不可读（`opendir` 失败）或不可搜索（`chdir` 失败），经常会遇到 `EACCES` 错误，因此在这种情况下我们希望只打印一条消息，而不是终止处理。

接下来，如果指定了 `-R` 参数，我们告诉回调函数打印当前目录路径。这样可以将所有常规打印局部化到一个回调函数中。

然后我们有第一遍的 `readdir` 循环（其中 `do_entry` 以 `stat_only` 设为真调用），一个 `rewinddir` 系统调用，以及如果指定了 `-R`，则进行第二遍的 `readdir` 循环（以 `stat_only` 设为假调用 `do_entry`）。递归发生是因为第二遍对 `do_dir` 的调用可能会递归调用 `do_dir`。注意两个 `readdir` 循环都跳过了 `.` 和 `..` 条目，`ls` 默认也会省略这些。

我们决定将来自 `readdir` 的错误视为非致命错误，以保持进程继续，而不是使用 `ec_nzero` 宏退出，这解释了对 `syserr_print` 的两次调用，该函数如下：

```c
void syserr_print(const char *msg)
{
    char buf[200];

    fprintf(stderr, "ERROR: %s\n", syserrmsg(buf, sizeof(buf), msg,
      errno, EC_ERRNO));
}
```

`syserrmsg` 在第 1.4.1 节中介绍过。

就这样了——我们自己的完全递归版本的 `ls`！

# 3.7 更改 I 节点

`stat` 系列系统调用（第 3.5.1 节）从 i 节点中检索信息，我在其中解释了当文件被操作时 i 节点中的各个数据字段如何变化。本节的讨论中的一些系统调用也可以直接更改部分字段。表 3.3 指出了哪些系统调用执行哪些更改。“固定”意味着该字段完全不可更改——如果你希望它是其他值，必须创建一个新的 i 节点——而“副作用”意味着它只能通过执行其他操作（例如使用 `link` 创建新链接）的副作用来更改，而不能直接更改。

表 3.3 更改 I 节点字段

| I 节点字段 | 描述 | 由...更改 |
| :--- | :--- | :--- |
| st_dev | 文件系统设备 ID | 固定 |
| st_ino | i 编号 | 固定 |
| st_mode | 模式 | chmod, fchmod |
| st_nlink | 硬链接数 | 副作用 |
| st_uid | 用户 ID | chown, fchown, lchown |
| st_gid | 组 ID | chown, fchown, lchown |
| st_rdev | 设备 ID（如果是特殊文件） | 固定 |
| st_size | 大小（字节） | 副作用 |
| st_atime | 最后访问时间 | utime |
| st_mtime | 最后数据修改时间 | utime |
| st_ctime | 最后 i 节点修改时间 | 副作用 |
| st_blksize | 最佳 I/O 大小 | 固定 |
| st_blocks | 已分配的 512 字节块 | 副作用 |

## 3.7.1 chmod 和 fchmod 系统调用

```
**chmod** — 通过路径更改文件模式

#include <sys/stat.h>
int chmod(
    const char *path,      /* 路径名 */
    mode_t mode            /* 新模式 */
); /* 成功返回 0，出错返回 -1（设置 errno） */
```

```
**fchmod** — 通过文件描述符更改文件模式

#include <sys/stat.h>
int fchmod(
    int fd,                /* 文件描述符 */
    mode_t mode            /* 新模式 */
); /* 成功返回 0，出错返回 -1（设置 errno） */
```

**chmod** 系统调用更改任何类型的现有文件的模式。然而，它不能用于更改类型本身，因此只能更改 `S_ISUID`、`S_ISGID` 和 `S_ISVTX` 标志或权限位。使用与 `stat` 结构（第 3.5.1 节）相同的宏。**fchmod** 类似，但它接受一个打开的文件描述符而不是路径。

调用者的有效用户 ID 必须与文件的用户 ID 匹配，或者调用者必须是超级用户。仅具有写权限或调用者的有效组 ID 与文件匹配是不够的。此外，如果正在设置 `S_ISGID`，有效组 ID 必须匹配（超级用户除外）。

除非你要设置整个模式，否则你必须先通过调用 `stat` 函数之一来获取现有模式，设置或清除你想要更改的位，然后使用修改后的模式执行 **chmod**。

在应用程序内部调用 **chmod** 的情况很少见，因为模式通常在文件创建时设置。然而，用户经常使用 **chmod** 命令。

## 3.7.2 chown, fchown, 和 lchown 系统调用

**chown** 更改文件的用户 ID 和组 ID。只有所有者（进程的有效用户 ID 等于文件的用户 ID）或超级用户可以执行它。如果 `uid` 或 `gid` 中任意为 –1，则对应的 ID 保持不变。

