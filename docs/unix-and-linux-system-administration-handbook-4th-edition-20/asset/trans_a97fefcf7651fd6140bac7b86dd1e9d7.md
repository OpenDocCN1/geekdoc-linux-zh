

## 复制文件系统与自动挂载 (automount)

附带有一个实用的 `/etc/auto.net` 可执行映射，它以主机名为键，并挂载该主机上所有导的文件系统。

由于自动挂载脚本根据需要动态运行，因此没有在每次更改后都分发主配置文件，也没有预先将其转换为自动挂载器格式；事实上，在 NFS 服务器上，全局配置文件可以使用一个宽松的名称。

## 自动挂载的可见性

当你列出自动挂载文件系统的父目录内容时，无论挂载了多少文件系统，该目录都显示为空。你无法在 GUI 文件系统浏览器中浏览自动挂载的内容。

示例下：

```
$ ls /portal
$ ls /portal/photos
art_class_2010      florissant_1003      rmnp003
blizzard2008       frozen_dead_guy_Oct2009  rmnp_030806
boston021133      greenville_021129      steamboat2006
```

`photos` 目录在 `/portal` 下自动挂载并运行正常。虽然可以通过其完整路径访问它，但查看 `/portal` 目录无法发现它的存在。如果你通过 `fstab` 文件或手动挂载命令挂载了此文件系统，它的行为将像其他目录一样，并作为父目录的成员可见。

解决浏览问题的一种方法是创建一个包含指向自动挂载点的符号链接的影子目录。例如，如果 `/automounts/photos` 是指向 `/portal/photos` 的链接，你可以 `ls` `/automounts` 的内容发现 `photos` 是一个自动挂载的目录。对 `/automounts/photos` 的引用仍然通过自动挂载器路由并正常工作。

遗憾的是，这些符号链接需要维护，除非由脚本定期重建，否则它们可能会与实际的自动挂载不同步。

## 复制文件系统与自动挂载

在某些情况下，只读文件系统（如 `/usr/share`）在多个不同的服务器上可能是相同的。在这种情况下，你可以告诉自动挂载器该文件系统的几个潜在源。它将根据网络号、NFS 协议版本以及对初始查询的响应，基于自己对哪些服务器更近的判断来选择服务器。

虽然自动挂载本身并不查看或不在乎它挂载的文件系统如何，但复制挂载应该代表只读文件系统，如 `/usr/share` 或 `/usr/local/X11`。自动挂载无法在一组服务器之间同步写入，因此复制的读写文件系统用途不大。

## 第 18 章

## 网络文件系统 (NFS)

![](img/579efec8c67772f31ecf34844bbb71a2_764_0.png)

在 Solaris 和 HP-UX 下，发生问题时，**automount** 可以平滑地从复制挂载的一个服务器切换到另一个。此功能本应只对只读挂载正常工作，但据传，读写挂载的处理比文档建议的要合理。然而，直到 **automount** 切换服务器，已打开写入的文件引用将保持有效，这也是为什么复制写挂载可能没用的另一个原因。

**automount** 可以根据自身的效率和局部性标准在复制服务器之间进行选择，如果你喜欢，也可以分配优先级。优先级是小整数，数字越大优先级越低。默认优先级为 0，最优先。

一个 **auto-direct** 文件将 **/usr/man** 和 **/cs/tools** 定义为复制文件系统，可能如下所示：

- - /usr/man -ro harp:/share/man monk(1):/usr/man
- /cs/tools -ro leopard:/cs/tools

注意，如果源路径在每个相同的设备上，可以列出服务器名称。第一行 `monk` 之后的 `(1)` 设置了相对于 **/usr/man** 的服务器优先级。`hard` 之后缺少优先级表示隐含的优先级 0。

## 自动挂载 (V3: Linux 外的所有版本)

与其在直接或间接映射中列出所有可能的挂载，不如告诉 **automount** 一些关于你的文件系统命名规范的信息，让它自己处理。实现此功能的关键胶水是运行在远程服务器上的挂载可以被查询，以找到服务器导出的文件。在 NFS 版本 4 中，导出为 `/`，这消除了对这种自动化的需求。

配置“自动挂载”有多种方法，最的是 `-hosts` 类型。如果你在主文件中将 `*-hosts` 列为映射名称，automount 就会将远程主机的导出映射到指定的自动目录：

```
/net      -hosts -nosuid,soft
```

例如，如果 `harp` 导出了 **/usr/share/man**，则可以通过自动挂载器通过路径 **/net/harp/usr/share/man** 访问目录。

`-hosts` 的实现并没有列出所有可以挂载文件系统的主机；这是不可能。它等待单个子目录名称被引用，然后运行并挂载请求主机的导出文件系统。

通过间接映射文件中的 `*` 和 `&` 通配符可以实现类似但更细粒的效果。此外，映射中可用的许多宏可以扩展为当前主机名、体系类型等。详情请参见 `automount(1M)` 手册页。

## Linux 特有

Linux 的 automount 实现与 Sun 的略有不同。更改主要与命令和文件的命名有关。

首先，automount 是实际上负责挂载和卸载远程系统的守护进程。它通常不需要手动运行。

默认映射文件是 `/etc/auto.master`。它的格式以及间接映射的格式之前已描述过。不过，文档可能很难找到。主映射描述在 `auto.master(5)`，间接映射描述在 `autofs(8)`。要使主映射生效，运行 `/init.d/autofs reload`。Linux 实现不支持 Solaris-hosts 子句。

## 推荐阅读

- CALLAGHAN, BRENT. *NFS Illustrated*. Reading, MA: Addison-Wesley, 1999.
- STERN, HAL, MIKE EISLER, RICARDO. *Managing NFS and NIS (2nd Edition)*. Sebastopol, CA: O'Reilly Media, 2001.

表 18.11 列出了 NFS 的 RFC。

| RFC | 标题 | 日期 |
|---|---|---|
| 1094 | Network File System Protocol Specification | Sun Microsystems | 1989 |
| 1813 | NFS Version 3 Protocol Specification | B. Callahan et al. | 1995 |
| 2623 | NFS Version 2 and Version 3 Security Issues | M. Eisler | 1999 |
| 2624 | NFS Version 4 Design Considerations | S. Shepler | 1999 |
| 3530 | NFS Version 4 Protocol | S. Shepler et al. | 2003 |

## 练习

- E18.1 探索你的本地 NFS 设置。使用了 NFS 吗？还是其他方案？是否使用了自动挂载？做了哪些权衡？
- E18.2 在 NFS 版本 2 和 3 中，`mount`、`nfsd` 和 `portmap` 之间是什么关系？NFS 对 `portmap` 的依赖在安全性方面意味着什么？
- E18.3 NFS 版本 3 和 4 之间有哪些概念上的变化？有状态与无状态的问题如何改变协议的其他属性？
- E18.4 你的雇主需要通过 NFS 导出 /usr 和 /usr/local。你有以下信息和请求：
  a) 因为办公室政治，你只想你的部门（本地子网 192.168.123.0/24）可以使用这些导出的文件系统。为了实现此配置需要在哪些文件中添加哪些行？注意正确的导出选项。
  b) 列出使 `mount` 和 `nfsd` 识别这些新共享文件系统所需的步骤。如何在不挂载的情况下验证这些目录已被共享？
  c) 概述一种策略，使本地子网上的所有机器都能自动将导出的目录挂载到挂载点 /mnt/usr 和 /mnt/usr/local。

