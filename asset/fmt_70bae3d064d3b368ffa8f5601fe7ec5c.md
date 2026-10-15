
## 内存与NFS性能测试

`BigTotal:    0 kB`

`BigFree:     0 kB`

`SwapTotal:   265032 kB`

`SwapFree:    258968 kB`

3. 系统总内存量显示在`total`列标题下；将此数字除以`1048576`（`1024×1024`）即可得到总（近似）内存大小（单位为`MB`）。在上面的示例中，该数值为`251MB`。有趣的是，大多数`PC`系统的`BIOS`都不会准确报告总内存，因此您必须根据对总内存的了解对数字进行四舍五入。在我的示例中，我知道系统应该有`256MB`的`RAM`，因此我将使用`256MB`作为此测试中的内存大小。
4. 现在切换到当前已挂载的`/mnt/nfs1``NFS`文件目录。运行`du`命令检查`NFS`目录上是否至少有`512MB`（`2×`总`RAM`）的可用空间。如果没有，您无法继续此实验。
5. 下一个任务是通过在`/mnt/nfs1`目录中写入一个名为`512MB.dat`的文件（`16K/块 × 32,768 块`），来测量当前`NFS`设置的写入性能。请使用以下命令执行此操作：

```
time dd if=/dev/zero \
    of=/mnt/nfs1/512MB.dat \
    bs=16k count=32768
```

此命令运行`time`命令，该命令记录名为第一个参数的程序的执行时间。在这种情况下，正在计时的是`dd`命令。给`dd`命令一个输入文件（使用`if`选项），名为`/dev/zero`。这是一个特殊设备，读取时返回`0`（零）字符。换句话说，如果您打开此文件进行读取，它将不断返回`0`字符，直到您关闭文件。这为我们提供了一个填充输出文件（使用`of`选项指定，名为`/mnt/nfs1/512MB.dat`）的便捷来源；`dd`命令被指示使用`16K`的块大小（使用`bs`选项指定）并总共写入`32,768`个块（使用`count`选项指定）。由于`16K/块`乘以`32,768`块等于`512MB`，您将创建预期的文件。执行此命令后，它会打印几行内容，例如以下所示：

```
32768+0 records in
32768+0 records out
1.610u 71.800s 1:58.91  61.7%  0+0k  0+0io 202pf+0w
```

这里，`dd`命令从`/dev/zero`设备读取了`32,768`条记录，并向`/mnt/nfs1/512MB.dat`文件写回了相同数量的记录。第三行表明复制操作耗时`1`分`58.91`秒。请按如下方式将此行记录在文本文件中：

```
Write, 1, 1.610u, 71.800s, 1:58.91, 61.7%
```

这里您正在记录这是第一次 (`1`) 写入实验。

6. 要测量当前`NFS`设置的读取性能，您只需读取步骤 5 中创建的`512MB`文件，看看读取它需要多长时间。要读取该文件并对读取访问进行计时，请运行以下命令：

```
time dd if=/mnt/nfs1/512MB.dat \
     of=/dev/null \
     bs=16k count=32768
```

这里，`dd`命令再次被计时，它将`/mnt/nfs1/512MB.dat`文件作为输入读取，并将文件内容输出到`/dev/null`，后者是`Linux`中官方的无底深渊。与此前一样，您应该在记录读取性能记录的同一文件中记录使用的时间。例如，在我的系统上，使用上述命令进行的读取测试显示了以下输出。

请按如下方式记录第三行：

```
Read, 1, 1.970u, 38.970s, 2:10.44, 31.3%
```

这里您正在记录这是第一次 (`1`) 读取实验。

7. 现在从`/mnt/nfs1`中删除`512MB.dat`文件，并使用`umount /mnt/nfs1`命令卸载该分区。卸载`NFS`目录可确保磁盘缓存不会影响您下一组测试。
8. 重复写入和读回测试（步骤 5 到 7）至少五次。您应该有如下所示的一组记录：

```
Read,   1. 1.971u, 38.970s,  2:10.44, 31.3%
Read,   2. 1.973u, 38.970s,  2:10.49, 31.3%
Read,   3. 1.970u, 38.971s,  2:10.49, 31.3%
Read,   4. 1.978u, 38.970s,  2:10.49, 31.3%
Read,   5. 1.978u, 38.971s,  2:10.49, 31.3%
Write, 1. 1.610u, 71.800s,  1:58.91, 61.7%
Write. 2. 1.610u, 71.801s, 1:58.92, 61.7%
Write. 3. 1.610u, 71.801s, 1:58.92, 61.7%
Write. 4. 1.610u, 71.801s, 1:58.92, 61.7%
Write. 5. 1.611u, 71.809s, 1:58.92, 61.7%
```

9. 现在从第五列（以粗体显示）计算平均读取和写入时间。

此测试的第一阶段现在已完成。您发现了`512MB`文件的平均读取和写入访问时间。对于测试的第二阶段，请遵循以下步骤：

1. 使用`umount /mnt/nfs1`命令在`NFS`客户端系统上卸载`/mnt/nfs1`目录。
2. 修改`NFS`客户端系统上的`/etc/fstab`文件，使`/mnt/nfs1`文件系统使用`size=8192, wsize=8192`选项挂载，如下所示。

```
nfs-server-host:/nfs1 /mnt/nfs1 nfs \
size=8192,wsize=8192 0 0
```

3. 使用`mount /mnt/nfs1`命令重新挂载`/mnt/nfs1`目录。
4. 执行实验第一阶段中的步骤 4 到 9。
5. 比较测试阶段 1 和阶段 2 的读取和写入访问平均值。如果测试阶段 2（此部分）的结果看起来更好，那么更改读取和写入块提高了您的`NFS`性能。如果没有，请从`/etc/fstab`中的该行移除`size=8192, wsize=8192`选项。读取和写入块大小的更改很可能会提高`NFS`性能。您还可以尝试其他块大小。建议使用`1024`的倍数作为块大小，因为`1024`是实际的文件系统块大小。此外，不要使用大于`8192`字节的数字。如果块大小更改对您有效，请在`/etc/fstab`中`/mnt/nfs1`定义的行中保留`size=8192, wsize=8192`（或通过进一步实验找到的最佳值）。

## 设置适当的最大传输单元

最大传输单元 (`MTU`) 值决定了单个数据包传输可以有多大。如果`MTU`设置得太小，`NFS`性能会严重受损。要发现合适的`MTU`设置，请执行以下操作：

1. 在`NFS`客户端系统上`su`切换到`root`用户。
2. 运行`trac-path nfsserver/2049`命令，其中`nfsserver`是您的`NFS`服务器的主机名。该命令将报告该路径的`MTU`。
3. 检查用于访问`NFS`服务器的网络接口的当前`MTU`。您可以简单运行`ifconfig`命令列出所有正在运行的网络接口的信息。
4. 如果您发现适当网络接口的`MTU`设置与`trac-path`命令报告的不一致，请使用带有`mtu`选项的`ifconfig`命令进行设置。例如，`ifconfig eth0 mtu 512`命令将网络接口`eth0`的`MTU`设置为`512`字节。

## 运行最优数量的 NFS 守护进程

默认情况下，您运行八个`NFS`守护进程。如果您想查看每个`nfssd`线程的使用强度，请运行`cat /proc/net/rpc/nfsd`命令。该文件中`th`行的最后十个数字表示`nfssd`线程使用率处于该百分比（最大允许值）的秒数。如果前三个十分位数中有较大的数字，您可能希望增加`nfssd`实例的数量。要更改服务器启动时启动的`NFS`守护进程数量，请执行以下操作：

1. 作为`root`，如果您当前正在运行它，请使用`/etc/rc.d/init.d/nfs stop`命令停止`nfssd`。
2. 修改`/etc/rc.d/init.d/nfs`脚本，将`RPCNFSDCOUNT=8`设置为适当数量的`NFS`守护进程。
3. 使用`/etc/rc.d/init.d/nfs start`命令重启`nfssd`。

## 控制套接字输入队列大小

默认情况下，`Linux`使用`65535`字节（`64KB`）的套接字输入队列。如果您在系统上运行`8`个`NFS`守护进程（`nfssd`），每个守护进程获得`8K`缓冲区来在输入队列中存储数据。您应该将队列大小增加到至少`256KB`，如下所示：

1. 作为`root`，如果您当前正在运行它，请使用`/etc/rc.d/init.d/nfs stop`命令停止`nfssd`。
2. 修改`/etc/rc.d/init.d/nfs`脚本，使得在通过守护进程行`rpc.nfsd $RPCNFSDCOUNT`启动`NFS`守护进程（`nfssd`）之前，添加以下行：
   ```
   echo 262144 > /proc/sys/net/core/rmem_default
   echo 262144 > /proc/sys/net/core/rmem_max
   ```
3. 在守护进程行`rpc.nfsd $RPCNFSDCOUNT`之后立即添加以下行：
   ```
   echo 65536 > /proc/sys/net/core/rmem_default
   echo 65536 > /proc/sys/net/core/rmem_max
   ```
4. 使用`/etc/rc.d/init.d/nfs start`命令重启`NFS`守护进程。

现在，由`/etc/rc.d/init.d/nfs`脚本启动的每个`NFS`守护进程将使用套接字输入队列中的`32K`缓冲空间。

## 监控数据包碎片

`Linux`内核使用从高到低的范围来控制其能够处理的未处理`UDP`数据包碎片数量。当未处理的`UDP`数据包碎片大小达到高阈值（通常为`262144`字节或`256K`）时，内核会丢弃传入的数据包碎片。换句话说，当`UDP`数据包碎片达到高阈值时，就开始出现丢包。数据包碎片的丢失会持续，直到未处理碎片的总大小达到低阈值（通常为`196608`字节或`192K`）。

由于`NFS`协议使用分片的`UDP`数据包，`Linux`使用的上述从高到低的阈值对`NFS`性能有很大影响。你可以通过运行`cat /proc/sys/net/ipv4/ipfrag_high_thresh`命令来查看当前高阈值大小的值。同样，你可以通过运行`cat /proc/sys/net/ipv4/ipfrag_low_thresh`命令来查看低阈值的值。你可以通过运行`echo high_number > /proc/sys/net/ipv4/ipfrag_high_thresh`来更改高值，类似地，运行`echo low_number > /proc/sys/net/ipv4/ipfrag_low_thresh`可更改低数值。

## 在 Web 服务器之间复制内容

通常，内容是在单个（主）服务器上开发和放置的，然后分发到参与`Web`网络的所有其他`Web`服务器。在本节中，我将讨论一个名为`rdist`的工具，它允许你将内容从一个`Linux`系统分发到其他系统。

### 使用 rdist 分发文件

`rdist`程序使你可以在多台主机上维护文件的相同副本。它使用`rcmd`函数调用或远程 shell（`rsh`）来访问每个目标主机计算机。

让`rdist`运行的最简单方法是在所有涉及的机器上创建一个通用账户，并为每个目标`Web`服务器系统创建`.rhosts`文件，以便命名服务器主机上的通用用户被允许运行`rsh`会话。为此，请在所有三个涉及的系统上创建一个名为`httpd`的用户。在每个`Web`服务器系统上，在`httpd`用户的主目录中添加一个`.rhosts`文件。此文件包含`rdist`服务器的主机名，位于单行中。

`.rhosts`文件必须由`root`用户拥有，并且对其他所有人只读。这允许在`rdist`服务器上名为`httpd`的用户在每个`Web`服务器系统上运行远程 shell 会话。如果你按照前面的章节说明创建了后端网络，你应该使用与后端网络接口关联的`rdist`服务器主机名，这使你能够将`rdist`生成的文件流量保留在后端网络中；因此，数据包不会与你的`Web`流量竞争。下一步是为`rdist`创建一个`distfile`。`distfile`是一个文本文件，其中包含`rdist`如何执行文件分发任务的指令。列表 23-2 显示了这样一个`distfile`，`rdist_distfile`。

#### 列表 23-2：rdist_distfile

```
# Distfile for rdist
#
# This is used to distribute files from ns.domain.com
# to www[12].domain.com systems
#
# $Author$ (kabir@ntec.com)
# $Version$
# $Date$
# $Id$
# List all the hosts that need to be updated.
# The list is created using user@hostname entries where each
# entry is separated by a whitespace character.
#
HOSTS = (httpd@www1.domain.com httpd@www2.domain.com)
# List the directories that need to be updated.
#
FILES = (//www)
# list the directories that need to be excluded from
# the update process.
EXCLUDE_DIR = (//www/cgi-data/ //www/apache //www/secured)
# Here are the commands:
# Install all directories listed in FILES for all hosts
# listed in HOSTS except for the directories that are
# listed in EXCLUDE_DIR
#
#!/FILES/ -> ${HOSTS}
install :
    except ${EXCLUDE_DIR};
```

这确实是一个非常简单的`distfile`。它定义了一个名为`HOSTS`的变量，该变量有两个条目作为值：`httpd@www1.domain.com`和`httpd@www2.domain.com`。这告诉`rdist`使用`www1.domain.com`和`www2.domain.com`上的`httpd`用户账户进行连接。下一个变量`FILES`定义了`rdist`要分发的文件和目录。此脚本假设暂存服务器将所有文件保留在`/www`目录或分区中。你可以更改此路径或添加多个路径（以空格分隔）。

第三个变量是`EXCLUDE_DIR`。该变量设置为列出我们希望从分发过程中排除的所有文件和目录。示例中看到的值很重要。第一个目录`/www/cgi-data/`是`CGI`数据目录，所有`CGI`脚本都将数据写入此目录。此目录将通过`NFS`导出到`Web`服务器主机，因此无需通过`rdist`复制到每个`Web`服务器。`/www/apache`目录是`makesite`写入`/www/apache/conf/httpd.conf`文件的位置，该文件需要复制，因为每个`Web`服务器在其本地的`/www/apache`目录中都有其自己的`Apache`配置文件。最后一个值是`/www/secured`，它由`secure`服务器用作文档根目录，需要复制到`Web`服务器上。文件的其余部分描述了一个简单命令：

```shell
$ {FILES} -> ${HOSTS}
    install ;
    except ${EXCLUDE_DIR};
```

此命令获取`FILES`变量指向的所有文件和目录，并将它们安装到`HOSTS`变量指示的主机上。它还告诉`rdist`排除`EXCLUDE_DIR`变量指定的文件和目录。要以`httpd`身份运行`rdist`，请使用以下命令行：

```shell
/usr/bin/rdist -p /usr/sbin/rdistd \
     -oremove,quiet \
     -f /usr/local/rdist/ rdist_distfile
```

`-p`选项指定`rdist`所需的`rdist`程序的位置；`-o`选项指定一个或多个选项将跟随——在这种情况下，是`remove`和`quiet`。`remove`选项告诉`rdist`删除目标系统中目标目录中发现的任何错误文件。这提供了一种简单的方法来维护每个`Web`服务器上暂存区域的相同副本。`quiet`选项告诉`rdist`在操作期间尽可能保持安静。最后一个选项`-f`指定`distfile`的位置。

为了减少运行此命令时的人为错误，请创建一个名为`rdistribute.sh`的`sh`脚本，如列表 23-3 所示。

#### 列表 23-3：rdistribute.sh 脚本

```shell
#!/bin/sh
#
# This script runs rdist to update Web servers via the
# non-routable lan domain.com. The script is run
```
