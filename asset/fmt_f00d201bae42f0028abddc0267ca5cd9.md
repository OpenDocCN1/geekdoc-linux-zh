
# 第 20 章：虚拟机和终端服务器

32. 当出现以下消息时，将虚拟机的目录设置为你主目录的子目录，或者设置为专用分区上的目录，可能会有所帮助。显然，你也可以接受默认值。

    你想将虚拟机文件保存在哪个目录中？[`/var/lib/vmware/Virtual Machines`]

33. 当你看到序列号提示时，输入 `yes`，并输入之前提到的注册序列号。

    现在要输入序列号吗？`(yes/no/help) [no] yes`

    请输入你的 20 位字符序列号。

    ```
    输入 XXXXX-XXXX-XXXX-XXXX 或按 'Enter' 取消：
    ```

34. 系统提示你继续安装过程，其中包含若干步骤支持虚拟机脚本的 VMware VIX API。接受默认设置。

35. 检查以下消息，这表示 VMware 正在运行：

    ```
    正在启动 VMware:
    虚拟机监视器完成
    虚拟机通信接口完成
    桥接网络在 /dev/vmnet0 完成
    仅主机网络在 /dev/vmnet1 (后台) 完成
    DHCP 服务器在 /dev/vmnet1 完成
    仅主机网络在 /dev/vmnet8 (后台) 完成
    DHCP 服务器在 /dev/vmnet8 完成
    NAT 服务完成
    正在启动 VMware 管理服务:
    VMware Server Host Agent (后台) 完成
    VMware Virtual Infrastructure Web Access
    正在启动 VMware 自动启动虚拟机:
    虚拟机完成
    ```

    适用于此运行内核的 Linux VMware Server 2.0.0 build-110949 配置已成功完成。

    如果在脚本运行时遇到问题，请按 CTRL-C。虽然这会停止脚本，但它允许你修复诸如缺少包等问题。你可以重新运行脚本。

    旧版本的 VMware Server 2.0 测试版本需要使用 root 管理员账户。现在不再需要了。

    要打开 VMware Server，请在 GUI 中打开一个命令行。运行 `vm` 命令。它将打开默认浏览器。如果你之前没有添加本地安全证书，将看到错误页面（图 20-1）。（Mozilla Firefox 以外的浏览器显示会有所不同。）

1. 假设错误页面出现在 Firefox 浏览器中（如图 20-1 所示），点击“你可以添加异常”(You Can Add An Exception）链接。

2. 在浏览器中出现的附加信息中，点击“添加异常”(Add Exception)。

3. 在弹出的“添加安全异常”窗口中，你应该在位置框中看到 `https://127.0.0.1:8333/`。如果是，点击“获取证书”(Get Certificate)。

4. 当“确认安全异常”(Confirm Security Exception）选项激活时，点击它。

5. 你将看到 VMware Infrastructure Web Access 界面；输入与安装过程中配置的管理员用户相关的凭据。你现在应该访问 VMware Server 2.0 了，如图 20-2 所示。

你现在应该可以使用所示的 GUI 选项创建虚拟机。暂时保持 Web Access 界面打开。

![](img/28cf881509dedde88f9e34e8cefb7020_526_0.png)

**图 20-1.** VMware 需要一个本地安全证书。

## 配置数据存储 (Datastore)

虚拟机硬盘是在文件中配置的。由于这些文件用于模拟硬盘，因此它们很大。因此，你为数据存储配置的卷应该有数 GB 的空闲空间。要配置数据存储，请采取以下步骤：

- 在 Web Access 界面的右侧命令面板中，点击“添加数据存储”(Add Datastore)。

- 在弹出的“添加数据存储”窗口中，为名称（Name）框指定一个任意描述性名称；为了本章，输入 `UbuntuVM`。

- 在路径（Directory Path）框中，指定位于具有大量空闲空间的分区或卷上的目录。你甚至可以看到通过 NFS 共享的远程系统目录。

- 点击“确定”(OK)。

- 检查数据存储。

## 配置虚拟机

### Ubuntu 服务器管理

为了本次练习，我给出了几项建议。配置一个 2GB 的系统，即之前配置的 `UbuntuVMs` 数据存储。将磁盘分为 2GB 的文件，这可以帮助你组织虚拟机。保留默认的持久性（Persistent）磁盘模式，并在第一个可用的虚拟 SCSI 模式上设置设备。对于写入缓存，选择“为安全优化”（Optimize For Safety）。这些是备选择，通常效果同样良好。做出所需的选择并点击“下一步”（Next）继续。

9. 除非主机系统没有网络（或你不想在虚拟机上添加网络），否则点击添加网络适配器（Add A Network Adapter）。

10. 你应该看到以下问题：虚拟机将访问哪个网络？通常情况下，你应该保留默认设置：使用桥接网络（Use Bridged Networking）和开机时连接（Connect At Power On）。做出适当的选择并点击“下一步”继续。

11. 你现在应该看到与 CD/DVD 驱动器相关的问题，三个选项：

    - 使用物理驱动器（Use A Physical Drive）：适用于从主机系统的物理 CD/DVD 进行安装

    - 使用 ISO 镜像（Use An ISO Image）：如果你刚刚下载了 Linux 安装磁盘镜像（通常为 ISO 格式），这是最好的

    - 不添加 CD/DVD 驱动器（Don't Add A CD/DVD Drive）：由于 VMware 网卡支持网络启动，可用于网络安装

    如果你已经下载了 Ubuntu JeOS CD 的 ISO 镜像（像我一样），请选择“使用 ISO 镜像”选项。

12. 你将自动跳转到 ISO 文件的属性页。在此页面，有“镜像文件”（Image File）以及是否“开机时连接”（Connect At Power On）的选项。镜像文件与相对于配置存储的 ISO 文件位置相关。你可以点击“浏览”（Browse）搜索下载（或复制）到数据存储的 ISO 文件。例如，如果我配置了 `UbuntuVMs` 数据存储，我将 Ubuntu JeOS 文件保存到了相应的目录，那么 Hardy Heron 版本的镜像文件框中的条目将是：

    ```
    [UbuntuVMs]/jeos-8.04-jeos-i386.iso
    ```

    输入数据存储，系统会提示你所需的 ISO 文件，然后点击“下一步”继续。

13. 在下一步中，系统会询问是否需要与 1.44MB 磁盘关联的软驱。为了本次练习，请选择“不添加软驱器”（Don't Add A Floppy Drive）。如果需要，以后可以添加。

14. 在接下来的步骤中，你有机会添加 USB 控制器。这将允许访问主机物理 USB 控制器。为了本次练习，选择“不添加 USB 控制器”（Don't Add A USB Controller）。如果需要，以后可以添加。

15. 最后出现“准备完成”（Ready To Complete）窗口，如图 20-5 所示。它显示了目前为止配置的虚拟硬件。窗口的“更多硬件”（More Hardware）部分包含可以配置的其他硬件组件。图中未显示串口、并行口和声音适配器等选项。

    如果你准备好了，勾选“现在启动虚拟机”（Power On Your Virtual Machine now）复框，并点击“完成”（Finish）继续。

16. 点击“虚拟机”（Virtual Machines）标签页。在某些情况下，你可能需要在新虚拟机出现之前点击“注销”（Log Out）并重新登录。

17. 你将在浏览器左侧的清单（Inventory）面板看到配置好的虚拟机。高亮“控制台”（Console）标签并点击出现的它。

    ![](img/28cf881509dedde88f9e34e8cefb7020_531_0.png)

    以下子步骤只需运行一次：

    - a. 如果你看到“VMware 远程控制台插件未安装”的消息，点击出现的“安装插件”（Install Plug-in）链接。通常，Firefox 会禁用弹窗；如果是这样，点击浏览器右上角的“允许”（Allow）按钮。

    - b. 在弹出的软件安装窗口中，点击“安装 VMware 远程控制台”（Install VMware Remote Console）。

    - c. 在弹出的软件安装窗口中...
