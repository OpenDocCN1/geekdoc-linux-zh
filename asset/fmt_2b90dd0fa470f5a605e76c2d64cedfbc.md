
`martyp $`

在此示例中，第一列是标志位 `F`。`F` 提供有关进程是否已交换、是否在内核中、是否为系统进程等的八进制信息。八进制值在不同系统间有时会有所不同，因此请查阅您系统的手册页以了解标志位的八进制值。

`S` 代表状态。状态可以是睡眠，如示例中大多数进程所示的 `S` 状态、等待、运行、中间状态、终止等。同样，这些值在不同系统间可能有所不同，请查阅您的手册页。

此输出中还有一些其他有用的信息：`NI` 代表 nice 值；`ADDR` 代表进程的内存地址；`SZ` 代表进程的物理页大小；以及 `WCHAN`，即进程正在等待的事件。

## 终止进程

如果您执行 `ps` 命令并发现其中一个进程已挂起，或者您启动了一个希望停止的大任务，可以通过 `kill` 命令来实现。`kill` 是一个向您指定的进程发送信号的工具。您可以 `kill` 任何您拥有的进程。此外，超级用户可以 `kill` 系统中的几乎所有进程。

要 `kill` 您拥有的进程，只需发出 `kill` 命令和进程 ID（`PID`）。以下示例展示了如何发出 `ps` 命令以查找 `martyp` 拥有的所有进程，终止一个进程，并检查该进程是否已消失：

```
martyp $ ps -ef | grep martyp
 martyp 19336 19334 0 05:24:32 pts/4 0:01 -ksh
 martyp 19426 19336 0 06:01:01 pts/4 0:00 grep martyp
 martyp 19424 19336 5 06:00:48 pts/4 0:01 find / -name .login
martyp $ kill 19424
martyp $ ps -ef | grep martyp
 martyp 19336 19334 0 05:24:32 pts/4 0:01 -ksh
 martyp 19428 19336 1 06:01:17 pts/4 0:00 grep martyp
[1] + Terminated        find / -name .login &
martyp $
```

该示例展示了如何终止进程 `19424`，该进程由 `martyp` 拥有。我们通过重新发出 `ps` 命令来确认该进程确实已被终止。

您可以发出 `kill` 命令，后跟以空格分隔的所有希望 `kill` 的进程号列表，从而在命令行上 `kill` 多个进程。

如果您是以超级用户身份登录，在终止进程时请格外小心。您可能会对系统的运行方式产生不利影响，并可能需要手动重启进程或重新启动系统。

### 信号

![](img/75f39fc91296b889c0653851accdfd46_904_0.png)

当您发出 `kill` 命令和进程号时，您也在发送与 `kill` 相关联的 *signal*（信号）。我们在我们的 `kill` 示例中未指定 *signal*；但是，默认的信号 15，或 `SIGTERM`，被使用了。这些 *signals* 用于系统与进程通信。我们用来终止进程的 *signal* 15 是一种软件终止 *signal*，通常足以终止用户进程，如我们启动的 `find`。难以终止的进程可能需要 `SIGKILL`，或 9 *signal*。此 *signal* 会导致进程立即终止。我仅在最后手段时才使用它，因为以 `SIGKILL` 终止的进程并不总是能平滑终止。对于 shell 等进程，有时必须使用 `SIGKILL`。

![](img/75f39fc91296b889c0653851accdfd46_904_1.png)

您可以使用 *signal* 名称或编号。这些信号编号在不同系统间有时会有所不同，因此请查看 *signal* 的手册页，通常在第 5 节，以查看您系统上的 *signals* 列表。以下是一些最常用的 *signal* 编号及其对应 *signals* 的列表：

| Signal number | Signal |
| :--- | :--- |
| 1 | `SIGHUP` |
| 2 | `SIGINT` |
| 3 | `SIGQUIT` |
| 9 | `SIGKILL` |
| 15 | `SIGTERM` |
| 24 | `SIGSTOP` |

要使用 `SIGKILL` 终止 id 为 `234` 的进程，您需要发出以下命令：

```
$ kill -9 234
```

- `kill` 命令以终止进程
- 信号编号
- 进程 ID（`PID`）

![](img/75f39fc91296b889c0653851accdfd46_905_0.png)

## 使用 `showmount` 显示远程挂载

`showmount` 用于显示所有已挂载本地文件系统的远程系统（客户端）。`showmount` 对于确定客户端最常通过 NFS 挂载的文件系统非常有用。`showmount` 的输出特别易于阅读，因为它列出了客户端挂载的主机名和目录。

NFS 服务器最终往往服务于许多原本未打算由其服务的 NFS 客户端。这种情况最终会消耗 NFS 服务器上额外的 UNIX 系统资源以及额外的网络带宽。请记住，从 NFS 服务器传输到 NFS 客户端的任何数据都会消耗网络带宽，并且在某些情况下，如果从 NFS 服务器向客户端传输大文件或应用程序，可能会消耗大量带宽。以下示例是来自某个系统的 `showmount` 的部分输出。`showmount` 在我整个章节中使用的 HP-UX、AIX 和 Linux 系统上运行，但在 Solaris 系统上不运行：

```
# showmount -a
sys100.ct.mp.com//applic
sys101.ct.mp.com//applic
sys102.cal.mp.com//applic
sys103.cal.mp.com//applic
sys104.cal.mp.com//applic
sys105.cal.mp.com//applic
sys106.cal.mp.com//applic
sys107.cal.mp.com//applic
sys108.cal.mp.com//applic
sys109.cal.mp.com//applic
```

```
# showmount -a
sys200.cal.mp.com:/usr/users
sys201.cal.mp.com:/usr/users
sys202.cal.mp.com:/usr/users
sys203.cal.mp.com:/usr/users
sys204.cal.mp.com:/usr/users
sys205.cal.mp.com:/usr/users
sys206.cal.mp.com:/usr/users
sys207.cal.mp.com:/usr/users
sys208.cal.mp.com:/usr/users
sys209.cal.mp.com:/usr/users
```

`showmount` 命令提供以下三个选项：

- `-a` 以“name:directory”格式打印输出，如上面所示。
- `-d` 列出客户端已远程挂载的所有本地目录。
- `-e` 打印已导出文件系统的列表。

以下是 `showmount -d` 和 `-e` 的示例：

```
# showmount -d
/applic
/usr/users
/usr/oracle
/usr/users/emp.data
/network/database
/network/users
```

![](img/75f39fc91296b889c0653851accdfd46_906_0.png)

```
# showmount -d
/tmp/working
```

```
# showmount -e
export list for server101.cal.mp.com
/applic
/usr/users
/cdrom
```

## 显示系统交换空间

如果系统的主内存不足以容纳其工作所需的所有信息，它会将信息页面移动到交换区域，或将整个进程移动到交换区域。最近使用的页面会保留在主内存中，而那些不常被使用的页面将首先被移出主内存。

系统管理员花费大量时间来确定其系统合适的交换空间大小。交换空间不足可能会阻止系统启动额外的进程，使应用程序挂起，或不允许更多用户访问系统。拥有足够的交换空间可以防止这些问题发生。系统管理员通常通过考虑许多重要因素来确定合适的交换空间大小，其中包括以下三点：

1. 你运行的应用程序推荐多少交换空间？请使用你的应用程序推荐的交换空间大小。应用程序供应商在推荐交换空间时往往比较现实。有时应用程序供应商之间会竞争声称最低的内存和 CPU 要求，以使解决方案的总体成本尽可能低，但交换空间推荐值通常是现实的。

2. 你将同时运行多少应用程序？如果你正在运行几个应用程序，请将你计划同时运行的每个应用程序推荐的交换空间相加。例如，如果你有一个数据库应用推荐 200 MBytes 的交换空间，和一个开发工具推荐 100 MBytes 的交换空间，那么请为你的系统配置至少 300 MBytes 的交换空间。
