
![](img/ba0161b65b37e94cffc801ecbacaba5e_73_0.png)

如果你来自 Windows 或 Macintosh 环境，shutdown 在想要执行操作时所接受的第二个参数可能会让你感到有些困惑。毕竟，为什么你会想要发出一条命令，让系统在稍后自行关机呢？想要这样做的主要原因在于 FreeBSD 的多用户特性。在可以供多人使用的服务器上，若没有任何警告就直接关机是不太礼貌的，这实际上相当于在用户脚下“抽走地毯”，导致他们可能在打开的文件中丢失未保存的更改等等。带延迟地发出 shutdown 命令会向所有用户发送广播消息，告知他们即将关机以及关机时间会发生。这些消息会随着关机时间临近而变得越来越频繁。这让用户有机会在实际关机前确保已保存所有打开的文件等。我们将在后面的章节中介绍如何设置延迟关机。

## Workshop

工作坊

The quiz questions are designed to test your understanding of the material covered in this hour.

测验题目旨在检验你对本小时所涵盖内容的理解。

## Quiz

测验

- 1. The command to create a new directory in FreeBSD is
- 1. 在 FreeBSD 中创建新目录的命令是
- A. `md`
- A. `md`
- B. `createdir`
- B. `createdir`
- C. `newdir`
- C. `newdir`
- D. `mkdir`
- D. `mkdir`
- E. `makedir`
- E. `makedir`
- 2. Which of the following directory names are legal? (Choose all applicable answers.)
- 2. 下面哪些目录名是合法的？（选择所有适用答案。）
- A. `mydir`
- A. `mydir`
- B. `This is a directory`
- B. `This is a directory`
- C. `"My Directory"`
- C. `"My Directory"`
- D. `_directory1`
- D. `_directory1`
- E. `-directory2`
- E. `-directory2`
- 3. The -a option to the ls command does which of the following?
- 3. ls 命令的 -a 选项执行以下哪一项？
- A. It causes all files to be listed.
- A. 它会导致列出所有文件。
- B. It shows files beginning with a period (.).
- B. 它显示以句点（.）开头的文件。
- C. All of the above.
- C. 以上全部。
- D. None of the above.
- D. 以上皆非。
- E. The ls command does not have a -a option.
- E. ls 命令没有 -a 选项。
4. The command rm * will perform which of the following actions? (Choose the best answer.)
4. 命令 rm * 会执行以下哪种操作？（选择最佳答案。）
- A. It will delete a file that is named *.
- A. 它会删除名为 * 的文件。
- B. It will delete a file that contains the * character.
- B. 它会删除包含 * 字符的文件。
- C. It will delete all the files in the current directory.
- C. 它会删除当前目录中的所有文件。
- D. It will do nothing at all because * is an illegal filename.
- D. 它什么都不会做，因为 * 是非法的文件名。
- E. rm is not a valid FreeBSD command.
- E. rm 不是有效的 FreeBSD 命令。

## Quiz Answers

测验答案

- 1. D is the correct answer. None of the other commands listed are valid FreeBSD commands.
- 1. 正确答案是 D。列出的其他命令都不是有效的 FreeBSD 命令。
- 2. A, C, and D are legal directory names. B is illegal because it contains spaces and is not quoted. E is illegal because directory names cannot begin with a dash unless quoted.
- 2. A、C 和 D 是合法的目录名。B 非法，因为它包含空格且未加引号。E 非法，因为目录名不能以连字符开头，除非加引号。
- 3. The correct answer is C.
- 3. 正确答案是 C。
- 4. The best answer is C. The * is a wildcard that will match all existing files in the directory.
- 4. 最佳答案是 C。* 是一个通配符，会匹配目录中所有现有文件。

![](img/ba0161b65b37e94cffc801ecbacaba5e_75_0.png)

## Hour 4

## 第 4 小时

## Basic UNIX Shell Use

## 基本 UNIX Shell 使用

The shell is the primary command line interface to FreeBSD. It is the principal means that the user has to communicate with the operating system. This hour covers the basics of working with the shell.

Shell 是 FreeBSD 的主要命令行界面。它是用户与操作系统通信的主要手段。本小时涵盖使用 shell 的基础知识。

In this hour, you will learn the following:

本小时你将学习以下内容：

- What the shell is and why you need it
- shell 是什么以及为什么需要它
- Different shells that are available
- 可用的不同 shell
- Working with files and directories
- 处理文件和目录
- Getting help in the shell
- 在 shell 中获取帮助
- Process management
- 进程管理
- Other basic shell commands
- 其他基本 shell 命令

## The Role of the Shell

## Shell 的作用

The primary purpose of the shell is to provide an interface through which the user can interact with the kernel. (The kernel and its configuration will be covered in Hour 10, “The FreeBSD Kernel and the Device Tree:”)

Shell 的主要目的是提供一个接口，让用户能够与内核交互。 （内核及其配置将在第 10 小时“FreeBSD 内核和设备树”中介绍：）

Basically, the kernel is the core of the operating system. It provides most of the functionality that the rest of the system needs in order to function. The user needs to be able to “talk” to the kernel in order to send commands to the operating system. However, the kernel doesn’t speak a language that is anything like any human language.

基本上，内核是操作系统的核心。它提供了系统其余部分运行所需的大部分功能。用户需要能够“与”内核“对话”以便向操作系统发送命令。然而，内核使用的语言与任何人类语言都不相似。

Attempting to communicate with the kernel in its own language would be extremely complicated and frustrating. This is where the shell comes in. The shell is basically an interpreter that understands commands in something resembling common English and translates those commands into a language the kernel can understand. The shell also accepts messages from the kernel and displays them in a language the user can understand. The shell, in effect, isolates the user from the kernel (and some would say protects the user from the kernel). The result is that normally, the user never has to deal directly with the kernel and doesn’t even have to care that it exists.

尝试用内核自己的语言与之通信将极其复杂且令人沮丧。这就是 shell 发挥作用的地方。Shell 基本上是一个解释器，它理解类似普通英语的命令，并将这些命令翻译成内核可以理解的语言。Shell 还接收来自内核的消息并以用户可以理解的语言显示出来。Shell 从本质上隔离了用户与内核（有些人会说它保护用户免受内核影响）。结果是，通常用户永远不必直接处理内核，甚至不必关心它的存在。

Figure 4.1 shows a diagram of how the kernel, shell, and system hardware relate to each other. The shell is an “abstraction layer”—it hides and protects the inner workings of the operating system from the user, in the way that the shell of a seed hides and protects its kernel from the outside world.

图 4.1 显示了内核、shell 和系统硬件之间关系的示意图。Shell 是一个“抽象层”——它隐藏并保护操作系统的内部运作不被用户看到，就像种子的外壳隐藏并保护其内核免受外界影响一样。

## FIGURE 4.1

## 图 4.1

The shell, kernel, and system hardware, using the “seed” metaphor.

使用“种子”隐喻的 shell、内核和系统硬件。

![](img/ba0161b65b37e94cffc801ecbacaba5e_76_0.png)

Windows or DOS command-line junkies will be familiar with this general concept because the FreeBSD shell is similar to the command line in Windows and DOS. (It is far less similar to the poorly named “DOS Shell” program that existed in some versions of MS DOS.)

习惯 Windows 或 DOS 命令行的用户会熟悉这一总体概念，因为 FreeBSD 的 shell 与 Windows 和 DOS 中的命令行类似。 （它与某些版本的 MS DOS 中存在的命名不佳的“DOS Shell”程序相似度要低得多。）

Windows users who do not make use of the DOS command-line feature, and Macintosh users as well, will probably be less familiar with the concept. But in a very loose sense, you can think of the graphical desktop as being similar to FreeBSD’s concept of the “shell” because it is also an abstraction layer, a user interface that isolates the user from having to deal directly with the kernel.

不使用 DOS 命令行功能 Windows 用户，以及 Macintosh 用户，可能对这一概念不太熟悉。但从很宽泛的意义上说，你可以将图形桌面视为与 FreeBSD 的“shell”概念相似，因为它也是一个抽象层，一个用户界面，它使用户不必直接处理内核。

## Different Shells Available

## 可用的不同 Shell

Unlike DOS/Windows, FreeBSD gives you a variety of different shells to choose from. The shells vary widely in the number of features they have, the ease of use for new users, and how they implement certain features. We aren't going to cover all the available shells here because there are far too many of them. However, we will cover some of the more popular ones.

与 DOS/Windows 不同，FreeBSD 为你提供了多种不同的 shell 可供选择。Shell 在功能数量、新用户易用性以及某些功能的实现方式上差异很大。我们在这里不会介绍所有可用的 shell，因为它们实在太多了。然而，我们将介绍其中一些更受欢迎的 shell。

## The Bourne Shell

## Bourne Shell

The Bourne shell (sh) is the oldest shell that is still widely used. It is named after its creator, Stephen Bourne. The Bourne shell is very primitive compared to more modern shells. It lacks advanced features like command history (the ability to recall previous commands) and command editing (the ability to edit a previously run command and run it again). FreeBSD does not include the original Bourne shell, but rather includes a shell known as the POSIX shell. The POSIX shell is an enhanced Bourne shell with complete backward compatibility with the original version, but that includes additional features such as history functions and command editing. If you don't specify otherwise, new user accounts will have POSIX as the default shell.

Bourne shell（sh）是最古老且仍被广泛使用的 shell。它以其创造者 Stephen Bourne 命名。与更现代的 shell 相比，Bourne shell 非常原始。它缺乏诸如命令历史（召回先前命令的能力）和命令编辑（编辑先前运行的命令并再次运行的能力）等高级功能。FreeBSD 不包含原始的 Bourne shell，而是包含一个名为 POSIX shell 的 shell。POSIX shell 是一个增强的 Bourne shell，与原始版本完全向后兼容，但它包含历史功能和命令编辑等附加功能。如果不另行指定，新用户账户的默认 shell 将是 POSIX。

## The C Shell

## C Shell

The C shell (csh) is so named because it was designed to have a syntax similar to the C programming language. It was developed by the University of California at Berkeley for the BSD version of UNIX. The C shell had many more features than the Bourne shell, including the ability to recall previous commands, the ability to edit and rerun previous commands, and the ability to automatically run a script of commands upon logging out of the system. (The Bourne shell could only run a script of commands upon logging in to the system.) Unfortunately, the C shell was not compatible with the Bourne shell and could not run scripts written for the Bourne shell.

C shell（csh）因此得名，因为它的语法设计得与 C 编程语言相似。它由加州大学伯克利分校为 BSD 版本的 UNIX 开发。C shell 比 Bourne shell 具有更多功能，包括召回先前命令的能力、编辑和重新运行先前命令的能力，以及在注销系统时自动运行命令脚本的能力。 （Bourne shell 只能在登录系统时运行命令脚本。）不幸的是，C shell 与 Bourne shell 不兼容，无法运行为 Bourne shell 编写的脚本。

![](img/ba0161b65b37e94cffc801ecbacaba5e_77_0.png)

> The original C shell no longer ships with FreeBSD. Instead, it has been replaced by the tcsh shell, which is an enhanced version of the C shell with additional features. The tcsh shell is explained a little later on in this hour. The default shell of the root user, or administrator, is csh—which in FreeBSD these days is the same thing as tcsh.

> 原始的 C shell 已不再随 FreeBSD 提供。取而代之的是 tcsh shell，它是 C shell 的增强版本，具有附加功能。tcsh shell 稍后在本小时中会有所解释。root 用户或管理员的默认 shell 是 csh——在当今的 FreeBSD 中，它与 tcsh 相同。

## The Korn Shell

## Korn Shell

The Korn shell (ksh or pdksh—FreeBSD uses the latter) was AT&T's response to the C shell. The Korn shell is backward compatible with the Bourne shell, so it will run any script written for the Bourne shell. However, the Korn shell adds features such as command history and editing—features that were missing from the original Bourne shell. The Korn shell is one of the most popular shells for UNIX operating systems. However, new users will probably prefer the Bash shell (discussed next).

Korn shell（ksh 或 pdksh——FreeBSD 使用后者）是 AT&T 对 C shell 的回应。Korn shell 与 Bourne shell 向后兼容，因此可以运行为 Bourne shell 编写的任何脚本。然而，Korn shell 增加了诸如命令历史和编辑等功能——这些功能在原始 Bourne shell 中是缺失的。Korn shell 是 UNIX 操作系统中最受欢迎的 shell 之一。然而，新用户可能更喜欢 Bash shell（接下来会讨论）。

## The Bash Shell

## Bash Shell

The Bash shell (bash) is short for Bourne Again Shell. This shell was developed by the Free Software Foundation; like the Korn shell, it is backward compatible with the Bourne shell. Also like the Korn shell, it includes history and command editing functions. However, Bash's history and command editing functions are more intuitive for new users than Korn's are. The Bash shell is also a very popular shell on UNIX systems today and is the standard default shell on all Linux distributions.

Bash shell（bash）是 Bourne Again Shell 的缩写。该 shell 由自由软件基金会开发；与 Korn shell 一样，它与 Bourne shell 向后兼容。与 Korn shell 一样，它也包含历史记录和命令编辑功能。然而，Bash 的历史记录和命令编辑功能对新用户来说比 Korn 的更直观。Bash shell 也是当今 UNIX 系统上非常流行的 shell，并且是所有 Linux 发行版的标准默认 shell。

## The Tcsh Shell

## Tcsh Shell

The Tcsh shell (tcsh) is an enhanced C shell. It adds features such as more intuitive command-line editing and history functions. In addition, it also includes command-line completion (the ability to automatically complete a command and save you some typing). One other feature of the Tcsh shell worth mentioning is its capability to recognize potentially dangerous commands and warn the user before carrying them out, thus giving the user a chance to abort the command. Tcsh is the default FreeBSD shell assigned to the root user. (But normal users are assigned the POSIX shell by default.)

Tcsh shell（tcsh）是增强版的 C shell。它增加了更直观的命令行编辑和历史功能等特性。此外，它还包括命令行补全（自动完成命令并为你节省输入的功能）。Tcsh shell 的另一个值得一提的功能是它能够识别潜在危险的命令并在执行前警告用户，从而给用户一个中止命令的机会。Tcsh 是分配给 root 用户的默认 FreeBSD shell。 （但普通用户默认分配的是 POSIX shell。）

## Which Shell Should You Use?

## 你应该使用哪种 Shell？

For most tasks you will do, it is not particularly important which shell you decide to use. Copying and moving files, listing directories, and running programs, for example, will work the same in all the shells. In this chapter and the next one, we will be working primarily with the Bash shell because it is one of the most popular shells, one of the most powerful, and also one of the easiest for new users to work with.

对于你将要执行的大多数任务，选择哪种 shell 并不是特别重要。例如，复制和移动文件、列出目录以及运行程序在所有 shell 中都是一样的。在本章和下一章中，我们将主要使用 Bash shell，因为它是 shell 中最受欢迎的之一，也是功能最强大的之一，同时也是新用户最容易使用的之一。

![](img/ba0161b65b37e94cffc801ecbacaba5e_78_0.png)

> One other reason to choose the Bash shell or some other Bourne compatible shell is that if you ever decide you want to do shell programming, these shells are a lot better candidates for shell programming than the C based shells are. You can, of course, use one shell for interactive use and a different one for programming use. But this can sometimes result in confusion because both shells handle certain tasks in different ways.

> 选择 Bash shell 或其他 Bourne 兼容 shell 的另一个原因是，如果你以后决定要进行 shell 编程，这些 shell 比基于 C 的 shell 更适合进行 shell 编程。当然，你可以使用一种 shell 进行交互式使用，另一种 shell 用于编程使用。但这有时会导致混淆，因为两种 shell 处理某些任务的方式不同。

