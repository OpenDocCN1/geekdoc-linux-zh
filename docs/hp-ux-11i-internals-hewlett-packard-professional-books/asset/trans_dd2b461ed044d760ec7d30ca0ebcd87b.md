
| 212 | 0 | 512 | 0 | char [512] | fs_fmmnt |
| 724 | 0 | 4 | 0 | int | fs_cgitoror |
| 728 | 0 | 4 | 0 | * | fs_csp |
| 732 | 0 | 4 | 0 | int | fs_csp_pad |
| 736 | 0 | 4 | 0 | int | fs_unused2 [30] |
| 856 | 0 | 4 | 0 | int | fs_qpc |
| 860 | 0 | 2 | 0 | short | fs_postbl [32] [8] |
| 1372 | 0 | 4 | 0 | int | fs_magic |
| 1376 | 0 | 6 | 0 | char [6] | fs_fname |
| 1382 | 0 | 6 | 0 | char [6] | fs_pack |
| 1388 | 0 | 1 | 0 | u_char | fs_rotbl [0] |

该文件系统的“魔数”（用于验证其类型）、其类型名称和包名

## vnode

接下来，我们将深入研究 vnode 结构的具体细节。我们已知 inode 包含文件的所有凭证和属性，因此它是文件系统中管理文件的关键。inode 号在单个文件系统的上下文环境中是唯一的，定义文件所需的全部信息即为 inode 号。在内核中，可能会挂载多个文件系统以组成一个看似无缝、更大的文件系统。在这个更大的上下文中，inode 号不再保证唯一。每个挂载的文件系统都可能有 inode 1、2 等。为了使内核能够通过唯一的句柄来引用已打开的文件，虚拟 inode（或称 vnode）应运而生。

类似于 vfs 结构，vnode 包含一个操作数组指针，指向内核中用于文件操作任务的特定类型例程（见图 8-14）。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_265_0.png)

图 8-14 vnode

vnode 的关键字段包括一个类型号、一个指向特定类型操作数组的指针，以及对文件 *inode* 数据内核副本的引用。列表 8.7 是一个带有注释的虚拟文件系统 vnode 列表：

### 列表 8.7 q4> fields struct vnode

```
0 0 2 0 u_short v_flag
0x01 VROOT 文件系统根目录
0x02 VTEXT vnode 是文本原型
0x04 VSWAP vnode 映射交换空间
0x08 VXOFFHOLD vnode 允许软保留
0x010 VEXLOCK 独占锁
0x020 VSHLOCK 共享锁
0x040 VLWAIT 锁上有等待者
0x080 VXDEVOK 允许跨设备重命名和链接
0x0100 VMMF vnode 是内存映射
0x04000 VNOBCACHE 数据缓存已禁用
0x08000 VN_MPSAFE 不需要信号量
```

```
共享锁计数、独占锁计数、私有数据计数和引用计数
2 0 2 0 u_short v_shlockc
4 0 2 0 u_short v_exlockc
6 0 2 0 u_short v_tcount
8 0 4 0 int v_count
如果此节点是挂载点，则指向 vfs 结构的指针
12 0 4 0 * v_vfsmountedhere
指向特定类型的 vnode 操作数组、unix ipc socket、流头以及文件所在的 vfs 的指针
16 0 4 0 * v_op
20 0 4 0 * v_socket
24 0 4 0 * v_stream
28 0 4 0 * v_vfsp
vnode 类型、设备号、特定类型的数据（vfs inode, vxfs inode, rmdb, ...）以及父文件系统类型
32 0 4 0 enum4 v_vtype
36 0 4 0 int v_rdev
40 0 4 0 * v_data
44 0 4 0 enum4 v_fstype
指向父伪 vas 的指针（如果此节点映射到可执行映像文件）
48 0 4 0 * v_vas
Beta 信号量锁结构
52 0 1 0 u_char v_lock.b_lock
54 0 2 0 u_short v_lock.order
56 0 4 0 * v_lock.owner
```

```
此文件的映射内存缓存缓冲区
60 0 4 0 * v_cleanblkhed
64 0 4 0 * v_dirtyblkhed
vnode 写入计数、FS 独立锁、软保留计数以及 va_nodeid 的副本
68 0 4 0 int v_writecount
72 0 4 0 * v_locklist
76 0 4 0 int v_scount
80 0 4 0 int v_nodeid
如果此 vnode 当前在目录名查找缓存中有描述，则是 DNLC 条目指针
84 0 4 0 * v_n cachelhed
88 0 4 0 * v_n cachehed
92 0 4 0 * v_pfdata
96 0 4 0 u_int v_last_fsync
```

## HFS 内存中的 inode 包含其 vnode

对于 HFS 文件，内存中的 inode 结构包含 vnode 结构及其驻留磁盘的 inode 的完整副本（即我们之前检查的 i_common 结构）以及其他附加信息字段（列表 8.8）：

```
Listing 8.8 q4> fields struct inode
0 0 4 0 * i_chain[0]
4 0 4 0 * i_chain[1]
此 inode 来源的设备号
8 0 4 0 int i_dev
inode 号
12 0 4 0 u_int i_number
状态标志、锁字以及最后一个锁定此 inode 的线程的 tid
16 0 4 0 u_int i_flag
20 0 2 0 u_short i_lockword
24 0 4 0 int i_tid
虚拟文件系统的该文件 vnode 存储在偏移 28 到 127 之间
inode 设备指针
128 0 4 0 * i_devvp
132 0 4 0 int i_diroff
继续 inode 指针
136 0 4 0 * i_contip
文件系统指针
140 0 4 0 * i_fs
配额指针
144 0 4 0 * i_dquot
148 0 4 0 int i_rdev
152 0 4 0 int i_un_if_lastc
```

```
152 0 4 0 * i_un.i_s_socket
156 0 4 0 * i_fr.if_fmode
160 0 4 0 * i_fr.if_fmod
164 0 4 0 * i_fsel.i_selp
168 0 2 0 short i_fsel.i_sflag
172 0 4 0 * i_fsel.i_selp
176 0 2 0 short i_fsel.i_sflag
180 0 4 0 * i_mout
```

基于磁盘的 inode（结构 icommon）的副本存储在偏移 184 到 311 之间

读者调用次数

```
312 0 2 0 u_short i_r_count
```

Beta 信号量锁结构

```
316 0 1 0 u_char i_b_sema_b_lock
318 0 2 0 u_short i_b_sema_order
320 0 4 0 * i_b_sema_owner
324 0 4 0 int filler[0]
328 0 4 0 int filler[1]
```

内存中 inode 数据与 vnode 之间的关系因文件系统类型而异，但 vnode 结构本身对所有支持的文件系统都是相同的。由于 vnode 使用操作数组指针，被引用例程的程序员必须对 inode 特定类型的内容有深入的了解。

当内核打开一个文件时，该文件由文件系统所在卷的设备号和其 inode 号来标识。通过使用这两个值，可以保证每个文件在操作系统范围内具有唯一的身份。

## 在内核中缓存 inode/vnode 数据

为了提高系统性能并减少访问磁盘元数据的时间，inode/vnode 数据维护在内核驻留的缓存中。每种类型的文件系统负责其 inode/vnode 缓存的分配和维护。在大多数实现中，缓存大小由内核可调参数或嵌入式公式确定。使用设备号和 inode 号形成哈希值。在从物理磁盘读取 inode 副本之前，始终检查 inode 缓存，看是否存在数据的副本。

## 障眼法：将文件系统抽象整合在一起

接下来，我们需要将这些抽象整合到一个无缝的 VFS 实现中（见图 8-15）。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_269_0.png)

**图 8-15 构建无缝文件系统**

让我们回顾一下之前的场景，只不过现在 /home 是挂载到系统根文件系统的一个独立文件系统。再次，我们的挑战是通过内核的虚拟结构跟踪路径名 /home/chris/stuff。

我们通过定位内核中 / inode（第一个卷上的 2）的副本来开始搜索。只要文件系统已挂载，所有挂载点和文件系统根目录的 inode/vnode 和根目录数据就会保留在缓存和缓冲区缓存中。为了加快此初始搜索速度，内核在符号 rootdir 中维护一个指向 / inode/vnode 缓存副本的永久快捷指针。

从此 vnode，我们确定文件系统设备号，并从相关的 inode 获取数据块指针。使用这两个数值，我们通过哈希方式进入缓冲区缓存，在那里找到根文件系统的根目录数据副本。我们将与 /home 目录相关的 inode 号和设备号用于通过哈希方式回到 inode 缓存，进行搜索的下一步。

当我们找到 /home 目录（第一个卷上的 5）的缓存 vnode 时，v_vfsmountedhere 指针有效，并将我们引导至内核挂载表和第二个已挂载卷（我们小时候玩的“滑滑梯”游戏了吗？）的 vfs 结构。然后我们跟随 v_data 指针找到已挂载 /home 文件系统的根 inode/vnode（第二个卷上的 2）和缓存数据块。

我们在 /home 文件系统内继续搜索，定位 /home/chris 目录的 inode/vnode（第二个卷上的 10）和缓存数据，最后定位 /home/chris/stuff 文件的 inode/vnode（第二个卷上的 14）和缓存数据。

