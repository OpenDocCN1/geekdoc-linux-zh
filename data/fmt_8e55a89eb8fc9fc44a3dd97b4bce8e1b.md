
一些观察者认为 Perl 5.10 的发布标志着现代 Perl 运动的开始。特别是，这一术语描述了一种开发风格，它倡导使用 CPAN，利用语言的最新发展（见表 1.1），并致力于编写高质量代码。

**表 1.1 发布时间和近期发展**

| 主要版本 | 最新更新 | 状态 |
| :--- | :--- | :--- |
| 5.5 | 2004/02/23 | 旧版本 |
| 5.6 | 2003/11/15 | 旧版本 |
| 5.8 | 2008/12/14 | 旧版本 |
| 5.10 | 2009/08/23 | 旧版本 |
| 5.12 | 2012/11/10 | 旧版本 |
| 5.14 | 2013/03/10 | 旧版本 |
| 5.16 | 2013/03/11 | 旧版本 |
| 5.18 | 2014/01/07 | 较旧版本，但仍受支持 |
| 5.20 | 2014/05/27 | 当前版本 |

> 3. Wikipedia.org, “Perl,” http://en.wikipedia.org/wiki/Perl.

### 1.3.2 什么是 Perl 6、Rakudo Perl 和 Parrot？

> *“Perl 5 是我对 Perl 的重写。我希望 Perl 6 成为社区对 Perl 和社区的重写。”*
>
> —Larry Wall, State of the Onion 演讲, TPC4

Perl 6 本质上是包含许多新特性的 Perl 5。尽管它们仍在并行开发，但 Perl 6 不会取代 Perl 5。基本语言语法、特性和用途

## 1.3 谁在使用 Perl？

将保持不变。如果你懂 Perl，那么将来你依然懂 Perl。如果你从本书学习 Perl，当 Perl 6 发布时，你就做好了深入钻研的准备。Perl.org 将 Perl 6 描述为：如果你说美式英语，学习 Perl 6 就像学习澳式英语，而不是试图从英语切换到中文。

Rakudo Star 是 Perl 6 的一个实用且可用的发行版，运行在 Parrot 虚拟机上，最近于 2013 年 10 月发布。要了解更多信息，请访问 http://rakudo.org。

Parrot 是一种虚拟机，旨在高效地编译和执行动态语言的字节码。Parrot 目前托管着多种处于不同完成阶段的语言实现，包括 Tcl、JavaScript、Ruby、Lua、Scheme、PHP、Python、Perl 6、APL，以及 .NET 字节码翻译器。

要了解关于 Perl 6、Rakudo 和 Parrot 的最新 Perl 核心开发信息，请访问 http://dev.perl.org（参见图 1.1）。

![](img/8556abcb353c0991f12099420ec28735_34_0.png)

图 1.1 Perl 6 开发网站。

关于 Larry Wall 的生平简介和 Perl 的历史，请访问 http://www.softwarebarn.org/People/Wall/Index.shtml#Perl_history。

## 1.4 从哪里获取 Perl

Perl 的下载和安装说明可以从多个来源获取。你可以检查以下流行网站，寻找适合你电脑的 Perl 发行版：`cpan.org`、`perl.org`、`activestate.com` 和 `strawberryperl.com`。

> **什么是 Strawberry Perl？**
>
> Strawberry Perl 是用于 Microsoft Windows 平台的 Perl。尽管大多数其他发行版依赖用户预先设置好软件开发工具来安装某些 Perl 组件，但 Strawberry Perl 预配置并打包了最常用的工具，包括 Perl 二进制文件、`gcc` 编译器、所有外部库、所有捆绑的数据库客户端等。截至写作时，最新版本是 Strawberry Perl 5.20.1.1，适用于 32 位和 64 位版本的 Windows。（你可以在 `http://strawberryperl.com` 下载）。Larry Wall 说：“当我在 Windows 上工作时，我使用 Strawberry Perl。”

### 1.4.1 CPAN (cpan.org)

Perl 发行版的主要来源是 CPAN，它位于 `www.cpan.org`（参见图 1.2）。CPAN，即“通往一切 Perl 的网关”，全称是 Comprehensive Perl Archive Network（全面 Perl 归档网络），是一个托管你所需的所有免费 Perl 材料的网站，包括文档、常见问题解答（FAQs）、模块和脚本、二进制发行版和源代码，以及公告。CPAN 在世界各地都有镜像站，你可以在以下位置找到最近的镜像：

- `www.perl.com/CPAN`
- `www.cpan.org`

如果你想寻找模块来辅助你的工作，CPAN 是你必去之地。CPAN 搜索引擎允许你在许多类别下查找模块。模块将在第 13 章“模块化它、打包它，并将其发送到图书馆！”中进行讨论¹

前往 `www.cpan.org/ports` 了解适合你平台的可用选项，Perl 支持 100 多种平台。

![](img/8556abcb353c0991f12099420ec28735_36_0.png)

**图 1.2** CPAN 网站。点击 Ports（移植）标签页以查找你的平台。

### 1.4.2 Perl 的下载及其他资源 (perl.org)

由 O'Reilly Media, Inc. 运营的官方 Perl 主页是 www.perl.com，但看起来你需要的一切都能在 www.perl.org 找到（参见图 1.3）。

![](img/8556abcb353c0991f12099420ec28735_37_0.png)

图 1.3 Perl.org 网站。

### 1.4.3 ActivePerl (activestate.com)

如果你希望快速轻松地安装 Perl，ActivePerl 是一个完整的、自安装的 Perl 发行版，基于 Windows、Mac OS X、Linux、Solaris、AIX 和 HP-UX 的标准 Perl 源代码。它在线发布在 ActiveState 网站（www.activestate.com）上。完整的 ActivePerl 软件包包含核心 Perl 发行版的二进制文件、完整的在线文档，以及 Perl 开发的所有基本工具，包括 PPM，一个便捷的 Perl 包管理器。这可以在 www.activestate.com/activeperl 获取（参见图 1.4）。

![](img/8556abcb353c0991f12099420ec28735_37_1.png)

图 1.4 ActiveState 网站，你可以在这里下载 ActivePerl。

### 1.4.4 我的是什么版本？

要获取你的 Perl 版本、二进制版本的构建日期、补丁以及某些版权信息，请输入示例 1.1 中显示的行（美元符号是 shell 提示符）。

> **示例 1.1**
>
> ```
> $ perl -v
> ```
>
> This is perl 5, version 18, subversion 2 (v5.18.2) built for darwin-thread-multi-2level (with 2 registered patches, see perl -V for more detail)
>
> Copyright 1987-2013, Larry Wall
>
> Perl may be copied only under the terms of either the Artistic License or the GNU General Public License, which may be found in the Perl 5 source kit.
>
> Complete documentation for Perl, including FAQ lists, should be found on this system using "man perl" or "perldoc perl". If you have access to the Internet, point your browser at http://www.perl.org/, the Perl Home Page.

> **解释**
>
> 1. 此 Perl 版本为 5.18.2，适用于 Mac。
> 2. Perl 的作者 Larry Wall 拥有版权。
> 3. Perl 可以在艺术许可证或 GNU 指定条款下复制。Perl 由自由软件基金会（Free Software Foundation）通过 GNU 分发，意味着 Perl 是自由的。

## 1.5 Perl 文档

如今，你只需使用你喜欢的搜索引擎或访问 Perl.org 网站，就可以找到任何 Perl 问题的答案。大多数 Perl 发行版还附带完整的文档，格式为 HTML 和 PDF。
