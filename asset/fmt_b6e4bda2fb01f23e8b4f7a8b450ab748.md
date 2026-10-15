
- `/dev/tty9`
- `/dev/tty10`
- `/dev/tty11`
- `/dev/tty12`
- `/dev/tty13`
- `/dev/tty14`
- `/dev/tty15`
- `/dev/tty16`
- `/dev/tty17`
- `/dev/tty18`
- `/dev/tty19`
- `/dev/tty20`
- `/dev/tty21`
- `/dev/tty22`
- `/dev/tty23`
- `/dev/tty24`
- `/dev/tty25`
- `/dev/tty26`
- `/dev/tty27`
- `/dev/tty28`
- `/dev/tty29`
- `/dev/tty30`
- `/dev/tty31`
- `/dev/tty32`
- `/dev/tty33`
- `/dev/tty34`
- `/dev/tty35`
- `/dev/tty36`
- `/dev/tty37`
- `/dev/tty38`
- `/dev/tty39`
- `/dev/tty40`
- `/dev/tty41`
- `/dev/tty42`
- `/dev/tty43`
- `/dev/tty44`
- `/dev/tty45`
- `/dev/tty46`
- `/dev/tty47`
- `/dev/tty48`
- `/dev/tty49`
- `/dev/tty50`
- `/dev/tty51`
- `/dev/tty52`
- `/dev/tty53`
- `/dev/tty54`
- `/dev/tty55`
- `/dev/tty56`
- `/dev/tty57`
- `/dev/tty58`
- `/dev/tty59`
- `/dev/tty60`
- `/dev/tty61`
- `/dev/tty62`
- `/dev/tty63`
- `/dev/tty64`
- `/dev/tty65`
- `/dev/tty66`
- `/dev/tty67`
- `/dev/tty68`
- `/dev/tty69`
- `/dev/tty70`
- `/dev/tty71`
- `/dev/tty72`
- `/dev/tty73`
- `/dev/tty74`
- `/dev/tty75`
- `/dev/tty76`
- `/dev/tty77`
- `/dev/tty78`
- `/dev/tty79`
- `/dev/tty80`
- `/dev/tty81`
- `/dev/tty82`
- `/dev/tty83`
- `/dev/tty84`
- `/dev/tty85`
- `/dev/tty86`
- `/dev/tty87`
- `/dev/tty88`
- `/dev/tty89`
- `/dev/tty90`
- `/dev/tty91`
- `/dev/tty92`
- `/dev/tty93`
- `/dev/tty94`
- `/dev/tty95`
- `/dev/tty96`
- `/dev/tty97`
- `/dev/tty98`
- `/dev/tty99`
- `/dev/tty100`
- `/dev/tty101`
- `/dev/tty102`
- `/dev/tty103`
- `/dev/tty104`
- `/dev/tty105`
- `/dev/tty106`
- `/dev/tty107`
- `/dev/tty108`
- `/dev/tty109`
- `/dev/tty110`
- `/dev/tty111`
- `/dev/tty112`
- `/dev/tty113`
- `/dev/tty114`
- `/dev/tty115`
- `/dev/tty116`
- `/dev/tty117`
- `/dev/tty118`
- `/dev/tty119`
- `/dev/tty120`
- `/dev/tty121`
- `/dev/tty122`
- `/dev/tty123`
- `/dev/tty124`
- `/dev/tty125`
- `/dev/tty126`
- `/dev/tty127`
- `/dev/tty128`
- `/dev/tty129`
- `/dev/tty130`
- `/dev/tty131`
- `/dev/tty132`
- `/dev/tty133`
- `/dev/tty134`
- `/dev/tty135`
- `/dev/tty136`
- `/dev/tty137`
- `/dev/tty138`
- `/dev/tty139`
- `/dev/tty140`
- `/dev/tty141`
- `/dev/tty142`
- `/dev/tty143`
- `/dev/tty144`
- `/dev/tty145`
- `/dev/tty146`
- `/dev/tty147`
- `/dev/tty148`
- `/dev/tty149`
- `/dev/tty150`

### 关键信息

下一批信息涉及定义你的显示器设置、显示器制造商和型号名称的字符串。这些是自愿的。

接下来是选择显卡。如果你愿意，可以浏览 124 显卡的列表并尝试匹配你的显卡。当你知道自己拥有哪种特定显卡时，这非常有用。你会被问以下问题：

你想查看显卡数据库吗？

按 `y` 查看数据库；按 `n` 跳过。如果你选择数据库，你将看到如下一系列行：

| 0 928Movie | S3-928 |
| 1 AGX (generic) | AGX |
| 2 ALG-5434(E) | CL-GD5434 |
| 3 ATI 8514 Ultra (no VGA) | ATI-Mach8 |
| .... | |

# 100 第 3 章：安装 Linux 和网络组件

此列表占据了多个屏幕。列出了特定的显卡（如 `AGX`）以及它使用的芯片组（`AGX`）。在每个屏幕的底部，你会被要求选择显卡编号，按 `Enter` 键进入配置过程的下一页，跳过剩余的显卡定义。如果你选择了特定的显卡，将看到有关该显卡的信息，包括支持它的 X 服务器的名称。

在那些不知道自己拥有哪种特定显卡但知道自己拥有什么类型的芯片组（例如基于 S3 的芯片组）的情况下，你不应该从此列表中选择特定的显卡。相反，直接按 `q` 跳到下一个菜单，在其中选择服务器。

选择服务器实际上比选择芯片组更重要。所有基于 S3 的显卡都使用 S3 X 服务器。这个过程使得选择 X 服务器看起来比实际要复杂。无论你是否选择了显卡，都会收到以下菜单，它显示为：

你必须确定要运行哪个服务器。请参考 `man` 手和其他文档。可用服务器如下（它们可能未安装在你的系统中）：

- 1. `XF86_Mono` 服务器。这是一个单色服务器，应该可以在任何兼容 VGA 的显卡上运行，分辨率为 640x480（某些 SVGA 芯片组支持更多信息）。
- 2. `XF86_VGA16` 服务器。这是一个 16 色 VGA 服务器，应该可以在任何兼容 VGA 的显卡上运行。
- 3. `XF86_SVGA` 服务器。这是一个 256 色 SVGA 服务器，支持多种 VGA 芯片。在某些 Cirrus 和 WD 芯片组上经过加速；它在某些 Cirrus 上支持 16/32 位色彩
- 4. 加速服务器。这些包括 `XF86_S3`、`XF86_Mach32`、`XF86_Mach8`、`XF86_8514`、`XF86_P9000`、`XF86_AGX`、`XF86_W32` 和 `XF86_Mach64`。

这四种服务器类型对应 `XF86Config` 中的四个不同的“Screen”（屏幕）部分（vga2, vga16, svga, accel）。

你打算默认运行哪一种屏幕类型（1-4）？

如果你选择了一个特定的显卡，在此处你会多出一行：

- 5. 从显卡定义中选择服务器，`XF86_S3`。

# 第 3 章：安装 Linux 和网络组件

基本上，X 服务器的类型与芯片组匹配。任何使用 S3 芯片组的人都会选择 `XF86_S3` X 服务器。如果你想使用加速服务器且没有指定芯片组，你应该选择 4，然后在 X 服务器列表中选择你的芯片组。

系统会提问你是否想在 X 程序文件和 X 服务器之间创建一个符号链接。你应该这样做；遵循默认设置即可，你就不会遇到任何问题。

下一个问题与你显卡上的内存有关：

- 你的显卡上有多少显存？
- 1 256K
- 2 512K
- 3 1024K
- 4 2048K
- 5 4096K
- 6 其他

输入正确的数字。如果你不知道，请选择 512K 或 1024K。大多数较新的显卡至少有 1024 KB 内存；这是显示 256 色 1024x768 分辨率所需的最小内存。

下一部分处理你的显卡的标识符，类似于之前的显示器标识符。这些信息是可选的。

如果你选择了加速服务器，系统会询问你关于显卡的一些技术设置：时钟芯片（Clockchip）和时钟频率。这是一个你可以直接跟随 `xf86config` 脚本区域。如果你不知道 clockchip 设置，直接按 `Enter` 即可。如果你不知道显卡的时钟频率，可以使用仅探测模式（probe-only mode）运行 服务器。你可以让 `xf86config` 为你探测时钟值。这些信息将自动插入到 `XF86Config` 文件中。如果你使用的显卡或芯片组不需要这些信息，那么 `xf86config` 将记录这一点不会询问时钟速度。这意味着你可以放心来，让 `xf86config` 脚本完成所有工作。

最后，你的最后一个重大决定关于你想要运行的分辨率：
