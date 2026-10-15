

+   1. 从 Basilisk II 主页 http://www.uni-mainz.de/~bauec002/B2Main.html 下载最新的 Basilisk II for Linux RPM 安装文件。文件名应为 BasiliskII-0.8-1.1386.rpm 格式，尽管版本号可能不同。

> 下一步可能需要你先使用 su 命令获取 root 级别访问权限。

+   2. 使用命令 rpm -install BasiliskII-0.8-1.1386.rpm 安装 Basilisk II，如有需要请替换为正确的版本号。

> RPM 将主可执行文件放置在 /usr/bin，文档文件放置在 /usr/doc/BasiliskII-0.8，共享设备文件放置在 /usr/share/BasiliskII。

+   3. 创建一个新目录用于存放 Basilisk II 相关文件。你可以选择将其放在共享位置，或放在你的主目录的子目录下，例如 /home/jcompton/mac。

+   4. 将你的 Macintosh ROM 映像（请参阅本章前面“Making Sense of Legalities”一节了解详情）放置在你的新 Basilisk II 存储目录中。取一个易于记住的名称，例如 ROM 或 basilisk.rom。

## Installing Basilisk II for Windows

Basilisk II 应该与运行 Windows 95 OSR2 或更高版本的任何 VMware 虚拟机兼容，尽管它更偏好（并且在 NT 4 和 2000 下更稳定）：

+   1. 启动你的 VMware 虚拟机。

+   2. 从 Basilisk II for Windows 主页 http://www.nic.fi/~jpesonen/BasiliskII 下载最新的 Windows 版本 Basilisk II。（注意，你也可以从主 Basilisk II 页面链接到此页面。）文件名应为 BasiliskII_win32_18062000.zip 形式，可能带有不同的日期代码。

the NT4/2000 version.) Users of Win 95 or Win 98 do not have to do anything special.

+   5. 如果你希望 Mac 仿真能够访问你的 CD-ROM 驱动器（并且你应该这样做），你需要将驱动程序复制到你的 CD-ROM 驱动器（并且你应该这样做），你需要将驱动程序复制到 Windows 系统目录。95/98 用户将在 CD-ROM drivers/9x 目录中找到其驱动程序 cdenable.vxd，并应将该文件复制到 C:\Windows\System。 对于 NT 4/2000 VM，请将 CD-ROM drivers/NT4 和 Win2k 中的文件 cdenable.sys 复制到 C:\WinNT\System32\drivers。

+   6. 将 Macintosh ROM 文件（请参阅本章前面“Making Sense of Legalities”一节了解详情）复制到与主 BasiliskII.exe 文件相同的目录中。取一个合理的名称，例如 ROM 或 basilisk.rom。

## Configuring Basilisk II

尽管 Basilisk II 的 Linux 和 Windows 版本在功能上几乎等效，但它们的配置界面却大不相同。Windows 版本有一个全面的（但有点令人望而生畏的）GUI 配置程序，而 Linux 版本有一个使用起来更容易但功能更少的 GUI 配置窗口。

> Basilisk II 在技术上能够与你的 PC 共享以太网连接。但共享驱动程序在 VMware 中似乎无法正常工作，并且 Linux 版本需要使用 Basilisk II 源代码或 Linux etherapt 系统，两者都是高级配置选项，除非你绝对确定需要它们，否则最好不要碰。有关详情请参阅 Basilisk II 文档。

![](img/b2b6702758c230ce537468351fc8af15_355_0.png)

### Configuring Basilisk II for Linux

值得庆幸的是，最近的 Basilisk II 版本已添加了一个 GUI 配置界面作为其基于文本的配置文件的前端。

+   1. 在命令提示符下输入 BasiliskII 启动仿真器。GUI 配置窗口应出现，如图 17.9 所示。

+   2. 你应该从第一个标签页 Volumes 开始。你需要创建一个硬盘文件（类似于 VMware 虚拟磁盘，只是它立即占用所有请求的空间）。点击 Create 按钮，并在你的 Basilisk II 文件目录中创建一个硬盘文件。使用简单的名称，例如 macdisk.HFV。（HFV 是 Mac 硬盘文件的常见扩展名。）磁盘的大小由你决定，但我建议至少 100MB。

![](img/b2b6702758c230ce537468351fc8af15_356_0.png)

Figure 17.9

3. 设置程序应自动将你的硬盘文件添加到 Volumes 列表中。列表下方有一个 Unix Root 条目。Basilisk II 将把你的 Linux 文件系统挂载为 Mac 仿真中的驱动器，但你可以指定初始挂载点的位置。你可能会选择 /（使整个文件系统对仿真器可见）或你的主目录，如 /home/jcompton。

4. 在正常情况下，保持 Boot From 选项不变。但如果你需要重新安装 MacOS，或希望强制仿真从某个 CD 启动，你可能需要将其更改为 CD-ROM。

5. 你永远不需要禁用 CD-ROM，除非某个程序对 CD-ROM 可见性特别挑剔，或者你计划频繁更换非 Macintosh 用途的 CD，并且不希望仿真 MacOS 发出抱怨。

6. SCSI 标签页只有在你想将真正的 Macintosh SCSI 驱动器连接到你的 Linux SCSI 控制器时才重要，如果你有的话。如果你有，可以将 Macintosh 仿真的 SCSI 控制器指向已连接的 Macintosh 驱动器，它们应位于 /dev/sg0（或不同的单元号）。

> 尽管 Windows 版本也可以直接访问 SCSI 控制器，但在 VMware 内部使用此功能没有好处，因此就本书而言，此功能仅与 Linux 版本相关。

7. Graphics/Sound 标签页，如图 17.10 所示，可让你选择 MacOS 窗口的大小。（如果你的显示器足够大，800x600 或 1024x768 是不错的选择。）默认情况下，Basilisk II 以窗口模式加载，但某些 X 安装可能允许你使用全屏模式。如有疑问，请使用 Window 模式。

