

## 手动配置 XFree86

如果您没有硬件 HOWTO 文档，或者您的显卡不在列表中且不想使用通用驱动程序，则必须手动配置 XFree86。即使您使用 `ConfigXFree` 或 `xf86config` 脚本来安装 XFree86，您可能仍需要进行手动修改来调整您的安装设置。

XFree86 2.X 版本的大多数配置细节包含在一个名为 `Xconfig` 的文件中，而 XFree86 3.X 版本则根据具体版本使用名为 `XF86Config` 或 `xconfig` 的文件。设置 `Xconfig` 或 `XF86Config` 文件的基本指令分散在 XFree86 发行版套装中附带的几个文本文件中。在大多数情况下，您应该检查 `README`、`VideoModes.doc`、`README.Config` 和 `README.Linux` 文件。这还不止于此：您还必须阅读 `Xconfig`、`XF86Config`、XFree86 和 `XFree86bd` 的手册页。最后，如果提供了对应的手册页，您还应检查当前运行的服务器版本的手册页。（打印出这些手册页以便参考是个好主意。）

要正确完成 `xconfig` 或 `XF86Config` 文件，您需要了解一些信息。在开始配置 XFree86 之前，请花点时间记录以下详细信息：

- 要使用的 XFree86 服务器。
- 系统上鼠标的类型及其连接的端口。
- 显卡的品牌名称和芯片组。如果不确定芯片组，请查阅文档或使用 `SuperProbe`（Linux）或 `MSD`（DOS）等实用程序。
- 显示器品牌和型号，以及显示器的尺寸。知道最大水平和垂直扫描频率也有帮助，这些通常可以从显示器的文档中获取。
- 如果不使用美国通用键盘，您打算使用的键盘类型。大多数用户使用的是美国类型，但某些国家拥有需要不同按键映射的自定义键盘。

如果您不知道某些信息，并且没有简便方法（例如实用程序）来获取，则应检查随 XFree86 提供的文档。许多发行版包含一个目录，例如 `/usr/X11/lib/X11/doc`（通常链接到 `/usr/X88/lib/X11/doc` 或 `/usr/X11R6/lib/X11/doc`），其中包含许多描述 XFree86 支持的显卡和显示器以及基本配置信息（例如显示器扫描速率，由于您总是想不起手册放在哪里，因此这些很难确定）的文件。

当您记录了所有这些配置信息后，就可以开始配置 XFree86 了。这一切始于 `Xconfig` 或 `XF86Config` 文件。

### 放置 Xconfig 或 XF86Config 的位置

*Xconfig* 或 *XF86Config* 文件可以位于 Linux 文件系统中的几个位置。通常，它位于 `/usr/X386/lib/X11` 目录中，这也是通常可以找到 *Xconfig* 或 *XF86Config* 示例文件的地方。如果您可以轻松访问 `/usr/X386/lib/X11` 目录，这是放置 *Xconfig* 或 *XF86Config* 文件的最佳位置。（正式来说，该文件在 `/usr/X11R6/lib/X11` 或 `/etc` 中引用，但由于 `/usr/X386` 链接到 `/usr/X11R6`，这两个目录指向同一位置。您可能会遇到文档中引用的 X11R6 目录，但只要 X386 目录的链接存在，您可以使用其中任何一个。）

**注意**

除非您正在手动安装配置信息，否则不必担心应该使用 *Xconfig* 还是 *XF86Config*。自动安装脚本将使用正确的文件。如果您正在进行手动配置，请对 XFree86 版本 2.X 使用 *XConfig*，对 XFree86 版本 3.X 使用 *XFConfig*。

如果您无法使用 `/usr/X386/lib/X11`（可能是只读的或位于远程服务器上），或者因为需要自定义版本的 *Xconfig* 文件而不想使用它，该文件也可以放置在 `/etc` 目录或您的主目录中。如果 *Xconfig* 文件位于您的主目录中，它将仅应用于您的会话，其他用户的配置信息将无效。将 XFree86 *Xconfig* 文件放在 `/etc` 目录意味着配置信息适用于所有用户。

您也可以将 *Xconfig* 文件放在特定主机机器的目录 `/usr/X386/lib/X11` 中。为此，*Xconfig* 文件名后需附加主机机器名称。例如，文件 `*Xconfig*.merlin` 将仅将配置信息应用于从机器“merlin”登录的用户。

Linux 约定将 *Xconfig* 文件放置在 `/etc` 目录中。由于这不是 XFree86 安装的常见位置，必须创建一个指向 `/etc/Xconfig` 文件的链接到 `/usr/X386/lib/X11` 或您的主目录。这允许 XFree86 正确找到 *Xconfig* 文件。

### SuperProbe

*SuperProbe* 是一种试图确定许多 PC 系统中显卡类型（以及该显卡上安装的显存容量）的实用程序。它在 ISA、EISA 和 VLB（本地总线）架构上工作，但在 MCA 或 PCI 架构上不适用（尽管在您阅读本书时，这些系统的 SuperProbe 版本可能已经可用）。如果您已经知道拥有的显卡型号，那么 SuperProbe 对您用处不大。SuperProbe 通过探测其认识的每张显卡上某些已知的唯一寄存器来尝试识别显卡。这有一个缺点：SuperProbe 执行的一些指令可能会导致您的机器死机！虽然由于 SuperProbe 导致损坏的可能性不大，但如果必须重置机器，文件系统将被清理。因此，请确保您是机器上唯一的用户。备份您的系统也是强烈建议的。

> **提示**
> 单独运行 SuperProbe 几乎肯定会锁死任何机器，因此请谨慎使用，并按照本节中的说明给 SuperProbe 一个关于应执行哪些测试的基本概念。

SuperProbe 作为 XFree86 发行版套装的一部分包含在许多 CD-ROM 中，可以从提供 Linux 软件的 FTP 和 BBS 站点获取。SuperProbe 并非 Linux 独有，但可以运行在许多其他 PC UNIX 系统上。SuperProbe 有可用的手册页。

SuperProbe 使用许多命令行选项来指定其行为。虽然确切的选项随着软件的每个新版本而变化，但您感兴趣的基本选项仅限于以下几项：

- `-bios` 指定显卡 BIOS 的地址，通常设置为 C0000。如果您应将 BIOS 地址设置为其他值，将使用此选项指定。
- `-info` 显示 SuperProbe 所知道的所有显卡列表以及 SuperProbe 识别的显卡名称。
- `-no_16` 禁用 16 位测试。仅用于旧的 8 位显卡。
- `-no_bios` 禁用显卡 BIOS 测试，并假设显卡是 EGA、VGA、SVGA 或更新类型。如果您的显卡较新，这是一个防止许多 BIOS 导致系统死机的有用选项。
- `-no_dac` 禁用 RAMDAC 类型测试。这可防止潜在的死机，可用于 VGA 和 SVGA 显卡。
- `-no_mem` 跳过对显卡上安装的显存容量的测试。
- `-order` 指定测试芯片组的顺序。如果您认为知道芯片组类型但希望得到确认，这很有用。或者，如果您怀疑显卡具有少数几种芯片组之一，您可以仅列出这些。
- `-verbose` 在屏幕上显示 SuperProbe 的操作和结果信息。这是一个在所有情况下都应使用的有用选项，以显示进度和潜在问题。

采取的第一步之一是显示 SuperProbe 所知道的所有显卡列表。发出以下命令：

```
SuperProbe -info
```

您将看到一个显示 SuperProbe 可以识别的显卡、芯片组和 RAMDAC 的列表。请注意，实用程序名称 SuperProbe 是混合大小写，S 和 P 为大写。这对于 Linux 系统来说不寻常，经验丰富的 UNIX 和 Linux 用户可能需要一点时间来适应。

如果您有较旧的 8 位显卡，可以使用以下命令确定芯片组：

```
SuperProbe -no16 -verbose
```

如果您有一个 16 位（或更高）显卡，并怀疑它是 S3、Cirrus Logic 或 Tseng 芯片组，例如，您可以使用 -order 选项简化测试（并防止潜在问题）：

```
SuperProbe -order S3,Cirrus,Tseng -verbose
```

在 order 选项后指定的芯片组之间没有空格。verbose 选项让您可以看到正在发生的事情。建议以这种方式缩小芯片组的搜索范围以防止死机。即使您确切知道系统中的显卡型号，也不要假设 SuperProbe 会正常运作。SuperProbe 有一个令人烦恼的习惯，会因为与其他卡或设备的冲突而挂起系统。请谨慎使用。

## 使用 ConfigFX86 和 fx86config

ConfigFX86 和 fx86config 使用简单的界面让您选择支持的显卡和视频监视器。如果您的显卡受 ConfigFX86 或 fx86config 实用程序支持（请检查 Hardware HOWTO 和 XFree86 README 文件），您可以使用 ConfigFX86 和 fx86config 安装例程极大地简化配置过程。如果随您的 XFree86 发行版提供，ConfigFX86 和 fx86config 将位于 `/usr/X386/bin` 目录中。ConfigFX86 由 Stephen Zwasca 编写。

