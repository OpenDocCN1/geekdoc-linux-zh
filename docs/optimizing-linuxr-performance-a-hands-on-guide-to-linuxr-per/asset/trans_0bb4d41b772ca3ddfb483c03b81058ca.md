

## 12.4. 为性能查找配置应用程序

调查的下一步是为性能查找配置应用程序。`prelink` 是一个小型且自独立的应用程序。事实上，它甚至没有使用共享库（它是静态链接的）。然而，使用所有符号重新编译它是一个好主意，这样我们在需要时就可以可以在调试器 (gdb) 中检查它。再次，这使用了 `configure` 命令来生成 Makefile。我们必须下载 `prelink` 的源码并带符号进行重新编译。我们可以再次从 Red Hat 下载 `prelink` 的 rpm。源码将安装在 `/usr/src/redhat/SOURCES`。一旦我们解压 `prelink` 的源码，就可以如列表 12.6 所示进行编译。

列表 12.6。

```
env CFLAGS=-g3 ./configure
gmake
```

在 `prelink` 配置并编译后，我们可以使用编译好的二进制文件来调查性能问题。

## 12.5. 安装并配置性能工具

查找的下一步是安装性能工具。在这种情况下，`ltrace` 或 `profile` 均无帮助。`profile` 用于分析消耗大量 CPU 时间的应用程序，由于 `preload` 在运行时仅使用约 3% 的 CPU，因此 `profile` 将无法无法提供帮助。由于 `preload` 二进制文件是静态链接且不使用任何共享库，`ltrace` 也无法我们提供帮助。然而，系统调用跟踪器 `strace` 可能有帮助，因此我们需要安装它。

## 12.6. 运行应用程序和性能工具

现在我们终于可以分析 `prelink` 不同模式的性能特征了。正如你所说，`prelink` 没有花费太多时间使用 CPU；它所有的时间都花在了磁盘 I/O 上。`prelink` 必须调用内核进行磁盘 I/O，我们应该能够使用 `strace` 工具跟踪它的执行。由于 `prelink` 的快速模式（quick mode）似乎并不比标准全运行快，我们比较两者的 `strace` 以查看是否有任何异常行为。

首先，我们使用 `strace` 跟踪运行较慢的 `prelink`。这是初始化了 `prelink` 在快速模式下使用的缓存的运行。最初，我们使用 `strace` 显示 `prelink` 所做调用的总结，并查看每个调用完成所需的时间。执行此操作的命令在列表 12.7 中。

列表 12.7。

```
[root@localhost prelink]# # strace -c -o af_sum
/usr/sbin/prelink -af

/* 31 vars */ = 0
/usr/sbin/prelink:
/usr/libexec/autopackage/luau-downloader.bin: Could not parse '/usr/libexec/autopackage/luau-downloader.bin: error while loading shared libraries: libau.so.2: cannot open shared object file: No such file or directory'
/..
/usr/sbin/prelink: /usr/lib/mozilla-1.6/regchrome: Could not parse '/usr/lib/mozilla-1.6/regchrome: error while loading shared libraries libxpcom.so: cannot open shared object file: No such file directory'
```

列表 12.7 也是 `prelink` 输出示例。当 `prelink` 尝试预链接某些系统可执行文件和库时，它非常吃力。这些信息以后会变得很有价值，请记住它。

列表 12.8 显示了列表 12.7 中的 `strace` 命令生成的输出文件。

列表 12.8。

```
[root@localhost prelink]# # cat af_sum
execve("/usr/sbin/prelink", "/usr/sbin/prelink", "-af")
% time          seconds         usecs/calls      errors syscall
77.87           151.249181      65 2315836 read
11.93          21.263231      55 421593 pread
3.59           6.976880       63 110585 pwrite
1.70           3.294193       17 196518 mmap
1.02           1.977343       32 61774 stat
0.97           1.897097       40 47820 open
0.12           1.406801       249 5369 vfork
```

## 12.7. 模拟解决方案

`strace` 揭的信息显示 `prelink` 花了大量时间尝试打开和分析无法预链接的二进制文件。测试链接二进制文件缓存是否能提高 `prelink` 性能的最佳方法是修改 `prelink`，将其所有链接二进制文件添加到初始缓存中。遗憾的是，向这些“未链接”二进制文件添加代码可能是一个复杂的过程，涉及大量关于 `prelink` 内部的知识。一种更简单的方法是用已知的链接二进制文件替换所有链接的二进制文件来模拟缓存。这会导致先先链接的二进制文件在运行时被忽略。这正是如果我们拥有缓存时会发生的情况，因此我们可以用它来估计如果 `prelink` 缓存并忽略链接二进制文件，我们将看到的性能提升。

为了开始实验，我们将 `/usr/bin/` 中的所有文件复制到沙箱目录并在该目录上运行 `prelink`。该目录包含了二进制文件、shell 和无法进行预链接的库。然后我们在沙箱目录上运行 `prelink`，让它创建一个新缓存而不是系统缓存。这如列表 12.5 所示。

列表 12.5。

```
/usr/sbin/prelink -C new_cache -f sandbox/
```

接下来，在列表 12.16 中，我们记录缓存 `prelink` 运行所需的时间。我们必须运行多次直到获得一致的结果（第一次运行为后续每次运行预热了缓存）。列表 12.16 中的基准时间为 .983 秒。我们必须优于这个时间，我们的优化（改进缓存）才有意义。

列表 12.16。

```
time /usr/sbin/prelink -C new_cache -q sandbox/
real    0m.983s
user    0m.597s
sys      0m.386s
```

接下来，在列表 12.17 中，我们对此 `prelink` 命令运行 `strace`。这是为了记录 `prelink` 在沙箱目录中打开了哪些文件。

列表 12.17。

```
strace -o strace_prelink_sandbox /usr/sbin/prelink -new_cache -q/
```

我们创建一个新目录 `sandbox2`，并将 `/usr/bin` 目录中的所有二进制文件复制其中。然而，我们将之前的 `strace` 输出中 `prelink` “打开”的所有文件覆盖为已知的、可以链接的良好二进制文件。我们复制到所有二进制文件而不仅仅是它们，以便两个沙箱包含相同数量的文件。在设置好第二个沙箱后，我们使用列表 12.18 中的命令在新目录上运行完整版本的 `prelink`。

列表 12.18。

```
[root@localhost prelink]#/usr/sbin/prelink -C new_cache2 -f sandbox/
```

## 12.8. 报告问题

由于我们在一个相当底层的系统软件中发现了一个问题和潜在解决方案，与作者合作解决该问题是一个好主意。我们至少必须提交一个错误报告，以便作者知道问题的存在。提交我们用于发现问题的测试将有助于他重现问题，并希望修复它。在这种情况下，我们将向 Red Hat 的 bug (zilla.redhat.com) 跟踪系统添加一个错误报告。（大多数发行版都有类似的跟踪系统。）我们的错误报告描述了我们遇到的问题以及我们发现的可能解决方案。

到达 bugzilla 时，我们首先搜索 `prelink` 的错误报告，查看是否其他人报告过此问题。在没有发现的情况下，我们查看列表 12.22 中的错误报告并等待作者或维护者的响应并修复 bug。

列表 12.22。

```
From Bugzilla Helper:
User-Agent: Mozilla/5.0 (X11; Linux i686; en-US; rv:1.6) Gecko/20040510

Description of problem:

在快速模式下运行时，prelink 不缓存某些二进制文件无法预链接这一事实。结果是，即使在快速模式下运行，它也会重新扫描这些文件。这导致磁盘剧烈工作并显著减慢整个系统。

有三种可执行文件在快速模式下重试：

- 1) 静态二进制文件
- 2) Shell 脚本
- 3) 依赖于不可链接二进制文件的文件。（例如 OpenGL）

对于 1 & 2，如果 prelink 缓存这些可执行文件无法预链接的这一事实，并在快速模式下检查它们的 ctime & mtime，如果它已经知道它们无法预链接，则甚至不尝试读取它们，那将很好。

对于 3，如果 prelink 能记录导致 prelink 失败的库（以 OpenGL 情况为例），并记录下来，那将很好。
```

