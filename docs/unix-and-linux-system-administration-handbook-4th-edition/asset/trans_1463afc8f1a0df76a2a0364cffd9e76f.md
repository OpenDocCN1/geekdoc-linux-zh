

例如，命令

```
linux$ sudo sysctl net.ipv4.ip_forward=0
```

会关闭 IP 转发。 （另外，你也可以直接手动编辑 /etc/sysctl.conf。） 你通过将 /proc/sys 目录结构中的斜杠替换为点来形成 sysctl 使用的变量名。

## 构建 Linux 内核

由于 Linux 发展迅速，你最终很可能会面临需要构建 Linux 内核的需求。 内核补丁、设备驱动程序和新功能不断涌现。 这其实是一种喜忧参半的事情。 一方面，始终支持“最新最好的”很方便，但另一方面，跟上不断涌现的新材料可能会非常耗时。

如果你运行的是“稳定”版本，你自己需要构建内核的可能性就更小了。 起初，Linux 采用了一种版本号方案，其中版本号的第二部分表示内核是稳定版（偶数）还是开发版（奇数）。 例如，内核版本 2.6.6 将是一个“稳定”内核，而 2.7.4 将是一个“开发”内核。 今天，这个方案并没有严格遵守，所以你最好在 kernel.org 的主页上查看有关此问题的官方说明。 kernel.org 网站也是 Linux 内核源代码的最佳来源，如果你不依赖特定的发行版（或供应商）为你提供内核的话。

## 如果它没有坏，就不要修它

一个好的系统管理员在规划内核升级和补丁时，会仔细权衡需求和风险。 当然，新版本可能是最新最好的，但它和当前版本一样稳定吗？ 升级或补丁是否可以推迟，并在月底与其他一组补丁一起安装？ 重要的是要抵制让“赶上琼斯一家”（在这种情况下，是内核黑客社区）主导你用户社区的最佳利益的诱惑。

一个好的经验法则是，仅在你预期获得的生产力提升（通常以可靠性和性能来衡量）将超过执行安装所需的工作量和损失的时间时，才进行升级或应用补丁。 如果你很难量化具体的收益，那就是补丁可以等到另一天的良好迹象。 （当然，与安全相关的补丁应及时安装。）

## 配置内核选项

在本章中，我们使用 path_to_kernel_src 作为你为内核源代码选择的目录的占位符。 大多数发行版将内核源文件安装在 /usr/src 中。 在所有情况下，在你的系统上构建内核之前，你需要安装内核源代码包； 请参阅第 380 页，了解有关包安装的提示。

内核配置过程围绕内核源代码目录根目录下的 .config 文件展开。 所有内核配置信息都指定在此文件中，但其格式有些晦涩。 使用
path_to_kernel_src/Documentation/Configure.help
中的解码指南来了解各种选项的含义。

为了避免人们不得不直接编辑 .config 文件，Linux 有几个 make 目标，可以让你使用不同的界面来配置内核。 如果你正在运行 KDE，最漂亮的配置界面由 make xconfig 提供。 同样，如果你正在运行 GNOME，make gconfig 可能是最好的选择。 这些命令会弹出一个图形配置屏幕，你可以在其中选择要添加到内核中的设备（或编译为可加载模块）。

如果你没有运行 KDE 或 GNOME，你可以使用 make menuconfig 调用的基于终端的替代方案。 最后，较旧风格的 make config 会提示你回答每个可用的配置选项，而不允许你在改变主意后返回。 我们建议如果你的环境支持，使用 make xconfig 或 make gconfig； 否则，使用 make menuconfig。 避免 make config，这是最不灵活、最痛苦的基于文本的 make 目标。

如果你将现有的内核配置迁移到新的内核版本（或树），你可以使用 make oldconfig 目标读取之前的配置文件，并仅询问新的问题。

就你可以打开的选项而言，这些工具很简单，但不幸的是，如果你想为多个架构或硬件配置维护多个版本的内核，使用起来很痛苦。

上面描述的各种配置界面都会生成一个看起来像这样的 .config 文件：

```
# Automatically generated make config: don't edit
# Code maturity level options
CONFIG_EXPERIMENTAL=y

# Processor type and features

# CONFIG_M386 is not set
# CONFIG_M486 is not set
# CONFIG_M586 is not set
# CONFIG_M586TSC is not set
CONFIG_M586=y
CONFIG_X86_WP_WORKS_OK=y
CONFIG_X86_INVLPG=y
CONFIG_X86_BSWAP=y
CONFIG_X86_POPAD_OK=y
CONFIG_X86_TSC=y
CONFIG_X86_GOOD_APIC=y
...
```
