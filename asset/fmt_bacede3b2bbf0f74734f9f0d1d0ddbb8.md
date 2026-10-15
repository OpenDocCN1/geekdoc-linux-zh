
现在在选择完你的设置（`i686` 或 `i486`）后，在 `/etc/profile` 文件的下方，向 "`export`" 行添加 "`CFLAG LANG=LESS`"：

`export PATH PATHNAME HISTSIZE HFILESIZE USERNAME MAIL INPUTPRC CFLAG LESS`

然后重新登录；新的 `CFLAG` 环境变量已设置，软件和其他配置将识别。`Pentium (Pro/II/III)` 的优化仅适用于 `gcc` 编译器。你的服务器默认已安装了 `egcs` 编译器，无需担心。

以下是我们使用的不同优化选项的解释：

- `-funroll-loops`
  `-funroll-loops` 优化选项执行循环展开优化，但适用于迭代次数在编译时或运行时可能的循环。

- `-funroll-all-loops`
  `-funroll-all-loops` 优化选项也会执行循环展开，并适用于所有循环。

- `-fast-math`
  `-fast-math` 优化选项允许 `GCC` 编译器为了优化优化代码而违反某些 `ANSI` 规则/规范。

- `-align-double`
  `-align-double` 优化选项控制 `GCC` 编译器将 `double` 和 `long` 变量对齐在双字边界还是单字边界。这将在“`Pentium`”上产生运行稍快的代码，但代价是消耗更多内存。

- `-mcpu-cpu-type`
  `-mcpu-cpu-type` 优化选项将在调度指令时设置用于该机器类型的默认 `CPU`。

- `-march-cpu-type`
  `-march-cpu-type` 优化选项将为机器和 `CPU` 类型生成指令。指定 `-march-cpu-type` 选项意味着隐含时也指定 `-mcpu-cpu-type` 选项。

- `-force-mem`
  `-force-mem` 优化选项通过强制在执行算术之前将内存操作数复制到寄存器中来产生更好的代码。

关于本书的意见和建议请邮寄至 `gmourani@videotron.ca`

- `-fomit-frame-pointer`
  `"-fomit-frame-pointer"` 优化选项是最有趣的选项之一，它允许在不需要的函数中不向寄存器中保留留栈帧指针（`frame pointer`）。这避免了保存、设置和恢复栈帧指针的指令；它还为许多函数留出了额外的寄存器，但也会导致在大多数机器上无法进行调试。

注意：我们在书中将描述的所有后续优化方案默认均适用于 `Pentium II/III/III CPU` 家族。因此，如果需要，你必须在 `/etc/profile` 文件中以及编译期间针对你的特定 `CPU` 处理器类型调整编译标记。

## 基准测试结果
### 按架构汇总

取决于你的处理器架构和编译器的版本（`GCC/EGCS`），优化选项可能会有所不同。下表将帮助你为你的编译器/`CPU` 架构选择最佳的编译标记。

你的 `RedHat Linux 6.1` 上安装的编译器版本为 `egcs 2.91.66`。但在选择编译器优化选项之前，请务必检查一下。

- 若要验证系统中安装的编译器版本，请使用命令：
`root@deep:/# egcs --version`
`egcs-2.91.66`

注意：所有的基准测试结果和未来的结果可以从以下地址 `GCC` 主页获取：`http://egcs.cygnus.com/`

现例如：
对于编译器版本为 `egcs-2.91.66` 的 `CPU pentium II/III (i686)`，最佳的优化选项将是：`FLAGS='-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions'`

### i686

![](img/4e12ba68f8ecabb49a9835b8d88a1c6d_65_0.png)

- `-O0`
- `-O9`
- `-O3 -funroll-all-loops`
- `-O2 -O9 -funroll-loops`
- `-O3 -funroll-loops -ffast-math`
- `-O9 -funroll-all-loops -ffast-math`
- `-O6 funroll all loops`

© Copyright 1999-2000 Gerhard Mourani and Open Network Architecture ®

对于编译器版本为 `egcs-2.91.66` 的 `CPU pentium (i586)`，最佳的优化选项将是：`CFLAGS='-O3 -march=pentium -mcpu=pentium -ffast-math -funroll-loops -fomit-frame-pointer -force-mem -fO3 -fmarch -force-addr -malign-double -fno-exceptions'`

### i586

![](img/4e12ba68f8ecabb49a9835b8d88a1c6d_66_0.png)

| -Os |
| -O2 |
| -O3 |
| -O3-funroll-all-loops |
| -O3-march=pentium-ffast-math-funroll-loops-fomit-frame-pointer-fforce-mem-fforce-addr-malign-double-maligr |
| -O3-march=pentium-ffast-math-funroll-loops-fomit-frame-pointer-fforce-mem-fforce-addr |

对于使用编译器 `egcs-2.91.66` 的 `CPU i486`，最佳的优化选项将是：
`CFLAGS=-O3 -funroll-all-loops -malignalign-double -mcpu=i486 -march=i486 -fomit-frame-pointer -fno-exceptions`

### i486

![](img/4e12ba68f8ecabb49a9835b8d88a1c6d_67_0.png)

© Copyright 1999-2000 Gerhard Mourani and Open Network Architecture ®

# 2. "bdfflush" 参数

`bdfflush` 与 `Linux` 内核虚拟内存（`VM`）子系统的运行密切相关，对磁盘空间的影响较小。该文件 (`/proc/sys/vm/bdfflush`) 控制 `bdfflush` 守护进程的操作。我们通常调整此文件来提高系统性能。通过如所示更改某些默认值，系统似乎响应更加迅速，例如它会稍微多等待一会儿进行写入并避免某些缓存竞争。

- 若要更改 `bdfflush` 的值，请在终端执行以下命令：
`[root@deep] # echo "1000 1200 512 15 5000 000 184" >/proc/sys/vm/bdfflush`

在我们的示例中，根据 `/usr/src/linux/Documentation/sysctl/vm.txt`，第一个参数 (`100`) 给出了缓冲区缓存中脏缓冲区的最大数量。脏缓冲区的内容还需要写入（与干净缓冲区相反，后者可以丢弃）。将其设置为高值意味着 `Linux` 可以长时间延迟脏写，但也意味着当内存不足时，它将必须执行大量的 `I/O`。低值则只会进行一次磁盘 `I/O`。

第二个参数 (`1200`) 给出了 `bdfflush` 一次可以写入磁盘的脏缓冲区数量。高值意味着延迟的、爆发式的 `I/O`，而小值可能在 `bdfflush` 未被充分唤醒时导致内存不足……

第三个参数 (`512`) 是在 `bdfflush` 不被唤醒时对应的脏缓冲区数量阈值。

第四个参数 (`15`) 定义了 `bdfflush` 唤醒的时间间隔。

第五个参数 (`5000`) 定义了脏缓冲区达到写入前的毫秒数。

第六个参数 (`000`) 定义了脏缓冲区占内存的百分比。

第七个参数 (`184`) 定义了脏缓冲区写入磁盘的阈值。

关于此书的意见和建议请邮寄至 `gmourani@videotron.ca`

文件 `file-max` `/proc/sys/file-max` 设置了 `Linux` 内核将分配的文件句柄的最大数量。我们通常会调优此文件，通过增加 `/proc/sys/file-max` 的值来提高打开文件的数量，例如，为每 `4M` 内存将其设置为 `256` 这样的合理数值，即：对于一台拥有 `128 MB` 内存的机器，将其设置为 `8192 (128/4=32*256=8192)`。

- 要将 `file-max` 的值调整为 `128 MB` 内存对应，请在终端中输入以下命令：
`[root]@deep $ echo "8192" > /proc/sys/file-max`

注意：当你定期从你的服务器收到大量运行文件句柄用尽的错误消息时，你可能需要限制此值。默认值为 `4096`。文件服务器或 `Web` 服务器需要大量的打开文件。

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，这样你下次服务器重启时就无需再次输入它们了。

## 7. "inode-max" 参数

`inode-max` `/proc/sys/inode-max` 设置了 `inode` 处理程序的最大数量。我们通常会调优此文件，通过将 `/proc/sys/inode-max` 增加到约为上述设置的 "`file-max`" 打开的文件数量的 `3` 到 `4` 倍 (`8192*4=32768`) 来提高 `inode` 的数量。这是因为每个打开的文件至少会占用一个 `inode`，而对于大文件，这个数量会更大。

- 要将 `inode-max` 的值调整为 `128 MB` 内存对应，请在终端中输入以下命令：
`[root]@deep $ echo "32768" > /proc/sys/inode-max`

注意：如果你经常耗尽 `inode`，则应该增加此值。不要忘记，你为 "`inode-max`" 参数输入的值取决于 "`file-max`" 的值。文件服务器或 `Web` 服务器需要大量的已打开状态的 `inode`。

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，这样你下次服务器重启时就无需再次输入它们了。

# 8. "ulimit" 参数

`Linux` 本身有一个针对每个用户的“最大进程数”（`Max Processes`）限制。此功能允许我们控制服务器上可能允许存在的进程数量。为了提高性能，可以将用户 "`root`" 的进程限制设置为无限制。

编辑 `.bashrc (vi /root/.bashrc)` 并添加以下行：

`ulimit -u unlimited`
