
# rm -rf user/

# cd ..

10. 运行 `mkisofs` 命令，将其通过 `create_compressed_fs` 命令压缩生成的 ISO 映像，并创建更新的 uci 文件（称为 `zile.uci`）。`mkisofs` 命令的选项允许 Rock Ridge 扩展用于 Linux 文件命名 (`-R`)、导致每个硬链接文件在 CD-ROM 映像上仅出现一次 (`-cache-inodes`)，并将映像填充 150 个扇区 (`-pad`)：

```
# mkisofs -R -hide-rr-moved -cache-inodes -pad zile/ \
| create_compressed_fs - 65536 > ../zile.uci
```

11. 删除工作目录：

```
# cd ..
# rm -rf work
```

执行此过程后，你应该在 `/home/ds1` 目录中拥有一个新的 `zile.uci` MyDSL 包。

## SHARING YOUR EXTENSION WITH THE WORLD

在你的扩展工作并且经过彻底测试后，你可能希望分享你的创作。DSL 为用户贡献提供了许多仓库 `extensions`。所有共享的扩展必须使用 GNU 公共许可证（GPL）或类似许可证。

参与社区仓库还需要几个额外的文件。第一个是信息文件。用户希望浏览描述您扩展的摘要。此摘要可通过仓库网站查看，并且也是用户选择 MyDSL 下载浏览器工具时显示屏幕的一部分。

### 所有人可读的信息文件

`.info` 文件是一个简单的文本文件，是扩展名称的附加后缀。例如，`zile.dsl` 的信息文件是 `zile.dsl.info`。使用 `beaver` 等文本编辑器，创建以下文件：

```
Title:              zile.dsl
Description:        Zile is an Emacs like text editor
Version:            2.2.29
Author:             http://www.my_program.org/
Original-site:      http://www.my_program.org/
Copying-policy:     GPL
--------------------------------------------------
Extension by:       <your email address>
Comments:           This is an Emacs like text editor.
                    It is a console-based application.
                    It can be run from CLI or X hosted by an aterm.
                    It requires the xxxx.dsl and the yyyy.dsl to function.
                    This was repackaged from my_program_42.0-0_i386.deb
                    found at ftp.us.debian.org woody.
                    Includes icon and menu.
Change-log:         2006/08/24 - First Version
Current:            2007/02/12 - Upgraded and Revised for xxxx-new.dsl
```

以上仅是一个示例。在 `Comments` 部分，您应包含您从何处获取该程序。列出您的扩展可能需要的其他 MyDSL 扩展。

### 质量保证校验文件

第二个必需文件是校验文件。该文件是强制性的，是用户使用 MyDSL 下载工具时自动化流程的一部分。此文件可确保用户已成功下载。

用户下载文件时可能会出现多种情况。自动化下载流程的一部分会验证校验和，并在校验和不同时通知用户。通过网络下载的用户也强烈建议在尝试使用扩展之前验证校验和。此文件的名称为基础扩展名称加上 `.md5.txt` 后缀。对于您的 Zile 示例，它将是 `zile.dsl.md5.txt`。要创建此文件，只需在 DSL 中使用 `md5sum` 程序为 Zile 创建它，输入以下命令：

```
# md5sum zile.dsl > zile.dsl.md5.txt
```

### 提交扩展以供发布

最后一步是将所有三个文件收集起来并通过电子邮件发送至 `extensions@damsmallinux.org`。对于您的 Zile 示例，您将发送一封电子邮件，主题行中至少包含以下词语：DSL Zile Extension。然后，附上 `zile.dsl`、`zile.dsl.info` 和 `zile.dsl.md5.txt`。

提交的扩展通常每周处理一次。一旦扩展被处理，会向您发送一封“感谢”邮件，表明提交的扩展已发布到 MyDSL 仓库的测试区域。DSL 论坛测试区也会发布公告。

每月为当月提交的扩展创建一个新主题。公告提醒用户社区开始测试新扩展。作为扩展提交者，您应回复问题并在必要时进行更正。

如果提交的扩展缺少其中一个必需文件或在处理过程中 `md5sum` 完整性检查失败，则会发送电子邮件说明在扩展被接受之前需要什么。

## SUMMARY

将应用程序添加到 DSL 可以像使用 Debian Apt 系统一样简单。由于使用 Apt 与 DSL 非常浪费内存，您学会了如何创建内存效率更高的 MyDSL 扩展。您看到它可以像运行两个脚本一样简单：`deb2dsl` 和 `dsl2unc`。

您看到添加菜单和图标可以通过易于制作的文本文件完成。您已了解 MyDSL 下载工具期望的结构，以及使用 `mydsl-load` 命令处理 MyDSL 桌面图标所需的结构。

您还看到了从源代码编译和创建自包含应用程序的更具挑战性的方面，以及如何打包最强大的 MyDSL 扩展类型：`uci`。

总体而言，MyDSL 扩展只是重新打包的文件和目录，外加一些通用元素，以支持 DSL 的 live CD-ROM 单用户环境。

## 设置完整的重制环境

使用许多基于 Live CD-ROM 的系统时，添加额外的软件包通常需要进行重制。在第 5 章“使用 MyDSL 扩展应用程序”中，你已经看到添加数十个名为 MyDSL 扩展的额外应用程序是多么容易。只需将它们复制到启动介质或放置在持久存储上（硬盘分区、U盘或 Compact Flash）；无需任何额外的启动选项，整个系统即可启动，并且看起来更大、更符合你的特定需求。

然而，总会有希望让单个可启动 CD-ROM 像你的 Damn Small Linux (DSL) 系统一样工作的愿望。你不能总是随身携带持久介质。DSL 提供了两种完成此任务的方法。

仅通过从 Live DSL CD-ROM 正常启动并在启动时加载所有 MyDSL 扩展，DSL 可以制作一个名为 `mydsl.iso` 的简单组合镜像；此过程称为 MakeMyDSL (`mkmydsl`)。此过程是增量的。它是将你所选的所有 MyDSL 选择和其他非更改数据组合成一个新的自包含、可启动的 CD-ROM 镜像。

这是一个极其简单的过程。事实上，它是会上瘾的。你可以用额外的 MyDSL 应用程序自定义 DSL，更改默认桌面和壁纸，然后帮助将 Linux 革命传播给你的朋友和亲戚。你可以创建自定义设备。通常，我建议只包含非机器和非本地环境特定的项目。毕竟，你仍然希望你的 `mydsl.iso` 能够像原始 DSL 一样享受相同的游牧式启动能力。

然而，有时你希望包含机器或网络环境功能。例如，教室可能共享一台常用打印机，或可能还有其他常用硬件设备。如果你能在 DSL 和/或 MyDSL 中配置它，你可以轻松创建一个自定义的 `mydsl.iso` 可启动 CD-ROM。

在你看到这个 `mkmydsl` 过程后，你可能不需要继续阅读。因为 DSL 非常小，使用增量方法非常有吸引力。然而，有时你希望实际删除核心 DSL 应用程序或更改系统内部结构。当这种情况发生时，你需要进行完整的 KNOPPIX 风格重制。关于重制 KNOPPIX 的书籍和文档有很多。本章的意图并不是重复这些努力。本章的意图是讨论特定于 DSL 的领域。

## 将你的 Frugal MyDSL 安装制作成可启动 CD-ROM

`mkmydsl` 过程是从本地运行的、从 CD-ROM 启动的 Live DSL 系统中完成的。它基于 MyDSL 扩展概念。这提供了一种快速简单的方法来制作自定义 DSL 版本，包括所有已知可与标准 DSL 系统配合使用的额外应用程序和配置。与完整重制过程相比，这有以下几个优势：

- **先试后烧**—你可以在承诺进行整个耗时的制作 ISO、刻录和测试周期之前下载扩展并试用它们。
- **构造集**—通过分部分下载，你真正拥有了一种构造集方法。这使得使用慢速调制解调器的用户能够分部分、随时间下载和测试。
