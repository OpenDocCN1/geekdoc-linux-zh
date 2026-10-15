

```
# make -j3 bzImage
```

除了 make dep 之外的所有 make 进程都可以使用这种并行编译方法正常工作。

- 8. 运行 make clean 为内核的实际编译准备源代码。
- 9. 运行 make bzImage 创建内核的二进制映像。

## NOTE

存在多种指令选择，尽管最常见的是如下几种：

zImage—此指令编译内核，生成一个名为 zImage 的未压缩文件。

bzImage—此指令创建压缩的内核映像，对于某些需要内核映像小于特定大小以便 BIOS 能够解析的系统来说是必要的；否则，新内核将无法启动。它是最常用的选择。然而，使用 bzImage 编译的 Ubuntu 内核仍然太大而无法放入软盘，因此用于启动软盘的版本会移除一些模块和功能，使用更小的版本。Ubuntu 建议您从救援 CD-ROM 启动。

bzDisk—此指令与 bzImage 做的事情相同，但它会将新的内核映像复制到软盘以供测试之用。这对于在不将内核文件写入硬盘的情况下测试新内核非常有帮助。请确保驱动器中已插入软盘，因为不会提示您插入。

- 10. 运行 make modules 编译新内核所需的任何模块。
- 11. 运行 make modules_install 将模块安装到 /lib/modules 并创建依赖文件。
- 12. 运行 make install 自动将内核复制到 /boot，创建它需要的任何其他文件，并修改引导加载程序以默认启动新内核。
- 13. 使用您喜欢的文本编辑器，验证对 /etc/lilo.conf 或 /boot/grub/grub.conf 所做的更改；如有必要进行修复并重新运行 /sbin/lilo。
- 14. 重启并测试新内核。
- 15. 如有必要重复该过程，选择配置界面。

随着时间的推移，配置 Linux 内核的过程发生了变化。最初，您通过对每个配置参数的一系列提示做出响应来配置内核（这是 make config 实用程序，稍后会描述）。虽然您仍然可以这样配置 Linux，但大多数用户发现这种类型的配置令人困惑且不方便；例如，无法返回之前的提示来纠正错误。

可用，您可以转向庞大的互联网资源来查找信息。）我们建议您避免使用 make config 实用程序，如图 32.1 所示。

![](img/8f9e74e2b343ff525bebfb720a3d8441_744_0.png)

## FIGURE 32.1 The make config utility in all its Spartan glory.

如果您更喜欢使用命令行界面，您可以使用 make menuconfig 来配置 Linux 内核。menuconfig 为文本界面提供了一个图形包装。虽然它不如 make config 原始，但 menuconfig 也不是花哨的图形界面；您不能使用鼠标，而必须使用键盘命令在其中导航。make config 中呈现的相同信息由 make menuconfig 呈现，但如您在图 32.2 中所见，它看起来更漂亮一些。现在，至少您可以在选择过程中前后移动，以防您改变主意或犯了错误。

![](img/8f9e74e2b343ff525bebfb720a3d8441_744_1.png)

## FIGURE 32.2 The make menuconfig utility, a small improvement over make config.

## Kernel and Module Management

在 make menuconfig 中，您使用方向键上下移动选择器，使用空格键切换选择。Tab 键在屏幕底部在 Select、Exit 或 Help 之间移动焦点。

如果没有可用的图形桌面，menuconfig 就是最好的选择了。然而，menuconfig 和 xconfig（见下文）都比直接编辑 .config 文件有所改进。如果您想通过真正的图形界面——带鼠标支持和可点击按钮——来配置内核，make xconfig 是最好的配置实用程序选项。要使用此实用程序，您必须运行 X Window System。应用程序 xconfig 实际上只是一个 Tcl/Tk 图形部件集，提供边框、菜单、对话框等。其界面用于在执行时解析数据文件。图 32.3 显示了 2.6.7 内核的 xconfig 主菜单。

![](img/8f9e74e2b343ff525bebfb720a3d8441_745_0.png)

FIGURE 32.3 The much nicer make xconfig GUI interface. We recommend that you use this interface if you are able.

加载此实用程序后，您可以通过单击列出配置选项的每个按钮来使用它。您单击的每个按钮都会打开另一个窗口，其中包含该子部分的详细配置选项。每个窗口底部有三个按钮：Main Menu、Next 和 Prev(ious)。单击 Main Menu 按钮会关闭当前窗口并显示主窗口。单击 Next 会带您进入下一个配置部分。从头开始配置内核时，单击标记为 Code Maturity Level Options 的按钮，然后继续在每个子部分窗口中单击 Next 按钮，直到完成所有内核配置选项。当您选择了所有选项后，主菜单会再次显示。主菜单右下角的按钮是

