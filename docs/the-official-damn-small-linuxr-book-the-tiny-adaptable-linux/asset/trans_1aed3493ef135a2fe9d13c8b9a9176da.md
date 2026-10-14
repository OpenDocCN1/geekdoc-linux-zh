

extensions. 所有共享的扩展必须使用 GNU 公共许可证（GPL）或类似许可证。

参与社区仓库还需要几个额外的文件。第一个是信息文件。用户希望浏览描述您扩展的摘要。此摘要可通过仓库网站查看，并且也是用户选择 MyDSL 下载浏览器工具时显示屏幕的一部分。

## 所有人可读的信息文件

`.info` 文件是一个简单的文本文件，是扩展名称的附加后缀。例如，`zile.dsl` 的信息文件是 `zile.dsl.info`。使用 beaver 等文本编辑器，创建以下文件：

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

以上仅是一个示例。在 Comments 部分，您应包含您从何处获取该程序。列出您的扩展可能需要的其他 MyDSL 扩展。

## 质量保证校验文件

第二个必需文件是校验文件。该文件是强制性的，是用户使用 MyDSL 下载工具时自动化流程的一部分。此文件可确保用户已成功下载。

用户下载文件时可能会出现多种情况。自动化下载流程的一部分会验证校验和，并在校验和不同时通知用户。通过网络下载的用户也强烈建议在尝试使用扩展之前验证校验和。此文件的名称为基础扩展名称加上 `.md5.txt` 后缀。对于您的 Zile 示例，它将是 `zile.dsl.md5.txt`。要创建此文件，只需在 DSL 中使用 md5sum 程序为 Zile 创建它，输入以下命令：

```
# md5sum zile.dsl > zile.dsl.md5.txt
```

## 提交扩展以供发布

最后一步是将所有三个文件收集起来并通过电子邮件发送至 extensions@damsmallinux.org。对于您的 Zile 示例，您将发送一封电子邮件，主题行中至少包含以下词语：DSL Zile Extension。然后，附上 `zile.dsl`、`zile.dsl.info` 和 `zile.dsl.md5.txt`。

提交的扩展通常每周处理一次。一旦扩展被处理，会向您发送一封“感谢”邮件，表明提交的扩展已发布到 MyDSL 仓库的测试区域。DSL 论坛测试区也会发布公告。

每月为当月提交的扩展创建一个新主题。公告提醒用户社区开始测试新扩展。作为扩展提交者，您应回复问题并在必要时进行更正。

如果提交的扩展缺少其中一个必需文件或在处理过程中 md5sum 完整性检查失败，则会发送电子邮件说明在扩展被接受之前需要什么。

## SUMMARY

将应用程序添加到 DSL 可以像使用 Debian Apt 系统一样简单。由于使用 Apt 与 DSL 非常浪费内存，您学会了如何创建内存效率更高的 MyDSL 扩展。您看到它可以像运行两个脚本一样简单：`deb2dsl` 和 `dsl2unc`。

您看到添加菜单和图标可以通过易于制作的文本文件完成。您已了解 MyDSL 下载工具期望的结构，以及使用 `mydsl-load` 命令处理 MyDSL 桌面图标所需的结构。

您还看到了从源代码编译和创建自包含应用程序的更具挑战性的方面，以及如何打包最强大的 MyDSL 扩展类型：uci。

总体而言，MyDSL 扩展只是重新打包的文件和目录，外加一些通用元素，以支持 DSL 的 live CD-ROM 单用户环境。

