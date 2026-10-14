
# 附录 B：使用 VMware 测试 Linux

## 安装 VMware Server

1. 下载 tarball。在本例中，我将名为 `VMware-server-1.0.5-80187.tar.gz` 的文件下载到 `/tmp` 目录。我也将“any”补丁下载到了同一个目录。

2. 虽然书中其他地方没有介绍，但从具有 `.tar.gz` 或 `.tgz` 扩展名的 tarball 中解包的方法是使用 `tar xzv` 命令，它从随后的文件名（`f`）提取（`x`）、解压缩（`z`），并在发生 evfs 的情况下详尽显示（`v`）：

   ```
   $ tar xzvf /tmp/VMware-server-1.0.5-80187.tar.gz
   $ tar xzvf /tmp/vmware-any-any-update117.tgz
   ```

3. 导航到包含 VMware Server 文件的目录。否则 VMware 安装脚本将报错。

   ```
   $ cd vmware-server-distrib
   ```

4. 运行 `vmware-install.pl` 脚本。脚本前面的 `./` 指定当前目录：

   ```
   $ sudo ./vmware-install.pl
   ```

5. 除非你真的知道自己在做什么，否则按 `ENTER` 接受将二进制文件安装在 `/usr/bin` 目录的默认设置。

   ```
   使用 tar3 格式创建新的安装数据库。
   正在安装软件包。
   你想在哪个目录下安装二进制文件 [/usr/bin]
   ```

6. 除非你真的知道自己在做什么，接受在 `/etc/rc.d/` 目录下设置 vmware 配置脚本的默认设置，其中 `x` 在 0 和 6 之间。按 `ENTER` 执行。

   ```
   包含 init 目录（rc0.d/ 到 rc6.d/）的目录是什么 [/etc]
   ```

7. 除非你真的知道自己在做什么，接受在 `/etc/init.d/` 目录下设置 vmware 服务脚本的默认设置。按 `ENTER` 执行。

   ```
   包含 init 脚本的目录是什么 [/etc/init.d]
   ```

8. 除非你真的知道自己在做什么，接受在 `/usr/bin/` 目录下设置 vmware 守护进程文件的默认设置。按 `ENTER` 执行。

   ```
   你想在哪个目录下安装守护进程文件 [/usr/sbin]
   ```

9. 除非你真的知道自己在做什么，接受在 `/usr/lib/vmware/` 目录下设置 vmware 库文件的默认设置。按 `ENTER` 执行。

   ```
   你想在哪个目录下安装库文件 [/usr/lib/vmware]
   ```

   如果目录已存在，你将被提示允许安装脚本创建该目录。

10. 除非你真的知道自己在做什么，接受在 `/usr/share/man/` 目录下设置 vmware 手册文件的默认设置。按 `ENTER` 执行。

    ```
    你想在哪个目录下安装手册文件 [/usr/share/man]
    ```

    如果目录已存在，你将被提示允许安装脚本创建该目录。

11. 除非你真的知道自己在做什么，接受在 `/usr/share/doc/vmware/` 目录下设置 vmware 文档文件的默认设置。按 `ENTER` 执行。

    ```
    你想在哪个目录下安装文档文件 [/usr/share/doc/vmware]
    ```

    如果目录已存在，你将被提示允许安装脚本创建该目录。

> 注：后续文本由于包含大量重复的 OCR 错误，此处已根据要求提取了核心内容并翻译。

## 继续安装与故障排除

20. 如果不存在适当的 VMware 模块，请接受以下提议以进行构建。如果已安装了来自 `gcc` 软件包的适当 GCC 编译器，它将可以工作：

    ```
    适用于 VMware Server 的所有预编译 vmmon 模块都不适用于你正在运行的内核。你是否希望此程序尝试为你的系统构建 vmmon 模块（你是否在系统中安装了 C 语言编译器？）[yes]
    ```

21. 下一条消息将查找 C 语言头文件（header files）：

    ```
    匹配你正在运行的内核的 C 头文件目录的位置何处？
    [/lib/modules/2.6.24-16-generic/build/include]
    ```

    这引用了 Ubuntu Hardy Heron 系统中这些文件的标准位置。如果你没有看到这些具体路径，可能没有安装 `linux-headers-uname -r` 软件包。

    注意版本号不匹配的情况。如果你使用的内核代码与系统上运行的内核版本不同，安装可能无法运行。如果引用了正确的版本，按回车键继续。

    如果一切顺利，最终会显示以下消息：

    ```
    模块在运行的内核中完美加载。
    ```

22. 随着安装的进行，你应该接受网络、网络桥接以及某些设置的默认值。在脚本配置有私有网络（privatenets）时，某些步骤可能会“卡住”一两分钟。

23. 虽然远程连接 VMware Server 的默认端口为 902，但它可能已被占用。如果是这样，安装脚本会提供替代方案。如果你只是在本地使用 VMware Server，端口号并不重要。相关消息如下：

    ```
    请为远程控制台连接指定一个端口 [902]
    ```

24. 当出现以下消息时，将虚拟机目录更改为你的家目录下的子目录可能会有所帮助：

    ```
    你想将虚拟机文件保存在哪个目录？
    [/var/lib/vmware/Virtual Machines]
    ```

25. 当你看到序列号提示时，输入之前在“获取 VMware Server”章节中描述的注册代码。查看以下消息，内容为 VMware 正在使用：

    ```
    Starting VMware services:
    Virtual machine monitor      done
    Virtual ethernet             done
    Bridged networking on /dev/vmnet0 (background) done
    Host-only networking on /dev/vmnet1 (background) done
    NAT service on /dev/vmnet8               done
    ```

    针对此运行内核的 Linux VMware Server 1.0.5 build-80187 配置成功。

    如果在脚本运行期间遇到问题，请按 `CTRL-C`。虽然这会停止脚本，但它允许你修复缺失包等问题。你可以重新运行脚本。

    此外，你可能需要安装 `gcc-3.4` 和 `gcc-4.2` 软件包。如果你看到类似的错误消息：

    ```
    /usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/
    libgcc_s.so.1: version `GCC_3.4' not found
    ```

    你可能需要移除注的库文件，以便 VMware 使用为 Ubuntu Linux 提供的并编译的版本。使用以下命令将文件移动到你的家目录：

    ```
    $ sudo mv /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1 ~
    ```

    如果发生错误，你可以随后将文件恢复到注记的位置。但如果一切顺利，从基于 GUI 的控制台运行 VMware 命令将正常启动 VMware Server。

## 为 Linux 安装准备 VMware

在本节中，我假设你已经下载并刻录了所选发行版之一的安装 CD/DVD。由于在 Microsoft 系统上（在我看来对于任何考虑参加 UCP 考试的人来说）刻录安装 CD/DVD 文件也是可能的，我将在此不再解释该过程。

在 GUI 中启动 VMware。在 Linux 中，一种标准方法是在 GUI 内部的命令行控制台中运行 `vm` 命令。当“连接到主机”（Connect To Host）窗口出现时，点击“连接”进入 VMware Server 控制台，如图所示：

![](img/8521db60567337b3b9ca1b288c5d36b6_498_0.png)

1. 为了准备 Linux 安装，点击“新建虚拟机”（Create A New Virtual Machine）。这将启动“新建虚拟机向导”。点击“下一步”，选择“自定义配置”（Custom configuration），然后点击“下一步”查看所示的操作系统选项。（如果选择了“典型”（Typical）配置，步骤会有不同。）

   ![](img/8521db60567337b3b9ca1b288c5d36b6_499_0.png)

2. 选择 Linux。点击“版本”（Version）下拉文本框箭头，查看 VMware Server 可以处理的各种 Linux 发行版。选择你计划安装的发行版，或至少是其可用版本。做出选择并点击“下一步”。
