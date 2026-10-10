

Linux 对 FFS 的支持并不完美。特别是，读写支持是独立于只读支持进行编译的，而且只读支持被视为实验性功能。因此，即使你已经在 Linux 内核中编译了基本的 FFS 支持，你也可能无法向 FreeBSD 分区写入数据。如果你需要向 FFS 分区写入数据，我建议你谨慎行事，因为 Linux 可能会损坏该分区。

## 关于外部访问的注意事项

从非 BSD 操作系统访问 FreeBSD 文件系统时，会遇到与从 FreeBSD 访问非 BSD 文件系统时类似的注意事项。特别是，由于多年来 FFS 的演变和差异，你可能无法从非 BSD 的类 UNIX 操作系统访问 FreeBSD 的文件系统，即使这些操作系统名义上支持 FFS。即使你可以挂载文件系统，如果你的 UID 和 GID 在安装之间不一致，你也可能会注意到文件的表观所有者和组存在差异。在创建用户和组时具备一定的前瞻性，可以极大程度地减少这些问题。

更令人担忧的是文件损坏的可能性，尤其是在使用 Linux 的读写 FFS 支持时。在你从 Linux 向 FFS 分区写入之前，应该备份你的 FreeBSD 文件。不过，Linux 的只读 FFS 支持危险程度低得多，因此如果你只是想读取一些 FreeBSD 文件，应该不会有什么大问题。

## 在 FreeBSD 中运行非 BSD 程序

FreeBSD 提供了广泛的软件，但偶尔你可能会发现需要运行一个 FreeBSD 上不可用的程序。与其使用第二台电脑或双启动进入另一个操作系统，你也许可以使用几种能够让 FreeBSD 运行旨在其他操作系统上使用的程序的工具之一。其中最为可靠的是 FreeBSD 的 Linux 仿真功能，它让 FreeBSD 可以运行 Linux 程序。其他工具可以让你运行 Windows 程序，或者在一个完整仿真的计算机中运行任何 x86 操作系统。

## 运行 Linux 程序

尽管谱系不同，但 FreeBSD 和 Linux 是非常相似的操作系统。事实上，在许多情况下，相同的源代码可以在两者上编译和运行。因此，绝大多数在其中一个操作系统上运行的开源程序也可以在另一个操作系统上原生运行。然而，并非所有程序都是开源的，而且一些商业程序仅在 Linux 上可用，而在 FreeBSD 上不可用。为此，FreeBSD 提供了运行 Linux 程序的能力。这种支持涉及一系列库和支持包。安装这些之后，你可以几乎像在 FreeBSD 上运行程序那样运行 Linux 程序。由于 FreeBSD 和 Linux 使用几乎相同的系统调用，在运行 Linux 程序时无需使用大量的仿真例程。因此，Linux 程序在 FreeBSD 下的运行速度与在 Linux 下大致相同。不过，内存会受到影响，因为 Linux 程序需要 Linux 兼容的系统库，其中许多库的功能与 FreeBSD 标准库中的功能重复。

### 准备运行 Linux 程序

在基本安装中，FreeBSD 并未配置为运行 Linux 程序。若要执行此操作，请完成以下步骤：

- **安装 Linux 基础端口。** *linux_base* 软件包包含核心 Linux 库和支持工具。其中大部分位于 `/compat/linux` 目录树中。你可以按照第 11 章中描述的其他软件包安装方式安装此软件包。
- **配置主机名解析。** 一些 Linux 程序在使用默认配置运行时，在将主机名解析为 IP 地址时会出现问题。如果你遇到此问题，应编辑 `/compat/linux/etc/host.conf` 文件，使其包含以下内容：
  ```
  order hosts,bind
  multi on
  ```
- **启动 Linux 兼容模式。** 输入 `kldload linux` 以启动 Linux 兼容模式。此后，你应该能够运行 Linux 程序。如果你希望系统在启动后自动启用此模式，请确保在 `/etc/rc.conf` 文件中添加以下行（如果尚未存在）：
  ```
  linux_enable="YES"
  ```
  此时，FreeBSD 应支持 Linux 二进制文件。若要检查是否确实如此，你可以使用 `kldstat` 程序，它会返回有关系统上加载的内核模块的信息，包括 FreeBSD 的 Linux 兼容模块。正常工作的 Linux 支持层应产生类似于以下内容的输出：

```
$ kldstat
Id Refs Address     Size      Name
1   5   0xc0100000  3ef2dc    kernel
2   1   0xc1cb2000  16000     linux.ko
```

可能会有更多行显示额外的模块。关键在于应存在引用 *linux.ko* 内核模块的行，例如前面示例中 ID 为 2 的那一行。

### 重新配置和运行 Linux 程序

FreeBSD 和 Linux 使用相同的基本格式来组织程序文件。这种格式被称为*可执行与链接格式*（ELF）。尽管基本格式相同，但一些细节存在差异，这有时会导致 FreeBSD 无法识别 Linux 二进制文件为有效文件。如果 FreeBSD 报告某个 Linux 二进制文件无效，你必须使用 `brandelf` 程序以 FreeBSD 能够识别的方式标记该程序文件。具体而言，你需要使用类似于以下命令：

```
# brandelf -t Linux linux-binary
```

在此示例中，`linux-binary` 是你想要运行的二进制程序文件的名称。在某些情况下，程序现在应该可以像 FreeBSD 程序一样正常工作：尝试输入其名称，看看它是否运行。文本模式程序应产生正常的输出，X 程序应打开窗口并运行。事实上，仅凭用户界面很难辨别出一个程序是 Linux 程序。

不幸的是，Linux 程序经常需要你的 FreeBSD 系统未安装的库。更准确地说，Linux 程序需要 Linux 版本的库。拥有本地 FreeBSD 版本的库是不够的；你必须安装该库的 Linux 版本。`linux_base` 软件包的大部分仅就是这些——许多 Linux 程序所依赖的库。然而，该软件包无法做到面面俱到，因此你可能需要追踪 Linux 版本的库。

追踪其中一种方法是使用 Linux 或 FreeBSD 中的 `ldd` 命令。应用于 FreeBSD 4.4 系统中 Caldera OpenLinux 3.1 的 `ls` 二进制文件的如下所示的结果应该类似于以下形式：

```
$ ldd ls
ls:
    /lib/libc.so.6: version `GLIBC_2.2' not found (required by ls)
    libc.so.6 => /lib/libc.so.6 (0x28068000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x28053000)
```

> **注意**
> 此示例使用较新版本的 Linux 和较旧版本的 FreeBSD，因为它说明了旧库（在 FreeBSD 4.4 的 Linux 兼容软件包中）可能无法与新二进制文件（较新的 Caldera 3.1 中常见的 `ls` 二进制文件）配合使用的事实。

在这种情况下，`ls` 程序依赖于两个库：`libc.so.6` 和 `ld-linux.so.2`。两者都存在，但 `libc.so.6` 的版本对于所涉及的 `ls` 程序来说太旧了，因此出现了未找到 `GLIBC_2.2` 的消息。也有可能所需的库在 FreeBSD 系统上根本不存在。

无论哪种情况，解决方案都是从 Linux 系统（或 Linux 库软件包）中将所需的库复制到 FreeBSD 系统的 `/compat/linux` 目录树中。在此特定情况下，Caldera Linux 系统有一个 `/lib/libc.so.6` 文件，它实际上是指向 `/lib/libc-2.2.1.so` 的符号链接。为了使其正常工作，你应该执行以下操作：

- 将实际的库文件（`/lib/libc-2.2.1.so`）复制到你的 `/compat/linux` 目录树中——也就是说，将 `libc-2.2.1.so` 复制到 `/compat/linux/lib`。
- 创建一个符号链接，以镜像 Linux 系统上存在的链接。例如，将 `libc-2.2.1.so` 链接到 `libc.so.6`。如有必要，替换指向较旧库的任何现有链接。

![](img/f34d37e3abe9f4517128e54f80ab2616_160_0.png)

你可能需要对几个库重复此过程。在某些情况下，解决一个问题会揭示另一个问题。例如，在从 FreeBSD 4.4 运行 Caldera 3.1 的 `ls` 的情况下，更新 `libc.so.6` 后发现 `ld-linux.so.2` 也需要更新，因此必须对该库重复此过程。当所有这些工作完成后，程序应该能够运行，尽管一些程序会产生无害的错误消息。例如，在 FreeBSD 4.4 中运行的 Caldera 3.1 的 `ls` 会抱怨 `fstat64` 和 `setup` 是过时的系统调用。

> **提示** 与其按个案升级库，你也许想寻找 `linux_base` 软件包的更新版本。安装它可能比追踪许多更新的库要简单得多。

Linux 二进制兼容性还有一些其他限制，你应该了解这些限制。尽管大多数在 Linux 上可用的功能在 FreeBSD 上也可用，但有些不可用，或者在 FreeBSD 中以不同的方式实现。一个重要的考量是 `/proc` 文件系统。此文件系统使程序能够访问各种类型的系统信息。其细节在 Linux 和 FreeBSD 之间有所不同，因此如果 Linux 程序依赖于从 `/proc` 获取的信息，该程序在 FreeBSD 中运行时可能无法正常工作。

总体而言，FreeBSD 的 Linux 二进制兼容性对于运行商业（或至少是非开源）程序非常有用，例如 WordPerfect、StarOffice、Oracle、VMware 和 quake。在大多数情况下，对于开源程序，由于可以访问源代码，Linux 二进制兼容性并不重要。

## 使用 WINE 运行 Windows 程序

不幸的是，大多数在 FreeBSD 上不可用的程序在 Linux 上也不可用，因此 FreeBSD 的 Linux 兼容性虽然有用，但适用范围有限。你可能想要运行的、通常不属于 UNIX 系统的大部分程序都是 Windows 程序。尽管 Windows 从 UNIX 世界借用了一些概念甚至代码，但它是一个非常不同的操作系统，因此在 FreeBSD 上运行 Windows 程序不像运行 Linux 程序那么容易。话虽如此，目前有一些项目正在向 FreeBSD 的功能集添加 Windows 兼容性。其中可以说最重要的一项是 **WINE**（根据询问对象不同，它代表 *Windows Emulator* 或 *WINE Is Not an Emulator*）。WINE 是一个开源项目，旨在在类 UNIX 操作系统（包括 FreeBSD）下实现 Windows 应用程序编程接口（API）。这意味着程序可以使用 Windows 调用来打开对话框、显示文本等。WINE 还包括一种加载和运行 Windows 可执行文件并提供运行 Windows 程序所需的其他各种支持的方式。最终结果是 Windows 程序可以在 FreeBSD 下运行。

WINE 是一个雄心勃勃的项目，特别是考虑到它的任务是瞄准一个“移动目标”——微软不断扩展和更改 Windows API，并且部分

