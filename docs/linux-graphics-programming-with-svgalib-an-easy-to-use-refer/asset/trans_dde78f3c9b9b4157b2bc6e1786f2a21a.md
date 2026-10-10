

## 控制虚拟控制台切换

以下函数涉及控制虚拟控制台（VC）切换：

### void vga_lockvc(void)

出于安全考虑，禁用虚拟控制台切换。建议在进行寄存器 I/O 或底层设备处理时使用。鼠标功能会用到此操作。与后台运行功能结合使用时也非常有用。

### void vga_unlockvc(void)

重新启用虚拟控制台切换。

### vga_oktowrite(void)

指示当前活动的程序是否正在屏幕上当前可见的控制台中运行。也就是说，它检查是否可以安全地写入显存（假设已允许上述函数中的后台运行）。请注意，这并不完全安全，因为虚拟控制台切换中断可能会在视频操作期间发生。因此，最好避免使用此函数。

通常，当您的程序没有屏幕访问权限时，它会被挂起，但请参阅 `vga_runinbackground()` 了解替代方案。

### void vga_runinbackground(int stat)

启用/禁用图形程序的后台运行。如果 `stat = 1`，则启用后台运行；如果 `stat = 0`，则禁用。通常，当程序不在当前虚拟控制台时会被挂起。只有当程序在此期间没有视频访问权限时，才可以在后台安全运行。

从版本 1.2.11 开始，Pekka T. Ala-riikka 和 Michael Friman 对此进行了修改，使得必须在您的 Makefile.cfg 中启用对此的支持（默认情况下已启用）。内部可能存在多种支持此函数的方式。目前，仅有一种使用 proc-fs 的方式有效。通过使用带有函数指针 `void goto(void)` 和 `void comefrom(void)` 的 `vga_runinbackground(VGA_GOTOBACK, void (*goto)())` 和 `vga_runinbackground(VGA_COMEFROMBACK, void (*comefrom)())`，您可以设置该函数，以便在程序进入后台模式以及返回前台时调用这些函数。这些可以随时更改，传递 NULL 作为函数将禁用此功能。

这两个新功能都需要 `vga_runinbackground_version()` 返回 1 或更高版本。如果正在使用的 SVGAlib 返回 0，则不应调用此函数。此外，在编写应用程序时，可以通过此方式进行检查：

```c
#define VGA_GOTOBACK
/* code using vga_runinbackground(VGA_GOTOBACK, goto) */
#else
/* code using no goto or comefrom function */
#endif
```

如果您使用支持此功能的 SVGA*lib 进行编译，请尝试重新排列您的源代码，以便在版本早于 1.2.11 的 SVGA*lib 中也能工作。应在调用 `vga_init()` 后立即调用此函数。`bg_test` 演示展示了其基本操作原理。

请注意，后台功能仍处于*非常早期的阶段*。不要期望在您的程序中启用后台功能时*所有*功能都能完美运行。以下是一个示例：

```c
vga_init();
vga_setmode(G32x200x256);
if (vga_runinbackground_version() >= 1)
{
vga_runinbackground(1);
}
```

请参阅手册页以获取更多信息。

### int vga_runinbackground_version(void)

此函数返回当前后台支持的版本。如果 SVGA*lib 在没有后台支持的情况下编译，则返回 0。关于后台支持的更多信息，请参阅 `vga_runinbackground()`。

## 调试辅助工具

这些函数是基本的调试辅助工具：

### int vga_dumpregs(void)

此函数以可以复制到源文件中的方式转储当前所有 VGA 寄存器的值。这仅用于调试目的。

### void vga_gettextfont(void *font)
### void vga_puttextfont(void *font)

这些函数提供了访问 SVGA*lib 保存内核所用字体的缓冲区的能力。`restorefont()`、`savetextmode()` 和 `textmode()` 工具使用这些功能来恢复可能已损坏的控制台字体。

字体缓冲区占用 8,192 字节。然而，版本 1.2.13 及更高版本内部使用了更大的缓冲区，并且传递给 `vga_gettextfont()` 和 `vga_puttextfont()` 的缓冲区大小可以通过 `vga_ext_set()` 设置。

这两个函数提供的是 SVGA*lib 内部缓冲区的访问权限，而不是 VGA 卡上的字体表。这意味着，在进入图形模式时必须调用这两个函数，并且新设置的字体仅在下次调用 `vga_setmode(TEXT)` 时生效。

> 请勿将文本模式字体（这些函数所涉及的字体）与第 7 章中讨论的图形字体混淆。

### void vga_gettextmoderegs(void *state)
### void vga_settextmoderegs(void *state)

这些函数提供了访问 SVGAlib 保存 VGA 状态的缓冲区的能力，该状态在内核于 SVGA 控制台上显示文本时使用。`restoretextmode()`、`savetextmode()` 和 `textmode()` 工具使用这些功能来恢复可能已损坏的控制台。该缓冲区当前占用 385 字节。允许将其显著扩大以容纳未来的增强功能并不会造成任何危害。

### int vga_flip(void)

此函数在不破坏屏幕内容的情况下在图形模式和文本模式之间切换。这使得您的应用程序可以同时使用文本和图形输出。然而，这是一个旧的 vgalib 函数。您应该仅出于调试目的使用它，因为它极不稳定。这是因为 SVGAlib 现在执行其自身的虚拟控制台管理。如果您想执行类似的操作，请执行以下步骤：

- 1. 使用普通的内存复制操作将当前屏幕内容复制到帧缓冲区或 `gl_getbox()`。
- 2. 设置 `vga_setmode(TEXT)`。
- 3. 调用 `vga_setmode()` 返回图形操作，并使用内存或 `gl_putbox()` 恢复屏幕内容。

您也可以使用 `vga_drawscansegment()` 和 `vga_getcsscansegment()` 调用。但是，避免在您的应用程序中调用 `vga_flip()`。

此函数应始终返回 0，但最好不要依赖这一点。如果您正在调试您的 SVGAlib 应用程序之一，它可能会很有用。如果您的程序在图形模式下到达断点，您可以使用 gdb 命令 `print vga_flip()` 切换到文本模式，并使用相同命令稍后恢复图形屏幕内容。在 gdb 中定义以下别名很有用：

```
define flip <Return> print vga_flip() <Return> end <Return>
```

### int vga_setflipchar(int c)

此函数设置导致 `vga_getch()` 在等待按键时切换图形模式和文本模式的按键的 ASCII 码。启动时默认为 Esc。由于现在可以直接在控制台之间切换（即使在图形模式下），并且由于不建议使用 `vga_flip()`（除调试外），此函数仅为了与 vgalib 兼容而存在，但没有实际效果。

### int vga_addtiming(int pixelClock, int HSyncStart, int HSyncEnd, int HTotal, int VDisplay, int VSyncStart, int VSyncEnd, int VTotal, int flags)

此函数根据给定值更改当前定时参数的值。不会检查新的定时值是否在显示器或卡规范范围内。请参阅 *sviduntune()* 查看使用此功能的示例。

## 附录 C

### Libvgagl 函数

本附录中包含的内容在很大程度上取材于由 Michael Weller 博士（eowmob@exp-math.uni-essen.de）编辑的手册页。不幸的是，随着时间推移，原始文档的确切来源已经丢失。可能至少有一些功劳应归于 Harm Hanemaayer，他最后已知的电子邮件地址是 H.Hanemaayer@inter.nl.net，但据信 Hanemaayer 现在已经离线，因此无法接受询问。

因此，一些较新的 SVGAlib 手册页和 HOWTO 是由 Matan Ziv-Av（matan@svgalib.org）及其同时代人编写的。如果功劳被错误地归属，请通过电子邮件通知 jlink@svgalib.org。

### 在 Vgagl.h 中定义的函数

本附录中显示的 libvgagl 函数定义在 vgagl.h 中。通常可以在 /usr/include 或 /usr/local/include 目录中找到此头文件。此外，独立的 threeDKit 函数需要单独的头文件（例如，triangle.h），这些文件保存在 SVGAlib 的 threeDKit 源子目录中。

### 上下文管理

以下函数涉及上下文管理。

