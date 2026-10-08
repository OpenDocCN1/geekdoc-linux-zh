
对于系统管理员来说，将应用程序与操作系统隔离开来是非常理想的，这样可以避免应用程序文件意外覆盖操作系统文件。此外，如果应用程序加载在独立的区域中，它们就是“模块化的”，这意味着系统管理员可以添加、删除和修改这些应用程序，而不会影响操作系统或其他应用程序。应用程序存储在 /opt 目录中。

- 系统内部文件与系统外部文件（即可通过网络访问的文件）分开保存在独立的区域中。/usr 和 /sbin 是共享的操作系统目录。这两个目录中不包含任何特定于主机的信息。/etc 用于存放特定于主机的配置文件。
- 可执行文件与系统配置文件分开保存，以便可执行文件可以在主机之间共享。将配置文件与使用它们的程序分开还意味着操作系统的更新不会影响配置文件。

我将描述文件系统布局中一些最重要的目录。

/ 这是根目录，是文件系统层次树结构的基础。目录在逻辑上被视为 / 的一部分。无论目录或逻辑卷存储在哪个磁盘上，它在逻辑上都被视为根层次结构的一部分。

*/dev* 包含特定于主机的设备文件。

*/etc* 包含特定于主机的系统和应用程序配置文件。此目录中的信息对于系统运行至关重要，且具有永久性质。*/etc* 下方还有额外的配置目录。有两个特定的 */etc* 子目录值得特别注意：

*/export* 服务器为网络客户端导出根目录。例如，服务器可能会导出诸如 */export/home/username* 这样的用户目录。

*/home* 用户的主目录位于此处。由于存储在用户主目录中的数据经常被修改，因此您可以预期此目录的大小会增加。

*/kernel* 包含启动系统（如 genux）所需的内核配置和二进制文件。

*/lost+found* 这是丢失文件目录。在这里您可以找到正在使用但未关联到任何目录的文件。这些文件通常由于系统崩溃而导致磁盘上的物理信息与逻辑目录之间的链接断开而变得“丢失”。在启动时运行的程序 **fsck** 会找到这些文件并将它们放入 **lost+found** 目录中。

**/mnt** 此目录保留作为本地文件系统的挂载点。您可以直接挂载到 **/mnt**，或者使用 **/mnt** 的子目录作为挂载点，例如 **/mnt1**、**/mnt2**、**/mnt3** 等。

**/net** 保留名称，作为远程文件系统的挂载点。

**/opt** 应用程序安装在此目录之下。通常，应用程序供应商从不指定其应用程序安装的具体位置。现在，有了 **/opt**，我们就有了一个标准的目录，应用程序应该安装在该目录之下。这对系统管理员来说是一个组织上的改进，因为我们现在可以预期应用程序加载在 **/opt** 及应用程序名称之下。

**/sbin** 包含用于启动、关闭以及修复文件系统挂载问题的命令和脚本。系统启动时 **/sbin** 是可用的，因为它包含启动系统所需的命令。

/stand 包含启动系统所需的内核配置和二进制文件。此目录中包含两个重要文件，即 system 文件和 vmunix（内核）文件。

/tmp 这是一个自由的目录，任何用户都可以*临时存储*文件。由于此目录性质松散，因此不应用于存储任何重要内容，并且用户应知道他们存储在 /tmp 中的任何内容都可能随时被删除，而无需通知。应用程序的工作文件应放在 /var/tmp 或 /var/opt/appname 中，而不是 /tmp。

/usr 大多数 UNIX 操作系统都包含在 /usr 中。此目录包含命令、库和文档。/usr 中只有限数量的子目录可以出现。

/var 存储主要是临时性的文件。像日志文件这样经常删除和修改的文件就存储在这里。可以将其视为一个“可变”大小的目录。应用程序或命令在运行时创建的文件应放置在此目录中，包括日志和打印输出文件。但是，某些应用程序可能会在 /var 中存储状态信息。

## Linux 文件系统布局

Linux 的文件系统布局与前面描述的其他 UNIX 变体非常相似，无论在概念上还是在实现上都是如此。文件包含在目录中，而目录可以拥有任意数量的子目录。大多数操作系统都是这样组织的，包括 UNIX。

以下是 Caldera Linux 系统根级别的长列表：

![](img/75f39fc91296b889c0653851accdfd46_105_0.png)

```
# ls -l /
total 439
-rw-mw-mw-    1 root      root          23 Nov  5 07:10 .lgdb
... (包含 ., .., amd, auto, bin, boot, dev, etc, home, initrd, install, LST, lib, lost+found, mnt, opt, proc, root, sbin, tmp, usr, var, vmlinuz 的多行文件列表)
... (截断)
```

大多数目录与前面描述的相同。有两个目录名称之前没有提到过，但具有重要意义。Linux 内核 **vmlinuz** 出现在根级别。目录 **/root** 是用户 *root* 的主目录。

**/proc** 目录包含有关 Linux 系统的信息。**/proc** 目录实际上是一组看起来像目录的数据结构信息。以下是 /proc 目录的长列表：

```
# ls -l /proc
total 0
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 1
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 1011
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 104
dr-xr-xr-x    3 bin      root            0 Nov  7 00:13 106
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 116
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 118
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 146
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 155
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 156
dr-xr-xr-x    3 daemon   root            0 Nov  7 00:13 162
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 167
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 170
dr-xr-xr-x    3 root     65535           0 Nov  7 00:13 178
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 18
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 19
dr-xr-xr-x    3 nobody   65535           0 Nov  7 00:13 193
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 199
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 2
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 20
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 200
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 201
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 202
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 203
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 204
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 205
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 21
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 273
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 274
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 276
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 3
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 307
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 327
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 358
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 375
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 443
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 444
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 445
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 45
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 482
dr-xr-xr-x    3 root     root            0 Nov  7 00:13 483
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 996
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 997
dr-xr-xr-x    3 root     root            0 Nov  7 00:16 998
-r--r-----    1 root     root            0 Nov  7 00:13 cmdline
-r--r-----    1 root     root            0 Nov  7 00:13 cpuinfo
-r--r-----    1 root     root            0 Nov  7 00:13 devices
-r--r-----    1 root     root            0 Nov  7 00:13 dma
-r--r-----    1 root     root            0 Nov  7 00:13 filesys
-r--r-----    1 root     root            0 Nov  7 00:13 interrupt
-r--r-----    1 root     root            0 Nov  7 00:13 ioports
-r--------    1 root     root        33558528 Nov  7 00:13 kcore
```
