
```
USER, HOME, CLOBBER, LIST, TIEHASH classna, LIST, FETCH this, key, STORE this, key,
value , DELETE this, CLEAR this , EXISTS this, key , FIRSTKEY this, NEXTKEY this,
lastkey , SCALAR this , UNTIE this , DESTROY this

# 绑定文件句柄 (Tying FileHandles)

TIEHANDLE classna, LIST, WRITE this, LIST, PRINT, LIST, PRTF this, LIST, READ
this, LIST, READLINE this, GETC this, EOF this, CLOSE this, UNTIE this , DESTROY this
UNTIE this

“untie”陷阱

错误 作者

# perldbmfilter - Perl DBM 过滤器

概要
描述
filter_store_key, filter_store_value, filter_fetch_key, filter_fetch_value
过滤器
一个示例：NULL 终止问题。
另一个示例：Key 是一个 C int。

另请 作者
perpc - Perl 进程间通信（信号、命名管道、管道、安全的子进程、套接字和信号量）

描述
信号
在守护进程中处理 SIGHUP 信号
延迟信号（安全信号）
长时间运行的操作码，中断 I/O，可重启的系统调用，作为“故障”的信号，
由操作系统状态触发的信号

管道 使用 open() 进行 IPC
文件句柄
后台进程
子进程与父进程的完全分离
安全的管道打开
避免管道死锁
与另一个进程的双向通信
与自身的双向通信
套接字：客户端/服务器通信
网络结束符
互联网 TCP 客户端和服务器
Unix 域 TCP 客户端和服务器
使用 IO::Socket 的 TCP 客户端
简单客户端
Proto, PeerAddr, PeerPort
一个 Webget 客户端
使用 IO::Socket 的交互式客户端

# perfork - Perl 的 fork()

概要
描述
forked 进程行为
$$PROCESS_ID, %ENV,wait(), exit(), 打开文件、目录和网络套接字
资源限制
杀死父进程
父进程的局限性
警告
文件句柄、目录句柄、管道 open 尚未由 XSUB 维护的全局状态

# perlner - Perl 中数据和数值操作的语义

概要
描述
存储数据
数值运算符和数值转换
Perl 的数值操作

- 算术运算符，用于整数的算术运算符，其他数学运算符，位运算符，用于整数的位运算符，期望整数的操作符，期望一个
作者
另请 错误 

# perlthut - Perl 线程教程

描述
什么是线程？
线程程序模型
老板/工人
工作组
流水

- 什么是线程？线程安全模块线程基础
关于示例的说明
创建线程
等待线程退出
忽略线程
进程与线程终止
线程与数据
共享数据与非共享数据
线程陷阅：竞争
同步与控制
控制访问：lock()
线程陷阅：死锁
队列：传递数据
信号量：同步数据访问

- 基础信号量
高级信号量
等待条件
释放控制
通用线程实用例程序
我在哪个线程中？
线程 ID
这些线程是安全的吗？
正在运行的线程？
完整示例不同的线程实现性能考虑
进程作用域变更
系统库的安全性结论 另请
参考文献
介绍性文本
操作系统参考
其他参考
感谢 作者 版权

# perlport - 编写可移植的 Perl

描述
并非所有 Perl 程序都是可移植的，大部分 Perl 都是可移植的

- 问题
换行符
字节序和宽度
文件和文件系统
系统交互
命令行与文件路径
网络
进程间通信 (IPC)
外部子程序 (XS)
标准模块
时间和日期
字符集和字符编码
国际化
系统资源
风格

CPAN 测试 平台
Unix
DOS 及其衍生版本
VMS
VOS
EBCDIC 平台
Acorn RISC OS
其他 Perl



## 函数实现

Perl 函数字母顺序列表
- X, alarm, atan2, binmode, chmod, chown, chroot, crypt, dbmclose, dbmpen, dump, exec, exit, fcnt, flock, login, getpgpr, getppid, getpriority, getpwnam, getnam, getbtyna, getpwuid, gettrgrid, getbyaddsr, getprotobyn, getservbyport, getpwent, gethostent, getostbyna, gethostent, getprootent, getservent, seekdir, sethsost, setnetent, setverserv, endpent, endgrunt, endhostent, endendent, endprotent, getservock, SCALAR, SOCKET, OPTNAME, glo, gmt, ioctl FILEHANDLE, FUNCTION, link, localti, lstat, msgctl, msgget, msgnd, msgsrc, opcode, readlink, rewindir, select, semcl, semget, semop, setgrp, setopt, priority, setprio, setsock, shmcl, shget, shmrd, shift, select, socket, sockpair, stat, synkall, sysop, system, teldir, t, truncate, umask, it, wait, waitpid

支持的 Perl  (x86, ARM, IA64), HP-UX, Aix, Windows 2000, Windows XP, Windows Server 2003, Windows, Windows Server 2008, Windows 7, Cygwin, Solaris (x86, SPARC), OpenVMS, Alpha (7.2 及更高), 164 (8.2 及更高), Syian, NetBSD, FreeBSD, Debian GNU/FreeBSD, Haiku, Irix (6.5. 还有?), OpenBSD, DragonBSD, Midnight BSD, GNU Neutrino RTOS (6.5), MirOS BSD, Stratus OpenVOS (17.0 或更高), ti_f 问题可能修复也可能未修复, Syian (Series 60 v3.2 和 5 - 还有?), Stratus / OpenVOS, AIX, Android, FreeMINE EOL 平台

(Perl 5.20)

AT&T 3b1

(Perl 5.14)

Windows 95, Windows 98, Windows ME, Windows NT4

Atari MINI, Apollo Domain/OS, Apple Mac OS 8/9, Tenon Machten

支持的平台 (Perl 5.8) 另另 其他 / 贡献者

# perlocale - Perl 区域设置处理（国际化和本地化）

描述

什么是区域设置 (LOCALE)

类别 LC_NUMERIC: 数字格式，类别 LC_MONETARY: 金额格式，类别 LC_TIME: 日期/时间格式，类别 LC_MESSAGES: 错误和其他消息，类别 LC_COLLATE: 排序，类别 LC_TYPE: 字符类型，其他类别

准备使用区域设置

使用区域设置

“use locale” 语法

不在 use locale 作用域内，uselocate 的残留影响，在“use locale” 下；

setlocale 函数

查找区域设置

区域设置问题

测试损坏的区域设置

临时修复区域设置问题

永久修复区域设置问题
永久修复系统区域设置配置
修复系统 localconv
localconv 函数
I18N::Langinfo

## 区域设置类别
类别 "LC_COLLATE": 排序
类别 "LC_TYPE": 字符类型
类别 "LC_NUMERIC": 数字格式
类别 "LC_MONETARY": 金额格式
LC_TIME
其他类别

安全环境 PER_SKIP_LOCALE_INIT, PER_BADLANG, LC_ALL, LANGUAGE, _CTYPE, LC_COLLATE, LC_MONETARY, LC_NUMERIC, LC_TIME, LANG
示例

## 注意
字符串 "eval" 和 "LC_NUMERIC"
向后兼容
I18N:Collate 已弃
排序速度和内存使用的影响
免费提供的本地定义
I18n 和 l10n
一个不完美的标准
Unicode 和 UTF-8 BUG
损坏的系统

另请 历史

# perluiintro - Perl Unicode 简介

描述
Unicode
Perl 的 Unicode 支持
Perl 的 Unicode 模型
Unicode 和 EBCDIC
创建 Unicode
处理 Unicode
遗留编码
Unicode I/O
将 Unicode 显示为文本
特殊情况
高级主题
杂项
问答
十六进制表示

## 更多资源

旧版本 Perl 中的 Unicode 另请 致谢 作者、版权和许可

# perlunicode - Perl 中的 Unicode 支持

描述

重要注意事项

如果使用 feature ‘unicode_strings’ 则最安全，输入和输出层，应将你的非 ASCII、非 UTF8 Perl 脚本转换为 UTF-8，仍需使用 utf8 在脚本中启用 UTF-8，带有 BOM 标记的脚本和 UTF-16 脚本会被字符和语义自动检测

ASCII 规则对比 Unicode

当字符串升级为 UTF-8 时，正则表达式模式有额外的线程

扩展属性簇（逻辑字符）

\p{All}, \p{Alnum}, \p{Any}, \p{ASCII}, \p{Assigned}, \p{Blank}, \p{Decomposition_Type: Non_Canonical} (简写: \p{Dt=NonCanon}), \p{Graph}, \p{Horizontal}, \p{In-*}, \p{PerSpace}, \p{PerWord}, \p{Title}, \p{Print}, \p{Vert}

用户自定义字符属性
大小写方法（针对早期的黑客）

输入输出的字符编码

Unicode 正则表达式级别
[1] \u{..} 和 \x{..}, [2] \p{..}, [3] 支持最小列表，但所有 Unicode 属性（见 Unicode 字符属性），[4] \d \S \W \[:prop:], [5] 从 v5.18 开始的实验性功能（使用 []）实现了这一点，[6] \b \W, [7] 注意 Perl 在匹配中进行的是大小写折叠而非简单；[8] Perl 将 \ 视为行边界符。Unicode 指定了更多应该被解释的字符，[9] 但可以使用 :LineBreak，[10] Perl 中使用的 UTF-8 不仅允许 U+0000 到 U+FFFF，还允许 U+1FFFF

Unicode 编码

非字符代码点

代码点之外

Unicode 的安全影响

EBCDIC 下 Perl 中的 Unicode

区域设置

当 Unicode 并不发生时

“Unicode Bug”

在 Perl 中强制使用 Unicode（使用 Unicode）

将 Perl 破解到早期版本（针对严肃的黑客）
从 perl-5.6 迁移代码
与扩展的交互
速度

另请

# perlunic - 处理 Unicode 的菜谱级示例

描述
示例
0: 标准区域设置
1: Unicode 敏感性
2: Unicode 警告
3: 在 utf8 中声明 Unicode
4: Unicode 字符
5: Unicode 字符
6: 区域设置查找字符
7: 区域设置查找 Unicode
8: Unicode 序列
9: Unicode 字符
10: 显式编码/解码
11: 将参数转换为 utf8
12: 将参数转换为区域设置
13: 将输入转换为 utf8
14: 将输出转换为区域设置
15: 将 I/O 默认设为 utf8
16: 以特定编码打开文件
17: 将 I/O 默认设为区域设置
18: 将所有参数默认设为 utf8
20: Unicode 大写
21: 不区分大小写的比较
22: 在正则中匹配换行符
23: 字符类别
24: Unicode 字符类
25: Unicode 属性
26: Unicode 归一化
27: Unicode 数字
28: 在正则中匹配簇
29: 按簇而非代码点提取（regex）
30: 按簇而非代码点提取（substr）
31: 反转字符串
32: 图形中的长度
33: Unicode 列宽打印
34: 排序
35: 不区分大小写的 Unicode 排序
36: Unicode 区域设置
37: 让 “cmp”作用于文本而非代码点
38: 不区分大小写的比较
39: 不区分大小写的区域设置比较
40: Unicode 换行
41: 在 DBM 哈希中使用 Unicode 的复杂方法
42: 在 DBM 哈希中使用 Unicode 的简单方法
43: 程序：Unicode 排序和打印

另请 1.3 默认大小写算法，页 113；4.2 大写，页 120-122；大小写映射，页 166-172，特别是无大小写匹配从页 170 开始，UAX #44: Unicode 字符数据库、UTS #18: Unicode 正则表达式、UAX #15: Unicode 归一化形式、UTS #10: Unicode 排序算法、UAX #29: Unicode 文本分段、UAX #14: Unicode 换行算法，作者、版权和许可，修订历史

# perlunifaq - Perl Unicode 常见问题

问与答
perlunit 真的是一个 Unicode 教程吗？
Perl 支持哪些字符编码？
我应该使用哪个版本的 perl？
二进制数据（如图片）怎么办？
什么时候应该解码或编码？
如果我不解码怎么办？
如果我不编码怎么办？
是否有方法可以自动解码或编码？
如果我不知道使用了什么编码怎么办？





我跟丢了；真的要编码内部格式吗？

## 作者 另请

# perluniprops - Perl 中 Unicode 版本 7.0.0 字符属性索引

描述

通过 `\p{n}` 和 `\p{}` 访问的属性

单形式 (`\p{na}`) 有更严格的规则；与非单词字符相邻的空白，下划线分隔数字中的数字；复合形式 (`\p{na=value}` 或 `\p{na:value}`) 有更严格的规则；已稳定、已弃用、过时
匹配无后续字符的合法 `\p{n}` 和 `\p{}`

- \p{Canonical_Naming_Class=Attached_Below,}
- \p{Canonical_Naming_Class=CCC133}
- \p{Graph_Cluster_Break=Prepend}

通过 `::UCD` 访问的属性

通过 Perl 不接受的其他 Unicode 字符属性访问的属性 展开在 NFC (XO_NFC)、展开在 NFD (XO_NFD)、展开在 NFKC (XO_NFKC)、展开在 NFKD (XO_NFKD)、图形链接 (GR_Link)、印地变音分类 (InMC)、印地音分类点 (oID)、Jamo 命名 (JS)、其他字母 (OAlpha)、其他默认忽略代码点 (oID)、其他扩展 (OGR)、其他起始 (OID)、其他小写 (OLower)、其他数学 (OMath)、其他大写 (OUpper)、脚本=片假或假名 (sc=Hrkt)、脚本扩展=片假或假名 (sc=Hrkt) Unicode 数据库中的其他信息 auxiliary/GrapheBreakTest.ht, auxiliary/LineBreakTest.ht, auxiliary/SentenceBreakTest.ht, auxiliary/WordBreakTest.ht, auxiliary/LBTest.txt, BidiCharTest.txt, BidiTextTest.txt, NormTest.txt, CJKRadicals.txt, EmojiSources.txt, Index.txt, IndicMatraCategory.txt, IndicSyllabicCategory.txt, NasList.txt, NormalizationCorrections.txt, Props.txt, ReadMe.txt, StandardizedVariants.txt, USourceData.txt, USourceGlyphs.txt 另请参

# perunitut - Perl Unicode 教程

描述

定义

你的新工具箱

I/O 流程（实际的 5 分钟教程）

总结 问答（或 FAQ）致谢 另请

# perblecdic - 在 EBCDIC 平台上运行 Perl 的考虑因素

描述

常用字符集

- ASCII
- ISO 8859
-  Latin 1 (ISO 8859-1)
- EBCDIC
- 0037, 1047, POSIX-BC

Unicode 代码点对比 EBCDIC 点
Unicode 和 UTF
使用 Encode

单字节表 配方 0, 配方 1, 配方 2, 配方 3, 配方 4, 配方 5, 配方 6
十六表，按 1047 排序

识别字符集 转换
utf8::unicode_to_native() 和 "utf8::native_to_unicode"
tr//
conv
C RTL

运算符差异 函数差异 chr(), ord(), pack(), print(), printf(),
sort(), sprintf(), unpack() 正则表达式差异 插槽 排序

忽略 ASCII 与 EBCDIC 之间的差异。
使用排序辅助函数
单大小写排序数据（针对非数字、非下划线）
仅在一种类型的平台上执行排序。

转换格式
URL 解码和编码
uu 编码和解码
Quoted-Printable 编码和解码
凯撒密码

哈希顺序和和 国际化 I18N 与本地化 L10N 多字节字符集 OS OS
OS/400
PARSE, IFS 访问
OS39, z/OS
sigaction, chcp, 数据集访问, iconv, locales
POSIX-BC?

缺陷 另请参 参考文献 历史 顺序

# perlsec - Perl 安全

描述
安全漏洞 联系信息
安全机制与考量
- 污染模式 (Taint mode)
- 清洗和检测污染数据
- "#!" 行上的开关
- 污染模式与 @INC
- 清理你的路径

安全漏洞
保护你的程序
Unicode
- 算法复杂度攻击
- 哈希种子随机化、哈希遍历随机化、桶排序
- 扰动、新默认哈希函数、替代性哈希函数

另请参

# perlmod - Perl 模块（包和符号表）

描述

这是你要找的文档吗？

此文档，perlnewmod, permodstyle

- 包
- 标表
- BEGIN, UNITCHECK, CHECK, INIT AND END
- Perl 类
- Perl 模块
- 使你的模块线程安全

另请参

# perlmodib - 构建新的 Perl 模块并查找现有的模块

PERL 模块库

实用模块
alias, attributes, autodie, autodie::exception, autodie::exception::system,
autie::hints, autodie::skip, autouse, bause, bigint, bignum, bigrat, blib, bytes,
arnas, constant, deprecate, diagnostics, encoding, encoding::warnings, experimental,
feature, fields, filetest, if, integer, less, lib, locale, mro, ok, opens, ops, overload,
overloading, parent, re, sigtrap, sort, strict, subs, threads, threads::shared, utf8, vars,
version, varnish, warnings::register.

标准模块
AnyDBM_File, App::Cpan, App::Approve, App::Approve::State,
State::Result,
::::,, File::,, File::Attribute, AutoLoader, B::Concise,
B::Debug, B::Deparse, B::Op_id, B::Show, B::Terse,
IO::Socket, IP, Socket, CORE, CPAN,



Locale::Codes::Language, Locale::Codes::Script, Locale::Country, Locale::Currency,
Locale::Marketext::Guts, Locale::Marketext::GutsLoader, Locale::Marketext::Simple,
Locale::Marketext::TP13, Locale::MIME::Base64::QuotedPrint,
Math::BigFloat, Math::BigInt, Math::BigCalc, Math::BigInt::Calc,
Math::BigInt::FastCalc, Math::BigRat, Math::Complex, Math::Trig, Memoize,
Memoize::MyDB_File, Memoize::Export, Memoize::ExpireFile,
Memoize::ExpireTimeTest, Memoize::NDBM_File, Memoize::SDBM_File,
Memoize::Storable, Module::CoreList, Module::Core::Utils, Module::Load,
Module::Conditional, Module::Loaded, Module::Metadata, NDB_File,
Net::Cmd, Net::Config, Net::DataObject, Net::FTP, Net::NTP, Net::NNTP,
Net::Netc, Net::Pop3, Net::Ping, Net::SMTP, Net::Ti, Net::host, Net::libnetFAQ,
Net::meten, Net::pop3, net::servent, o, ODBM_File, Opcode, posix,
Params::Check, Parse::CPAN::Meta, Perl::OSType, Perl::IO, Perl::encoding,
Perl::map, Perl::scale, Perl::vio, Perl::QuotedPrint, Pod::Escapes,
Pod::Find, Pod::Functions, Pod::Ht, Pod::Objects, Pod::Man::ParseLink,
Pod::ParseUtils, Pod::Parser, Pod::Perlod, Pod::Perlod::BaseTo,
Pod::Perlod::GetsOO, Pod::Perlod::ToANSI, Pod::Perlod::ToCheck,
Pod::Perlod::Man, Pod::Perlod::ToNoff, Pod::Perlod::ToPod,
Pod::Perlod::ToRTf, Pod::Perlod::ToTerm, Pod::Perlod::ToText,
Pod::Perlod::ToTk, Pod::Perlod::ToX, Pod::PlainText, Pod::Simple::Simple,
Pod::Simple::Checker, Pod::Simple::Debug, Pod::Simple::DumpAsText,
Pod::Simple::DumpXML, Pod::Simple::HTML, Pod::Simple::HTMLBatch,
Pod::Simple::LinkSection, Pod::Simple::Method, Pod::Simple::PullParser,
Pod::Simple::PullParserEnd, Pod::Simple::PullParserToken,
Pod::Simple::PullParserText, Pod::Simple::PullParserText,
Pod::Simple::RTF, Pod::Simple::Search, Pod::Simple::SimpleTree,
Pod::Simple::Simple::Subclassing, Pod::Simple::Text, Pod::Simple::TextContent,
Pod::Simple::HTML, Pod::Simple::XMLOutStream, Pod::Text::Color,
Pod::Text::Tcmp, Pod::Text::Usage, SDBM_File, Safe, Scalar::Util, Search::Dict,
SaverSelect, SelfLoader, Storable, Sub::Uyl, Sys::Hostna, Sys::Syslog,
Sys::Syslog::Win32, TAP::Base, TAP::Formatter::Base, TAP::Formatter::Color,
TAP::Formatter::Console, TAP::Formatter::ParallelSession,
TAP::Formatter::Console::Session, TAP::Formatter::File,
TAP::Formatter::File::Session, TAP::Formatter::Session, TAP::Harness,
Harness::Harness::Env, TAP::Object, TAP::Parser, TAP::Parser::Aggregator,
TAP::Parser::Grammar, TAP::Parser::Iterator, TAP::Parser::Array,
TAP::Parser::Iterator::Process, TAP::Parser::Iterator::Stream,
TAP::Parser::IteratorFactory, TAP::Parser::Multiplexer, TAP::Parser::Result,
TAP::Parser::Result::Bailout, TAP::Parser::Result::Comnt, TAP::Parser::Result::Plan,
TAP::Parser::Result::Pragma, TAP::Parser::Result::Test,
TAP::Parser::Result::Unknown, TAP::Parser::Result::Version,
TAP::Parser::Result::Y::, TAP::Parser::ResultFactory, TAP::Parser::Scheduler, Source,
TAP::Parser::SourceHandler::TAP::Parser::SourceHandler::Executable,
TAP::Parser::SourceHandler::File, TAP::Parser::SourceHandler::Handle,
TAP::Parser::SourceHandler::Perl, TAP::Parser::SourceHandler::RawTAP,
TAP::Parser::YAMLish::Reader, TAP::Parser::YAMLish::Writer, Term::ANSIColor,
Term::Cap, Term::Complete, Term::ReadLine, Test::Builder:
Test::Builder::IO::Scalar, Test::Builder::Module, Test::Builder::,
Test::Builder::Color, Test::Harness, Test::Harness::Beyond, Test::,
Test::Simple, Test::Tester, Tester::Capture, Tester::CaptureRunner,
Test::Usual, Testual::ok, Test::Abrev, Test::Balanced, Test::ParseWords
Test::Tabs, Test::Wrap, Thread::Queue, Thread::Semaphore, Tie::Array,
Tie::File, Tie::Thread, Tie::Hash, Tie::Nash::NadCapture, Tie::Memoise,
Tie::RefHash, Tie::Scalar, Tie::IDHandle, Tie::SubHash, Tie::HiRes, Tie::Local,
Tie::Piece, Tie::Seconds, Tie::gmt, Tie::localtime, Tie::tm, Universal, Unicode::Collate
Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::::late::CJK::Big5, Unicode::::late::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::::late::::::Big5, Unicode::::late::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
,::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
,::Col::::CJK::GB2312, Unicode::Col::::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, Unicode::Collate::CJK::Big5, Unicode::Collate::CJK::GB2312,
Unicode::Collate::CJK::GB2312, 



高级文档工程师和翻译员
