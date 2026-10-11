

b. `xwininfo` 返回的所点击窗口名称是什么？这与窗口标题栏中的名称是否一致？

c. 窗口的大小是多少？`xwininfo` 以什么单位显示这个大小？窗口的深度（depth）是多少？

d. 如何让 `xwininfo` 显示相同的信息，而无需点击窗口？

9. 找到并安装 `xeyes`。编写一条 `xeyes` 命令，显示一个宽度为 600 像素、高度为 400 像素的窗口，该窗口位于屏幕右边缘向左 200 像素、屏幕顶部向下 300 像素的位置，并且包含蓝色轮廓、红色瞳孔的橙色眼睛。（*提示*：参考 `xeyes` 的手册页。）

## 9 Bourne Again 外壳

### 本章内容

- 启动文件 … 281
- 重定向标准错误 … 284
- 编写简单的 Shell 脚本 … 286
- 作业控制 … 294
- 参数和变量 … 299
- 进程 … 314
- 历史 … 316
- 重新执行和编辑命令 … 318
- 别名 … 332
- 函数 … 335
- 控制 bash 特性和选项 … 338
- 处理命令行 … 342

本章承接第 7 章的内容。第 27 章将扩展本章内容，探讨控制流命令以及 Bourne Again Shell 编程的更高级方面。bash 的官方主页是 www.gnu.org/software/bash。bash 的信息页（info page）是完整的 Bourne Again Shell 参考文档。

Bourne Again Shell 是一个命令解释器，也是一种高级编程语言。作为命令解释器，它处理你在提示符后输入的命令行指令。当你使用 shell 作为编程语言时，它会处理存储在称为 shell 脚本的文件中的命令。与其他语言一样，shell 拥有变量和控制流命令（例如 for 循环和 if 语句）。

当你使用 shell 作为命令解释器时，你可以自定义工作环境。你可以让提示符显示当前工作目录的名称，为 `cp` 命令创建函数或别名以防止其覆盖某些类型的文件，利用关键变量改变 shell 的工作方式，等等。你还可以编写 shell 脚本来执行各种任务，从存储长而复杂的命令的单行脚本，到运行一组报告、打印它们并在任务完成后发送邮件提醒你的较长脚本。更复杂的 shell 脚本本身也是程序；它们不仅仅是运行其他程序。第 27 章提供了一些此类脚本的示例。

大多数系统 shell 脚本都是为在 Bourne Again Shell 下运行而编写的。如果你曾经需要在单用户模式下工作——例如在启动系统或进行系统维护、管理或修复工作时——熟悉这个 shell 是个好主意。

本章扩展了第 7 章中描述的 shell 的交互特性，解释了如何创建和运行简单的 shell 脚本，讨论了作业控制，介绍了 shell 编程的基本方面，讲述了历史和别名，并描述了命令行扩展。第 27 章呈现了一些更具挑战性的 shell 编程问题。

### 背景

Bourne Again Shell 基于 Bourne Shell（早期的 UNIX shell；为了避免混淆，本书将其称为*原始 Bourne Shell*），它由 AT&T 贝尔实验室的 Steve Bourne 编写。多年来，*原始 Bourne Shell* 已经得到扩展，但它仍然是许多商用 UNIX 版本提供的基本 shell。

由于其悠久且成功的历史，原始 Bourne Shell 被用于编写许多帮助管理 UNIX 系统的 shell 脚本。其中一些脚本在 Linux 中以 Bourne Again Shell 脚本的形式出现。虽然 Bourne Again Shell 包含许多原始 Bourne Shell 中未发现的扩展和特性，但 bash 保持了对原始 Bourne Shell 的兼容性，以便你可以在 *bash* 下运行 Bourne Shell 脚本。在 UNIX 系统中，原始 Bourne Shell 命名为 *sh*。在 Linux 系统中，*sh* 是指向 *bash* 的符号链接，确保需要 Bourne Shell 存在的脚本仍然可以运行。当作为 *sh* 调用时，*bash* 会尽力模拟原始 Bourne Shell。

System V UNIX 引入了由 David Korn 编写的 Korn Shell（ksh）。此 shell 扩展了原始 Bourne Shell 的许多特性并添加了许多新特性。Bourne Again Shell 的一些特性，如命令别名和命令行编辑，是基于 Korn Shell 的类似特性。

POSIX（可移植操作系统接口）相关标准家族正在由 PASC（IEEE 可移植应用标准委员会，www.pasc.org）开发。一个关于 POSIX 的全面常见问题解答（FAQ），包含许多链接，出现在 www.opengroup.org/papers/posix_faq.html。

POSIX 标准 1003.2 描述了 shell 功能。Bourne Again Shell 提供了符合此 POSIX 标准要求的功能。目前正在努力使 Bourne Again Shell 完全符合 POSIX 标准。在此期间，如果你使用 `--posix` 选项调用 *bash*，Bourne Again Shell 的行为将更紧密地匹配 POSIX 要求。

## Shell 基础

本节涵盖启动文件的编写和使用、重定向标准错误、编写和执行简单的 shell 脚本、命令的分离和分组、实现作业控制以及操纵目录栈。

### 启动文件

当 shell 启动时，它会运行启动文件来初始化自己。Shell 运行哪些文件取决于它是登录 shell、非登录的交互 shell（例如通过输入命令 bash 获得的 shell），还是非交互 shell（用于执行 shell 脚本的 shell）。要执行启动文件中的命令，你必须对该启动文件具有读权限。Fedora/RHEL 在这些文件中放置了适当的命令。本节介绍 bash 的启动文件。

### 登录 Shell

本节涉及的由登录 shell 以及使用 --login 选项启动的 shell 执行。登录 shell 本质上都是交互式的。

- /etc/profile
    Shell 首先执行 /etc/profile 中的命令。超级用户（Superuser）可以设置此文件以建立 bash 用户的系统级默认特性。
- .bash_profile
    接下来，shell 按顺序查找 ~/.bash_profile、~/.bash_login 和 ~/.profile（~ 是主目录的简写），并执行它找到的第一个文件中的命令。你可以在这些文件之一中放置命令，以覆盖 /etc/profile 中设置的默认值。
- .bash_logout
    当你注销时，bash 执行 ~/.bash_logout 文件中的命令。通常，清理会话后遗留项的命令（例如删除临时文件的命令）会放在此文件中。

### 交互式非登录 Shell

上述启动文件中的命令不会被交互式的非登录 shell 执行。然而，这些 shell 从登录 shell 继承由这些启动文件设置的变量。

- /etc/bashrc
    虽然不被 bash 直接调用，但许多 ~/.bashrc 文件会调用 /etc/bashrc。这种设置允许超级用户（Superuser）为非登录的 bash shell 建立系统级默认特性。
- .bashrc
    交互式非登录 shell 执行 ~/.bashrc 文件中的命令。通常，登录 shell 的启动文件（如 .bash_profile）会运行此文件，从而使登录和非登录 shell 都能受益于 .bashrc 中的命令。

### 非交互 Shell

之前描述的启动文件中的命令不会被非交互 shell（例如运行 shell 脚本的 shell）执行。然而，这些 shell 从登录 shell 继承由这些启动文件设置的变量。

**BASH_ENV** 非交互 shell 会查找环境变量 **BASH_ENV**（如果 shell 被作为 **sh** 调用，则查找 **ENV**），并执行该变量命名的文件中的命令。

### 设置启动文件

虽然存在许多启动文件和类型的 shell，但通常你只需要主目录中的 **.bash_profile** 和 **.bashrc** 文件。类似于 **.bash_profile** 中以下内容的命令会为登录 shell 执行 **.bashrc** 中的命令（当 **.bashrc** 存在时）。通过这种设置，**.bashrc** 中的命令将由登录和非登录 shell 执行。

```
if [ -f ~/.bashrc ]; then source ~/.bashrc; fi
```

`[ -f ~/.bashrc ]` 测试主目录中名为 **.bashrc** 的文件是否存在。有关 **test** 及其同义词 `[ ]` 的更多信息，请参阅第 889 页和第 891 页。

### 使用 **.bash_profile** 设置 **PATH**

提示 由于 **.bashrc** 中的命令可能被执行多次，并且由于子 shell 继承导出的变量，最好将添加到现有变量的命令放在 **.bash_profile** 文件中。例如，以下命令将 **home** 目录的 **bin** 子目录添加到 **PATH**（第 306 页），应该放在 **.bash_profile** 中：

```
PATH=$PATH:$HOME/bin
```

当你将此命令放在 **.bash_profile** 而不是 **.bashrc** 中时，该字符串仅在登录时添加到 **PATH** 变量一次。

在 **.bash_profile** 中修改变量允许在交互会话中做的更改传播到子 shell。相反，在 **.bashrc** 中修改变量会覆盖从父 shell 继承的更改。

以下是 **.bash_profile** 和 **.bashrc** 文件的示例。这些文件中使用的某些命令在本章后面才介绍。在任何启动文件中，你必须导出你希望子进程可用的变量和函数。有关更多信息，请参阅第 926 页的“变量的局部性”。

```
$ cat ~/.bash_profile
if [ -f ~/.bashrc ]; then
   source ~/.bashrc        # 如果本地启动文件存在则读取
fi
PATH=$PATH:.
export PS1="[\h \w \u]\\$ '  # 将工作目录添加到 PATH
                            # 设置提示符'
```

前一个 **.bash_profile** 文件中的第一个命令执行用户 **.bashrc** 文件中的命令（如果该文件存在）。下一个命令添加到 **PATH** 变量（第 306 页）。通常 **PATH** 在 /etc/profile 中设置并导出，因此无需在用户的启动文件中导出。最后一个命令设置并导出 **PS1**（第 307 页），它控制用户的提示符。

接下来是一个 **.bashrc** 文件示例。第一个命令执行 /etc/bashrc 文件中的命令（如果该文件存在）。接下来，**LANG**（第 312 页）和 **VIMINIT**（用于 **vim** 初始化）变量被设置并导出，并建立几个别名（第 332 页）。最后一个命令定义一个函数（第 335 页），该函数交换两个文件的名称。

