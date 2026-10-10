

## 表 F.10 1.27 版本变更（1995年8月21日）。

| 程序员 | 贡献 |
| :--- | :--- |
| Michael Weller<br>(eowmob@exp-math.uni-essen.de) | • 与 Mach32 相关的更改：<br>• 外观修复。<br>• 新的配置命令 svgaclocks。<br>• RAMDAC。<br>• 厂商支持帮助 alien（不符合原始 ATI 规范）显卡（现在应该可以支持 Dell）。<br>• 修复了几个在 ELF 下导致 dclk 错误的空指针引用。 |
| David Mosberger-Tang<br>(davidm@azstarnet.com) | • 使 SVGAlib 在 Linux/Alpha 上运行的补丁。（已知仅适用于 #9 GXE PCI；其他显卡可能无法工作。） |
| Harm Haanemayer<br>(hhanaemaa@cs.ruu.nl) | • 修改了重复包含检查 vgmouse.h。<br>• 修复了 3 字节/像素模式下的 gl_getpixelo() 中的 bug。<br>• 允许在原始键盘接口中禁用 Ctrl-C 检测。 |
| Gregory Margo<br>(gmargo@newton.vip.best.com) | • 支持 Logitech Mouseman 鼠标系列。<br>• 通过环境变量覆盖鼠标模式 (SVGA_MOUSE_OVERRIDE)。对 Doom 有用。 |
| Stephen Lee<br>(sl14@cruix1.cit.cornell.edu) | • ELF 支持。<br>• 无数的代码清理补丁。<br>• S3 15/16/24bpp 中的 bug 修复。<br>• 更多芯片的自动检测（但，遗憾的是，没有对它们的支持）。 |
| Michael Weller<br>(eowmob@exp-math.uni-essen.de) | • 应要求将配置文件移至 /etc/vga。<br>• 修补 Makefile 以实现自动重新配置。 |

## 表 F.11 1.26 版本变更（1995年4月27日）。

| 程序员 | 贡献 |
| :--- | :--- |
| 未知 | • 真正修复了原始键盘模式下的控制台切换。<br>• 修复了 SDAC 支持。<br>• 修复了 Trio64 检测。不过模式不起作用（使用 RAMDAC "normal"）。<br>• 移动了 ET4000 芯片类型检测，使其在配置文件强制设置芯片时也能工作。<br>• 修复了 Cirrus 5420/22/24 支持。<br>• Mach32 相关更改：修复了 mach32info 中的几个拼写错误。68800-6 现在应该能正确报告。修复了由于接口变更导致 mach32.c 中的编译器警告（还没有新的加速接口）。Mach32 带有 DAC 4 时，24bpp 红先顺序的 NewLAG 返回了。<br>• 支持整个 svgalib + vgagl 中的 24bpp 红先顺序。<br>• 在 vgadraw.c 中添加了对 32bpp 的支持。<br>• 在 vgatest 中添加了对 24bpp 红先顺序的检测。<br>• TODO—修复当 Alt 键保持按下时的原始键盘控制台切换（例如，在 Doom 中）。 |

## 表 F.12 1.25 版本变更（1995年3月7日）。

| 程序员 | 贡献 |
| :--- | :--- |
| 未知 | • 最终修复了不调用 vga_init 的程序的问题。<br>• 修复了 svga/lm 原始键盘模式下的控制台切换（**vgakeyboard.h**）。<br>• 可用的 **ARK** 驱动程序（包括加速）。<br>• 修改了线性寻址检测（支持部分帧缓冲区）。<br>• 增加了更多 **RAMDAC** 支持—S3 支持 AT&T490 兼容的真彩色 DAC。<br>• 调整了鼠标/键盘头文件以修复与 **libgrx** 编译的冲突。 |

## 表 F.13 1.24 版本变更（日期未知）。

| 程序员 | 贡献 |
| :--- | :--- |
| 未知 | • 修复了若未调用 **vga_init** 则导致“not running in ...”消息的 bug。<br>• 更好的驱动程序接口结构（“DriverSpecs”）。可以包含除基本驱动程序函数以外的字段。类型检查也更好了。大多数驱动程序尚未针对新的返回类型进行更新；欢迎发送补丁。某些东西可能坏了。请小心。<br>• 更好的加速接口。<br>• 修复了 **ARK** 芯片类型检测。<br>• 更好的 **ARK** 芯片支持。<br>• 大幅修复了 S3-864 和 **SDAC** 支持。<br>• S3 驱动程序中 Trio64 的时钟/**DAC** 支持未经测试。<br>• 在配置文件中强制 Cirrus 时解锁扩展寄存器。<br>• 尝试在切换某些模式时避免 Cirrus 硬件锁定。<br>• 添加了“accele”程序来测试新的加速接口。 |

## 表 F.14 1.23 版本变更（1995年2月8日）。

| 程序员 | 贡献 |
| :--- | :--- |
| 未知 | • ET4000/W32 调整。<br>• 添加了 **gl_allocatecontext()**。请改用此方法而不是静态声明 **GraphicsContext** 变量。演示程序已相应更改。<br>• 使用位进行更安全的 VC 切换。<br>• 允许具有 512K 内存的 Cirrus SVGA 模式。<br>• 可能修复了 Cirrus 5422 MCLK 检测。<br>• 集成了 Scott Heavner 的 ATI “drive”（允许 132 列文本模式下的 VGA）。<br>• 未经测试的 **ARK** 驱动程序和未经测试的通用 S3 支持（60Hz 下 640×480×256）。<br>• 未使用的加速接口草图 (accel/h/cirrus.c)。 |

## 表 F.15 1.22 版本变更（日期未知）。

| 程序员 | 贡献 |
| :--- | :--- |
| 未知 | • ET4000 对 STG170X **DAC** (tseng3.c 和驱动程序) 的添加，W32p 的线性寻址支持，使用新驱动程序函数更好地处理一般线性寻址，AT&T **DAC** 的 8 位颜色分量 CLUT 支持 (David Etherton)。<br>• Cirrus 驱动程序调整。<br>• 使用新接口重写了针对 S3-864 和 **SDAC** (目前尚不起作用) 的 S3 驱动程序。<br>• 使用 **vga_setlinearaddressing** 进行线性寻址探测。启用线性寻址时切换控制台不是一个好主意。<br>• 将 Oak 077 视为标准 **VGA** (与 OTI-087 模式转储不兼容)。<br>• 修复了平面 **gelpixel** (未测试)。<br>• 原始键盘模式下的 VC 切换 (例如，Doom) (并不总是有效) (是拼写错误，已在 1.25 中修复)。<br>• **VGAGLI** 状态—应能在使用小改动的情况下独立于 SVGAlib 使用。**GraphicsContext** 应由库动态分配 (**malloc**) 以获得兼容性/可扩展性。添加的非标准字体文本写入函数（未测试）。缺少适当的直接页面翻转支持（视频内存中的双缓冲）。这将需要所有操作都在帧缓冲区的特定偏移量处执行。 |

## 表 F.16 1.21 版本变更（1994年12月23日）。

| 程序员 | 贡献 |
| :--- | :--- |
| 未知 | • 部分重构了使用干净的、XF86e86 风格 **SVGA** 通用接口的 Cirrus 驱动。请查看 **timing.*, vgares.*,** 和 **circus.c。**<br>• Cirrus 驱动程序 **init** 现在应支持所有 542x/543x 卡。<br>• 修复了 **MouseSystems** 移动溢出。<br>• 修复了 PS/2 鼠标支持（终于。抱歉）。<br>• 修复了 (旧) Logitech 协议鼠标处理（希望如此—我丢失了包含修复内容的消息）。<br>• 修复了 Cirrus **bitblt** bug。<br>• Gvga6400 驱动程序 BIOS 检查更改；**munmap** 似乎会造成混乱。<br>• 添加了 **vga_gelpixel()** (未测试)。<br>• 整合了 Charles Blake 的 **restorepalette** 补丁，该补丁允许自定义文本模式控制台颜色（参见 **utils/README**）。 |
| Michael Weller<br>(eowmb@exp-math.uni-essen.de) | • 使 **CGVGA MODE** 解析不区分大小写，并为 16M32 模式添加了名称。<br>• **Vgatest** 更好地显示 16M32 模式的信息。<br>• Mach32—支持 Type 2 DAC 上的 8 位 **CLUT**。<br>• 添加了 **testaccel** 演示。<br>• Mach32—支持所有加速功能。<br>• 添加了 **vga_hlineint()**, **vga_blwait()**, **vga_rs_ext()**, 和 **vga_accel()**。<br>• Mach32—对愚蠢的 AST 板上的 **EEPROM** 解释更加健壮和可配置。<br>• Mach32—为兼容性将 **16M4 -> 16M32** 更改。<br>• 修复：在每次 **EACH** setmode 调用中保留一个屏幕的内存（如 **README** 所述）。<br>• Mach32—添加了对 AST 风格 **EEPROM** 校验和的支持。<br>• 添加了控制多协议鼠标的 **RTS/DTR** 线的命令。<br>• 修复：Mach32—即使是在 132 列文本模式下，VGA 模式现在也应该能正常工作。<br>• **vga.c** 中 **MAX_REGS** 的健全性检查。<br>• 修复：按实际需求提高了 **MAX_REGS**。<br>• 修复：文本模式工具现在在访问文件出现问题时给出错误。<br>• 修复：时钟探测后 Mach32 寄存器的恢复坏了（外观问题；未报告问题）。<br>• 修复：Mach32 **DAC1&4** 在 16/24bpp 下必须使用双/三时钟。<br>• 清理了一些 **VT** 代码。<br>• **ET4000/W32p** 检测的小修复。<br>• 可能的 Mach32 32bpp **copy screen** 修复。<br>• 允许带鼠标支持的 **VT** 切换（因为它与旧版本选择功能的交互而被禁用，我想现在情况好多了？）。<br>• Cirrus 5434 的初步支持（未测试，目前仅支持 1,280x1,024x256）。将很快修复。<br>• 新的 **Oak** 驱动程序 (Christopher Wiles)。<br>• 使用 **seteuid** 代替 **setuid** 来放弃 **setuid-root** 权限。<br>• 可能修复 **ET4000** 上 132 列文本模式/VGA 问题的 Hack。<br>• 修复了颜色/单色配置选项（单色坏了）。<br>• 禁用了 **ET4000** 的 320x200x56 页面翻转。<br>• 修复了 Cirrus **fillbt** 寄存器损坏问题。<br>• **GVGA6400** 驱动程序 (Arno Schafer)。<br>• **Vga_init()** 现在如果在适当的控制台上返回 -1（否则为 0）；硬退出只能在 **vga_setmode()** 中发生 (David Liu)。这应该有助于具有多个输出设备的程序，如 **gnuplot**。<br>• 添加了 **mouse_init_return_fd** 和 **keyboard_init_return_fd** 以供 **select()** 使用。<br>• 在原始键盘接口中添加了 **SIGKILL** 捕获。<br>• 可能修复了 PS/2 鼠标支持。<br>• 共享库 **1.2.0** (对应主 **SVGAlib** 版本号)。<br>• 将控制台检查延迟到实际设置模式时（应修复 **gnuplot** 等设备探测程序的问题）。<br>• 修复了 Trident 和其他厂商的平面模式 **getmode** bug（应修复 **zgv** 中的浮点异常）。<br>• 在配置文件中支持 PS/2 鼠标。<br>• 修复了一字节/像素 **gl_putxoremask**。<br>• 共享库 **1.1.8**。 |

