
| S | root | 19 | 0 | f60b1d10 | 2473 | | 0:00 | 18 |
| S | root | 20 | 0 | f61d0b10 | 750 | | 0:00 | 19 |
| S | root | 21 | 0 | f50f2028 | 513 | | 0:00 | 18 |
| S | root | 22 | 0 | f55e7720 | 407 | | 0:00 | 19 |
| S | root | 23 | 0 | f52e5520 | 161 | | 0:00 | 18 |
| S | root | 24 | 0 | f62ad1d8 | 2851 | | 0:00 | 19 |
| S | root | 25 | 0 | f66e5520 | 1601 | | 0:00 | 18 |
| S | root | 26 | 0 | f28bf0d8 | 2350 | | 0:00 | 19 |
| S | root | 27 | 0 | f52a428 | 504 | | 0:00 | 18 |
| S | root | 28 | 0 | f553528 | 734 | | 0:00 | 19 |
| S | root | 29 | 0 | f61f8228 | 804 | | 0:00 | 18 |
| S | root | 30 | 0 | f55e72c | 734 | | 0:00 | 19 |
| S | root | 31 | 0 | f66e4720 | 1637 | | 0:00 | 18 |
| S | root | 32 | 0 | f52e1714 | 2041 | | 0:00 | 19 |
| S | root | 33 | 0 | f62a1a18 | 1040 | | 0:00 | 18 |
| S | root | 34 | 0 | f61de8d30 | 799 | | 0:00 | 19 |
| S | root | 35 | 0 | f60e5260 | 631 | | 0:00 | 18 |
| S | root | 36 | 0 | f62e1238 | 1450 | | 0:00 | 19 |
| S | root | 37 | 0 | f62e18b8 | 1952 | | 0:00 | 18 |
| S | root | 38 | 0 | f52f5728 | 2275 | | 0:00 | 19 |
| S | root | 39 | 0 | f21b6a3a | 2163 | | 0:00 | 18 |
| S | root | 40 | 0 | f61bd8739 | 427 | | 0:00 | 19 |

## 杀死进程

`ps` 提供了系统中运行进程的快速概览。要获取更详细的信息，可以包含 `-ef` 选项，它包含了许多有用信息，如下所示：![](img/696df54e51231f8e64fd117ac1127_756_0.png)

在多处理器系统上，你可能会看到此数字超过 100%。双处理器系统可能会显示 200%。这因变体而异。

## 信号

当你执行 `kill` 命令和进程号时，你同时也发送了与 `kill` 相关的信号。我们在 `kill` 示例中没有指定信号；但是，使用了默认信号 15，即 `SIGTERM`。这些信号被系统用于与进程进行通信。我们用于终止进程的信号 15 是一种软终止信号，通常足够终止用户进程，如我们发现的那样。难以杀死的进程可能需要 `SIGKILL` 或 9 信号。

...该过程的一部分。我仅将其作为最后手段，因为使用 `SIGKILL` 杀死的进程并不总是能平稳退出。要在外壳（`shell`）中杀死此类进程，你有时必须使用 `SIGKILL`。

你可以使用信号名称或数字。这些信号数字在不同系统之间可能有所不同，请查看信号的手手册页（通常在第 5 节）以查看你系统上的信号列表。以下是一些最常用的信号编号及其对应的信号：

| 信号编号 | 信号名称 |
|---|---|
| 1 | SIGHUP |
| 2 | SIGINT |
| 3 | SIGQUIT |
| 9 | SIGKILL |
| 15 | SIGTERM |
| 24 | SIGSTOP |

要用 `SIGKILL` 杀死 ID 为 234 的进程，你需要执行以下命令：

```
$ kill -9 234
```

> 进程 ID (PID)
> 信号编号
> 终止进程的 `kill` 命令

## 使用 showmount 显示远程挂载

`mount` 用于显示所有挂载了本地文件系统的远程系统（客户端）。`showmount` 有助于确定 NFS 客户端最常挂载的文件系统。`showmount` 的输出特别易读，因为它列出了客户端挂载的主机名和目录。

![](img/6969df54e516231f8e64fd1177ac1127_759_0.png)

### NFS 信号与资源消耗

NFS 服务器通常会为许多最初并非旨在服务的 NFS 客户端提供服务。这种情况会导致 NFS 服务器消耗额外的 UNIX 系统资源，以及额外的网络带宽。请记住，从 NFS 服务器传输到 NFS 客户端的任何数据都会消耗网络带宽，在某些情况下，如果从 NFS 服务器向客户端传输大文件或应用程序，可能会消耗大量的带宽。以下示例是从系统中获取的 `showmount` 部分输出。`showmount` 运行我在在本章中使用的 HP-UX、AIX 和 Linux 系统上，但在 Solaris 系统上不运行：

```
# showmount -a
ys100.ct.mp.com:/applic
ys101.ct.mp.com:/applic
ys102.cal.mp.com:/applic
ys103.cal.mp.com:/applic
ys104.cal.mp.com:/applic
ys105.cal.mp.com:/applic
ys106.cal.mp.com:/applic
ys107.cal.mp.com:/applic
ys108.cal.mp.com:/applic
ys109.cal.mp.com:/applic
sys200.cal.mp.com:/usr/users
sys201.cal.mp.com:/usr/users
sys202.cal.mp.com:/usr/users
sys203.cal.mp.com:/usr/users
sys204.cal.mp.com:/usr/users
ys205.cal.mp.com:/usr/users
sys206.cal.mp.com:/usr/users

# showmount -a
sys207.cal.mp.com:/usr/users
sys208.cal.mp.com:/usr/users
sys209.cal.mp.com:/usr/users
```

`showmount` 命令有以下三个选项可用：

- `-a` 以“名称:目录”的格式输出，如上所示。
- `-d` 列出所有被客户端远程挂载的本地目录。
- `-e` 打印导出文件系统的列表。

以下是 `showmount -d` 和 `showmount -e` 的示例：

```
# showmount -d
/applic
/usr/users
/usr/oracle
/usr/users/emp.data
/network/database
/network/users
/tmp/working
```

```
# showmount -e
export list for server101.cal.mp.com
/applic
/usr/users
/edrom
```

## 显示系统交换 (Swap)

如果你的系统内存不足以处理工作所需的所有信息，它会将信息页移动到交换区域，或将整个进程交换到交换区域。最近使用的页面保留在主内存中，而最近未使用的将首先被移出内存。

系统管理员花费大量时间为他们的系统确定正确的交换空间大小。交换不足可能会防止系统启动额外的进程、导致应用程序挂起或不允许额外的用户访问系统。足够的交换空间可以防止这些问题的发生。系统管理员通常通过考虑许多重要因素来确定正确的交换空间大小，包括以下：

- 1. 你运行的应用程序推荐多少交换空间？使用应用程序推荐的交换大小。应用程序供应商在推荐交换空间时往往是实际的。应用程序供应商之间有时会竞争声明最低的内存和 CPU 要求，以保持解决方案的整体成本最低，但交换空间的建议通常是实际的。
- 2. 你将同时运行多少应用程序？如果你正在运行多个应用程序，请汇总计划同时运行的每个应用程序推荐的交换空间。如果你有一个推荐 200 MBytes 交换空间的数据库应用程序和一个推荐 100 MBytes 交换空间的开发工具，那么请至少为你的系统配置 300 MBytes 的交换空间。
