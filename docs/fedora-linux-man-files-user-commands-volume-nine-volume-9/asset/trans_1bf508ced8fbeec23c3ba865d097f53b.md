
## 描述

以下是由 Tom Christianen <> 编写的旧版 c2ph.doc 文档。日期：1991 年 7 月 25 日 08:10:21 GMT

曾经，我写了一个名为 pstruct 的程序。它是一个 Perl 程序，试图解析 C 结构体并显示其字段偏移量。这对那些查看二进制转储或在内核中折腾的人特别有用。

Pstruct 并不是一个漂亮的程序。它也不特别健壮。问题在于，C 编译器解析 C 语言的能力远超我所能达到的水平。

于是我变得聪明了：我决定偷懒，让 C 编译器去解析 C，它会为我输出调试器 stabs（符号调试信息）供我读取。解析这些要容易得多。它仍然不是一个漂亮的程序，但至少更健壮了。

Pstruct 可以处理任何 .c 或 .h 文件，或者更推荐 .s 文件，因为反正它最终会将它们整理成这种格式，并输出如下列表：

```
struct tty {
  int tty.t_locker            000 4
  int tty.t_tex_index         004 4
  struct tty * tty.t_tp_virt  008 4
  struct clist tty.t_rawq     00c 20
    int tty.t_rawq.c_cc       00c 4
    int tty.t_rawq.c_cmax     010 4
    int tty.t_rawq.c_cfx      014 4
    int tty.t_rawq.c_clx      018 4
    struct tty * tty.t_rawq.c_tp_cpu  01c 4
    struct tty * tty.t_rawq.c_tp_iop  020 4
    unsigned char * tty.t_rawq.c_buf_cpu  024 4
    unsigned char * tty.t_rawq.c_buf_iop  028 4
  struct clist tty.t_canq     02c 20
    int tty.t_canq.c_cc       02c 4
    int tty.t_canq.c_cmax     030 4
    int tty.t_canq.c_cfx      034 4
    int tty.t_canq.c_clx      038 4
    struct tty * tty.t_canq.c_tp_cpu  03c 4
    struct tty * tty.t_canq.c_tp_iop  040 4
    unsigned char * tty.t_canq.c_buf_cpu  044 4
    unsigned char * tty.t_canq.c_buf_iop  048 4
  struct clist tty.t_outq     04c 20
    int tty.t_outq.c_cc       04c 4
    int tty.t_outq.c_cmax     050 4
    int tty.t_outq.c_cfx      054 4
    int tty.t_outq.c_clx      058 4
    struct tty * tty.t_outq.c_tp_cpu  05c 4
    struct tty * tty.t_outq.c_tp_iop  060 4
    unsigned char * tty.t_outq.c_buf_cpu  064 4
    unsigned char * tty.t_outq.c_buf_iop  068 4
  (*int()) tty.t_oproc_cpu    06c 4
  (*int()) tty.t_oproc_iop    070 4
  (*int()) tty.t_stopproc_cpu 074 4
  (*int()) tty.t_stopproc_iop 078 4
  struct thread * tty.t_rsel  07c 4
}
```

等等。

实际上，这是由一组特定选项生成的。你可以控制每一列的格式，无论是宽格式还是粗体，十六进制还是十进制，前导零或其他内容。

要使用此工具，你只需要一个能生成 BSD/GCC 风格 stabs 的 C 编译器。在原生 BSD 编译器和 GCC 上使用 **-g** 选项即可实现这一点。

要了解更多信息，只需输入一个无效的选项，例如 -!?，系统会提供一条详细的用法说明。有很多可能性可供选择。

如果你只是一名 C 程序员，那么本消息到此为止。你现在就可以退出了，如果你愿意，可以保存源码并在想要的时候运行它。或者不运行。

但如果你是 Perl 程序员，那么对于你来说，我还拥有比结构体偏移量打印器更奇妙的东西。

你看，如果你以它的另一种化身 c2ph 来调用 pstruct，你就是一个代码生成器，可以将 C 代码转换为 Perl 代码！至少可以转换结构体和联合声明，但这已经相当不错了。

在此之前，任何想要与 C 程序（如内核）交互的 Perl 程序员都不得不猜测 C 结构体的布局，然后将这些布局硬编码到他们的程序中。当然，当你把你精心制作的程序带到结构体布局不同的系统上时，你的程序就会崩溃。这真是令人遗憾。

我们已经有 Larry 的 h2ph 转换器，这很有帮助，但它只适用于 cpp 符号，而不是真正的 C，而后者也是急需的。我提供给你的是获取所有 C 结构体符号化方法。我将它们封装在包和函数中。请考虑以下程序：

```perl
#!/usr/local/bin/perl
require 'syscall.ph';
require 'sys/ti.ph';
require 'sys/resource.ph';
$ru = "\0" x &rusage'sizeof();
syscall(&SYS_getrusage, &RUSAGE_SELF, $ru) && die "getrusage: $!";
@ru = unpack($t = &rusage'typefdef()), $ru);
$uti = $ru[ &rusage'ru_utime + &tival'tv_sec ] + ($ru[ &rusage'ru_utime + &tival'tv_usec ]) / 1e6;
$sti = $ru[ &rusage'ru_stime + &tival'tv_sec ] + ($ru[ &rusage'ru_stime + &tival'tv_usec ]) / 1e6;
print "you have used %.3fs+%8.3fu seconds.\n", $uti, $sti;
```

如你所见，包的名称就是结构体的名称。常规字段就是它们自己的名称。此外，为了方便你，还提供了以下访问器函数：

```
- struct: 这不接受参数，实际上是结构中第一级元素的数量。你会用它来索引结构体数组，也许像这样：$usec = $ut@user'u_utime + (&INTIMER_VIRTUAL * &itimer'sizeof()) + &itimer'it_value + &tival'tv_usec];
- sizeof: 返回结构体的字节数，或者你传入参数的大小的字节数，例如 &rusage'sizeof(&rusage'ru_stime)
- typedef: 这是传递给 pack 和 unpack 的 Perl 格式定义。如果你请求空的 typedef，你会得到整个结构体，否则你会得到你请求字段的定义。填充问题已得到处理，以及保证联合被解包到所有别名的魔术。不过，位域目前尚不支持。
- offsetof: 这个函数是该字段在数组中的字节偏移量。如果你懒得解包，可能会希望使用它通过 vec() 直接索引到打包的结构体中。
- typeoff: 不要与 typedef 访问器函数混淆，这个函数返回该字段的 C 类型。这将允许你打印出任何结构体的美观结构化漂亮打印，而无需预先了解它的任何信息。这个函数没有参数时为空操作。总有一天我会发布这样一个东西，为你 dump 出你的用户结构体。
```

我认为它的使用方式基本上是这样的：

```
% h2ph <so_include_file.h > /usr/lib/perl/tmp.ph
% c2ph so_include_file.h >> /usr/lib/perl/tmp.ph
% install
```

使用 c2ph 会稍微复杂一些，因为你必须确保包含项正确。我不知道你的系统具体情况，但这通常不会太难。

正如我提到的，代码并不漂亮——一开始我从未想过它会是一个 1000 行的程序，否则我可能根本不会开始。:) 但我会更谨慎地处理程序各部分之间的通信方式等。如果我不必临时去推测 stabs 的构成，并且考虑我的编译器和 gcc 之间的细微差别，情况可能会好一些。

无论如何，这里就是它。应该在 perl v4 或更高版本上运行。也许更低版本也行。

-- tom

## pulseaudio

### 名称

pulseaudio - PulseAudio 声音系统

### 概要

- **pulseaudio** [*选项*]
- **pulseaudio** **—help**
- **pulseaudio** **—version**
- **pulseaudio** **—dump-conf**
- **pulseaudio** **—dump-modules**
- **pulseaudio** **—dump-resample-methods**
- **pulseaudio** **—cleanup-shm**
- **pulseaudio** **—start**
- **pulseaudio** **—kill**
- **pulseaudio** **—check**

### 描述

PulseAudio 是一个适用于 Linux、POSIX 和 Windows 系统的网络低延迟声音服务器。

### 选项

- -h | --help
    - 显示帮助。
- --version
    - 显示版本信息。
- --dump-conf
    - 加载守护进程配置文件 `daemon.conf`（见下文），解析命令行中剩余的配置选项，并以与 `daemon.conf` 兼容的格式打印结果守护进程配置。
- --dump-modules
    - 列出可用的可加载模块。与 `-v` 结合使用以获得更详细的列表。
- --dump-resample-methods
    - 列出可用的音频重采样器。
- --cleanup-shm
    - 识别 `/dev/shm` 中的陈旧 PulseAudio POSIX 共享内存段，并在可能时将其删除。每当新的守护进程启动或客户端尝试连接守护进程时，都会隐式执行此操作。通常不需要手动发出此命令。仅可在通过挂载到 `/dev/shm` 的虚拟文件系统实现 POSIX 共享内存段的系统上可用（例如 Linux）。
- --start
    - 如果 PulseAudio 尚未运行，则启动 PulseAudio。这与不带 --start 选项启动 PulseAudio 不同，后者在 PA 已经运行时将失败。当此调用返回时，PulseAudio 保证已完全初始化。隐含 --daemonize。
- -k | --kill
    - 终止调用用户已运行的 PulseAudio 守护进程（等效于发送 SIGTERM）。
- --check
    - 当调用用户的 PulseAudio 守护进程已在运行时，返回 0 作为返回代码，否则返回非零。除向 stderr 输出错误外，控制台无其他输出。
- --system[=BOOL]
    - 作为系统级实例运行，而不是每用户实例。请注意，这将禁用 PulseAudio 的某些功能，除非系统没有本地用户（例如瘦客户机），否则一般不建议这样做。此功能需要特殊配置和设置专用 UNIX 用户。强烈建议将此选项与 --disallow-module-loading（见下文）结合使用。
- -D | --daemonize[=BOOL]
    - 在启动后守护进程化，即从终端分离。
- --fail[=BOOL]
    - 当启动脚本 `default.pa`（见下文）中指定的任何命令失败时，让启动失败。
- --high-priority[=BOOL]
    - 尝试获取高的 Unix nice 级别。仅当调用用户具有足够权限时才会成功。

