
## 比较 INFO 和 MAN 页面导航

`pinfo` 命令和 `man` 命令使用的导航键略有不同。下表比较了两个命令的导航键：

| 导航 | PINFO | MAN |
| --- | --- | --- |
| 向下滚动一屏 | PageDown 或 Space | PageDown 或 Space |
| 向上滚动一屏 | PageUp 或 b | PageUp 或 b |
| 显示主题目录 | D | - |
| 向下滚动一半屏 | - | D |
| 显示主题的父节点 | U | - |
| 显示主题的根节点 | HOME | G |
| 向上滚动一半屏 | - | U |
| 向下滚动到下一个超链接 | DownArrow | - |
| 在光标处打开主题 | Enter | - |
| 向下滚动一行 | - | DownArrow 或 Enter |
| 向上滚动到上一个超链接 | UpArrow | - |
| 向上滚动一行 | - | UpArrow |
| 搜索模式 | /string | /string |
| 显示主题中的下一个节点 | N | - |
| 重复向下向下搜索 | / then Enter | n |
| 显示主题中的上一个节点 | P | - |
| 重复向上向上搜索 | - | Shift+N |
| 退出程序 | Q | Q |

> 参考文献
`pinfo` info (Info: 简介)
`pinfo` (`pinfo` 文档)

GNU 项目
http://www.gnu.org/gnu/theproject.html
`info(1)` 和 `info(1)` man 页面

## 引导练习

### 阅读文档

在本次练习中，你将使用命令行工具查找 GNU Info 文档中存储的信息。

### 结果

你应该能够使用命令行工具导航 GNU Info 文档。

### 开始之前

使用 `student` 作为密码登录工作站。
在工作站上运行 `lab help-info` 命令。

```
[student@workstation ~$ lab help-info start
```

- 1. 在工作站上不带任何参数启动 `info`。

```
[student@workstation ~$ info
```

- 2. 导航到常用选项主题。
使用 `UpArrow` 或 `DownArrow` 直到 `(coreutils) Common options` 被高亮。

- 基础
- Bash (`bash`): GNU Bourne Again Shell。
- 常用选项 (`coreutils`): Common options。

> 图 4.2：Bash 文档

- 3. 按 `Enter` 查看此主题。

```
File: coreutils.info, Mode: Common options, Next: Output of entries, Prev: Introduction, Up: Top options
```

这些程序提供了某些可用选项。与其为每个程序编写描述，不如在这里进行描述（事实上，每个 GNU 程序都接受（或应该接受）这些选项）。通常选项和参数以任何顺序出现，但选项出现在参数之前。例如，`sort -t` 类似于 `sort -r -t`，因为 `-t` 是一个选项。然而，如果设置了 `POSIX_COR` 环境变量，除非单独指定，否则选项必须出现在参数之前。

> 图 4.3：常用选项 info 主题

- 4. 浏览此 `info` 主题。长格式选项可以缩写。
使用 `PageUp` 和 `PageDown` 浏览主题。是的，许多程序允许选项缩写。

- 5. 确定当用命令参数时符号 `--` 表示选项的结束和命令参数的开始。在复杂命令中，shell 的命令行解析器可能无法正确区分。

- 6. 在不退出 `pinfo` 的情况下，移动到 GNU Coreutils 节点。
按 `U` 移动到主题的根节点。

- 7. 返回根节点主题。
按 `U`。观察当位于主题根节点时，移动会返回主题目录。或者，从任何级别或主题按 `D` 会直接跳转到主题目录。

- 8. 搜索模式 `coreutils` 并选择它。
- 9. 选择主题。通过搜索 "`coreutils`"。
- 10. 向上移动两层返回主题目录。
- 11. 按 `Q` 退出 `pinfo`。
- 12. 再次使用 `pinfo` 命令，指定 `coreutils` 为命令行。

```
[student@workstation ~$ pinfo coreutils
```

- 13. 选择 Disk usage 主题。
按 `DownArrow` 高亮 `Disk usage`，然后按 `Enter` 选择此主题。

- 14. 使用你研究的各种 `evince` 选项查看你的 PostScript 文件。完成后关闭文件。

### 完成

在工作站上运行 `lab help-info finish` 完成本次练习。

```
[student@workstation ~$ lab help-info finish
```

引导练习结束。

## 在红帽企业版中获取帮助

### 检查清单
在本实验中，你将查找信息来帮助完成 man 页面和 GNU Info 文档中的任务。

### 结果
你应该能够：

- 通过搜索 man 页面和 Info 节点找到相关命令。
- 学习常用命令的新选项。
- 使用适当工具查看和打印文档以及非文本格式文件。

### 开始之前
使用 `student` 作为密码登录工作站。
在工作站上运行 `lab help-review start`。

```
[student@workstation ~$ lab help-review start
```

- 1. 在工作站上，确定如何准备打印 man 页面。具体而言，找到用于打印的格式或渲染语言。

- 2. 创建 `password` man 页的格式化输出文件。命名为 `password.ps`。确定文件内容格式。检查 `password.ps` 文件的内容。

> 注意
使用以下命令创建 `password` man 页的输出：

```
[student@workstation $] man -t password > password.ps
```

符号将 man 页的内容重定向到 `password.ps` 文件。该命令将在后续章节中进行详细介绍。

- 3. 使用 `man` 学习查看和打印 PostScript 文件的命令。

- 4. 学习如何在预览模式下使用 `evince()` 查看器。还要确定如何从特定页面打开文档。

- 5. 使用你研究的各种 `evince` 选项查看你的 PostScript 文件。完成后关闭文件。

- 6. 使用 `man` 命令研究 `lp(1)`，以确定如何从特定页面打印任何文档。在不实际输入任何命令的情况下（因为没有打印机），学习使用一条命令仅打印你的 PostScript 文件的第 2 和第 3 页。

- 7. 使用 `quinto` 查找关于 `evince` 查看器的 GNU Info 文档。

- 8. 使用 Firefox 打开系统的软件包文档目录，并进入 `man-db` 包子目录。查看提供的手册。

- 9. 使用 Firefox 浏览器定位并浏览到 `initscripts` 包子目录。查看 `sysconfig.txt` 文件，该文件描述了存储在 `/etc/sysconfig` 目录中的重要系统配置选项。

### 评估

在工作站上运行 `lab help-review grade` 以确认本次练习是否成功。

```
[student@workstation ~]$ lab help-review grade own
```

# 结束

在工作站上运行 `lab help-review finish` 脚本以完成本次练习。

```
[student@workstation ~]$ lab help-review finish
```

本实验结束。

# 第 4 章 | 在 Red Hat Enterprise Linux 中获取帮助

## 解决方案

# 在 RED HAT ENTERPRISE LINUX 中获取帮助

### 性能清单
在本实验中，你将查找信息来帮助你在 man 页面和 GNU 文档中完成任务。

### 成果
你应该能够：

- 通过搜索 man 页面和 Info 节点定位相关命令。
- 学习常用文档命令的新选项。
- 使用适当的工具查看和打印文档以及非文本格式的文件。

### 开始之前
使用密码 `student` 以 `student` 身份登录工作站。
在工作站上，运行 `lab help-review start` 命令。

```
[student@workstation ~]$ help-review start
```

1. 在工作站上，确定如何为打印准备 man 页面。具体来说，找到打印使用的是什么格式或渲染语言。

1.1 使用 `man` 命令确定如何为打印准备 man 页面。

```
[student@workstation ~]$ man man
```
