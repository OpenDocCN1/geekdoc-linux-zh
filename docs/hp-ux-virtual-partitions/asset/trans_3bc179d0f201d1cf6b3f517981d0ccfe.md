
设备 on which is l resides. 通常，该设备由 pdc 在稳定存储中维护的主启动路径（Primary Boot Path）标识。路径规范是一种 I/O 子系统助记符，根据硬件型号不同而有所变化。

当处理器在初始化和自检完成后复位，pdc 从稳定存储中读取控制台路径（Console Path），并尝试初始化控制台设备。如果初始化失败，pdc 将尝试查找并初始化一个控制台设备。查找控制台设备所使用的算法根据硬件型号不同而有所变化。

-   如果启用了自动启动（autoboot）和自动搜索（autosearch）（参见 `is l (1M)`），pdc 会等待大约 10 秒，在此期间操作员可以通过按下并按住控制台上的 ESC（转义）键来覆盖自动启动序列。

然后，系统开始搜索潜在的启动设备。如果允许搜索完成，系统将显示一个潜在启动设备的列表，并标记为缩写路径标识符（P0、P1 等）。随后显示一个简单菜单，用户在其中可以：

-   使用缩写路径标识符或完整的 Anomic 启动特定设备。
-   启动设备搜索，搜索内容包括 IPL 镜像（请注意，第一次搜索仅识别设备，未检查其内容）。
-   进入启动管理级别。
-   退出菜单并返回自动启动。
-   获取有关选项的帮助。

通过按下并按住转义键可以中止对潜在启动设备的搜索。通过按下并按住转义键也可以中止对设备内容的搜索。

如果操作员没有中断搜索过程，pdc 将从主启动路径（Primary Boot Path）初始化并读取 `is l`。

如果自动启动序列不成功、被操作员覆盖或首先未启用，pdc 将执行设备搜索并进入上述菜单。

主启动（Primary Boot）、备用启动（Alternate Boot）和控制台路径，以及自动启动和自动搜索的启用状态，可以通过 `is l` 或在 pdc 启动管理级别进行修改。

**另请参阅**
`boot(1M)`, `hpxu boot(1M)`, `is l(1M)`。

## 第 4 章

## 构建 HP-UX 内核

### 虚拟分区与内核

如第 3 章所述，使用 vPars 启动与不使用 vPars 启动不同，因为使用 vPars 的启动是通过虚拟分区监视器（**vpmo**）管理的。你仍然像平常不使用 vPars 那样启动一个 HP-UX 内核，但：**vpmo** 管理虚拟分区，允许你在同一台计算机上运行多个 HP-UX 实例。

每个虚拟分区都运行自己的 HP-UX 11i 操作系统，包括一个独特的内核。你可以定制每个虚拟分区中的操作系统和内核，以满足你的需求。

在本书前面的示例中，**vparcreate** 命令指定了内核 */stand/vmunix*，这是默认内核。你可能会以某种方式修改这个内核，以便优化用于你在每个虚拟分区中运行的应用程序。根据每个 vPar 的应用程序和特定需求，你最终可能会为每个虚拟分区拥有截然不同的内核。

在涵盖启动 vPars 的第 3 章中，我们介绍了一个指定内核路径的示例。你在 HP-UX 中的默认内核是 */stand/vmunix*。你可以对你的系统上 vPars 的内核进行实验，并可能需要在 */stand/vmunix* 之外启动这些实验内核。

![](img/eff8b9287a5f38c5adf538f24aacf29e_224_0.png)

以下示例展示了使用 **vparload** 的 *-b* 选项从一个名为 **vunix_test1** 的内核进行启动：

```
MON> vparload -p symboll -b /stand/vunix_test1
```

上述内核路径通过此 **vparload** 加载，但未进行永久更改。要对 vPars 数据库文件进行永久更改以更新内核路径，你需要发出以下命令：

```
# vparmodify -p symboll -b "stand/vunix_test1"
```

此时，vPar 已修改为具有 */stand/vunix_test1* 的默认内核。

我们首先介绍第 2 章中用于执行虚拟分区内核相关工作的流程。接下来，我们将概述设备驱动程序以及在一个虚拟分区中使用磁带设备及其设备驱动程序的示例。本章后面，在提供 HP-UX 内核背景知识时，将详细介绍修改内核参数和 HP-UX Ili 内核参数的详细描述。

## 虚拟分区内核相关工作

每个虚拟分区都有自己 HP-UX Ili 的实例，拥有自己的 HP-UX 内核。你很可能会以各种方式定制这些内核，以适应你在各自 vPars 中运行的应用程序。安装 vPars 软件时会自动为你构建内核。内核中包含了多个驱动程序，并且内核配置为可在内存中重新定位。重新定位是必需的，因为内存中会有多个 HP-UX 内核，它们必须驻留在不同的位置。在本节中，为了使 vPars 运行，你需要重新配置内核以包含 vPar 驱动程序并使内核可重定位。新内核的创建将在每个带有 HP-UX Ili 且将运行 vPar 的卷上自动完成。让我们来看看一些在幕后为你进行内核相关工作的情况。

由于内存由多个 vPar 共享，内核必须在内存中可重定位。在撰写本文时，存在允许内核作为可重定位内核构建的补丁。我们不执行与补丁相关的任何检查。

文件 `/sbin/vecheck` 是系统中需要的 vPar 文件。以下是 `/usr/conf/gen/config.sys` 的一部分列表，用于检查 `/sbin/vecheck` 是否已加载到系统中：

```
#
& if $vparvecheck
"vecheck supports kernel relocation. If it does,"
"enable the relocation options"
then
vrel= : "00 - /92453-07 linker (\\ 
spilt($57, vvers, ":") \
if { vver[1] == "B" && \
     vver[2] == 11 && vver[3] >= 25 } 
    print "${LOADOPTS_6ELOC}"
else print "${LOADOPTS_STATIC}"
fi 
fi
```

以下是随 vPar 软件加载的 `/sbin/vecheck` 的长列表：

```
# ll /sbin/vecheck
# -r-xr-xr-x  1 bin    bin    20533 Mar  5 19:01 /sbin/vecheck
```

接下来，让我们查看 `/stand/system`，看看已添加到文件中的 *vpar* 驱动程序：

```
# cat /stand/system
***************************************
* Source: /usr/core/kern/filesets.info/CORE-KRN/generic
* @(#)B.11.11_LR
* vpar
***************************************
* Additional drivers required in every machine-type to
* create a complete
* system file during cold install. This list is every driver that the
* master.d/ files do not force on the system or is not identifiable by
* ioscan.
* Other CPU-type specific files can exist for their special cases.
* see create_sysfile (lm).
```

- 驱动程序/子系统
- sba
- lba
- c720
- sctl
- sdisk
- aslo0
- cdfs
- cxperf
- dlar_psm
- dlar_psm_if
- dev_olar
- diag0
- diag1
- diag2
- dmem
- dev_config
- iomem
- nfs_core
- nfs_client
- nfs_server
- btilan
- maclan
- dlpi
- token_arq
- inet
- uipc
- tun
- telm
- tels
- netdiag1
- rms
- hpstreams
- cione
- strlog
- sad
- echo
- sc
- timod
- tirdwr
- pipedev
- pipemod
- ffs
- ldterm
- ptem
- pus
- ptm
- pckt
- ld
- fddi4
- elian
- GSCtOPCI
- i6p_drv
- bs_cam
- vxis
- vxportal

```
lvm
lv
nfsm
rpcmod
autofsc
cache5fsc
cifs
prm
vpar     <--- vpar 驱动程序在此处添加
STRMGSQ5Z 65535
nstrpty  60
dump lvol  60
maxswappchunks 2048
#
```

`vpar` 驱动程序是一个主驱动程序，在 `/usr/conf/master.d` 中描述如下所示：

```
# pwd
/usr/conf/master.d
# cat vpar
$CDIO

        vpar                  0


$$$   


$DRIVER_INSTALL

        vcs       -1                 209
        vc$       -1                  -1
        vpar_driver -1                -1


$$



$DRIVER_DEPENDENCY

        vpar
        vcs
        vpar      vpar

        vpar      vcs vcn vpar_driver
        vpar_driver       vpar


$$$

$DRIVER_LIBRARY

* The driver/library table.  This table defines which libraries a given driver depends on.  If the driver is included in the dfile, then the libraries that driver depends on will be included on the ldl(1) command line.  Only optional libraries `need' to be specified in this table. (but required ones can be included, as well). * Driver handle          <libraries> *
* subsystems first
vcs               libvpar-pdk_a
vc$               libvpar-pdk_a
vpar              libvpar-pdk_a
vpar_driver       libvpar-pdk.a
```
