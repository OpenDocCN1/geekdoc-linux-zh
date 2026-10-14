

除了解释命令外，shell 还可以用作编程语言。你可以创建包含命令的 shell 过程。Shell 过程的执行方式与你执行程序的方式相同——在 shell 提示符后的命令行上执行。

当你运行一个 shell 过程时，你当前的 shell 会创建或 **spawns** 一个子 shell。子 shell 是你当前 shell 为运行程序而创建的新 shell。因此，shell 过程执行的任何命令（例如 cd）都不会影响调用 shell。

Shell 过程提供了一种执行繁琐命令、大量或复杂的命令序列以及例行或重复任务的方法。

有关 shell 编程的更多信息，请参阅第 7.10 节。

## 7.2 C、Bourne、Korn 和 POSIX Shell 功能摘要

操作系统提供了以下具有命令执行和编程能力的 shell：

- Bourne shell (sh)

  这是一个简单且易于在编程中使用的 shell。它通常由美元符号 ($) 提示符表示。该 shell 不提供 C shell 或 Korn 和 POSIX shell 的交互式功能或复杂编程结构（数组和整数运算）。

  Bourne shell 还提供受限 shell (Rsh)。有关更多信息，请参阅第 7.2.2 节。

- C shell (csh)

  该 shell 设计用于交互式使用。它通常由百分号 (%) 系统提示符表示。C shell 提供了一些用于交互式输入命令的功能：

  - 命令历史缓冲区
  - 命令别名
  - 文件名补全
  - 命令行编辑

  有关这些功能的更多信息，请参阅第 7.2.1 节。

- Korn shell (ksh)

  该 shell 结合了 C shell 的易用性和 Bourne shell 的编程简便性。系统提示符通常是美元符号 ($) 提示符。Korn shell 提供了以下功能：

  - C shell 的交互式功能
  - Bourne shell 的简单编程语法
  - 命令行编辑
  - 最快的执行时间
  - 与 Bourne shell 的向上兼容性（即大多数 Bourne shell 程序可在 Korn shell 下运行）

有关这些功能的更多信息，请参阅第 7.2.1 节。

- POSIX shell (sh)

该 shell 符合 IEEE POSIX 标准。它与 Korn shell 非常相似。在本书中，Korn shell 和 POSIX shell 的讨论是合并的。有关此标准的更多信息，请参阅 sh(1) 和 standards(5) 参考页。

POSIX shell 是 Korn shell 的另一个名称。

### 7.2.1 有关 C 和 Korn 或 POSIX Shell 功能的更多信息

C shell 和 Korn 或 POSIX shell 提供了以下交互式功能：

- 命令历史

命令历史缓冲区存储你输入的命令，并允许你在任何时候显示它们。因此，你可以选择之前的命令，或之前的命令的部分内容，然后重新执行它们。此功能可以为你节省时间，因为它让你重用长命令而不是重新输入它们。在 C shell 中，此功能需要在 .cshrc 文件中进行一些设置；在 Korn 和 POSIX shell 中，此功能会自动提供。

- 命令别名

命令别名功能让你可以缩写长命令行或重命名命令。你可以通过为经常使用的长命令行创建别名来实现。例如，假设你经常需要移动到目录 /usr/chang/reports/status。你可以创建一个别名 status，每当你在命令行输入 status 时，它就可以将你移动到该目录。此外，别名让你可以为操作系统命令创建更具描述性的名称。例如，你可以为 mv 命令定义一个名为 rename 的别名。

- 文件名补全

在 C shell 中，文件名补全功能通过允许你输入文件名的部分内容来节省输入。当你按下 Escape 键时，shell 会为你补全文件名。有关 C shell 中文件名补全的更多信息，请参阅第 8.2.4 节。

在 Korn 或 POSIX shell 中，你可以要求 shell 显示与你输入的部分名称匹配的文件名列表。然后你可以选择

