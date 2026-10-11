
13. 现在，使用以下命令开始编译内核，以生成所有依赖项（即之前保留选择的所有模块）：

    ```bash
    make dep
    ```

14. 当此过程完成并在屏幕上输出大量信息后，使用以下命令清理之前编译会话留下的残留物：

    ```bash
    make clean
    ```

15. 这通常需要几分钟时间；然后该进行内核的实际编译了：

    ```bash
    make bzImage
    ```

编译内核时可以选用以下四种选项：

- `lilo`—不仅用于生成镜像，还用于将其安装为 LILO 菜单中的默认条目。此内核未压缩。
- `zlilo`—与 `lilo` 类似，但使用压缩技术。
- `zImage`—使用 gzip 压缩选项生成压缩内核。
- `bzImage`—使用 bzip2 压缩选项生成压缩内核。

请记住，内核通常使用 gzip 进行压缩，例如 `make zImage` 命令。从英语语义上看，`make bzImage` 使用 bzip2 压缩内核似乎更合理，但事实是 `bzImage` 生成的压缩内核体积比 `zImage` 更大。

16. 制作此内核所需的模块；这可能需要几分钟，在较慢的机器上可能需要数小时：

    ```bash
    make modules
    ```

模块的构建和安装是冗长的内核编译过程中最容易被遗漏的两个步骤。请列出一个步骤清单，以便你能够记住它们。

17. 模块编译完成后，使用以下命令安装新模块：

    ```bash
    make modules_install
    ```

此命令会覆盖当前的模块，尽管我们没有做任何可能导致问题的更改。执行此操作时要小心，切勿在生产机器上进行此操作。

18. 安装完成后，将新的压缩内核安装到引导加载程序中。使用以下命令将压缩镜像复制到 `/boot` 目录：

    ```bash
    cp /usr/src/linux-2.4-lpic/arch/i386/bzImage /boot
    ```

19. 现在，使用以下命令将 `bzImage` 内核文件移动到新名称：

    ```bash
    mv /boot/bzImage /boot/vmlinuz-2.4.18-lpic
    ```

如果你使用的是除编译新内核外的同一系统，则不需要更新 `System.map` 文件。如果需要更新，花些高质量的时间阅读 man 手册页面并搜索 Google 是恰当的，因为这比我们能在此涵盖的内容更复杂。

20. 如果你使用的是 LILO，你需要编辑 `/etc/lilo.conf` 文件并将现有的 Linux 镜像复制到新条目。

21. 要启用新条目，只需将 `image=kernelName` 部分后的文件名更改为新的文件名即可。

22. 保存并退出 `/etc/lilo.conf` 文件。

23. 重新运行带有详细选项的 `lilo` 命令，以查看正在执行的操作：

    ```bash
    lilo -v
    ```

这将返回类似于以下所示的输出：

    ```text
    Reading boot sector from /dev/sda
    Merging with /boot/boot.b
    Mapping message file /boot/message
    Boot image: /boot/vmlinuz-2.4.18-3
    Mapping RAM disk /boot/initrd-2.4.18-3.img
    Added linux *
    /boot/boot.0000 exists - no backup copy made.
    Writing boot sector.
    ```

24. 重启并测试新内核的功能，确保手边备有你的 vi 速查表，以便在排查配置文件中出现的任何错误时参考。

请记住，可以使用 `dmesg` 命令或 `less` `/var/log/dmesg` 命令查看内核和系统初始化消息。`/var/log/boot.log` 日志文件几乎完全由服务启动消息组成，而不是与内核相关的消息。

25. 如果新内核不起作用，请再次检查步骤，确保没有拼写错误。

![img](img/49f4f38f3aec011238fa50f89e643db3_399_0.png)

务必弄清楚编译新内核时使用了哪些步骤，哪些没有。请记住，在本次会话中你使用了 **dep**、**clean** 和 **bzImage**（zlilo, bzli0, 和 **zImage**）模块以及 **modules_install**。

## 备考题

1. 你需要将一个名为 module1.o 的模块加载到正在运行的内核中。当你发出以下命令时，该模块未能正确加载：
    `insmod module1`
    你会使用哪个命令来加载模块 module1.o 及其依赖项？在下面的空白处仅填写命令名称：

    `______________________`

    正确答案是 modprobe。没有其他替代答案。

2. 哪个命令可以卸载单个未被引用的内核模块？
    （选择最简单的答案。）
    - A. modprobe
    - B. rmmod
    - C. rmautoclean
    - D. moduload

    答案 B 是正确的，因为 rmmod 是卸载该模块的最简单命令。答案 A 是错误的，因为 modprobe 用于卸载模块组，尽管它也可以卸载单个模块。答案 C 是错误的，因为不存在 rmauto-clean 这样的命令。答案 D 是错误的，因为不存在 moduload 这样的命令。

3. 包含编译内核所有选项的文件名是什么？在下面的空白处仅填写文件名：

    `______________________`

    正确答案是 .config。没有其他替代答案。

4. 以下哪个命令可用于生成编译后的内核？（选择所有适用的选项。）
    - A. make bzImage
    - B. make lilo
    - C. make zImage
    - D. make gzlilo
    - E. make zlilo

    答案 A、C 和 E 是正确的，因为它们都是生成压缩内核的有效目标。答案 B 和 D 是错误的，因为它们不是生成编译内核的有效目标。

5. 在编译新内核并在引导管理器中配置后，你重启并收到多条 `module not found`（模块未找到）的消息。问题最可能的原因是什么？
    - A. 你忘记制作模块了。
    - B. 你没有运行 `lilo`。
    - C. 你没有复制压缩镜像。
    - D. 你忘记重命名内核镜像了。

    答案 A 是正确的，因为忘记制作模块是此错误的常见原因。答案 B 是错误的，因为没有运行 `lilo` 会导致你*没有*收到这些错误消息。答案 C 是错误的，因为没有复制压缩内核镜像不会导致模块错误。答案 D 是错误的，因为在运行时 `lilo` 会抱怨缺少内核镜像。

6. 你需要创建一个比传统的 `zImage` 选项所能处理体积更大的压缩内核。在下面的空白处填写生成此内核的命令行，包括任何必要的选项或参数：

    `______________________`

    正确答案是 `make bzImage`。没有其他替代答案。

7. 你需要确定内核版本，并在脚本文件中使用该版本。哪条命令行可以完成以下命令？

    `cd /lib/modules/`

    在空白处填写正确的字符串，使命令能够读取正确的目录并转到该目录：

    `cd /lib/modules/`

    正确答案是 `uname -r`。没有其他替代答案。

8. 以下哪个命令读取 `/etc/modules.conf` 文件并生成一个依赖列表，该列表存储在正确目录（针对内核版本）下的 `modules.dep` 文件中？
    - A. `conf.modules`
    - B. `modprobe`
    - C. `depmod`
    - D. `ldmodules`

    答案 C 是正确的，因为 `depmod` 读取 `/etc/modules.conf` 文件并生成一个名为 `modules.dep` 的依赖文件。答案 A 是错误的，因为 `conf.modules` 是 `modules.conf` 文件的旧名称，并且不是一个命令。答案 B 是错误的，因为 `modprobe` 用于以组的形式加载和卸载模块。答案 D 是错误的，因为它不是一个有效的命令。

