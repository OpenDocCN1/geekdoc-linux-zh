
| 10/12/5.2 | target | |

| 10/12/5.2.0 | disk | TOSHIBA CD-ROM–5401TA |

| 10/12/5.7 | target | |

| 10/12/5.7.0 | ctl | Initiator |

| 10/12/6 | lan | Built-in LAN |

| 10/12/7 | ps2 | Built-In Keyboard/Mouse |

| 32 | processor | processor |

| 34 | processor | processor |

| 49 | memory | Memory |

### 3.3.2.2 Solaris prconf 命令

在 Solaris 平台上，`prconf` 命令显示系统配置信息。输出包括内存总量和格式化为设备树的系统外设。

`prconf` 命令有几个选项：

- `P` 包含伪设备的信息；默认省略有关伪设备的信息。
- `v` 指定详细模式。
- `F` 返回控制台缓冲区的设备路径（如果存在）。如果没有帧缓冲区，`prconf` 返回非零退出码。
- `p` 显示源自固件（PROM）提供的设备树信息。
- `V` 显示平台相关信息。
- `D` 对于设备树中的每个系统外设，显示用于管理该外设的设备名称。

下面的示例是在 Sun4/65 系列机器上运行命令的部分输出：

```
# /usr/sbin/prconf.conf
System configuration: Sun Microsystems sun4c
Memory size: 16 megabytes
System peripherals (software nodes):
  Sun_65
    options, instance #0
    zs, instance #0
    zs, instance #1
    fd (driver not attached)
    audio (driver not attached)
    sbus, instance #0
    dma, instance #0
    esp, instance #0
    sd (driver not attached)
    st (driver not attached)
    sd, instance #0
    sd, instance #1 (driver not attached)
    ...
    ...
    le, instance #0
    cgsis (driver not attached)
    auxiliary-io (driver not attached)
    interrupt-enable (driver not attached)
    memory-error (driver not attached)
    counter-timer (driver not attached)
    eeprom (driver not attached)
    pseudo, instance #0
```

`prconf` 命令的输出高度依赖于系统中安装的 PROM 版本。输出在任何情况下都会受到影响。

“driver not attached”（驱动未附加）信息意味着当前没有驱动程序附加到该特定设备。通常情况下，驱动程序根据需要在需要时加载和安装（并附加到硬件实例），并在设备未使用时可能被卸载和载出。

## 3.3.2.3 Solaris sysdef 命令

另一个可用于此目的的 Solaris 命令是 `sysdef`。`sysdef` 命令以表格形式输出当前的系统定义。它列出了所有硬件设备、伪设备、系统设备、可加载模块以及所选内核可调参数的值。它通过分析启动的操作系统文件（名称文件列表）并从中提取配置信息来生成输出。默认系统为 `/dev/kmem`。然而，该命令的输出对于配置基础硬件并不完全全面；它更适用于内核相关的信息。此命令可能不应是首选。

## 3.4 个人文档

UNIX 管理是一项具有挑战性的工作；它需要大量的专业知识和技能。UNIX 管理也是一项例行性工作，通过遵循要求的程序就可以成功完成任务。要安装 UNIX，必须遵循厂商的说明和建议；要配置应用程序，必须严格遵守配置规则。没有发挥发挥的空间；不当的设置是系统不稳定及所有相关问题的主要原因。软件 Bug 是我们错误行为的良好借口，但它们很少是我们所经历的问题的真实原因。

正确地配置系统并确保所有设置都正确并不是一项易事。通常有许多我们必须注意的小细节。如果我们只是偶尔处理这些小问题，很容易忘记它们。对系统能做的每件事都做笔记对未来的工作将非常有帮助；此类笔记在关键时刻可以成为救命稻草。这些时刻总是充满压力，管理员必须快速、准确地行动。没有比遵循你自己的、过测试和证明的笔记更好的建议了。

许多管理员会重复执行许多操作；在不同的机器上安装相同的 UNIX 版本、在相同的网络环境中配置主机、多次设置应用程序软件等，都是很常见的。任何你之前做的关于自己的笔记都可能非常有帮助；任务之间的时间间隔可能长到让你忘记许多重要细节。

由于将通过大量的个人文档来建立体系；这是你的“知识数据库”，对于高效工作非常重要。你对自己的文档的熟悉程度将高于任何厂商提供的文档。不需要担心风格、语法或语言——只要它们显式且清晰，你就能理解自己的任务。

成功进行 UNIX 管理的关键在于良好的组织能力。系统管理基于他人设计的规则：不同的配置文件具有不同的格式和语法。每一个要求的字母、数字、点、破折号或任何字符都必须完全遵守——没有很大的选择自由。UNIX 管理员不能发明另一套配置规则，即使这些规则看起来并不符合逻辑或不方便。它根本行不通。过去的经验可以节省时间并让一切变得更容易；复制一个可行的程序绝对比重新发明已经做过的东西要高效得多。

在大多数情况下，UNIX 管理也是一项团队任务。需要许多 UNIX 管理员（以及 NT 管理员、帮助热线人员等）来支持大型公司网络。那么，一个重要问题是如何让他们的集体工作高效。一个逻辑上的解决方案是将所有个人文档合并，并让所有团队成员可以使用这些文档。然而，这项工作的组织至关重要。

一种非常高效的方法是将所有文档可用，并在公司网络上组织到个人的个人文档中，创建大量的公司内部特定文档，并让所有相关人员都能访问这些文档。通过将这些文档发布在内部网站上（如有必要，为此目的创建一个内部网站），每个人都能获得有关任何描述的主题的必要信息。文档保持开放，可进行任何更新或更改。为了防止潜在欺诈，对文档的访问应仅限于管理人员。

有第三方产品提供了创建内部知识数据库的工具；在大多数情况下，它们也提供其他功能。然而，它们可能昂贵，有时操作起来太复杂。创建自己的基于 Web 的文档系统是简单、廉价且高效的。

## 3.5 Shell 脚本编程

Shell 编程是 UNIX 管理最强大的部分之一。这也是来自 UNIX 管理员整体成功声明的关键要素之一。UNIX 管理员热爱 Shell 编程。这一权威陈述源于：Shell 编程提供了一个极其强大的工具，用于自定义和自动化你的 UNIX 系统，并让许多手动管理活动变得更简单。

直观且色彩丰富的用户界面（GUI）对于复杂的管理操作听起来具有挑战性。然而，GUI 操作对我们来说是隐藏的。当一切进展顺利时，GUI 非常棒，但一旦开始故障就会非常令人沮丧。当 GUI 因为底层问题而不运行时，你该怎么办？或者，你如何自动化重复的操作？在 GUI 管理中记录步骤并不是一项易事。

良好的 UNIX 管理员往往将所需的管理操作封装到相应的 Shell 脚本中，然后使用脚本代替手动操作。编写良好且经过测试的 Shell 脚本始终正常工作，即使在 UNIX 管理员压力极大的关键时刻。Shell 脚本实现中没有类型错误或拼写错误，也没有错误的命令——没有手动操作过程中频繁发生的错误。一切都以最快的方式正确地进行。简单来说，Shell 脚本是救命稻草。

还有许多理由支持密集的 Shell 编程。定时计划的脚本会根据需要多次执行相同的工作，而无需冗长的日志、电子邮件、分页或任何其他操作。我们只需要在编写脚本时花费时间，之后只需使用脚本即可。

Shell 编程是良好的 UNIX 管理的前提提。假设 UNIX 管理员熟悉 Shell 编程。本节并不是 Shell 编程的教程，而是指向可能让管理员感到困惑的 Shell 编程某些方面。

### 3.5.1 Shell

UNIX Shell 是用户与 UNIX 系统之间的接口层。如图 3.1 所示。

![849eeed37051e04ac7ecd956adb0ba2_] 图 3.1：用户 Shell 层。

有很多 Shell 变体：Bourne `sh`、Korn shell `ksh`、C shell `csh`、Bourne again shell `bash`、enchanted C shell `tsch`。某些 Shell 非常相似——例如 `ksh` 和 `bash`，`bash` 是 `ksh` 的子集——但它们通常是不通用的。在调用 Shell 脚本时，这一点很重要。

### 3.5.2 Shell 脚本

Shell 脚本是符合 Shell 编程语言的程序。Shell 脚本不是编译程序；相反，它们是可读的文本文件，在执行时由解释器读取并处理每一行命令。

```
sh# cat /tmpMyScript.sh (查看内容)
```

#### 仅测试 x 权限

```sh
ls -l /tmp/MyScript.sh  (查看权限)
-rw-r--r-- 1 root root 39 Aug 21 18:27 /tmp/MyScript.sh
```

```sh
sh# /tmp/MyScript.sh (调用 shell 脚本)
sh: /tmp/test4.sh: Permission denied
```

脚本也可以通过显式指定的 shell 来调用。在这种情况下，执行权限不是强制性的。某些 UNIX 变体在没有授予读取权限的情况下也能执行脚本。

```sh
sh# /bin/sh /tmp/MyScript.sh
Just a test of permission
```

当直接调用时，shell 在当前用户 shell 的环境中执行。当前用户 shell 会被填充，然后 shell 脚本的每一行命令都由 shell 解释器处理（已经讨论过程序的 fork--exec 启动）。如果两种 shell 变体不匹配（脚本和父 shell —— 例如在 `csh` 环境中调用 `bash` 脚本），即使对于一个基本正确的脚本，也会遇到很多错误。

以下示例展示了不同的情况。在 `bash` 和 `csh` 环境中调用名为 `myscript.bash` 的任意脚本：

```bash
bash# cat /tmp/myscript.bash
######################################
# 定义变量
export TEXT1="This is a bash script myscript.bash"
export TEXT2="Running the script myscript.bash"
#
# 执行命令
echo "$TEXT1"
echo "$TEXT2"
######################################
```

```bash
bash# /tmp/myscript.bash
This is a bash script myscript.bash
Running the script myscript.bash
```

```bash
bash# /bin/csh (切换到 csh)
csh# /tmp/myscript.bash
export: Command not found.
export: Command not found.
TEXT1: Undefined variable.
```

上述问题情况可以通过两种方式避免。首先，正如我们之前提到的，脚本可以通过显式指定的 shell 来调用：

```bash
bash# /bin/bash /tmp/myscript.bash (这里 shell 匹配)
This is a bash script myscript.bash
Running the script myscript.bash
```

```bash
csh# /bin/bash /tmp/myscript.bash (这里 shell 不匹配)
This is a bash script myscript.bash
Running the script myscript.bash
```

或者可以在脚本本身中隐式指定 shell。脚本的第一行格式为 `#!/bin/shellname` —— `'/bin/shellname'` 标识了所需 shell 的完整路径，该 shell将被调用，然后在该 shell 环境中执行脚本。记住，它是任何其他可执行程序，而不一定是 shell。然而，我们假设它是 shell。以下是示例：

```bash
cat /tmp/myscript1.bash
#!/bin/bash
#######################################
# 定义变量
TEXT1="This is a bash script myscript1.bash"
TEXT2="Running the script myscript1.bash"
#
# 执行命令
echo "$TEXT1"
echo "$TEXT2"
#######################################
```

```bash
/tmp/myscript1.bash
This is a bash script myscript1.bash
Running the script myscript1.bash
```

```bash
csh /tmp/myscript1.bash
This is a bash script myscript1.bash
Running the script myscript1.bash
```

在所有示例中，当前 shell 都会产生自身或另一个 shell，在两个 shell（当前用户的 shell 和被调用的 shell）之间建立“父子关系”。然而，shell 脚本也可以直接在用户的环境中执行。为了实现这一目的，必须对脚本进行“source”。使用特殊命令来 source 脚本。

```sh
source myscript.sh # 用于 csh 和类 csh shell
.myscript.sh # 用于 ksh, bash 和 Bourne shell
```

`source` 一个 shell 意味着跳过用户 shell 的启动，直接在用户的环境中执行脚本。

### 3.5.2.2 Shell 变量

我们可以在 shell 中定义和重新定义环境。通过调用一个新的 shell 脚本，当前环境会被传递，并创建一个新的初始 shell 环境。记住，这是单向传递，从父 shell 向子 shell（子 shell 继承父的环境）；反之是不可能的。关于 shell 变量，只有全局（即导出的）变量可以被继承；局部变量始终保留在当前环境中，并在 shell 终止时消失。这对于 UNIX 管理的初学者来说有时听起来很困惑。

从这个角度来看，我们可以更好地理解 shell 命令 `source` 的需要和目的。如果我们想在一个脚本内定义一个 shell 环境（我们称之为环境定义脚本），然后在其他 shell 脚本之间共享这些定义，我们必须 `source` 环境定义脚本。否则，所有的定义将只持续到环境定义脚本执行结束为止。下面的示例说明了这种情况。

用户的 shell 是 Bourne shell。变量 `VARA` 和 `VARB` 未定义。

```sh
sh# echo $VARA # 检查 $VARA 是否定义
sh# echo $VAR # 检查 $VAR 是否定义
```

脚本 `/tmp/myscript.sh` 定义了全局变量 `VARA` 和 `VARB`：

```sh
sh# cat /tmp/myscript.sh
# 变量定义
#################
VARA="Variable"
VARB="Variable"
export VARA VARB
#################
```

在脚本执行后，变量 `VARA` 和 `VARB` 是未定义的（注：此处根据上下文逻辑，变量应为定义）。

Here Document（在此文档）允许在 shell 脚本中以非交互方式执行非 shell 和非 UNIX 命令。它被频繁用于将 SQL、FTP 以及其他命令序列注入到 shell 环境中。遗憾的是，Here Document 不支持交互式过程——前一个命令一完成，就会立即提交下一条命令行。通常，shell 编程的主要缺点是它在非交互状态下无法进行交互。为了这一目的，需要使用 Expect 或 Perl 补丁。

Here Document 使 shell 脚本编程变得更简单、更强大。更多详细信息请参阅第 21 章中的 FTP 示例。

### 3.5.2.5 小贴士

在对 shell 编程主题的简要概述结束之际，关于使用 shell 脚本有以下建议：

- shell 脚本会继承调用者的环境，通常是用户的 shell。然而，对于初始环境的设置没有规定。在脚本之外定义的所有内容都是不定的，包括脚本中执行的命令的搜索路径。以下是一些良好的建议：
  - 在脚本中定义 `PATH` 变量。
  - 或者，使用全路径的命令名。
- 从命令行运行经过充分测试的 shell 脚本时，将其作为 `cron` 任务运行的情况非常常见。原因很简单：`cron` 环境被精简为几个默认值，通常不足以实现脚本的成功执行。
- 始终清理 shell 脚本创建的所有临时文件。每个文件都归创建者所有，残留的临时文件可能会成为其他脚本调用者的障碍。
- 注意标准输出和错误输出。shell 脚本通常也会在后台运行。

## 第 4 章：系统启动与关机

## 4.1 导言

UNIX 系统在正常情况下持续运行。关闭和断电 UNIX 系统不应该经常执行，通常只在进行硬件升级或分配系统时，或者偶尔在执行其他需要关机的操作时进行。在现实生活中，系统关机更为频繁，因为会发生不可预测的情况。
