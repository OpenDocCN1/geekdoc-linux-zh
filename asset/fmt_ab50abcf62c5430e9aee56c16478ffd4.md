
该命令更新所有已安装软件包的基础 `pacman` 命令。其他软件包管理器遵循相同的原理。它们遵循与 `pacman` 相同的步骤来安装和删除软件包。区别在于它们的名称和命令行参数。

表 4-1 显示了不同 Linux 发行版中操作软件包的命令。

### 表 4-1. 操作软件包的命令

| 命令 | MSYS2 和 Arch Linux | Ubuntu | CentOS | Fedora |
|---|---|---|---|---|
| 下载软件包索引 | `pacman -Sy` | `apt-get update` | `yum check-update` | `dnf check-update` |
| 通过关键字查找软件包 | `pacman -Ss KEYWORD` | `apt-cache search KEYWORD` | `yum search KEYWORD` | `dnf search KEYWORD` |
| 从仓库安装软件包 | `pacman -S PACKAGE_NAME` | `apt-get install PACKAGE_NAME` | `yum install PACKAGE_NAME` | `dnf install PACKAGE_NAME` |
| 从本地文件安装软件包 | `pacman -U FILENAME` | `dpkg -i FILENAME` | `yum install FILENAME` | `dnf install FILENAME` |
| 移除已安装的软件包 | `pacman -Rs PACKAGE_NAME` | `apt-get remove PACKAGE_NAME` | `yum remove PACKAGE_NAME` | `dnf erase PACKAGE_NAME` |
| 更新所有已安装软件包 | `pacman -Syu` | `apt-get upgrade` | `yum update` | `dnf upgrade` |

# 结语

我们完成了对 Bash 的介绍。我们只涵盖了该语言的基础知识。本书将许多主题排除在范围之外，这些主题对于高级 Bash 开发是必须的。很可能，你在日常计算机工作中并不需要它们。

如果你想深入学习 Bash，这些高级主题可能会很有趣：

- 字符串操作³。
- 正则表达式⁴。
- 流编辑器⁵。
- `awk` 文本处理语言⁶。

这些主题非常重要。它们是进阶学习的素材。如果你只是用 Bash 执行简单任务和基础自动化，可以跳过它们。如果你打算用 Bash 编写复杂的应用程序，请学习这些主题。

也许你喜欢编程。你发现它很有用。读完这本书后该做些什么？

首先，让我们承认 Bash 并不是一种通用编程语言。该术语指的是用于在各个领域³开发应用程序的语言。这类语言不包含那些在某领域有用而在另一个领域无用的构造结构。

Bash 是一种领域特定语言⁷。这意味着它没用处吗？不，并不是。Bash 是软件开发人员强大的辅助工具。今天，它被用于集成大型项目、构建软件和自动化常规任务。你不会发现一个仅用 Bash 编写的商业项目。这种语言很好地处理了它被创造的任务。但在许多领域，它不如现代通用语言。

没有人仅仅为了好而创造编程语言。它的作者面临某些任务。当时存在的语言不适合解决这些任务。于是这位开发者编写了专注于特定任务的新语言。因此，现代通用语言在某些领域内具有优势。没有一种语言能完美适应任何类型的任务。这导致了由应用来决定软件开发的语言。

所以，你已经读完了这本书。现在是时候选择你感兴趣的领域了。阅读互联网上的文章。思考一下：软件开发的哪个领域适合你？只有在回答了这个问题之后，再选择一种编程语言进行学习。

³⁶⁶⁵https://tldp.org/LDP/abs/html/string_manipulation.html
³⁶⁶⁶https://tldp.org/LDP/abs/html/x31729.html
³⁶⁶⁷https://tldp.org/LDP/abs/html/x23170.html
³⁶⁶⁸https://tldp.org/LDP/abs/html/awk.html
³⁷⁰https://en.wikipedia.org/wiki/Domain_(software_engineering)
³⁷⁰https://en.wikipedia.org/wiki/Domain-specific_language

### 表 5-1. 软件开发的应用领域

| 领域 | 编程语言 |
| --- | --- |
| 移动应用 | Java, C++, JavaScript |
| Web 应用（前端） | JavaScript, PHP, CSS, SQL |
| Web 应用（后端） | JavaScript, PHP, Ruby, C#, Go |
| 高负载系统 | C++, Python, Ruby |
| 运维管理 | Bash, Python, Ruby |
| 嵌入式系统 | C, C++ |
| 机器学习与数据分析 | Python, Java |
| 信息安全 | C, C++, Bash |
| 企业级软件 | Java, C++, SQL |
| 视频游戏 | C++ |

仅仅了解一种编程语言不足以成为高级开发人员。有必要了解特定领域中所使用的技术。例如，信息安全专家必须理解计算机网络和操作系统的架构。随着你职业发展的成长，你将理解自己需要学习的技术。

假设你已经选择了你的应用领域和编程语言。现在是时候参加免费课程了。这本书向你介绍了编程的基础。因此，学习新语言将会进展得快。Python 或 C++ 的语句对你来说将很熟悉。然而，这些语言拥有你必须从零开始学习的概念。不要失去你的动力。将新知识付诸实践并从错误中学习。这是获得结果的唯一途径。

¹https://en.wikipedia.org/wiki/Mobile_app
²https://en.wikipedia.org/wiki/Web_application
³https://en.wikipedia.org/wiki/Front_end_and_back_end
⁴https://en.wikipedia.org/wiki/Web_application
⁵https://en.wikipedia.org/wiki/Front_end_and_back_end
⁶https://en.wikipedia.org/wiki/Server
⁷https://en.wikipedia.org/wiki/System_administrator
⁸https://en.wikipedia.org/wiki/Embedded_system
⁹https://en.wikipedia.org/wiki/Machine_learning
⁸https://en.wikipedia.org/wiki/Data_Analysis
¹https://en.wikipedia.org/wiki/Information_security
²https://en.wikipedia.org/wiki/Enterprise_software
³https://en.wikipedia.org/wiki/Video_games

# 结语

我希望你从书中中学到了一些新知识，并在阅读过程中过得愉快。如果你喜欢这本书，请与你的朋友分享。如果你愿意花几分钟在 Goodreads 上写写评论，我将不胜感激。

如果你对这本书有任何问题或建议，请写信至 `petrusm@gmail.com`。也可以在书籍 GitHub 仓库的“Issues”部分提问。

感谢阅读《从零开始学 Bash 编程！》

# 致谢

没有人独自写书。几个人帮助我完成了这本书。其中一些人提出了总体想法。另一些人给了我意见和建议。这些是我感谢的人。

感谢 Sophia Kayunova 对学习编程的愿望。这引发了我编写一本编程指南的想法。

感谢 Vitaly Lipatov 向我介绍了 Linux 和 Bash。他为我的专业技能奠定了基础。

感谢 Ruslan Piasky 在 Bash 方面的咨询。他向我解释了语言的惯用法和陷阱。

同时也感谢所有支持并激励我完成工作的人。

## 术语表

### A

**抽象 (Abstraction)** 是模拟对象属性的软件模块、应用程序或库。抽象有助于管理复杂性。它们隐藏了无关细节。抽象允许相同的算法处理不同的对象。

**算法 (Algorithm)** 是执行器理解的有限指令序列。算法的目标是计算某些内容或解决任务。

**别名 (Alias)** 是用于简化字符串的 Bash 内命令。它在 shell 模式运行时。

**应用程序编程接口 (API)** 是信息系统组件交互的一组约定。这些约定回答了以下问题：

- 调用组件执行什么函数
- 函数需要什么输入？
- 函数返回什么输出？

**参数 (Argument)** 是程序通过命令行界面接收的单词或字符串。这是 `grep` 工具的参数示例：

```
grep "GNU" README.txt
```

**算术扩展 (Arithmetic expansion)** 计算算术表达式并将其结果替换到 Bash 命令或语句中。这是一个扩展的示例：

```bash
echo $((4+3))
```

**数组 (Array)** 是由一组元素组成的数据结构。序列号或索引决定每个元素的位置。数组元素逐个存放在计算机内存中。

**ASCII** 是一种八位字节字符编码。它包含以下字符：

## 术语表

- 十进制数字
- 拉丁字母
- 国家字母表
- 标点符号
- 控制字符

异步（¹³⁹⁷）指独立于主程序执行流发生的事件。异步指的是处理此类事件的方法。

### B

后台（Background¹⁹⁶）是 Bash 中的一种进程执行模式。当激活时，进程标识符不属于终端的标识符组¹⁹⁷。此外，执行的进程不会处理键盘中断。

`Bash`¹⁹⁸（Bourne again shell）是由 Brian Fox 开发的命令行解释器。Bash 已经取代了 Linux 发行版和某些专有 Unix 系统中的 Bourne shell。Bash 兼容 POSIX 标准。然而，该标准并不包含该解释器的一些特性。

Bash 脚本¹⁹⁹是一个包含解释器命令的文本文件。Bash 以非交互模式执行脚本。

最佳实践（Best practices²⁰⁰）是使用编程语言或技术的推荐方法。Bash 最佳实践的一个示例是将字符串括在双引号中以避免单词拆分。

瓶颈（Bottleneck²⁰¹）是计算机系统中限制其性能或吞吐量的组件或资源。

布尔表达式²⁰²是一种编程语言。执行时，它会产生“真”或“假”值。

Bourne shell²⁰³是由 Stephen Bourne 开发的命令行解释器。它取代了原始的 Thompson's shell²⁰⁴。POSIX 标准²⁰⁵包含了 Bourne shell 的所有特性。该 shell 缺少了危险中的某些特性。

> ¹⁹⁹ https://en.wikipedia.org/wiki/Asynchrony_(computer_programming)
¹⁹⁷ https://www.gnu.org/software/bash/manual/html_node/Basic-Controls.html#Job-Controls
¹⁹⁸ https://en.wikipedia.org/wiki/Process_group
¹⁹⁹ https://en.wikipedia.org/wiki/Bash_(Unix_shell)
²⁰⁰ https://www.gnu.org/software/bash/manual/html_node/Shell-Scripts.html#Shell-Scripts
²⁰⁰ https://github.com/wiki/Guide/Practices
²⁰¹ https://en.wikipedia.org/wiki/Bottleneck_(software)
²⁰² https://en.wikipedia.org/wiki/Boolean_expression
²⁰³ https://en.wikipedia.org/wiki/Bourne_shell
²⁰⁴ https://en.wikipedia.org/wiki/Thompson_shell
²⁰⁵ https://en.wikipedia.org/wiki/POSIX
²⁰⁶ https://en.wikipedia.org/wiki/Version_7_Unit
²⁰⁷ https://pubs.opengroup.org/onlinepubs/9699917999/V3_chap02.html

大括号扩展（Brace expansion^{367}是 Bash 的一种从给定部分生成单词的机制。POSIX 标准缺少这一机制。
以下是大括号扩展的示例：

```
cp test.{{txt,md,log} Documents
```

它生成了以下命令：

```
cp test.txt test.md test.log Documents
```

内置命令（Builtin commands^{368}是解释器自行执行的命令。它不会为此调用实用程序或程序。例如 `pwd` 内置命令。

### C

子进程（Child process^{36⁹}是由另一个进程（称为父进程）产生的进程。

代码风格（Code style^{3⁷⁰}是编写程序源代码的规则和约定。这些规则有助于多个程序员编写、读取和理解通用的源代码。

命令是在输入命令提示符后输入的文本。它匹配解释器通过其自身或另一个应用程序所执行的操作。

命令行参数（Command-line parameter^{3⁷¹}是命令参数的一种类型。它向程序传递信息。参数也可以某些选项的一部分。例如，它指定了程序运行的选模式。
以下是 `find` 实用程序的调用：

```
find ~/Documents -name README
```

第一个参数 `~/Documents` 指定搜索路径。第二个参数 `README` 指选项 `-name`。它指定了要搜索的文件或目录。

命令提示符（Command prompt^{3⁷²}是一个字符序列。当 shell 准备好处理用户的命令时会打印提示符。

命令替换（Command substitution^{3⁷³}是 Bash 的一种机制，用命令的输出替换调用。以下是一个示例：

```
echo "$(date)"
```

> 367} mywiki, woodge/BraceExpansion
368} https://www.gnu.org/software/bash/manual/html_node/Shell-Builtin-Commands.html
369} https://en.wikipedia.org/wiki/Child_process
370} https://en.wikipedia.org/wiki/Programming_style
371} https://stackoverflow.com/a/3649540/6562278
372} https://www.gnu.org/software/bash/manual/html_node/Controlling-the-Prompt.htmlControlling-the-Prompt
373} https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.htmlCommand-Substitution

编译器（Compiler^{⁴¹⁴}）是将编程语言的源代码翻译为机器码的程序。

计算机程序（Computer program^{⁴¹⁵）是计算机可以执行的指令集。每个程序解决一个应用任务。

条件语句（Conditional statement^{⁴¹⁶是编程语言的一种结构。它根据布尔表达式的结果执行一个命令块。

控制字符（Control character^{⁴¹⁷）是一个字符。

控制流（Control flow^{⁴¹⁸）是程序执行的顺序。

### D

字节序（Endianness^{⁴¹⁹）是计算机使用的字节顺序。有两种常用的选项：大端和小端。这里是一个示例：

```
0A big-endian

0D little-endian
```

环境变量（Environment^{⁴²⁰是一组变量。如果你调用 `env` 实用程序它会打印所有。

易错的（Error-prone^{⁴²¹是技术的定义。解决方案在某些情况下有效，但在某些输入时会导致错误。

>414$ https://en.wikipedia.org/wiki/Compiler
415$ https://en.wikipedia.org/wiki/Computer_program
416$ https://en.wikipedia.org/wiki/Conditional_(programming)
417$ https://en.wikipedia.org/wiki/Control_character
418$ https://en.wikipedia.org/wiki/Control_flow
419$ https://en.wikipedia.org/wiki/Endianness
420}$ http://my.org/Environment

转义序列（Escape sequence^{⁴²二是一组没有自身的字符。相反，它们控制输出设备。例如，换行符 `\n` 命令输出设备开始新行。

退出状态（Exit status^{⁴²³是命令完成时返回的 0 到 255 之间的整数值。零状态表示命令执行成功。所有其他代码表示错误。

### F

文件描述符（File descriptor^{⁴²⁴是指向文件或通信通道（流、管道或网络套字）的抽象指针）。描述符是 POSIX 接口的一部分。它们是非负整数。

文件名扩展（Filename expansion^{⁴²⁵是 Bash 的一种替换模式的机制。模式包含通配符：`?`、` * `、`[`。这里有一个示例：

```
rm -rf *
```
