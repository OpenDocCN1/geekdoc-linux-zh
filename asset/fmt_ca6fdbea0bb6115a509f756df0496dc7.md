
| ProcessName | PM(MB) |
| --- | --- |
| swping | 96.1756 |
| svhost | 62.5418 |
| Search | 41.9768 |
| svchost | 24.2812 |

图 10-26 cmdlet 中的缩放表示数值除以 1 MB。实际缩放发生在 `Expression`，其中 PM 当前值除以 1 MB。

## 活动 10-5：报告内存

时间：15 分钟
目标：报告 Windows 10 上运行的内存。
描述：在此活动中，启动 PowerShell 脚本报告进程。此活动将采用增量开发，以便尽可能编写代码。边开发边测试该脚本。练习使用 `Sort-Object`、`Where-Object`、`Select-Object` 和 `Format-Table` 常用命令。

在执行后续活动之前，你必须完成并保存活动 10-4 中的脚本。

1. 如果需要，使用活动 10-1 中的相应说明启动虚拟机。
2. 如果需要，以管理员权限登录。
3. 如果需要，打开 ISE。在任务栏上右键点击 PowerShell ISE 图标，然后“以管理员身份运行”。点击 Yes。
4. 如果需要，打开脚本文件。点击 File，点击 Script，然后点击 Open。

为了满足本教材的要求，cmdlet 在行之间拆分。在 PowerShell 中，在行尾使用管道符 (`|`) 拆分行。![](img/290e46d5832f20e3707f4841e4e6d75a_495_0.png)

5. 为了在下一行继续脚本，在第 1 行 `Get-Process` 后添加 `|`。
6. 按内存排序数据，在第 2 行输入 `Sort-Object -Property PM -Descending`。
7. 点击 Save 按钮，点击 Console Pane，然后点击 Run (F5) 按钮。验证结果，根据需要进行修正，并重复此步骤。
8. 为了在下一行继续脚本，在第 2 行末尾添加 `|`。
9. 为了排除与 PowerShell 相关的进程，在第 3 行输入 `Where-Object $_ProcessName -ne 'powershell_ise'`。
10. 重复步骤 7。
11. 为了在下一行继续脚本，在第 3 行末尾添加 `|`。
12. 将报告限制前 10 个进程，在第 4 行输入 `Select-Object -First 10`。
13. 重复步骤 7。
14. 为了在下一行继续脚本，在第 4 行末尾添加 `|`。
15. 为报表指定属性，在第 5 行输入 `Format-Table -Property ProcessName, PM`。
16. 重复步骤 7。
17. 为了在下一行继续 cmdlet，从第 5 行删除 PM。
18. 为了缩放内存值，输入 `@{Label="PM (MB)";Expression={$_.PM/1MB}}`。
19. 重复步骤 7。
20. 关闭 PowerShell ISE。
21. 要关闭虚拟机，点击 Start，点击 Power，然后点击 Shut Down 按钮。
22. 等待片刻让 Windows 10 虚拟机完全关闭。

```powershell
@{Label="PM (MB)";Expression={$_.PM/1MB}}
```

# 脚本脚本

在 PowerShell 中构建和测试时，你可能会遇到错误，或对 PowerShell 如何得出特定结果感到困惑。本节介绍了一些你可以解决问题的工具。

## 清晰输入

在 PowerShell 中清晰输入将节省你的时间并减少沮丧。考虑这一点：如果输入清晰，PowerShell 有可能正确解释。以下建议可以使你的脚本对其他用户更易读，并减少 PowerShell 误解你的 cmdlet 的概率：

- 将每个单词的首字母大写，其余字母小写。例如，`Get-ChildItem` 遵循此约定。
- 确保在 cmdlet 和第一个属性之间、属性和值之间放置空格。额外的空格会混淆 PowerShell。考虑以下格式：
  - `Get-Process | Sort-Object -Property PM`
- 延续行是另一回事。可以在 cmdlet 之间通过 `|` (管道) 终止行。
- 你可以使用反引号键 (`` ` ``) 在参数之间拆分 cmdlet。反引号位于 Esc 键下方。
- 清晰输入看起来很专业！

## 解释错误

构建和运行脚本时遇到错误是不可避免的。在 PowerShell 中，你会看到解析显示中的红色文本来指示错误。PowerShell 错误消息指出了执行命令中问题所在的位置。可疑文本会被报告出来，并紧接着是对问题的解释，如图 10-27 所示。

错误信息几乎总是包含 PowerShell 无法解释你的 cmdlet 的行号和字符数。在图 10-27 中，注意 `Where-Object` 常用命令中拼写错误的 `wert whe-object` 被下划线。

![](img/290e46d5832f20e3707f4841e4e6d75a_496_0.png)

图 10-27 拼写 cmdlet 错误
来源：Windows10/PowerShell ISE

# 476 第 10 章在 Windows 10 和 CentOS 7 中编写脚本

以下是使用 PowerShell 和避免错误的一些规则：

- 命令行（Cmdlet）名称始终是动词和名词的组合

## 跟踪脚本

调试脚本的最简单方法之一是使用脚本级跟踪。当你开启脚本级跟踪时，执行的每条命令都会显示在 Windows PowerShell 控制台中。跟踪是开发者用于调试和完善程序的方法。通过观察这些显示的命令，你可以确定某行代码是否被执行了。要启用跟踪，请使用 `Set-PSDebug` 命令行程序并为 `-trace` 参数指定三个级别之一：

- 0-关闭跟踪。
- 1-在执行时跟踪脚本的每一行。脚本中未执行的行也会被跟踪。。此级别不显示变量赋值。
- 2-在执行时跟踪脚本的每一行。脚本中未执行的行也会被跟踪。此级别会显示变量赋值。

图 10-28 显示了跟踪信息中的语句，其中 `ProcessName` 为 `powershell_ise`。寻找以下行：

`Where-Object {$ProcessName -ne 'powershell_ise'} >>>`

![](img/290e46d5832f20e3707f4841e4e6d75a_497_0.png)

图 10-28 跟踪脚本
源：Windows 10|PowerShell ISE

## 在 CentOS 7 中创建脚本文件

![](img/290e46d5832f20e3707f4841e4e6d75a_498_0.png)

图 10-29 脚本中的逻辑错误

源：Windows 10/PowerShell ISE

图 10-29 显示了逻辑错误的结果。语句 10 应该是 `Set-Location Technology`，但脚本返回的当前目录是 `Science`而不是 `Technology`。要修正此问题，请将脚本中的语句改为 `Set-Location Technology`。

## 在 CentOS 7 中创建脚本文件

在本节中，你将学习如何构建脚本文件，并通过添加决策能力和循环结构来增强它们，以处理 CentOS 7 中的简单任务。

你在 CentOS 7 中使用 Vim 等文本编辑器编写脚本。编写良好的脚本的基本设计应包含以下部分的组件。

### 头部行

头部行是脚本的第一行。该语句指示了运行脚本的 shell 环境的类型。当你编写脚本时，应该包含一个头部行，以确保脚本在正确的 shell 下运行。例如，以下行显示了 bash 脚本的头部行：

```bash
#!/bin/bash
```

### 退出返回代码

如果一切顺利，则需要 `exit 0` 语句来结束脚本，因为脚本必须返回一个代码。返回代码 0 表示成功。

### 执行权限

当你创建和执行 shell 脚本时，必须在运行之前更改文件的权限；通常情况下，默认权限不包含执行权限。

`chmod` 命令用于修改文件的权限。以下命令将 `myScript` 设置为可执行：

```bash
chmod 755 myScript
```

你将在第 11 章中学习更多关于 Linux 权限的内容。

### 文件扩展名

与你在 CentOS 7 中看到的其他文件类型一样，脚本文件使用扩展名是可选的。然而，为了避免与其他文件类型混淆，一些系统管理员倾向于对脚本使用 `.sh` 扩展。

### 脚本参数

脚本参数可以包含你在执行批程序时需要传递给它的任何信息。参数 `$0` 到 `$9` 由空格、逗号或分号分隔。参数 `$0` 包含批处理执行时在命令行上显示的批命令名称。参数 `$1` 代表输入的第一个字符串，`$2` 代表第二个字符串，依此类推。表 10-2 列出了命令行引用参数列表。

例如，要将 `myfile1` 的内容复制到 `myfile2`（其中 `$1` 被替换为值 `myfile1`，$2` 被替换为 `myfile2`），请输入以下 `cp` 命令：

```bash
cp $1 $2
```
