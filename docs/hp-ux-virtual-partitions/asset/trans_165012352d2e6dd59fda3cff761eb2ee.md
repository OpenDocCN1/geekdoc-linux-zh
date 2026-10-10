
## 数据库

包含所有*vPar*相关信息的*虚拟分区*数据库是/stand/vp.db。该数据库已为您管理并同步（如第8章所述），因此如果您不想过多关注，完全可以忽略它。不过，如果您愿意，可以创建一个替代数据库。您可能会希望这样做，以便为您的系统创建完全不同的*虚拟分区*配置，而不影响当前正在运行的数据库。

![](img/eff8b9287a5f38c5adf538f24aacf29e_121_0.png)

在使用**vpcreate**创建*虚拟分区*时，您可以使用*-D*选项并指定一个位于/stand目录下的替代数据库文件名，例如/stand/vpdb.app2。当您从此数据库启动vParS时（通过**ISL>** hpux /stand/vpmon -D db_file），该数据库将成为默认数据库，因此所有对此数据库中定义的*vParS*所做的修改都将应用于该数据库，而不是默认数据库。

## 第二个vPar *cable2*

我们将在下文中为*cable2*列出与*cable1*相同类别的组件：

- 名称：*cable2*
- 处理器：最少1个（绑定），最多3个（其中2个未绑定）
- 内存：绑定和未绑定总数等于1的1024 MB
- 局域网：0/10/0/0
- 引导磁盘：0/8/0/0/0.8.0.5.0.0.0 /stand/vmunix（这是默认值）
- 自动引导：关闭（手动）
- 控制台：将创建虚拟控制台

现在，我们拥有了两个*vParS*的组件列表。其结果是我们的L-Class系统被划分为两个如图2-4所示的*vParS*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_122_0.png)

图 2-4 包含两个vPar的L-Class（未显示的组件未展示）

图2-4反映的是我们在执行即将进行的步骤来创建两个vPar时，系统的最终形态。请注意，两个*未绑定*处理器（在图2-4中显示为2,3）可以根据需要分配给*cable1*和*cable2*。

## 5) 虚拟分区内核相关工作

每个虚拟分区都有自己的HP-UX 11i实例，并且拥有自己的HP-UX内核。您很可能会以多种方式定制这些内核，以适应在相应vPar中运行的应用程序。当您安装vPars软件时，它会自动重新配置内核以包含vPar驱动程序并使内核可重定位。由于在加载vPars软件时已为您执行了这些内核相关步骤，因此您无需手动执行本节中的内核相关步骤。不过，查看本节中手动执行的步骤仍然具有信息价值，有助于更好地理解vPars的工作方式。在这一步中，我们将调查由vPars应用程序更新的构建新内核所需文件。请记住，每个安装了HP-UX 11i并运行vPar的卷上都需要构建新内核。

由于内存由多个vPar共享，内核必须在内存中可重定位。在撰写本文时，存在允许将内核构建为可重定位内核的补丁。我们不会执行与补丁相关的任何检查。

文件/sbin/vrecheck是系统中必需的vPar文件。以下是/usr/conf/gen/config.sys中用于检查/sbin/vrecheck是否已在系统上加载的部分内容：

```
# 确定链接器是否支持内核重定位。
# 使用重定位选项链接内核。
LOADOPTS_ADDL=`
        if [ -f /sbin/vrecheck ]; then  \
            $(WRK)/$(IZ) \
            $(AWK) '$0 == "92453-7 linker" { \
                if ( vers[1] == 9 && \
                    ( vers[2] == 11 || vers[3] >= 25 ) || vers[2] > 11 ) \
                        print "${LOADOPTS_RELOC}"; \
                    else print "${LOADOPTS_STATIC}"; }
            fi;`
```

以下是随vPar软件加载的/sbin/vrecheck的较长列表：

```
# ll /sbin/vrecheck
-r-Xr-Xr-X 1 bin     bin  20533 Mar  5 19:01 /sbin/vrecheck
#
```

接下来让我们查看/stand/system，看看已添加到文件中的vpar驱动程序：

```
# cat /stand/system
****************************************************************
* 源文件: /ux/core/kern/filesets.info/CORE-KRN/generic
* @(#)B.11.11_LR
*
****************************************************************
* 在每种机器类型中创建完整
* 系统文件时所需的其他驱动程序。此列表包括所有
* master.d/ 文件未强制安装到系统或 ioscann 无法识别的驱动程序。
* 可能还存在针对特殊情况的CPU类型特定文件。
* 参见 create_sysfile (1m)。
****************************************************************
*
* 驱动程序/子系统
gba
lba
c720
sctl
tdisk
as100
cdfs
cxperf
clar_psm
clar_psm_if
dev_Clar
diag0
diag1
diag2
Dmem
dev_Config
iomem
nfs_core
nfs_client
nfs_server
htlan
maclan
dlpi
token_arq
inet
uipc
tun
telm
tels
netdiag1
nms
```

```
hpstreams
c1one
strlog
sad
echo
sc
timod

tirdwr
pipede
pipemod
ffs
ldterm
ptem
pts
ptm
pckt
td
tddi4

gelan

gsCtoPCI
iop_drv
bs_Gem
vxfs
vxporta1
lvm
lv
n
tm
xpcmod
auto
fsc
cache
fsc
cifs
prn
vpar

tRMMS
G

str
ptp

在此处添加vpar驱动程序

st

lvol
dump
l
v
o1

maxsw
apchunks

#STRMMS
G
SZ# st
r
pt
p
lvo1dump
maxswap
chunks

#STRMMS
G
SZ# st
r
pt
p
lvo1dump
maxsw
apchunks

655
35

60

2048

#str
p
G

n		
d	ump

l
vol

maxswapchunks


#STRMMS
G
SZ# st
r
pt
p
lvo1dump
maxswapchunks
```

vpar驱动程序是一个主驱动程序，描述在`/usr/conf/master.d`中，如下所示：

```
$ pwd
/usr/conf/master.d
$ cat vpar
$CDIO

vpar

0

$$

$DRIVER
INSTALL
vcl

-1

209
vcs

-1
```

vpar_driver -1 -1
$$$

$DRIVER_DEPENDENCY
vcc vpar
vcs vpar
vpar vcs vcn vpar_driver
vpar_driver vpar
$$$

```
$DRIVER_LIBRARY

* 驱动程序/库表。此表定义了给定驱动程序
* 依赖于哪些库。如果驱动程序包含在dfile中，则
* 该驱动程序所依赖的库将包含在ld(1)命令
* 行中。只有可选库*需要*在此表中指定，
* （但必需库也可以包含在内）。

* 驱动程序句柄 <库>

* 子系统优先。

vcc libvpar-pdk.a
vcs libvpar-pdk.a
vpar libvpar-pdk.a
vpar_driver libvpar-pdk.a ,
$$$
```

```
$LIBRARY

* 库表。库表中的每个元素描述
* 一个唯一的库。标志成员是一个布尔值，如果库应*始终*
* 包含在ld(1)命令行中，则初始化为1；
* 如果是可选库（即只有在
* 一个或多个驱动程序需要时才包含），则初始化为0。
* 库表的顺序决定了ld(1)命令
* 行中库的顺序（即定义了隐式加载顺序）。
* 新库必须添加到该表中。
* 注意：libhp-ux.a必须是最后一个条目，请勿在其后
* 放置任何内容。
* 库 <必需>
libvpar-pdk.a 0
$$$
#
```

您可以在此文件中看到存在多个驱动程序。vcn和vcs驱动程序用于支持vPars环境中的控制台。由于您通常只为多个分区配备一个物理控制台，因此需要一种共享物理设备的方式。第4章介绍了这些驱动程序的使用方法，其中涵盖了内核配置。目前，只需知道这些驱动程序作为vPars安装的一部分存在，并且必须构建到内核中即可。

既然内核已具备构建可重定位内核所需的条件，且vPars所需的驱动程序也已就位，我们就可以运行**mk_kernel**来构建新内核，并运行**kmpudate**将新的内核相关文件放入指定位置。此过程会自动为您完成，但以下命令展示了如何手动执行此过程：

```
# mk_kernel
正在生成模块: krm....
正在编译 /stand/build/conf.c...
正在加载内核...
正在生成内核符号表....
# kmpudate

已安排内核更新请求。

默认内核 /stand/vmunix 将在下一次系统关机或启动时
由新构建的内核 /stand/build/vmunix_test 更新。
#
```

请记住，此过程需要对所有将运行虚拟分区的HP-UX 11i操作系统执行。如第11章所述，内核的创建和修改也可以在SAM中进行。

## 6) 创建第一个虚拟分区

![](img/eff8b9287a5f38c5adf538f24aacf29e_127_0.png)

**vparscreate**命令用于创建vPar。该命令的摘要如表2-1所示，其手册页位于附录A。该命令的一般形式如下：

```
vparscreate -p vp_name [-B boot_attr] [-D db_file] [-S static_attr]
[-b kernel_path][-o boot_opts] [-a xsrc] [-a...]
```
