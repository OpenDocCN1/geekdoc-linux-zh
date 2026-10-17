
```
-rw-- 1 taylor 512 Oct 09:53 bin/
-rw-- 1 taylor 3843 Oct 6 18:02 iecc.list
-rw-rw- 1 taylor 20832 Oct 6 09:57 mailing.lists
-rw-rw- 1 taylor 1031 Oct 7 15:44 newlists
drwx-- 2 taylor 512 Sep 14 22:14 src/
```

目录的大小通常恰好是 512 字节，尽管 Unix 会确切显示其中文件目录有多大（它并不指示文件名的大小）。

### 4.3 ls 标志汇总

| 标志 | 含义 |
| :--- | :--- |
| `-1` | 强制单列输出 |
| `-a` | 列出所有文件，包括隐藏文件 |
| `-C` | 强制多列输出 |
| `-d` | 列出目录本身而非其内容 |
| `-F` | 在文件类型后添加指示符 |
| `-l` | 使用详细格式列出 |
| `-m` | 用逗号分隔 |
| `-n` | 按用户 ID 排序 |
| `-r` | 反序排序 |
| `-R` | 递归列出 |
| `-s` | 显示大小 |
| `-t` | 按修改时间排序 |
| `-u` | 按访问时间排序 |
| `-v` | 按版本号排序 |
| `-X` | 显示扩展安全上下文 |
| `-z` | 不排序 |

# 任务 4.10：使用 du 检查磁盘空间占用

Windows 和 Macintosh 系统相对于 Unix 的优势在于，它们可以轻松找到你使用了多少磁盘空间以及剩余多少可用空间。在 Mac 上，通过磁盘空间大小查看文件夹，并且任何 Finder 窗口的顶部都会显示可用空间。

Unix 就像一个守口如瓶的线人，从不主动提供任何信息，因此你需要学习两个新命令。`du`（disk usage，磁盘使用）命令用于查找多少磁盘空间；`df`（disk free，磁盘剩余）命令用于查找有多少可用空间。

`du` 命令列出文件系统中当前点或其以下所有目录的大小（以千字节为单位）。

```
du /OWL
11 /elm
38 /Archives
20 /InfoWorld/PIMS
14 /InfoWorld
28 /Mail
710 /News
191 /bin
25 /src
35 1627
```

注意 `du` 深入了两个级别找到 `InfoWorld/PIMS` 子目录，并将其大小加到 `InfoWorld` 目录显示的大小中。在最后，它列出 1,627 千字节作为点目录（当前目录）的大小。如你所知，1,024 千字节是一个兆（MB）。通过除法，你会发现此目录仅占用了 1.5MB 的磁盘空间。

如果你觉得输出有点困惑，且你的 Unix 版本支持，请尝试 `du -h` 以获得更易于读的输出。

如果你只对总计感兴趣，可以使用 `-s` 标志只输出信息的摘要。

```
du -s
1627
```

当然，你可以查看文件系统的任何地方，但子目录越多，耗的时间就越长。

使用 `du` 可能会出现错误信息：

```
du -s /etc
/etc/shadow: Permission denied
4417 /etc
```

在这个示例中，`/etc` 目录内的目录设置了拒绝访问的权限：

```
% ls -ld /etc/shadow
drw------ 2 root 512 Oct 10 16:34 /etc/shadow
```

`du` 命令会汇总它能够读取的文件和目录的磁盘使用情况，无论 `shadow` 目录的大小如何，它仍会显示 4,417 千字节。

尽管默认情况下 `du` 列出目录的大小，但它也会计算所有文件的大小。如果你对这些信息感兴趣，可以通过添加 `-a` 标志让程序列出所有文件。

```
% cd InfoWorld
% du -a
9 ./PIM.review.Z
5 ./Expert.opinion.Z
4 ./PIMS/proposal.txt.Z
1 ./PIMS/task1.txt.Z
2 ./PIMS/task2.txt.Z
2 ./PIMS/task3.txt.Z
2 ./PIMS/task4.txt.Z
2 ./PIMS/task5.txt.Z
2 ./PIMS/task6.txt.Z
1 ./PIMS/contact.info.Z
14 ./PIMS
28 .
```
