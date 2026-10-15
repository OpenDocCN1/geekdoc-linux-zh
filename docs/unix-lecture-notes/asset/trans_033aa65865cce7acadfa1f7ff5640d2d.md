

```c
exit(1);

/* Get the size of the terminal window */
get_tty_size(fp_tty, &tty_rows, &tty_cols);
num_of_lines = tty_rows;

while ( fgets( line, LINELEN, fp ) ) {
    if ( num_of_lines === 0 ) {
        // reached screen capacity so display prompt
        reply = get_user_input( fp_tty ); // note call here
        switch ( reply ) {
            case SPACEBAR:
                // allow full screen
                num_of_lines = tty_rows;
                printf("\033[1A\033[2K\033[1G");
                break;
            case RETURN:
                // allow one more line
                printf("\033[1A\033[2K\033[1G");
                num_of_lines++;
                break;
            case QUIT:
                printf("\033[1A\033[2K\033[1B\033[7D");
                return;
            default: // in case of invalid input
                break;
        }
    }
    if ( fputs( line, stdout ) === EOF )
        exit(1);
    num_of_lines--;
}
```

这个版本仍然存在一些缺陷。其中之一是它在循环的每次迭代中检查终端是否已被调整大小，即在每次检索用户输入时。虽然这可行，但浪费了周期。稍后我们将学习如何异步地完成此操作，仅在终端实际被调整大小时才查找终端大小。

另一个缺陷是它仍然要求用户按下回车键。解决这个问题需要进一步理解终端，这将在第 4 章中再次介绍。我们可以轻松集成到程序中的一个功能是计算迄今为止显示的文件百分比。这留作练习。

## 1.12 我们接下来要去哪里

尝试编写更复杂的程序的真正目的是为了说明，仅使用通常的高级 I/O 库，我们无法编写出像 more 那样的程序，例如忽略键盘输入和抑制输入字符的显示。这些笔记的目标是为您提供解决此类问题的工具，并让您接触内核 API 的主要组件，同时解释内核在“内部”看起来如何。我们将查看内核的每个重要组件。您将学习如何翻阅文件系统和手册页以查找所需的资源。

## 附录 A UNIX 的简史

1957 年，Bill Norris 创立了 Control Data Corporation (CDC)。1959 年，Ken Olsen 凭借 70,000 美元的风险投资资金创立了 DEC。第一台 PDP-1（由 DEC 制造）于 1960 年出货。1963 年，Project MAC（多路访问计算机）于 MIT 组织成立，以开展交互式计算和分时系统研究。1965 年，AT&T、GE 和 IBM 的 Project MAC 联合开发分时系统 MULTICS（多路复用信息和计算服务）。

1966 年，Ken Thompson 在加州大学伯克利分校（UCB）完成学业后加入 AT&T 贝尔电话实验室的技术人员，参与 MULTICS 工作。两年后，Dennis Ritchie 在哈佛完成了博士工作并加入贝尔实验室参与 MULTICS 项目。

Thompson 开发了基于 BCPL 的解释性语言 B。Ritchie 在“B”的基础上改进并称之为“C”。

1969 年，在为 AT&T 贝尔实验室工作期间，Ken Thompson 和 Dennis Ritchie 为 DEC 制造的 PDP-7 编写了 UNICS 的第一个版本。它运行在一台具有 4K 个 18 位字的机器上。UNICS 是对 MULTICS 的戏仿，代表 Uniplexed Information and Computing Services。三年后，它被重写为 C，以便他们可以将其移植到其他架构。到 1973 年，贝尔实验室内部成立了第一个 UNIX 支持小组，一些基本的 UNIX 设计理念也随之出现。Ritchie 和 Thompson 当年在 IBM 的 ACM 操作系统研讨会上就新操作系统做了演示。这成为引发 UNIX 系统传播的催化剂。加州大学伯克利分校（UC Berkeley）很快从贝尔实验室获得了第 4 版，并着手为 UNIX 增加现代功能。

在接下来的四年里，几项事件塑造了 UNIX 的未来。AT&T 开始向大学授权。Boggs 和 Metcalfe 在帕洛阿尔托的 Xerox 发明了以太网。Bill Joy 加入 UC Berkeley 并开发了 BSD 版本 1。UNIX 被移植到非 DEC 机器上。（DEC 不愿支持 UNIX。）P.J. Plauger 编写了第一个商业 C 编译器，Doug 和 Larry Michel 成立了 Santa Cruz Operations（SCO）公司，开始为 PC 销售商业版 UNIX。

1974 年，Ken Thompson 和 Dennis Ritchie 在 CACM 上发表了“UNIX Time-Sharing System”。同年，加州大学伯克利分校（UCB）获得了 UNIX 第 4 版，Keith Standiford 将 UNIX 转换为 PDP 11/45。Kernighan 和 Plauger 的《编程风格要素》出版，AT&T 正式开始向大学授权 UNIX。

1976 年，Kernighan 和 Plauger 的《Software Tools》出版，Boggs 和 Metcalfe 在帕洛阿尔托的 Xerox 发明了以太网。

到 1978 年，UNIX 基本上已经具备了今天所见的主要功能。一年后，微软从 AT&T 许可了 UNIX 并宣布了 XENIX（甚至在发布 MS-DOS 之前）。

UNIX 迅速传播的原因是：

- 它是用高级语言（C）编写的，不像其他操作系统，因此可以轻松地从一个架构移植到另一个架构。

