
## Linux 启动过程

1. ROM 启动代码初始化 CPU、内存控制器和片上设备，并初始化内存映射。随后 ROM 启动代码执行引导程序（`bootloader`）。
2. 引导程序从 Flash 内存或 TFTP 服务器传输将 Linux 内核解压到 RAM 中。它跳转到第一条指令。内核首先配置微处理器寄存器，然后调用架构无关的启动点 `start_kernel`。
3. 内核初始化其缓存和各种硬件设备。
4. 内核挂载根文件系统。
5. 内核执行 `init` 进程。
6. 执行进程加载共享运行时库。
6. `init` 读取其配置文件 `/etc/inittab` 并执行脚本。通常情况下，`init` 执行启动脚本 `/etc/rc.d/rcS`，该脚本配置并启动网络和其他系统服务。
7. `init` 进入运行级别，可以在其中执行系统任务或启动登录过程，允许用户会话。

Project Trailblazer 的工程师们从板厂商文档了解到步骤 1、2 和 3 易于理解、配置和执行。步骤 4 取决于内核编译配置。步骤 5 提供了多种选择，包括挂载本地磁盘驱动、挂载网络驱动器和使用 RAM disk。

工程师们读到在步骤 6 中直接用 `bash` 替换 `init` 程序。他们选择使用它有两个原因：首先，`init` 可以通过脚本调用 `bash` 初始化网络和系统服务；其次，在步骤 9 中，工程师们将使用它直接调用 `bash` 而不是使用登录过程。`init` 可以重新产生终止的进程。这意味着如果 `bash` 终止，`init` 将重新执行。使用 `init` 实现了 PBR-2。让 `bash` 执行而非登录允许在没有安全的情况下进行控制台操作。工程师们打算在将目标板投入现场运行之前添加登录过程。

> **提示**
>
> 直接调用 `bash` 而不是登录可以节省时间，因为你不需要在开发期间登录。在安全的实验室中，便利性大于安全性。当你部署设计时，应该修改 `/etc/inittab`，让 `init` 调用 `login` 以提供第一层认证。

## Linux 根文件系统

Linux 根文件系统包含内核所需的文件和可执行文件，以及用于系统管理的可执行文件。在桌面工作站安装中，内核将磁盘分区挂载在 `/` 目录下。`/` 目录下存在以下目录：

- `/bin` 和 `/sbin` 包含系统可执行文件，如 `init`、`ifconfig`、`mount`、`mkdir` 和 `ping`。
- `/lib` 包含共享库（`libc` 等其他）和 Linux 动态加载器。
- `/etc` 包含系统配置文件和脚本。
- `/dev` 包含特殊设备文件。
- 内核在内存中动态创建 `/proc` 提供系统信息。
- `/usr` 包含额外的程序和库。
- `/var` 包含运行期间变化的文件，如锁和日志文件。

Trailblazer 工程师通过检查 `tbdev1`（Debian 发行版计算机，见第 3 章“选择平台和安装工具集”）开始理解根文件系统。他们发现根文件系统包含 10,734 个文件，占用 67.428MB。他们发现默认的 Red Hat 安装包含 29,296 个文件，占用 382.020MB。显然，直接从 Debian 或 Red Hat 复制内容超过了工程师目标平台的存储能力（范围从 4MB 到 16MB）。工程师们需要确定哪些文件对于启动 Linux 和执行 `bash` 提示符是真正必需的。

> **提示**
>
> 通过研究从 `start_kernel` 到 `bash` 提示符的 Linux 启动过程来开发根文件系统，可以获得最所需的文件集，并让你理解 Linux 与进程及库的交互。

# 第 4 章 启动 Linux

```
root@tbdev1[514]: ldd /sbin/init
libc.so.6 => /lib/libc.so.6 (0x40015000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

新的根文件系统需要 `/sbin/init`，它需要 `/lib/libc.so.6` 和 `/lib/ld-linux.so.2`。通过阅读 `init` 的手册页，工程师们确定 `init` 使用一个名为 `/etc/inittab` 的配置文件，该文件包含了 `init` 的指令。在桌面或服务器 Linux 上，`init` 进程初始化网络和系统服务，然后进入运行级别（`runlevel`），通常是登录进程。在目标系统中，工程师们并不关心运行级别本身；而是想要启动系统并使其运行。因此，他们使用了 Unix/Linux 世界中预定义的运行级别。他们配置 `init` 仅用于初始化网络。然后，他们配置 `init` 在不进行身份验证的情况下执行 `bash`，并在 `bash` 终止时重新启动 `bash`。

### 提示

内核通过执行第一个用户进程完成启动，`init` 的脚本会启动所有服务。你可以配置 `init` 来启动程序，并在它们终止时重启它们。

工程师们检查了 `tbdev1` 工作站上的 `/etc/inittab` 文件。然后他们创建了一个简化版本，用于初始化网络然后执行 `bash`。以下是他们简化的 `inittab` 文件：

```
id:2:initdefault:
12:2:wait:/etc/init.d/rcS
1:2435:respawn:/bin/bash
2:6:wait:/etc/init.d/umountfs
```

在这个版本的 `/etc/inittab` 文件中，`id:2:initdefault` 告诉 `init` 进入的默认级别。`12:2:wait:/etc/init.d/rcS` 告诉 `init` 在进入运行级别 2 之前运行 `/etc/init.d/rcS` 脚本，然后等待完成。`1:2435:respawn:/bin/bash` 告诉 `init` 运行 `/bin/bash` 并在 `bash` 终止时重新启动它。`2:6:wait:/etc/init.d/umountfs` 告诉当进入运行级别 6 时（有人正在重启目标板），运行 `umountfs` 脚本并等待其完成。

## bash 所需的文件

Shell 需要库来执行。在 `tbdev1` 上，工程师们再次使用 `ldd` 来发现 `bash` 的共享库依赖项。以下是 `ldd` 的输出：

```
root@tbdev1:[516]: ldd /bin/bash
libncurses.so.5 => /lib/libncurses.so (0x40016000)
libdl.so.2 => /lib/libdl.so.2 (0x40055000)
libc.so.6 => /lib/libc.so.6 (0x40059000)
/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

除了 `init`、`inittab`、`rcS`、`mountfs`、`ld-linux.so.2` 和 `libncurses.so.5` 之外，新的根文件系统还需要 `bash`，以及 `/bin`、`/sbin` 和 `/usr/bin` 目录，并且为了运行功能完整的系统还需要以下程序：`cat`、`ls`、`mount`、`ps`、`df`、`kill`、`chmod`、`touch`、`ifconfig`、`telnet` 和 `gdbserver`。他们检查了共享库和配置文件的依赖，经过尝试，他们在表 4.1 中编译了根文件系统文件列表。这些文件存在于以下目录组成的目录中：`/bin`、`/dev`、`/etc/init.d`、`/lib`、`/proc`、`/sbin`、`/tmp`、`/usr/bin`。有了这个根文件系统，内核调用 `init`，初始化网络然后执行 `bash`。用户可以 `ping` 其他网络计算机并运行 `helloworld`。这个启动后的系统将满足所有七项 PBR。

> **提示**
>
> Linux 程序 `ldd` 输出程序或库所需的共享库列表。在将程序添加到根文件系统时，理应使用 `ldd` 来确定是否需要额外的库。

## 表 4.1 Trailblazer 项目目标根文件系统文件

| bash | /dev | /etc | /lib | /sbin | /usr/bin |
| --- | --- | --- | --- | --- | --- |
| Console | fstab | ld.so.1 | ifconfig | gdbserver | |
| cat | null | inittab | ld-2.2.3.so | init | telnet |
| chmod | ram | protocols | libc.so.6 | route | |
| echo | tty | resolv.conf | libc-2.2.3.so | | |
| df | tty0 | services | libdl.so.2 | | |
| kill | ttyS0 | | libdl-2.2.3.so | | |
| ls | | libm.so.6 | | | |
| mount | | libm-2.2.3.so | | | |
| ping | | libncurses.so.5 | | | |
| ps | | libncurses.so.5.2 | | | |
| rm | | libnns-so.5 | | | |
| sh | | libnns-2.2.3.so | | | |
| touch | | libnns-files.so | | | |
| mount | | libproc.so.2 | | | |

## 表 4.1 Trailblazer 项目目标根文件系统文件（续）

| bash | /dev | /etc | /lib | /sbin | /usr/bin |
| --- | --- | --- | --- | --- | --- |
| | | | thread.so | | |
| | | | thread-0 | | |
| | | | resolv-2.2.3.so | | |
| | | | rt.so | | |
| | | | rt-2.2.3.so | | |
| | | | libstdc++-6.1 | | |
| | | | libstdc++-2.2.3 | | |
| | | | util.so | | |
| | | | util-2.2.3 | | |

## 第 4 章 启动 Linux

### 列表 4.1 继续

```bash
# 特定用途的适用性。更多详情请参阅 GNU 库通用公共许可证。
#
# 您应该已经随此程序收到了一份 GNU 库通用公共许可证
#；如果没有，请写信至自由软件会：
# 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA
#

umask 022

SRCFILELOC=/root/cross
BUILDLOC=$SRCFILELOC/builds
```

```bash
case "$1" in
"ppc")
    ARCH=powerpc
    TARGET=powerpc-linux
    MVRMLOC=http://ftp.mvista.com/pub/Journeyman/cd2/ppc_8xx/apps/
    #MVRMLOC=http://www.embeddedlinuxinterfacing.ftp.mvista.com/pub/Journeyman/cd2/ppc_8xx/apps/
    TEMPFSLOC=$BUILDLOC/$ARCH-rootfs/opt/hardhat/devkit/ppc/8xx/target/
    ;;
"arm")
    ARCH=arm
    TARGET=arm-linux
    MVRMLOC=http://ftp.mvista.com/pub/Journeyman/cd1/arm_sa_le/apps/
    #MVRMLOC=http://www.embeddedlinuxinterfacing.ftp.mvista.com/pub/Journeyman/cd1/arm_sa_le/apps/
    TEMPFSLOC=$BUILDLOC/$ARCH-rootfs/opt/hardhat/devkit/arm_sa_le/target/
    ;;
"i386")
    ARCH=i386
    TARGET=i386
    MVRMLOC=http://ftp.mvista.com/pub/Journeyman/cd1/x86_586/apps/
    #MVRMLOC=http://www.embeddedlinuxinterfacing.ftp.mvista.com/pub/Journeyman/cd1/x86_586/apps/
    TEMPFSLOC=$BUILDLOC/$ARCH-rootfs/opt/hardhat/devkit/x86/586/target/
    ;;
*)
    echo -n "Usage `basename $0`"
    echo " i386|ppc [ramdisk]"
    exit 1
    ;;
esac

# 步骤 1 - 确定下载哪些包
echo "Step 1 - Determine what packages to download"
PACKAGES="glibc-2 bash procps textutils fileutils sysvinit netbase libltdc mount telnet-client-net-tools ping gdbserver moduli"
echo "packages are $PACKAGES"
echo "Step 1 - Complete"
echo

# 步骤 2 - 创建构建目录和新的目标根文件系统目录
echo "Step 2 - Create build and new target root filesystem directories"
if [ ! -e /tftpboot ]; then
    mkdir /tftpboot
fi
if [ ! -e $SRCFILELOC ]; then
    mkdir $SRCFILELOC
fi
if [ ! -e $BUILDLOC ]; then
    mkdir $BUILDLOC
fi
ROOTFSLOC=/tftpboot/$ARCH-rootfs
echo "Creating root file system for $ARCH"
```

```bash
rm -rf $ROOTFSLOC
mkdir $ROOTFSLOC
```

```bash
if [ ! -e $BUILDLOC/$ARCH-rootrpms ]; then
    mkdir $BUILDLOC/$ARCH-rootrpms
fi
```

```bash
cd $ROOTFSLOC
mkdir dev etc/init.d bin sbin lib usr usr/bin proc tmp
chmod 755 dev etc/init.d bin sbin lib usr usr/bin proc tmp
```

```bash
echo "Step 2 - Complete"
echo

# 步骤 3 - 下载包
echo "Step 3 - Download the packages"
cd $BUILDLOC/$ARCH-rootrpms
```

```bash
lynx -dump $MVRMLOC | grep /tmp/rpmlist
for i in $PACKAGES; do
    a=$(grep "$i" /tmp/rpmlist)
    rpmurl=$(echo "$a" | cut -d '"' -f 2)
    rpm=$(basename "$rpmurl")
    if [ ! -f "$BUILDLOC/$ARCH-rootrpms/$rpm" ]; then
        echo "Getting $rpm"
        wget "$rpmurl"
    else
        echo "$rpm"
    fi
done
```

```bash
echo "Step 3 - Complete"
echo

# 步骤 4 - 将包的内容提取到临时目录
echo "Step 4 - Extract the package's contents into a temporary directory"
cd $BUILDLOC/$ARCH-rootrpms

# this is the old way, too slow because it converts RPMs
# alien -t rpm
# find -name "*tgz" -exec xzvf {} \;
IFS='
'
for rpm in $(ls *rpm); do
    if [ ! -f "$rpm.extracted" ]; then
        alien -t "$rpm"
        tgz=$(ls *tgz)
        tar xzvf "$tgz"
        rm -rf "$tgz"
        touch "$rpm.extracted"
    fi
done

echo "Step 4 - Complete"
echo

# 步骤 5 - 复制所需的程序
echo "Step 5 - Copy the required programs"
echo
```

### 列表 4.1 继续
