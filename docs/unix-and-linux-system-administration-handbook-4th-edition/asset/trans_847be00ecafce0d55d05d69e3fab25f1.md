

在 Solaris 和 HP-UX 上，**automount** 在出现问题时可以平滑地从一个复制的挂载服务器切换到另一个服务器。此功能仅 supposed 适用于只读挂载，但据传读写挂载的处理比文档所述更合理。当 **automount** 切换服务器时，对已打开用于写入的文件的引用仍会挂起，这也是复制的读写挂载可能不太有用的又一个原因。

尽管 **automount** 可以根据自身的效率和局部性标准在复制服务器中进行选择，但你也可以根据需要分配显式优先级。优先级是小整数，数字越大优先级越低。默认优先级为 0，最优选。

一个定义 **/usr/man** 和 **/cs/tools** 为复制文件系统的 **auto.direct** 文件可能如下所示：

```
    /usr/man    -ro harp:/usr/share/man monk(1):/usr/man
    /cs/tools   -ro leopard,monk:/cs/tools
```

请注意，如果每个服务器上的源路径相同，则可以一起列出服务器名称。第一行中 monk 后的 (1) 设置了该服务器相对于 **/usr/man** 的优先级。harp 后没有优先级表示隐式优先级为 0。

## 自动 automount（V3；除 Linux 外）

不必在直接或间接映射中列出每个可能的挂载，你可以告诉 **automount** 一些关于你的文件系统命名约定的信息，让它自行推断。使这项工作得以实现的关键粘合部分是，远程服务器上运行的 **mountd** 可以被查询以了解服务器导出了哪些文件系统。在 NFS 版本 4 中，导出始终是 /，这消除了对这种自动化的需求。

有几种方法可以配置“自动 automount”，其中最简单的是 -hosts 挂载类型。如果你在主映射文件中将 -hosts 列为映射名称，**automount** 就会将远程主机的导出映射到指定的 automount 目录中：

```
    /net    -hosts -nousid,soft
```

例如，如果 harp 导出了 **/usr/share/man**，则该目录可以通过 automounter 在路径 **/net/harp/usr/share/man** 下访问。

-hosts 的实现不会枚举所有可能挂载文件系统的主机；那是不可能的。相反，它会等待对各个子目录名称的引用，然后再去挂载所请求主机导出的文件系统。

在间接映射文件中使用 * 和 & 通配符可以实现类似但更精细的效果。此外，还有许多可在映射中使用的宏可扩展为当前主机名、体系结构类型等。详情请参阅 automount(1M) 手册页。

## Linux 的具体说明

Linux 对 automount 的实现与 Sun 的有所分化。变化主要与命令和文件的命名有关。

首先，automount 是实际挂载和卸载远程文件系统的守护进程。它填补了其他系统上 automountd 守护进程的角色，通常无需手动运行。

默认的主映射文件是 /etc/auto.master。其格式和间接映射的格式如前所述。然而文档很难找到。主映射格式在 auto.master(5) 中描述，间接映射格式在 autofs(5) 中；请小心，否则你会得到 autofs(8)，它记录了 autofs 命令的语法。 （正如其中一个手册页所说，“文档还有很多不足之处。”）要使对主映射的更改生效，请运行 /etc/init.d/autofs reload，这相当于 Sun 环境下的 automount。

Linux 实现不支持 Solaris 风格的 -hosts 子句用于自动 automount。

## 18.9 推荐阅读

CALLAGHAN, BRENT. NFS Illustrated. Reading, MA: Addison-Wesley, 1999.

STERN, HAL, MIKE EISLER, AND RICARDO LABIAGA. Managing NFS and NIS (2nd Edition). Sebastopol, CA: O'Reilly Media, 2001.

表 18.11 列出了 NFS 协议的各种 RFC。

## 表 18.11 NFS 相关 RFC

| RFC | 标题 | 作者 | 日期 |
|---|---|---|---|
| 1094 | Network File System Protocol Specification | Sun Microsystems | Mar 1989 |
| 1813 | NFS Version 3 Protocol Specification | B. Callaghan et al. | Jun 1995 |
| 2623 | NFS Version 2 and Version 3 Security Issues | M. Eisler | Jun 1999 |
| 2624 | NFS Version 4 Design Considerations | S. Shepler | Jun 1999 |
| 3530 | NFS Version 4 Protocol | S. Shepler et al. | April 2003 |

