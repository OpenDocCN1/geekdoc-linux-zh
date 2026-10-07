
在第 5 章中，你把此 `helloworld-powerlinux` 可执行文件传输到 Embedded Planet RPX-CL 板板。你还将对其进行远程调试。

恭喜你构建了 GNU 工具链！如果你需要为 ARM 处理器构建工具链，请运行 `buildtoolchain arm`，然后等待、编译并安装 ARM 版本的 GNU 工具链。

### 总结

Silverjack 工程师研究了嵌入式 Linux，发现了关于端口、工具、板卡、发行版和内核版本的在线信息。他们通过开发 Project Trail 战略方向总结了发现，包括内核移植、源代码和内核版本。经过研究、思考以及与供应商的讨论，他们确定了目标硬件。他们从 Tri-M、Embedded Planet 和 Brightstar Engineering 订购了板。在等待期间，他们学习了交叉编译 GNU 工具链并开发了构建脚本。工程师现在已准备好在系统到达时启动它们。

## 第 4 章 Linux 启动

![](img/c075000fa5feb4594b1442d501c7c8d8_79_0.png)

图 4.1 Project Trailazer 开发者布局。

### 目标 PBR（平台基础要求）

为了能够用于 Project Trailazer 设计，每个目标平台都需要满足以下所有要求：

- **PBR-1**——目标板将使用 2.4 或更高版本的 Linux 内核。在所有目标平台上运行相同的内核版本是最好的，但并非必须。工程师们发现 i386、ARM 和 PowerPC 的内核开发速度各异。ARM 和 PowerPC 内核补丁并不总是存在于最新版本的内核中。
- **PBR-2**——目标板将执行 bash 壳（shell）。退出 bash 壳会导致 bash 壳重新执行。

> 提示
> 定义启动要求并评估目标板构成了一套开发系统的基准。在你的所有目标机上拥有 bash 提示符意味着 Linux 正在运行。这简化了代码和脚本从一个架构迁移到另一个架构的过程。

- **PBR-3**——目标板将在无安全认证的情况下执行 bash 壳。这减少了开发时间，但留下了未来的安全漏洞。稍，工程师将添加安全机制，例如登录过程。

### Linux 启动过程

- **PBR-4**——目标板将启动、初始化以太网硬件、设置静态 IP 地址，并配置使用域名服务（DNS）。
- **PBR-5**——目标板将包含 ping 程序用于调试网络程序。
- **PBR-6**——目标板将能够执行交叉编译版本的 helloworld。
- **PBR-7**——目标板将使用当前版本的 GNU glibc。所选目标平台包含足够的 RAM 和存储资源来使用 GNU glibc。BusyBox、sglibc、uClibc、dietlibc、newlib 和 libc 等项目将不被考虑。

在准备就绪并拥有这七项目标 PBR 后，工程师开始学习 Linux 启动过程、根文件系统、编译还是下载根文件系统二进制文件、目标平台的异同、内核编译以及一些 i386 硬启动细节。我们将在本书的后续部分回到这些启动要求。

### Linux 启动过程

目标板启动 Linux 在重位后会经过几个步骤以获得系统提示符。初始步骤（如 ROM 启动代码和寄存器配置）依赖于微处理器硬件。内核本身包含依赖于微处理器的初始化代码，这些代码首先执行。这些初始化代码配置微处理器寄存器以进行保护模式运行，并调用架构无关的内核启动点 `start_kernel`。从这一点开始，内核的启动过程对于所有架构来说都是相同的。Linux 启动过程涉及以下步骤：

1. 处理器重位后，它执行 ROM 启动代码。
2. ROM 启动代码初始化 CPU、内存控制器和片上设备，并配置内存映射。随后 ROM 启动代码执行引导程序（bootloader）。
3. 引导程序从 Flash 内存或通过 TFTP 服务器传输将 Linux 内核解压到 RAM 中。内核首先配置微处理器寄存器，然后调用内核的第一条指令——`start_kernel`，这是架构无关的启动点。
4. 内核初始化缓存和各种硬件设备。
5. 内核挂载根文件系统。
6. 内核执行 init 进程。
7. 执行中的 init 进程加载 `/etc` 共享运行时库。
8. init 读取其配置文件 `/etc/inittab` 并执行脚本。通常情况下，init 执行一个启动脚本 `/etc/rc.d/rcS`，该脚本配置并启动网络和其他系统服务。
9. init 进入一个运行级别（runlevel），可以在可以在其中执行系统任务或启动登录过程以允许用户会话。

Project Trailblazer 的工程师从板卡制造商的文档了解到步骤 1、2 和 3 是易于理解、配置和执行的。步骤 4 取决于内核编译配置。步骤 5 提供了多种选择，包括挂载本地磁盘、挂载网络驱动器和使用 RAM disk。步骤 7 需要对 glibc 和其他库进行正确编译。

工程师读到了关于在步骤 6 中直接用 bash 替换 init 程序的内容。他们选择使用 init 有两个原因：首先，init 可以通过脚本处理网络和系统的初始化。在步骤 9 中，工程师将使用直接调用 bash 而不是使用登录过程。init 可以重新启动终止的进程。这意味着如果 bash 终止，init 将重新执行它。使用 init 满足 PBR-2。使用 init 指令代替登录允许在没有安全的情况下进行控制台操作。工程师打算在将目标板投入现场运行之前添加登录过程。

> 提示
> 让 init 直接调用 bash 而不是登录可以节省时间，因为你不需要在开发期间登录。在安全的实验室中，便利性优于安全性。当你部署设计时，你应该修改 `/etc/inittab` 使 init 调用 login，以提供第一层认证。

## Linux 根文件系统

Linux 根文件系统包含内核所需的文件和可执行文件，以及用于系统管理的可执行文件。在桌面安装中，内核将硬盘分区挂载在 `/` 目录下。`/` 目录下存在以下目录：

- `/bin` 和 `/sbin` 系统可执行文件，如 `init`、`ifconfig`、`mount`、`cd`、`mkdir` 和 `ping`。
- `/lib` 包含共享库（libc 等）和 Linux 动态加载器。
- `/etc` 包含配置文件和脚本。

## Linux 根文件系统

- `/dev` 包含设备文件。
- 内核在内存中动态创建 `/proc` 目录提供系统信息。
- `/usr` 包含额外的程序和库。
- `/var` 包含运行期间变化的文件，例如锁文件日志文件。

Trailazer 工程师通过检查 Debian 发行版（开发计算机，在第3章“选择平台和安装工具集”中描述）开始理解根内容。他们发现根文件系统包含 10734 个文件，占用 67.428MB。他们发现默认的 Red Hat 安装包含 29296 个文件，占用 382.020MB。显然，仅仅从 Debian 或 Red Hat 拷贝内容的简单方法超过了工程师四个目标平台的存储容量，其范围从 4MB 到 16MB。工程师们需要决定哪些文件对于启动 Linux 和执行 bash 提示符是真正需要的。

在内核初始化缓存和各种硬件设备之后，它执行第一个用户进程 init，由它产生所有其他进程。为了让 init 运行，文件系统中必须存在某些文件和库。在 `tbdev1` 上，工程师使用名为 `ldd` 的程序来发现 init 的共享库依赖项。这是 `ldd` 的输出：

# 第 4 章 启动 Linux

```
root@tbdevi[514]: ldd /sbin/init

libc.so.6 => /lib/libc.so.6 (0x40015000)

/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

第一个需要的根文件系统是 `/sbin/init`，它需要 `/lib/libc.so.6` 和 `/lib/ld-linux.so.2`。通过阅读 `init` 的帮助页，工程师们确定 `init` 使用名为 `/etc/inittab` 的配置文件，其中包含了 `init` 的指令。在桌面或服务器 Linux 工作站上，`init` 初始化网络和系统服务，然后进入运行级别（runlevel）——通常是登录进程。在目标系统中，工程师们并不关心运行级别本身；他们只想启动系统并让 bash 运行。他们没有使用 Unix/Linux 世界中那种预定义的运行级别。他们正在配置 `init` 仅初始化网络。他们正在配置 `init` 在无需身份验证的情况下执行 bash，并在 bash 终止时重新启动。

> 提示
内核核通过执行第一个用户进程 `init` 来完成启动。`start` 脚本会启动所有系统服务。你可以配置 `init` 来启动程序并在它们终止时重启它们。

工程师们检查了 tbdevi 工作站上的 `/etc/inittab` 文件。他们创建了一个简化版本，用于初始化网络并执行 bash。以下是他们的简化 `inittab` 文件：

```
id:2:initdefault:

12:2:wait:/etc/init.d/rcS

1:2435:respawn:/bin/bash

2:6:wait:/etc/init.d/umountfs
```

在这个版本的 `/etc/inittab` 文件中，`id:2:initdefault` 指定了默认进入的级别。`2:12:2:wait:/etc/init.d/rcS` 告诉 `init` 在进入级别 2 之前运行 `/etc/init.d/rcS` 脚本，然后等待完成。`1:2435:respawn:/bin/bash` 告诉 `init` 运行 `/bin/bash` 并在终止时重新启动它。`2:6:wait:/etc/init.d/umountfs` 告诉 `init` 当进入级别 6 时（有人正在重启目标板），运行 `umountfs` 脚本并等待其完成。

## bash 所需的文件

bash shell 需要库文件来执行。在 tbdevi 上，工程师们再次使用 `ldd` 来发现 bash 的共享库依赖。以下是 `ldd` 的输出：

```
root@tbdev1[516]: ldd /bin/bash

libncourses.so.5 => /lib/libncourses.so.5 (0x40016000)

libld.so.2 => /lib/libld.so.2 (0x40055000)

libc.so.6 => /lib/libc.so.6 (0x40059000)

/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

为了初始化 `init`、`inittab`、`rcs`、`umountfs`、`ld-linux.so.2` 和 `libc.so.6`，新的根文件系统需要 `bash`、`libld.so.2` 和 `libncourses.so.5`。工程师反复尝试，为了使系统功能正常，`/bin`、`/sbin` 和 `/usr/bin` 目录也是必要的：`cat`、`ls`、`mount`、`ps`、`df`、`kill`、`ping`、`touch`、`rm`、`ifconfig`、`route`、`telnet` 和 `gdbserver`。他们检查了共享库和配置文件的依赖关系，在反复尝试后，编译出了表 4.1 所示的根文件系统列表。这些文件存在于由以下目录组成的结构中：/bin /dev /etc /init.d /proc /sbin /tmp /usr /usr/bin。有了根文件系统，内核调用 `init`，由它初始化网络并执行 bash。用户可以 ping 其他网络计算机并运行 `helloworld`。这个启动后的系统将满足所有的 PBR（项目需求要求）。

> Linux 程序 `ldd` 输出一个程序或库所需的共享库列表。在将程序添加到根文件系统时，您应该使用 `ldd` 来确定是否需要额外的库。

## 表 4.1 Project Trailazer 项目目标根文件系统文件

| /bin | /dev | /etc | /lib | /sbin | /usr/bin |
|---|---|---|---|---|---|
| bash | Console | fstab | ld.so.1 | ifconfig | gdbserver |
| cat | null | inittab | ld-2.3.so | init | telnet |
| chmod | ram | protocols | libc.so.6 | route | |
| echo | tty | resolv.conf | libc-2.2.3.so | | |
| df | tty0 | services | libld.so.2 | | |
| kill | tty0 | | libld-2.2.3.so | | |
| ls | | | libm.so.6 | | |
| mount | | | libm-2.2.3.so | | |
| ping | | | libncourses.so.5 | | |
| ps | | | libncourses.so.5.2 | | |
| rm | | | libn.so.5 | | |
| sh | | | libn-2.2.3.so | | |
| touch | | | libproc.so | | |
| umount | | | libproc-2.2.3.so | | |
| | | | libutil.so | | |

## 表 4.1 Project Trailazer 项目目标根文件系统文件（续）

| /bin | /dev | /etc | /lib | /sbin | /usr/bin |
|---|---|---|---|---|---|
| | | | libutil-2.2.3.so | | |
| | | | libstdc.so | | |
| | | | libstdc-2.2.3.so | | |
| | | | libthread.so | | |
| | | | libthread-2.2.3.so | | |
| | | | libz.so | | |
| | | | libz-2.2.3.so | | |

# 列表 4.1 继续

```
# 特殊用途的适用性。更多信息请参阅 GNU 库通用公共许可证。

#

# 您应该随此程序收到一份 GNU 库通用公共许可证的副本；

# 如果没有，请信至自由软件基金会

# 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA

#

umask 022

SRCFILELOC=/root/cross

BUILDLOC=$SRCFILELOC/builds

case $1 in

  "ppc" )

    ARCH=powerpc

    TARGET=powerpc-linux

    MVRMPLOC=http://ftp.mvista.com/pub/Jouryman/cd2/ppc_8xx/apps/

    #MVRMPLOC=http://www.embeddedlinuxinterfacing.ftp.mvista.com/pub/
    Jouryman/cd2/ppc_8xx/apps/
    TEMPSLOC=$BUILDLOC/ARCH-rootmps/opt/hardhat/devkit/ppc/8xx/target/
    ;;

  "arm" )

    ARCH=arm

    TARGET=arm-linux

    MVRMPLOC=http://ftp.mvista.com/pub/Jouryman/cd1/arm_sa_le/apps/
    #MVRMPLOC=http://www.embeddedlinuxinterfacing.ftp.mvista.com/pub/
    Jouryman/cd1/arm_sa_le/apps/
    TEMPSLOC=$BUILDLOC/ARCH-rootmps/opt/hardhat/devkit/arm/sa_le/target/
    ;;

  "i386" )

    ARCH=i386

    TARGET=i386

    MVRMPLOC=http://ftp.mvista.com/pub/Jouryman/cd1/x86_586/apps/
    #MVRMPLOC=http://www.embeddedlinuxinterfacing.ftp.mvista.com/pub/
    Jouryman/cd1/x86_586/apps/
    TEMPSLOC=$BUILDLOC/ARCH-rootmps/opt/hardhat/devkit/x86/586/target/
    ;;

  *)

  echo -n "用法 " *basename $0"
  echo i386|arm|ppc [ramdisk]"
```

# 列表 4.1 继续

```
exit 1

;;

esac

#
# 步骤 1 - 确定需要下载的包
#

echo 步骤 1 - 确定需要下载的包

PACKAGES="glibc-2 bash procs fileutils textutils shellutils sysvinit
- netbase libncurses libstdc mount telnet-client net-tools
- ping gdbserver moduli"

echo 包有 $PACKAGES

echo 步骤 1 - 完成

echo

#
# 步骤 2 - 创建构建目录和新的目标根文件系统目录
#

echo 步骤 2 - 创建构建目录和新的目标根文件系统目录

if [ ! -e /tftpboot ]
then
  mkdir /tftpboot
fi

if [ ! -e $SRCFILELOC ]
then
  mkdir $SRCFILELOC
fi

if [ ! -e $BUILDLOC ]
then
  mkdir $BUILDLOC
fi
```
