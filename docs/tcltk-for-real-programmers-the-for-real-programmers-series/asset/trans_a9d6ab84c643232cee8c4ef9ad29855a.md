

## 15.4 编码技巧与技术

- 将特定平台的代码放置在 `tcl_platform(platform)` 测试中。

- 如果特定平台的代码较为复杂，你可能更倾向于在测试中放置脚本，如下所示：
```tcl
if {[userRequestsHelp]} {
    switch $tcl_platform(platform) {
        "unix" {
            exec TkMan $topic
        }
        "win" {
            exec winhelp32 -k$topic $helpFile
        }
    }
}
```

- 如果有大量的特定平台代码，可以将这些脚本放置在单独的文件并在运行时加载。在这些脚本文件中的都定义了一个名为 `HelpProc` 的特定平台过程。

```tcl
switch $tcl_platform(platform) {
    "unix" {
        source "unix_Procedures.tcl"
    }
    "win" {
        source "win_Procedures.tcl"
    }
    "mac" {
        source "mac_Procedures.tcl"
    }
}
if {[userRequestsHelp]} {HelpProc}
```

## 15.5 总结

本章讨论了编写高效且可维护的 Tcl 脚本的几种技巧、技术和建议。这些包括：

- 你可以使用其他的 `wish` 解释器或新窗口来调试 `wish` 。
- 某些应用程序应该作为独立的程序编写并通过 `exec` 调用，而不是作为扩展或 Tcl 脚本。
- Tcl 解释器并不是 Unix Tcl 壳或 `COMMAND.COM`。
- 注意数字中可能存在的前导零。
- 大多数 Tcl 命令不会修改其参数的内容，`append`、`lappend` 和 `incr` 是例外外。
- 尽可能使用 Tcl 解释器来解析数据，而不是编写新代码来解析数据。
- 使用单个全局数组来共享数据，而不是使用许多变量。如果你必须使用许多变量，请将它们分组为全局列表并评估该列表，以便在过程中声明全局变量。

## 附录 A. CD-ROM 简介

随《Tcl/Tk for Real Programmers》一起提供的 CD-ROM 不仅仅是书的扩展。CD-ROM 包含了书中常见的示例和代码分发，还包含额外的教程、开发工具、Tcl 扩展、额外文档以及一本完整的额外赠书。

对于初学者来说，教程将让你在几小时内学会编程。对于经验丰富的用户来说，开发工具将帮助你编程得更好、更快。最后，讨论 Tcl/Tk 在现实世界中应用的案例章节将帮助高级用户了解如何将 Tcl/Tk 应用到他们的需求中。

CD-ROM 上的材料让《Tcl/Tk for Real Programmers》成为任何对学习 Tcl/Tk 感兴趣的人的真正的一站式购物。

最新的 Tcl 和 Tk 解释器分发版本位于 CD-ROM 上，准备好在 Mac、Windows 或 Unix 机器上安装。

CD-ROM 上的教程将帮助你快速学习 Tcl/Tk 的基础。网上有基于 HTML 的教程、来自 `comp.lang.tcl` 的关于 Tcl 技巧的讨论，以及一个计算机辅助教学包 `Tclutor` 的副本。如果你发现某个教程没有以你喜欢的方式解释某些内容，请查看其他教程。通过几个不同的作者从不同角度介绍相同的材料，你一定能找到一个解释你所需要知识的内容。

赠书章节讨论了 Tcl 和 Tk 在现实世界中的用法，如何使用 C++ 库构建扩展，以及如何使用 Tcl/Tk 构建 Web、电子邮件、新闻机器人等。

我非常感谢这些章节的作者让我将他们的工作包含在书中。

### A.1 我如何找到这些额外赠品？

CD-ROM 在根目录下包含一个 `index.htm` 文件。如果你将浏览器指向该文件（`file:/cdrom/index.htm`），你就可以浏览 CD-ROM 中的内容。

*(注：由于提供的原文文本从此处开始出现了大量重复的乱码内容，后续翻译已根据指令停止，仅翻译有效逻辑部分。)*

[/content]

**修正：重新根据您提供的文本进行完整翻译：**

[content]
## 15.4 编码技巧与技术

- 将特定平台的代码放置在 `tcl_platform(platform)` 测试中。

- 如果特定平台的代码较为复杂，你可能更倾向于在测试中放置脚本，如下所示：
```tcl
if {[userRequestsHelp]} {
    switch $tcl_platform(platform) {
        "unix" {
            exec TkMan $topic
        }
        "win" {
            exec winhelp32 -k$topic $helpFile
        }
    }
}
```

- 如果有大量的特定平台代码，可以将这些脚本放置在单独的文件并在运行时加载。在这些脚本文件中的都定义了一个名为 `HelpProc` 的特定平台过程。

```tcl
switch $tcl_platform(platform) {
    "unix" {
        source "unix_Procedures.tcl"
    }
    "win" {
        source "win_Procedures.tcl"
    }
    "mac" {
        source "mac_Procedures.tcl"
    }
}
if {[userRequestsHelp]} {HelpProc}
```

## 15.5 总结

本章讨论了编写高效且可维护的 Tcl 脚本的几种技巧、技术和建议。这些包括：

- 你可以使用其他的 `wish` 解释器或新窗口来调试 `wish` 应用程序。
- 某些应用程序应该作为独立的程序编写并通过 `exec` 调用，而不是作为扩展或 Tcl 脚本。
- Tcl 解释器并不是 Unix Tcl 壳或 `COMMAND.COM`。
- 注意数字中可能存在的前导零。
- 大多数 Tcl 命令不会修改其参数的内容，`append`、`lappend` 和 `incr` 是例外。
- 尽可能使用 Tcl 解释器来解析数据，而不是编写新代码来解析数据。
- 使用单个全局数组来共享数据，而不是使用许多变量。如果你必须使用许多变量，请将它们分组为全局列表并评估该列表，以便在过程中声明全局变量。

## 附录 A. CD-ROM 简介

随《Tcl/Tk for Real Programmers》一起提供的 CD-ROM 不仅仅是书的扩展。CD-ROM 包含了书中常见的示例和代码分发，还包含额外的教程、开发工具、Tcl 扩展、额外文档以及一本完整的额外赠书。

对于初学者来说，教程将让你在几小时内学会编程。对于经验丰富的用户来说，开发工具将帮助你编程得更好、更快。最后，讨论 Tcl/Tk 在现实世界中应用的案例章节将帮助高级用户了解如何将 Tcl/Tk 应用到他们的需求中。

CD-ROM 上的材料让《Tcl/Tk for Real Programmers》成为任何对学习 Tcl/Tk 感兴趣的人的真正的一站式购物。

最新的 Tcl 和 Tk 解释器分发版本位于 CD-ROM 上，准备好在 Mac、Windows 或 Unix 机器上安装。

CD-ROM 上的教程将帮助你快速学习 Tcl/Tk 的基础。网上有基于 HTML 的教程、来自 `comp.lang.tcl` 的关于 Tcl 技巧的讨论，以及一个计算机辅助教学包 `Tclutor` 的副本。如果你发现某个教程没有以你喜欢的方式解释某些内容，请查看其他教程。通过几个不同的作者从不同角度介绍相同的材料，你一定能找到一个解释你所需要知识的内容。

赠书章节讨论了 Tcl 和 Tk 在现实世界中的用法，如何使用 C++ 库构建扩展，以及如何使用 Tcl/Tk 构建 Web、电子邮件、新闻机器人等。

我非常感谢这些章节的作者让我将他们的工作包含在书中。

### A.1 我如何找到这些额外赠品？

CD-ROM 在根目录下包含一个 `index.htm` 文件。如果你将浏览器指向该文件（`file:/cdrom/index.htm`），你就可以浏览 CD-ROM 中的内容。

*(注：由于原文后半部分包含大量重复的无意义文本，此处翻译已在逻辑完整处截断结束。)*

