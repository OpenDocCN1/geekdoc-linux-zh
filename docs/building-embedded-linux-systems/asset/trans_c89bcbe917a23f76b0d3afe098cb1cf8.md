
从 1.3 版本开始，编译器或交叉编译器的选择不再通过配置文件进行，而是采用与 Linux 内核相同的方式，使用相同的 `ARCH` 和 `CROSS_COMPILE` 设置。这在第 5 章中有详细说明。

配置好 BusyBox 后，就可以编译并安装它。当与 glibc 链接时，请使用以下命令：

```bash
$ make ARCH=mips CROSS_COMPILE=mipsel-linux- \
> CONFIG_PREFIX=${PRJROOT}/rootfs install
```

`CONFIG_PREFIX` 被设置为目标根文件系统的基础目录。*Makefile* 会将所有 BusyBox 组件安装到此目录内。

若要使用 uClibc 替代 GNU C 库来构建 BusyBox，请使用以下命令：

```bash
$ make ARCH=mips CROSS_COMPILE=mipsel-uclibc- \
> CONFIG_PREFIX=${PRJROOT}/rootfs install
```

BusyBox 现已安装到目标系统的根文件系统，并准备就绪可供使用。

### 用法

为了了解如何最佳地使用 BusyBox，让我们首先查看 BusyBox 构建过程安装在目标根文件系统上的组件。正如预期，只安装了一个可执行文件，*/bin/busybox*。这是支持所有已配置命令的单一二进制文件。该二进制文件永远不会被直接调用；相反，为 */bin/busybox* 创建了带有原始命令名称的符号链接。这些符号链接已创建在所有原本包含原始命令的目录中，包括 */bin*、*/sbin*、*/usr/bin* 和 */usr/sbin*。

当在系统正常运行期间输入命令时，*busybox* 命令通过符号链接被调用。进而，*busybox* 使用运行它所采用的名称来确定你实际调用的命令。例如，*/bin/ls* 指向 */bin/busybox*。当你输入 *ls* 时，*busybox* 命令被调用，并且它确定你试图使用 *ls* 命令，因为 *ls* 是命令行上的第一个参数。¹

虽然这种方案简单有效，但它意味着你不能为符号链接使用任意名称。创建指向 */bin/ls* 或 */bin/busybox* 的名为 */bin/dir* 的符号链接是行不通的，因为 *busybox* 不识别 dir 命令。

请注意，虽然符号链接是将命令链接到 */bin/busybox* 的常用方式，但在安装过程中，BusyBox 也可以被指示创建硬链接而非符号链接。无论使用何种类型的链接，其运行时行为都是一样的。

> ¹ 与许多其他应用程序一样，*busybox* 的 *main()* 函数接收用于调用它的命令行作为参数。

项目网站上的文档（随包提供）描述了每个受支持命令的所有可用选项。在大多数情况下，BusyBox 支持的选项与原始命令提供的选项具有相同的功能。例如，在 BusyBox 的 ls 中使用 -al 选项与在原始 ls 中使用相同选项的效果是一样的。

当使用 BusyBox 提供的 shell 之一（例如 ash、hush、lash 或 msh）时，你会发现使用 `/etc/profile` 文件为所有 shell 用户定义一些全局变量非常方便。下面是一个针对单用户目标的示例 `/etc/profile` 文件：

```bash
# Set path
PATH=/bin:/sbin:/usr/bin:/usr/sbin
export PATH
```

除了设置路径外，你还可以设置 LD_LIBRARY_PATH 环境变量，该变量在每个应用程序启动时用于定位其依赖的库。虽然库的默认位置是 /lib，但你的系统中可能在其他目录中也有库。如果是这种情况，你可以通过将适当的目录路径添加到 LD_LIBRARY_PATH 来强制动态链接器查找其他库。与 PATH 环境变量一样，你可以通过在目录路径之间放置冒号来向库路径添加更多目录。

请注意，在工作站或服务器上，LD_LIBRARY_PATH 实际上仅用作新库路径的临时存放处。要永久添加另一个库路径，管理员会编辑 `/etc/ld.so.conf` 并运行 `ldconfig` 命令以咨询该文件并生成 `/etc/ld.so.cache`，该文件本身由动态链接器读取以查找动态链接应用程序的库。尽管 `ldconfig` 在我们在第 4 章中编译 glibc 时生成，但它是目标二进制文件，无法在主机上运行以生成目标 `ld.so.cache`。因此，你可以预期许多嵌入式系统没有 `/etc/ld.so.conf`，而是依赖 LD_LIBRARY_PATH 技术。

## TinyLogin：BusyBox 登录工具

TinyLogin 曾经是 BusyBox 开发者维护的另一组工具。它像 BusyBox 一样是一个单一的二进制文件，实现了以下命令：addgroup、adduser、delgroup、deluser、getty、login、passwd、su、sulogin 和 vlock。将 TinyLogin 功能与 BusyBox 分开有几个原因。主要原因是，TinyLogin 实现的大多数命令必须以 root 权限运行，这反过来要求 TinyLogin 二进制文件属于 root 用户并启用其“设置用户”权限位，这种配置通常称为“setuid root”。由于 TinyLogin 使用与 BusyBox 相同的方式使用符号链接，包含两个包功能的一个单一二进制文件也会导致诸如 ls 和 cat 等命令以 root 身份运行，这增加了任何命令中的编程错误被利用以获取 root 权限的可能性。

然而，正如你在原始 TinyLogin 网站 http://tinlogin.busybox.net 上看到的，该项目自 2003 年以来未再更新。这些登录工具现在在 BusyBox 中积极维护。

为解决 setuid 安全问题，BusyBox 为不需要 root 访问权限的小程序（applets）放弃其 root 权限。它也可以配置为检查指定这些特权小程序的 /etc/busybox.conf 配置文件。对于最警惕的用户来说，最安全的解决方案仍然是构建两个独立的 BusyBox 二进制文件，一个用于特权小程序，另一个用于非特权小程序。

在你可以配置的选项中，请特别注意 CONFIG_FEATURE_SHADOWPASSWD、CONFIG_USE_BB_SHADOW 和 CONFIG_USE_BB_PWD_GRP 配置选项，这些选项在配置界面中有记载。最重要的是 CONFIG_FEATURE_SHADOWPASSWD，它添加了对在单独的 etc/shadow 文件中加密的密码的支持。

传统上，/etc/passwd 可以被系统中的任何人读取，这反过来又成了一种安全风险，因为有越来越多用于破解密码的程序可用。因此，使用所谓的影子密码（shadow passwords）成了规范。当启用此功能时，/etc/passwd 中的密码字段只包含填充字符。真正的加密密码存储在 /etc/shadow 中，该文件只能由以 root 权限运行的进程读取。请注意，如果你配置 uClibc 时没有启用影子密码支持，那么启用 CONFIG_FEATURE_SHADOWPASSWD 并与 uClibc 链接将导致构建失败。

你应启用 CONFIG_USE_BB_SHADOW，让 BusyBox 使用其自身的 shadow 函数来访问影子密码，除非你计划使用 glibc 的 NSS 库以及正确配置的 /etc/nsswitch.conf 文件。

如果你启用 CONFIG_USE_BB_PWD_GRP，登录工具将直接使用 /etc/passwd 和 /etc/group 文件，而不是使用 glibc 提供的密码和组函数。否则，你还需要 C 库的 NSS 库和一个 /etc/nsswitch.conf 文件。

请注意，你不需要手动创建和管理 /etc/group、/etc/passwd 和 /etc/shadow 文件，因为 addgroup、adduser、delgroup 和 deluser 命令负责创建或更新这些文件。

有关创建和操作组、密码或影子密码文件的更多信息，以及一般的系统管理，请参阅《Linux 系统管理员指南》（O'Reilly 出版，也可从 Linux 文档项目 [LDP] 获取）、《Running Linux》以及前文在“完整标准应用程序”中提到的《Linux From Scratch》一书。

## embutits

embutits 是另一组针对主流 Unix 命令的迷你化并优化的替代品。虽然 embutits 将某些命令分组在单一二进制文件中，
