
## 未实现
- afs.syscall
- break
- gotty
- lock
- mpx
- prof
- quotactl
- sstty
- ustat

## 已过时
- oldfstat
- oldlstat
- oldstat
- oldolduname
- olduname

## 隐藏接口
目前，我的系统的内核调度表中有二十八个条目，它们并不能精确映射到运行时库中的某个子例程。其中一些条目是在运行时库中的例程完成大量计算之后被调用的。另一些条目在发布新的运行时库之前处于隐藏状态，但在此之前开发人员可以直接使用它们。

# 附录 C

# 人物简介

- **Gordon Bell** —— DEC 公司工程副总裁。在 DEC 工作期间，他在 PDP-11 和 VAX-11 系列计算机的开发过程中发挥了重要作用。尽管 DEC 对这些系统上的 Unix 支持有限，但这些系统仍是 Unix 开发的基础，这一地位持续了 15 年以上。

- **Stephen R. Bourne** —— Bourne Shell 的作者。令 Unix 爱好者感到困惑的是，贝尔实验室曾有两位“Stephen R. Bourne”。一场趣味测验曾要求参赛者说出其中一人的电话号码。

- **Fred Brooks** —— OS/360 项目的负责人，《人月神话》一书的作者，该书是对大型软件产品开发的一部评述。布鲁克斯博士目前参与北卡罗来纳大学的虚拟现实系统研究。

- **John Lions** —— 出版了一本考察早期 Unix 系统内核的书籍，该书由新南威尔士大学出版，供操作系统理论专业的学生使用。这本书的副本被广泛分发。

- **Dennis Ritchie** —— 贝尔实验室的 Unix 创建者。他的名字通常与 Ken Thompson 的名字并列。如果非要区分两者的话，Ritchie 更倾向于语言设计，而 Thompson 则更倾向于内核设计。

- **Richard Stallman** —— 自由软件基金会创始人，旨在推广创建和分发不受商业限制的软件。FSF 支持 GNU 软件。

- **Andrew Tannenbaum** —— Minix 的作者。这个操作系统是 Linux 诞生的火花。坦嫩鲍姆博士是荷兰阿姆斯特丹自由大学的教职人员。

- **Ken Thompson** —— Unix 创建者。参见 Dennis Ritchie 的条目。

- **Linus Torvalds** —— Linux 内核的作者。Linux 系统源于 Torvalds 学习如何使用 Intel 386 内存管理在虚拟内存系统中的努力。

- **Alan Turing** —— 计算理论先驱。在参与 Enigma 项目期间，图灵对计算分析做出了重大贡献。他创造的通用机为整个研究领域奠定了基础。

# 附录 D

# 时间线

- 1991年1月 - Linus Torvalds 获得一台 386 电脑
- 1991年4月 - Linus 开始对探索 386 的任务切换能力感兴趣
- 1991年7月3日 - Linus 在 comp.os.minix 询问 POSIX 规范
- 1991年10月5日 - 在 comp.os.minix 宣布 0.02 版本可用
- 1991年12月 - 0.11 支持需求加载、代码共享、更好的驱动程序、自举支持（Linux 上的 gcc）
- 1991年12月 - 0.11+VM（有限分发）
- 1992年1月5日 - 0.12 虚拟内存，Ted Ts'o 添加了作业控制
- 1992年3月 - 0.95
- 1992年4月 - NetNews comp.os.linux 成立
- 1992年9月 - Hamish Macdonald 开始 Amiga A3000 移植工作
- 1992年8月1日 - 0.97
- 1992年8月25日 - 0.97p12 Ross Biro 的 TCP/IP/以太网 beta 版本
- 1992年10月（日期不详） - 0.98
- 1992年12月13日 - 0.99
- 1993年6月 - A3000 移植版本发布
- 1993年6月 - 0.99p110 包含 Net-2 代码
- 1993年秋 - CD-ROM Vgddrasil - 首个商业发行版。
- 1993年末 - Knor 发起 Atari 移植
- 1993年12月 - CD-ROM Morse Telecommunications `Winter'93'`
- 1994年1月31日 - Amiga 0.7
- 1994年2月 - Atari，Amiga 移植的第一个补丁
- 1994年3月14日 - 1.0
- 1994年3月 - Atari，Amiga 移植的第二个补丁
- 1994年4月 - Amiga 0.08plxx
- 1994年4月 - Atari，针对 Amiga 0.08pl2 的第三个补丁
- 1994年4月 - Atari Falcon 启动成功
- 1994年5月 - CD-ROM Morse Telecom. 升级 `Winter '93'`；1994年6月 - Slackware 2.0.0 发布
- 1994年6月 - CD-ROM (2) 套件 InfoMagic 开发者资源
- 1994年6月 - CD-ROM Morse Telecom. 带手册的 Slackware 2.0
- 1994年6月22日 - Atari 0.01pl3
- 1994年夏 - CD-ROM Red Hat 预览版（或 Beta 版）
- 1994年7月21日 - Amiga/Atari 版本 0.9
- 1994年7月29日 - Amiga/Atari 版本 0.9pl1
- 1994年8月 - CD-ROM (2) 套件 Walnut Creek Linux 工具包
- 1994年10月 - CD-ROM (2) 套件 InfoMagic 开发者资源
- 1994年秋 - CD-ROM Red Hat 万圣节版
- 1994年11月 - Atari 帧缓冲和 X11
- 1994年12月 - CD-ROM (3) 套件 InfoMagic 开发者资源
- 1995年5月24日 - Amiga/Atari 0.9pl6 发布
- 1995年3月8日 - 1.2
- 1995年3月 - CD-ROM (4) 套件 InfoMagic 开发者资源
- 1995年6月14日 - Amiga/Atari 1.2 代码与 `386 Linux` 同步
- 1995年夏 - CD-ROM Red Hat 母亲节版 1.0
- 1995年8月 - CD-ROM (4) 套件 InfoMagic 开发者资源
- 1995年8月 - SPARC - 有限的控制台、软驱、键盘、MMU 支持
- 1995年 - CD-ROM Red Hat 母亲节版 1.1
- 1995年9月 - DEC Alpha
- 1995年9月1日 - 1.3.18 的 SMP 测试版本宣布
- 1995年9月12日 - VIPER 项目宣布带有线程的内核
- 1995年9月24日 - Amiga/Atari 1.2.13pl2 发布
- 1995年9月25日 - Amiga/Atari 0.9.12 发布
- 1995年 - CD-ROM Red Hat 2.0 beta
- 1995年 - CD-ROM Red Hat 2.0
- 1995年10月2日 - 1.3.31 包含 SMP
- 1995年 - CD-ROM Red Hat 2.1
- 1995年12月 - CD-ROM (5) 套件 InfoMagic 开发者资源
- 1995年 - CD-ROM Red Hat Linux/AXP 2.1 beta

# 附录 E

# Shell 语法

## SH

```
command:
if list then list
{ elif list then list }*
{else list } fi
case word in [pattern list;]* esac

while list do list done
for name in word ; do list done
for name in $@ ; do list done

simple_command
list:
pipeline ;
pipeline ; list
pipeline & list
pipeline && list
pipeline || list
pipeline:
command
command | pipeline
```

## KSH

```
if list then list { elif list then list }*
case name in ( { word { | word } ) list ; }* esac
list:
cond;
cond; list
cond & list
cond:
pipe
pipe && cond
pipe || cond
pipe:
statement { | statement }*
```

## BASH

```
if list then list
[ elif list then list ]*
[else list] fi
case word in [ pattern [ | pattern]*) list ; ] ... esac
pipeline:
[!] command [ | command]*
list:
pipeline ;
pipeline ; list [; & or <newline>]
pipeline & list [; & or <newline>]
pipeline && list [; & or <newline>]
pipeline || list [; & or <newline>]
```

## CSH

```
if ( expr ) commands
if ( expr ) then
commands
else if ( expr2 ) then
commands
else
    commands
endif

switch ( string )
case str1:
breaksw
default:
endsw

while ( expr )
    commands
end

foreach name (wordlist)
    commands
end

expr:
== != =~ !~
<= >= < >
<< >>
+ -
* / %
{ cmd }
-[rwxoeozfd] filename
```

# 附录 F

# GNU 通用公共许可证

以下印出的是 GNU 通用公共许可证（GPL 或 Copyleft），Linux 即基于此许可证授权。此处重新刊登该许可证，旨在澄清关于 Linux 版权状况的一些混淆——Linux 不是共享软件，也不属于公有领域。Linux 内核的大部分版权 © 1993 归 Linus Torvalds 所有，而其他软件和内核的部分则由其各自的作者拥有版权。因此，Linux 受版权保护；但是，您可以按照下方印出的 GPL 条款重新分发它。

**GNU 通用公共许可证**  
版本 2，1991 年 6 月  
版权 (C) 1989, 1991 自由软件基金会，Inc. 675 Mass Ave, Cambridge, MA 02139, USA.

任何人被允许逐字复制和分发本许可证文件的副本，但禁止修改它。

### F.1 前言

大多数软件的许可证旨在剥夺您分享和修改它们的自由。相比之下，GNU 通用公共许可证旨在保证您分享和修改自由软件的自由——确保软件对所有用户都是自由的。本通用公共许可证适用于自由软件基金会的大部分软件，以及任何作者承诺使用它的其他程序。（自由软件基金会的某些其他软件则受 GNU 库通用公共许可证的约束。）您也可以将其应用于您的程序。

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保您拥有分发自由软件副本的自由（如果您愿意，可以为此服务收费），确保如果您想要源码，您能收到或获取它，确保您可以修改软件或将其中的一部分用于新的自由程序；并且确保您知道您可以做这些事。

为了保护您的权利，我们需要施加限制，禁止任何人拒绝您这些权利或要求您放弃这些权利。如果您分发软件的副本或对其进行修改，这些限制就转化为您对这些软件副本承担的一定责任。

例如，如果您分发此类程序的副本，无论是免费还是收费，您必须向接收者提供您所拥有的所有权利。您必须确保他们也能收到或获取源代码。并且您必须向他们展示这些条款，以便他们知道他们的权利。

我们通过两个步骤来保护您的权利：(1) 对软件进行版权保护，以及 (2) 向您提供本许可证，给予您复制、分发和/或修改软件的法律许可。

此外，为了每位作者和我们自身的保护，我们要确保每个人都理解，对于这款自由软件不存在保修。如果软件被他人修改并传递，我们希望接收者知道他们拥有的并非原始版本，从而防止由他人引入的问题牵连到原始作者的声誉。

最后，任何自由程序都 constantly 受到软件专利的威胁。我们希望避免一种危险：自由程序的分发者分别获得专利许可，实际上从而使程序成为专有软件。为防止这种情况，我们已明确声明，任何专利都必须授权给所有人免费使用，否则就不授权。

复制、分发和修改的精确条款和条件如下：

