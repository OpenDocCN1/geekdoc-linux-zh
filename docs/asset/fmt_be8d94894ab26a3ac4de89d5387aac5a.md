
由于 C 语言库是工具链的主要组件之一，且 `uClibc` 是嵌入式 Linux 系统的替代 C 语言库，使用它需要构建一个定制的交叉工具链。与 `glibc` 交叉工具链一样，构建基于 `uClibc` 的交叉工具链的最佳方法是使用自动化构建框架来处理繁重的工作。`uClibc` 发行版包含一个名为 `Buildroot` 的自有框架。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_137_0.png)

从 `http://buildroot.uclibc.org` 网站下载 `Buildroot` 并解压压缩的 `tar` 归档文件：

```
$ cd $SPRROOT/build-tools/
$ wget http://buildroot.uclibc.org/downloads/snapshots/buildroot-snapshot.tar.bz2
$ tar jxvf buildroot-snapshot.tar.gz
$ cd buildroot/
```

运行配置菜单工具：

```
$ make menuconfig
```

你将看到 `Buildroot` 配置菜单，如图 4-3 所示。与 `Ptxdist` 菜单一样，你可以使用 `?` 键获取有关每个选项的信息。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_138_0.png)

图 4-3. `uClibc` `Buildroot` 主菜单

确实，`Ptxdist` 和 `Buildroot` 共享相同的配置系统，`uClibc`、Linux 内核以及许多其他项目也使用该系统。

`Buildroot` 主菜单包括以下选项：

*   **目标架构**
    允许你选择交叉工具链创建二进制文件的目标架构。

*   **目标架构变体（可选）**
    配置要构建的子架构或代次，例如对于 `x86` 家族，如果是适用的话，可以是 `386`、`486` 或 `686`。

*   **目标 ABI（仅限 MIPS）**
    目标 `ABI` 选项仅提供给 `MIPS` 架构，控制使用三个可用的应用程序二进制接口（`ABI`）中的哪一个。大多数嵌入式系统构建者可能会选择新的面向嵌入式的 `ABI`，称为 `EABI`。

*   **目标选项**
    此子菜单控制几个仅对使用 `Buildroot` 构建整个根文件系统的人感兴趣的设置。它们不影响交叉工具链编译。

*   **构建选项**
    此子菜单允许你设置关于交叉工具链构建过程的几个不同选项：

    ![](img/617fee0f2d5cdaf31b3f8601bc6c454f_139_0.png)

    *   用于执行此类任务（如从 `FTP` 和网站检索文件、从 `Subversion` 和 `Git` 源代码控制库签出源代码、解压 `Gzip` 和 `Bzip2` 归档）以及传递给 `tar` 命令的任何特殊命令行选项的命令。提供的默认值非常合理，在大多数现代 Linux 系统上可以开箱即用。

    *   诸如 Linux 内核、GNU 软件（如 `GCC`、`binutils` 和 `GDB` 包）以及 `Debian` 项目镜像（用于获取额外包）等组件的镜像和下载位置。保留默认值是安全的，但如果你碰巧知道附近镜像的 `URL`，在此配置它可能会节省大量时间。

    *   交叉工具链和头文件将安装到的目录。将此更改为我们配置为 `$SPRROOT/tools/` 的目录。

    *   支持无硬件浮点目标的命令的可执行文件名上的 `nofpu` 后缀。

    *   构建目录名称的自定义前缀和后缀，以便在单个位置构建多个架构。不推荐使用这些选项。

    *   可选的自定义 `GNU` 目标后缀。你可以使用它来“品牌化”你的交叉工具链。

    *   `strip` 工具的版本。建议使用传统的 `strip` 命令，而不是较新的 `sstrip`。

    *   配置工具链使用静态库而非动态可加载库的选项。不推荐给新手用户。

    *   几个与使用 `Buildroot` 构建根文件系统相关的其他选项，这些选项与工具链无关。

*   **工具链**
    此子菜单（如图 4-4 所示）控制基于 `Buildroot` 的工具链构建器的几个关键配置选项：

    *   选择是否希望使用外部工具链还是构建一个新的工具链。使用默认的“`Buildroot toolchain`”，因为应该让 `Buildroot` 生成工具链，而不是依赖外部提供的工具链。

    *   选择内核头文件版本。选择与你的目标内核版本最接近的版本。

    *   选择 `uClibc` 库版本。建议选择最新发布的版本（而不是每日快照）。

    *   配置 `uClibc` 库配置文件的位置。暂时保留默认设置；我们稍后会说明如何自定义 `uClibc` 配置。

    *   支持国际化 (`i18n`)。通常对嵌入式系统无用。

    *   选择线程库实现。推荐 `NPTL`。

    *   控制是否构建带有调试符号的线程库。大多数人希望在此处选择 `"Yes"`。

    *   设置支持 `GNU` `"程序调用名称"` 扩展的选项，该扩展被某些第三方程序（如 `GNU tar`）使用，但通常并非必需。在此处选择 `"Yes"`。

    *   选择 `binutils` 包的版本。选择提供的最新版本。

    *   设置构建 `binutils` 包时传递的额外选项。通常此选项留空。

    *   选择 `GCC` 编译器版本。较旧版本通常产生更小的代码，但支持的特性较少且存在已知问题。

    *   使交叉工具链使用独立的自定义 `sysroot`，与系统的分开。启用此选项对于将交叉工具链与工作站上可能安装的本机工具链和库干净地分离至关重要。

    *   使用 `setjmp/longjmp` 实现异常处理，而不是更正统的栈展开，以克服栈展开代码的问题。除非异常无法正常工作，否则选择 `"No"`。

    *   设置构建 `GCC` 期间传递的额外选项。将此选项留空。

    *   配置是否除 C 支持外，还构建 C++、`FORTRAN` 和 `Objective-C` 编译器和运行时支持。

    *   构建并安装 `libgcc`（`GCC` 运行时代码库）的共享库版本。大多数人将在此处选择 `"Yes"`。

    *   构建支持 `ccache` 编译器缓存工具的工具链。

    *   设置作为工具链一部分构建和安装 `GDB`（`GNU` 调试器）的选项。有关 `GDB` 的更多讨论，请参见第 11 章中的 `"构建和安装 gdb 组件"`。

    *   支持 `FLT` 格式，该格式用于 `uClinux` 系统（针对无 `MMU` 支持系统的 Linux）。

    *   选择是否构建和安装 `sstrip`（一种用于编辑 `ELF` 二进制段条的增强版 `strip` 工具）。由于这是一个有用的工具，建议设置此选项。

    *   选择是否构建和支持支持多个目标 `ABI` 的库。通常不需要也不推荐。

    *   支持大于 2 GB 的文件。启用此选项将需要更多的运行时资源。

    *   在 `uClibc` 库中启用对 `IPv6` 和 `RPC` 网络协议的支持。

    *   支持宽字符，或 `WCHAR`，某些第三方软件包需要此功能。

    *   选择是否在工具链中包含软件浮点仿真。对于没有 `FPU` 的目标很有用，并且出于性能原因，在这些系统上优于使用基于 Linux 内核的仿真。

    *   选择是否在工具链目录中安装一些有用的目标二进制文件（如调试器代理）。

    *   配置与使用 `Buildroot` 生成根文件系统相关的其他选项。

## 为 target 选择包

顾名思义，此子菜单允许用户要求 `Buildroot` 使用交叉工具链获取、构建和打包用于目标文件系统的额外软件包。虽然这是一个非常实用的选项，但目前对我们没有兴趣。取消此菜单中所有选项的标记。下一章将讨论构建目标文件系统。

## 目标文件系统选项

此子菜单允许用户配置 `Buildroot` 将如何打包其构建的根文件系统。如前一条目所述，此时应取消此子菜单中所有选项的标记。

## 内核

此子菜单允许用户配置要由 `Buildroot` 使用交叉工具链自动获取和构建的 Linux 内核版本和配置文件。像以前一样，此时请取消所有选项的标记。

完成后，选择 `< Exit >` 按钮并按 `Enter`，然后选择 `< Yes >` 按钮以保存配置。

接下来，运行 `make` 让 `Buildroot` 获取、打补丁、配置、构建和安装新的基于 `uClibc` 的交叉工具链：

```
$ make
```

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_141_0.png)

此阶段可能需要相当长的时间，并且需要有效的互联网连接。

构建完成后，生成的工具链将安装在 `$PRJ/ROOT/tools/bin` 目录中。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_142_0.png)

## 自定义 uClibc 配置

前一节使用 `Buildroot` 构建了基于 `uClibc` 的工具链，针对目标架构使用了默认的 `uClibc` 选项。这些默认选项非常合理，建议至少在第一次构建基于 `uClibc` 的系统时保持这些设置。

话虽如此，我们认识到有时希望微调并优化 `uClibc` 配置本身的某些选项。这可以通过 `Buildroot` 完成，在使用前一小节概述的过程进行配置后，发出以下命令：

```
$ make uclibc-menuconfig
```

将显示 `uClibc` 配置菜单，其中包含以下子菜单和选项：

*   `Target Architecture`
*   `Target Architecture Features and Options`
*   `General Library Settings`
*   `Advanced Library Settings`
*   `Networking Support`
*   `String and Stdio Support`
*   `Big and Tall`
*   `Library Installation Options`
*   `Security Options`
*   `uClibc Development/Debugging Options`

请注意，`uClibc` 配置菜单中的许多选项（如架构类型和安装路径）将已经根据您之前在 `Buildroot` 配置菜单中的选择进行了设置。

现在让我们看看每个配置子菜单中的选项。如前所述，您可以使用 `?` 键从配置系统获取有关每个选项的更多信息。由于某些选项依赖于其他选项的设置，因此此处列出的一些选项可能不会在您的配置中显示。虽然大多数选项是二元选择（启用或禁用），但其他选项是文本字段。

`Target Architecture` 选项指定了将为其构建 `uClibc` 的目标架构。我们之前描述的 `Buildroot` 配置菜单已设置此选项。

`Target Architecture Features and Options` 子菜单包含以下选项：

### Target Processor Type

要优化的特定架构的哪个型号。

### Target file format

要使用的可执行文件格式。对于使用 `MMU` 的目标，该选项预设为 `ELF`。对于非基于 `MMU` 的目标，提供了二进制文件类型选择。关于各种格式及其相对优缺点的讨论，请参见 `http://www.linuxdevices.com/articles/AT3186625227.html`。

### Target CPU has a memory management unit (MMU)

指定指定的目标 `CPU` 是否有 `MMU`。如果在 `Target Processor Type` 选项中选择了一个特定的目标型号，此字段可能会为您预设。

### Do you want to utilize the MMU?

即使硬件支持 `MMU`，您可能也希望通过不使用它来节省 `RAM` 和 `CPU` 周期。

### Enable floating-point number support

此选项允许您从 `uClibc` 中省略所有浮点数支持。这将导致浮点函数（如 `strtod()`）从 `uClibc` 中省略。其他浮点函数，如 `printf()` 和 `scanf()`，仍将包含在库中，但不包含对浮点数的支持。

### Target CPU has a floating-point unit (FPU)

如果您的目标 `CPU` 没有浮点单元 (`FPU`) 或内核 `FPU` 模拟器，但仍希望支持浮点函数，则可以使用软浮点支持（使用 `gcc` 的 `-msoft-float` 选项）编译 `uClibc`。取消选中此选项将启用此行为。

### Enable full C99 math library support

如果您希望 `uClibc` 数学库包含完整的 `C99` 数学库特性，请设置此选项。如果不设置，数学库将仅包含 `POSIX/IEEE 1003.1b-1993` 标准中列出的数学函数，从而根据架构保存几十 KB 的库大小。

### Linux kernel header location

此字段包含内核头文件路径，并由 `Buildroot` 系统预设。

`General Library Settings` 子菜单包含以下选项：

### Generate position-independent code (PIC)

完全以位置无关代码构建 `uClibc`，即使是静态部分（共享库部分始终构建为 `PIC` 代码）。仅当您希望在共享库内静态链接 `uClibc` 时，此选项才有用，且很少开启。

### Enable support for shared libraries

除非正在构建仅静态库系统，否则应启用此选项。

### Only load shared libraries which can share their text segment

此选项将阻止共享库加载器加载在加载期间修改程序代码段以支持重定位的共享库（因此需要为每个共享库使用者额外内存）。此类修改通常发生在共享库在构建时未使用 `-fPIC` 或 `-fpic` 选项（强制位置无关代码）的情况下。

由于构建没有位置无关代码的共享库通常不是个好主意，此选项可以捕获其他会导致不必要 `RAM` 浪费的构建错误。

### Native 'ldd' support

启用支持传统 `ldd` 所需的所有代码，`ldd` 执行共享库加载器以解析所有依赖项，然后显示应用程序运行所需的共享库列表。禁用此选项会使 `uClibc` 的共享库加载器稍小，但使调试某些链接问题变得更困难。

### Enable library loader cache (ld.so.conf)

启用此项以使用 `etc/ld.so.conf`，即共享库加载器缓存配置文件，以支持非标准库路径，类似于 `glibc` 中的等效行为。

### Enable library loader preload file (ld.so.preload)

启用此项以使用 `etc/ld.so.preload`。此文件包含在程序加载之前要加载的共享库的空格分隔列表。它在 `glibc` 中也有等效项。

### 共享库加载器命名前缀

设置所有共享库加载器文件的自定义前缀。只有当您计划在同一系统上同时支持 `glibc` 和 `uClibc` 时才需要此选项。在实际的生产嵌入式系统中，这种情况几乎不会发生，因此建议保留默认值。

### 静态链接 ldconfig

启用此选项以静态链接 `ldconfig` 二进制文件（从而使其体积略微增大），这在调试共享库链接问题时非常有用。否则，您可能无法运行 `ldconfig` 工具，因为它也依赖于共享库。如果空间要求允许，建议启用此选项。

### 启用 ELF RUNPATH 标签支持

`ELF` 可执行文件格式支持动态 `RPATH/RUNPATH` 标签，允许基于单个可执行文件动态覆盖共享库的默认搜索路径。此功能的使用并不普遍，因此禁用对其的支持是缩小共享库加载器大小和减少共享库加载时间的好方法。

### 支持全局构造器和析构器

如果您没有计划使用 C++ 或 `GNU` 扩展构造器和析构器属性（使用 `__attribute__((constructor))` 和 `__attribute__((destructor))` 语法），您可以完全省略对它们的支持，从而使系统中的每个可执行文件略微变小。

### POSIX 线程支持

启用此选项将为 `uClibc` 添加对 `POSIX` 线程的支持，这将增加 `uClibc` 的体积，并对运行时性能产生轻微影响，因为需要添加锁原语以保护内部关键的 `uClibc` 数据结构。除非您从不打算使用线程，否则建议启用此选项。

### 构建 pthreads 调试支持

启用此选项将构建 `libthread_db` 共享库，这对于调试多线程应用程序是必需的。除非您从不打算在目标上调试多线程代码，否则建议启用此选项。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_145_0.png)

为了使多线程调试成为可能，`GDB` 也必须使用 `uClibc` 进行构建。

### 使用旧版（稳定）LinuxThreads

目前，`uClibc` 仅支持遗留的（`LinuxThreads`）线程库，但也提供了对 `NPTL` 的实验性支持。

然而，`uClibc` 支持两个版本的 `LinuxThreads`。旧版（稳定版）在 `uClibc` 中存在时间较长，但除了 bug 修复外，没有太多更新。新版本测试较少，并且缺乏针对 `glibc` 不支持的架构（如 `Blackfin` 和 `FRV`）的移植，但它是基于 `glibc` 的最新代码，因此可能是较新移植（如 `Alpha`、`AMD64` 和 `HPPA`）的唯一选择。

### 大文件支持

启用此选项允许 `uClibc` 支持大于 2 GB 的文件，代价是占用更多空间。

### Malloc 实现

此子菜单允许在三种 `malloc()` 实现中进行选择，从适合小 `RAM` 系统和较小分配的简单实现，到相当于 `glibc` 中找到的标准实现不等。

### Malloc 为 malloc(0) 返回存活指针

此选项控制 `malloc()` 在请求返回零大小分配时的行为。为此完全兼容 `glibc`，请启用此选项。

### 动态 atexit() 支持

控制是否支持多个动态 `atexit()` 回调。这是正确支持 C++ 所必需的。

### 旧版（可见）atexit 支持

这是一个过时的选项，包含在内以与旧版 `uClibc` 发行版保持向后兼容。请保持未设置状态。

### 启用 SuSv3 遗留函数和启用 SuSv3 遗留宏

启用对某些软件包可能仍需要的已废弃函数和宏（`bcopy`、`bzero`、`bcmp`、`index` 和 `rindex`）的支持。

### 影子密码支持

启用将用户密码存储在影子文件中，并与主用户数据库分离以提供更好安全性的支持。建议启用此选项。
