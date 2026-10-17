
- `-bios` 指定显卡 BIOS 的地址，通常设置为 `C0000`。如果您应将 BIOS 地址设置为其他值，将使用此选项指定。

- `-info` 显示 `SuperProbe` 所知道的所有显卡列表以及 `SuperProbe` 识别的显卡名称。

- `-no_16` 禁用 16 位测试。仅用于旧的 8 位显卡。

- `-no_bios` 禁用显卡 BIOS 测试，并假设显卡是 `EGA`、`VGA`、`SVGA` 或更新类型。如果您的显卡较新，这是一个防止许多 BIOS 导致系统死机的有用选项。

- `-no_dac` 禁用 `RAMDAC` 类型测试。这可防止潜在的死机，可用于 `VGA` 和 `SVGA` 显卡。

- `-no_mem` 跳过对显卡上安装的显存容量的测试。

- `-order` 指定测试芯片组的顺序。如果您认为知道芯片组类型但希望得到确认，这很有用。或者，如果您怀疑显卡具有少数几种芯片组之一，您可以仅列出这些。

- `-verbose` 在屏幕上显示 `SuperProbe` 的操作和结果信息。这是一个在所有情况下都应使用的有用选项，以显示进度和潜在问题。

采取的第一步之一是显示 `SuperProbe` 所知道的所有显卡列表。发出以下命令：

```
SuperProbe -info
```

您将看到一个显示 `SuperProbe` 可以识别的显卡、芯片组和 `RAMDAC` 的列表。请注意，实用程序名称 `SuperProbe` 是混合大小写，`S` 和 `P` 为大写。这对于 `Linux` 系统来说不寻常，经验丰富的 `UNIX` 和 `Linux` 用户可能需要一点时间来适应。

如果您有较旧的 8 位显卡，可以使用以下命令确定芯片组：

```
SuperProbe -no16 -verbose
```

如果您有一个 16 位（或更高）显卡，并怀疑它是 `S3`、`Cirrus Logic` 或 `Tseng` 芯片组，例如，您可以使用 `-order` 选项简化测试（并防止潜在问题）：

```
SuperProbe -order S3,Cirrus,Tseng -verbose
```

在 `order` 选项后指定的芯片组之间没有空格。`verbose` 选项让您可以看到正在发生的事情。建议以这种方式缩小芯片组的搜索范围以防止死机。即使您确切知道系统中的显卡型号，也不要假设 `SuperProbe` 会正常运作。`SuperProbe` 有一个令人烦恼的习惯，会因为与其他卡或设备的冲突而挂起系统。请谨慎使用。

## 使用 ConfigFX86 和 fx86config

`ConfigFX86` 和 `fx86config` 使用简单的界面让您选择支持的显卡和视频监视器。如果您的显卡受 `ConfigFX86` 或 `fx86config` 实用程序支持（请检查 `Hardware HOWTO` 和 `XFree86 README` 文件），您可以使用 `ConfigFX86` 和 `fx86config` 安装例程极大地简化配置过程。如果随您的 `XFree86` 发行版提供，`ConfigFX86` 和 `fx86config` 将位于 `/usr/X386/bin` 目录中。`ConfigFX86` 由 `Stephen Zwasca` 编写。

## 详解 Xconfig 和 XF86Config 文件

`ConfigFX86` 和 `fx86config` 都有可用的文档，通常与可执行文件一起放置在 `/usr/X386/bin` 目录下。不过，某些版本的 `Linux` 和 `XFree86` 并不提供这些文档。文档通常以多种格式提供。有一个 `ASCII` 版本名为 `ConfigFX86.txt`，还有一个 `PostScript` 版本名为 `ConfigFX86.ps`（或 `fx86config` 的对应版本）。

当您运行 `ConfigFX86` 或 `fx86config` 时，系统会显示一些通用信息，然后提示您输入之前收集的关于系统的信息。在大多数情况下，系统会显示一个受支持值的列表，并要求您选择其中一个。按顺序完成这些选择后，该工具就会获得构建 `Xconfig` 文件所需的正确信息。

例如，`xf86config` 工具会询问您的鼠标类型、是否要启用鼠标的特殊功能（如三键鼠标的中键）、鼠标连接的设备、显示器的水平和垂直同步范围、显示器的名称、视频卡使用的芯片组、要运行的服务器、链接到服务器的文件位置、视频卡上安装的 `RAM` 量、是否要设置时钟芯片，以及视频卡支持的分辨率顺序。在您回答了所有问题后，`xf86config` 会询问该工具是否应创建 `XF86Config` 文件。

使用脚本创建 `XF86Config` 或 `Xconfig` 文件后，您应该克制立即启动 `X` 的冲动。相反，请花点时间手动检查该文件，以防止因设置不正确而对硬件造成任何潜在损坏。接下来关于手动配置 `Xconfig` 或 `XF86Config` 文件的章节将解释所有设置。当您对一切都满意后，使用命令 `startx` 启动 `X`。

如果您手动将配置信息输入 `Xconfig` 或 `XF86Config` 文件，您需要了解这些文件的布局以及如何输入您的具体细节。所有版本的 `XFree86` 都至少有一个示例配置文件，通常名为 `Xconfig.sg` 或 `XF86Config.sg`，位于 `lib` 目录中。您应该使用此文件作为创建自己配置文件的模板。将示例文件复制到一个不带 `.eg` 扩展名的新文件中，并进行以下描述的更改。

`Xconfig` 和 `XF86Config` 文件并不短，但其中散布着大量注释。配置文件的格式是一组部分，每个部分对应 `XFree86` 配置的各个方面。部分的一般顺序如下：

- 二进制文件和屏幕字体的路径名
- 键盘信息
- 鼠标信息
- 服务器文件
- 视频信息

让我们更详细地查看每个部分。如果您已运行过自动配置文件生成工具（如 `xf86config` 或 `XF86Config`），请检查生成文件中的条目。如果您正在手动编辑文件，请缓慢且有条理地进行操作，以防止出错。

**注意**

本节其余部分显示的代码摘录来自 `XFree86` 版本 `3.X` 创建的 `XF86Config` 文件，因为它是最新版本，并且通常包含在新的软件发行版中。`XFree86` 版本 `2.X` 的 `Xconfig` 文件类似，通过检查 `Xconfig` 文件，您在执行相同步骤时不应遇到任何问题。

请注意，`Xconfig` 或 `XF86Config` 文件中的每个部分都以关键字 `"section"` 开头，随后是该部分的名称。部分以关键字 `"EndSection"` 结束。这使得查找您要操作的部分更容易。文件中的注释都以井号（`#`）开头。

### 路径名

在大多数情况下，除非您将 `XFree86` 安装在默认值以外的目录中，否则配置文件中提供的路径名无需更改。`XFree86` 用于屏幕字体和其他文件的路径在配置文件的以下部分中给出：

```
Section "Files"

# The location of the RGB database. Note, this is the name of the
# file minus the extension (like ".txt" or ".db"). There is normally
# no need to change the default.

RgbPath "/usr/X11R6/lib/X11/rgb"

# Multiple FontPath entries are allowed (which are concatenated together),
# as well as specifying multiple comma-separated entries in one FontPath
# command (or a combination of both methods)
	FontPath 	"/usr/X11R6/lib/X11/fonts/misc/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/Type1/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/Speedo/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/75dpi/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/100dpi/"

EndSection
```

上述代码定义了屏幕字体和 `RGB` 数据库的搜索路径。如果您将 `XFree86` 安装到默认目录，或让安装例程使用默认值继续，则此处不应更改任何内容。

请注意，此 `XF86Config` 文件中引用的目录遵循 `X` 的正式命名约定，使用 `/usr/X11R6`。然而，由于在大多数安装中，这些目录链接到 `/usr/X11`、`/usr/X386`，以及潜在的其他目录，因此可以沿链接到达目标文件。请通过依次进入每个目录并检查其中包含的文件，以验证这些目录是否确实指向屏幕字体。如果目录不存在或为空，`XFree86` 将无法正确加载字体，并可能崩溃或生成错误消息。

如果您向 `XFree86` 安装中添加新字体，它们应放在 `XF86Config` 文件中指定的某个字体目录中。

### 键盘设置
