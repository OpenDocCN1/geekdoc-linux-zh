

## 7.2 V7 ls 代码

```c
356  if (argfl || statreq) {
357      if (stat(file, &statb) < 0) {
358          printf("%s not found\n", file);
359          statb.st_ino = -1;
360          statb.st_size = 0;
361          statb.st_mode = 0;
362          if (argfl) {
363              lastp--;
364              return(0);
365          }
366      }
367      rep->lnum = statb.st_ino;   /* stat() OK, copy info */
368      rep->lsize = statb.st_size;
369      switch(statb.st_mode & S_IFMT) {
370          case S_IFDIR:
371              rep->ltype = 'd';
372              break;
373          case S_IFBLK:
374              rep->ltype = 'b';
375              rep->lsize = statb.st_rdev;
376              break;
377          case S_IFCHR:
378              rep->ltype = 'c';
379              rep->lsize = statb.st_rdev;
380              break;
381      }
382      rep->lflags = statb.st_mode & ~S_IFMT;
383      rep->luid = statb.st_uid;
384      rep->lgid = statb.st_gid;
385      rep->lnl = statb.st_nlink;
386      if(uflg)
387          rep->ltime = statb.st_atime;
388      else if (cflg)
389          rep->ltime = statb.st_ctime;
390      else
391          rep->ltime = statb.st_mtime;
392      nblocks += nblock(statb.st_size);
393      }
394      return(rep);
395  }
```

第 356–396 行处理对 `stat()` 的调用。如果这是命令行参数，或者由于某个选项导致 `statreq` 为真，代码将按如下方式填充 `struct lbuf`：

- 第 357–366 行：调用 `stat()`，如果失败，打印错误消息并相应地设置值，然后返回 NULL（表示为 0）。
- 第 367–368 行：如果 `stat()` 成功，从 `struct stat` 中设置 inode 编号和大小字段。
- 第 369–384 行：处理目录、块设备和字符设备的特殊情况。在所有情况下，代码都会更新 `ltype` 字段。对于设备，`lsize` 的值会被 `st_rdev` 的值替换。
- 第 385–388 行：从 `struct stat` 的对应字段填充 `lflags`、`luid`、`lgid` 和 `lnl` 字段。第 385 行移除了文件类型位，留下 12 个权限位（用户/组/其他的读/写/执行权限，以及 setuid、setgid 和 save-text 标志）。
- 第 389–394 行：基于命令行选项，使用 `struct stat` 中的三个时间字段之一来填充 `struct lbuf` 中的 `lmtime` 字段。
- 第 395 行：使用文件中的块数更新全局变量 `tlblocks`。

```c
400 compare(pp1, pp2)    int compar(struct lbuf **pp1, struct lbuf **pp2)
401 struct lbuf **pp1, **pp2;    
402 {
403 register struct lbuf *p1, *p2;
404 
405 p1 = *pp1;
406 p2 = *pp2;
407 if (dflg==0) {
408 if (!p1->lflags&ISARG && p1->ltype=='d') {
409 if (!p2->lflags&ISARG && p2->ltype=='d')
410 return(1);
411 } else {
412 if (p2->lflags&ISARG && p2->ltype=='d')
413 return(-1);
414 }
415 }
416 if (tflg) {
417 if(p2->lmtime == p1->lmtime)
418 return(0);
419 if(p2->lmtime > p1->lmtime)
420 return(rflg);
421 }
422 return(strcmp( * strcmp(p1->lflags&ISARG p1->ln.namep; p1->ln.lname, p2->lflags&ISARG p2->ln.namep; p2->ln.lname)));
425 }
```

`compare()` 函数非常密集：在很小的空间里发生了很多事情。首先要记住的是返回值的含义：负值意味着第一个文件应排在数组中第二个文件之前的位置，零意味着两个文件相等，正值意味着第二个文件应排在第一个文件之前的位置。

接下来要理解的是，`ls` 在打印文件信息之后才打印目录的内容。因此，排序的结果应该是所有*在命令行中指定的*目录跟随所有在命令行中指定的文件之后。

最后，`rflg` 变量有助于实现 `-r` 选项，该选项反转排序顺序。它初始化为 1（第 30 行）。如果使用 `-r`，`rflg` 会被设置为 `-1`（第 89–91 行）。

以下伪代码描述了 `compar()` 的逻辑；左边页边距中的行号对应 `ls.c` 的行号：

```
407    if ls has to read directories # dflg == 0
408        if p1 is a command-line arg and p1 is a directory
409            if p2 is not a command-line arg and is not a directory
410                return 1 # first comes after second
                   else
411                    else fall through to time test
                       # p1 is not a command-line directory
412                    if p2 is a command-line arg and is a directory
413                        return -1 # first comes before second
                                else fall through to time test
416 if sorting is based on time # tflg is true
417     # compare times:
            if p2's time is equal to p1's time
418             return 0
419             if p2's time > p1's time
420                 return the value of rflg (positive or negative)
# p2's time < p1's time
421             return opposite of rflg (negative or positive)
423 Multiply rflg by the result of strcmp()
424     on the two names and return the result
```

第 423–424 行中 `strcmp()` 的参数看起来很乱。这是因为根据文件名是命令行参数还是从目录中读取的，需要使用 `struct lbuf` 中 `ln` 联合体的不同成员。

### 7.3 总结

- V7 版本的 `ls` 是一个相对较小的程序，但它涉及 Unix 编程的许多基本方面：文件 I/O、文件元数据、目录内容、用户和组、时间和日期值、排序以及动态内存管理。
- V7 版本 `ls` 与现代 `ls` 之间最显著的外部差异在于对 `-a` 和 `-l` 选项的处理方式。V7 版本的选项远少于现代版本；一个明显的缺失是递归选项 `-R`。
- 对 `flist` 的管理是一种利用 PDP-11 架构有限内存的清晰方式，同时尽可能提供大量信息。`struct lbuf` 很好地将从 `struct stat` 中提取的感兴趣的信息进行了抽象；这大大简化了代码。打印九个权限位的代码紧凑而优雅。
- `ls` 的某些部分使用了惊人微小的限制，例如文件数的上限为 1024，或者 `makename()` 中缓冲区大小为 100。

## 练习

1. 考虑 `getname()` 函数。如果请求的 ID 号为 216，且 /etc/passwd 中存在以下两行，顺序如下，会发生什么：
    joe.xzyzy:216:10:Joe User:/usr/joe:/bin/sh
    jane.xzyxx:216:12:Jane User:/usr/jane:/bin/sh
2. 考虑 `makename()` 函数。它能否使用 `sprintf()` 来创建拼接后的名称？原因是什么？
3. `readdir()` 中的第 319–320 行真的有必要吗？
4. 取你在第 6 章第 205 页“练习”中编写的 stat 程序。添加来自 V7 版本 `ls` 的 `nblock()` 函数，并打印结果以及 `struct stat` 中的 `st_blocks` 字段。当它们不同时添加一个可见的标记。
5. 你会如何给 V7 版本 `ls` 对 `malloc()` 的使用打分？（提示：`free()` 调用的频率如何？它应该在哪里被调用？）
6. 你会如何给 V7 版本 `ls` 的代码清晰度打分？（提示：有多少注释？）
7. 概述将 V7 版本 `ls` 移植到现代系统所需的步骤。

![](img/766b5597246d532412fad21b1c59ccec_259_0.png)

# 第 8 章

# 文件系统和目录遍历

本章内容

- 8.1 挂载和卸载文件系统 第 228 页
- 8.2 文件系统管理文件 第 238 页
- 8.3 检索每个文件系统信息 第 244 页
- 8.4 在文件层次结构中移动 第 256 页
- 8.5 遍历文件树：GNU du 第 269 页
- 8.6 更改根目录：chroot() 第 276 页
- 8.7 总结 第 277 页
- 练习 第 278 页

本章完成了对 Linux（以及 Unix）文件系统和目录的讨论。我们首先描述如何将从包含文件系统的磁盘分区添加（和移除）到逻辑文件系统命名空间中，这样通常用户既不需要知道也不关心文件物理位置在哪里，以及用于处理文件系统的 API。

然后，我们描述如何在分层文件命名空间中移动，如何获取当前工作目录的完整路径名，以及如何使用 `nftw()` 函数轻松处理任意的目录层次结构（树）。最后，我们描述了专门但重要的 `chroot()` 系统调用。

## 8.1 挂载和卸载文件系统

统一的分层文件命名空间是 Linux/Unix 设计的巨大优势。本节探讨管理文件、命令和操作系统如何协作，从包含文件数据和元数据的独立物理设备构建命名空间。

### 8.1.1 回顾背景

第 5 章“目录和文件元数据”，第 117 页，介绍了用于文件元数据的 inode，并描述了目录条目如何将文件名链接到 inode。它还描述了分区和文件系统，并且您看到硬链接被限制在单个文件系统中工作，因为目录仅包含 inode 编号，而 inode 编号在整个正在使用的文件系统中并不是唯一的。

除了 inode 和数据块，文件系统还包含一个或多个超级块副本。这是一个描述文件系统的特殊磁盘块；随着文件系统本身的变化，其信息会被更新。例如，它包含空闲和已用 inode 的计数、空闲和已用块的计数以及其他信息。它还包含一个魔数：位于特殊位置的唯一特殊值，用于识别文件系统的类型。（我们将很快看到这与何处相关。）

使包含文件系统的分区可用被称为挂载文件系统。令人惊讶的是，从使用中移除文件系统被称为卸载文件系统。

