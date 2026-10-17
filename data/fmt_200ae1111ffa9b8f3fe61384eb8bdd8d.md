
# Scratch

Scratch 是一种主要为教育工作者和儿童设计的编程语言。它由 MIT 构建，旨在让人们轻松互动故事、动画、游戏、音乐和艺术，同时教授创造性思维、系统推理能力、数学和计算思想以及协作。作品可以在 Web 上共享，并从任何地方访问。Scratch 是一个在线组件，但开发在本地机器上进行。

要在 Ubuntu 上使用 Scratch，请安装`scratch`并访问 https://scratch.mit.edu 开始使用。

# Vala

Vala 是一种非常新的语言。它的设计初衷是将现代语言的特性引入 C 语言，从而让 GNOME 桌面环境开发的开发者的工作更加轻松。它的语法与 C# 非常相似。Vala 是一种编译型语言，但它不是直接编译为字节码，而是编译为 C 代码，然后使用 C 编译器针对特定的平台进行编译。

在 C 语言中，程序员必须手动管理内存中的引用。在 Vala 中，如果使用内置的引用类型而不是裸指针，这一过程就是自动的。Vala 还使用 GNOME 对象系统来提供引用计数。在大多数情况下，Vala 主要由开发 GNOME 的人员使用，这是很合理的，因为这正是开发 Vala 的原因。时间将证明它是否会获得更广泛的关注。

要在 Ubuntu 上使用 Vala，你可以在你喜欢的编辑器中编写程序。要进行编译，你需要 `valac` 包，它是 Vala 编译器。然后，你需要使用 C 编译器（如 GNU 编译器，见第 38 章“使用编程工具”）对输出结果进行编译。

## 参考文献

- **www.adaic.org**—Ada 信息清理中心，学习 Ada 的极佳资源
- **https://clojure.org**—Clojure 主网站
- **https://dlang.org**—D 语言主网站
- **www.dartlang.org**—Dart 的主网站
- **https://elixir-lang.org**—Elixir 的主网站
- **https://elm-lang.org**—Elm 的主网站
- **www.erlang.org**—Erlang 的主网站
- **www.forth.org**—Forth 兴趣小组主网站，学习更多 Forth 的绝佳之地
- **www.gnu.org/software/gfort/**—Gfort 的主网站，GNU 项目对 Fortran 的实现
- **https://gcc.gnu.org/fortran**—Fortran 的主网站
- **https://groovy-lang.org**—Groovy 的主网站
- **https://haskell.org**—Haskell 的主网站
- **www.java.com**—Java 的主网站
- **www.w3schools.com/js/default.asp**—W3C JavaScript 教程页面，也是学习 HTML 和 CSS 的绝佳之地
- **https://kotlinlang.org/**—Kotlin 的主网站
- **https://lisp-lang.org/**—Common Lisp 的主网站
- **www.clisp.org**—GNU Clisp（Common Lisp 的实现）主网站
- **www.lua.org**—Lua 的主网站
- **www.perl.org**—Perl 的主网站
- **https://php.net**—PHP 的主网站
- **www.python.org**—Python 的主网站
- **https://raku.org**—Raku 的主网站
- **www.ruby-lang.org/en/**—Ruby 的主网站
- **www.scala-lang.org**—Scala 的主网站
- **https://live.gnome.org/Vala**—Vala 的主网站
- **https://scratch.mit.edu**—Scratch 的主网站
- **https://help.ubuntu.com/community/PowerUsersProgramming**—关于使用 Ubuntu 作为开发平台的编程 wiki

# 第40章

## 本章内容

- Ubuntu 开发简介
- 搭建你的开发系统
- 修复 bug 与打包
- 参考文献

本章重点关注如何成为更大团队的一员——具体来说，就是为整个 Ubuntu 开发和打包软件的才俊群体。Ubuntu 由数千个不同的组件组成，这些组件使用多种不同的编程语言编写。每个组件都以源码的形式提供，并被收集到源包中。源包还包含其他内容，专门描述了如版权和许可信息、所需的依赖项以及编译或组装软件的说明。这些源包被用于构建二进制 .deb 包，这些包包含在 Ubuntu 软件仓库中，并供用户快速方便地安装。对于任何感兴趣并愿意稍微研究的人来说，都有方法利用自己的技能来帮助。

当发现 bug 时，只有当有人帮助并花时间探索程序以找到并修复它时，它会被修复。然后，如果有人花时间构建包含该修复的新的新包，并将其上传到 Ubuntu 软件仓库中的适当位置，该修复就可以面向更广泛的社区。

本章包含几个部分。每个部分都在前部分的基础上构建，让你对整个过程有一个全面的理解。如果你只对过程中的某一部分感兴趣——例如后期的部分，如打包——那也没关系。即使你最终只专注于过程中后期步骤的工作，阅读本章的前几节也会让你受益匪浅。只要你愿意学习如何操作，你可以参与过程中的任何部分。本章将带你入门。本章描述的过程是准确的，但还有更多复杂的细节。软件开发，特别是在大型项目中，是不容轻率的。由于资源限制，补丁修复仅接受愿意投入精力的人。Ubuntu 社区非常友好，但他们也很忙。他们会花时间指导新开发者和打包人员。

## Ubuntu 开发简介

Ubuntu 开发遵循六个月的周期。该过程始于规划和讨论，通过所有参与者的共同努力来充分利用有限资源。开发者通过在线参与进行集会，并在即将发布或当前版本的优先级做出决策。这些会议每三个月举行一次，分别在开发周期的开始和中间。当创建一个新版本时，它会被赋予代号，例如 "Focal Fossa"。在正式发布日期之前，版本将使用该代号引用，之后则开始正式按版本号引用，如 20.04。https://wiki.ubuntu.com/Releases Ubuntu 使用的所有版本名称。

部分开发通过从上游开发者获取软件最新版本开始，通过 Debian 或直接来自特定应用程序。在某些情况下，会对代码进行修改或补丁。所有添加到代码中的修改和补丁都被转换为 Ubuntu 包。

其他开发在内部开始，因为某些包完全由 Ubuntu 开发者编写，包括 Canonical 的付费员工以及来自 Ubuntu 社区的志愿者，他们是为了个人或社区利益或仅仅是为了乐趣。这些包接收发布说明中的新功能，然后转换为 Ubuntu 包。

测试在整个周期内进行，从第一批包开始上传就开始。测试会发现 bug，即软件问题，即程序运行时发生的错误。bug 报告使用 Launchpad 创建，它是 Canonical 为 Ubuntu提供的问题跟踪器和代码托管解决方案。开发者和社区成员阅读并根据重要性对 bug 进行分类。严重的 bug 必须尽快修复。其他 bug 可能会令人讨厌，但对程序运行或整个 Ubuntu 系统至关重要，由于资源限制，它们可能会被推迟，直到有人时间处理。每当修复 bug 时，必须为软件制作一个新的包，以便其再次上传到仓库进行测试和审查。

Alpha 版本已发布。Beta 版本已发布。测试和错误修复仍在继续。某些软件可能会被发现包含新的错误，导致软件无法使用，此时可能会使用软件的之前的版本。这被称为回滚（rolling back）到之前的版本。

最终，发布了。一切运行正常。Ubuntu 社区欢呼鼓舞，并休息一或两周。然后，是时候进行下一轮规划会议了。

## 设置你的开发系统

在开始帮助开发 Ubuntu 之前，你必须设置你的系统，使其与 Ubuntu 社区的其他部分无缝衔接。有一套标准的软件包需要安装，并且你必须执行一些标准的步骤。

### 安装基础软件包并进行配置

Ubuntu 开发社区创建了一个方便的软件包，可以安装启动所需的所有内容。从 Ubuntu 软件仓库安装 `packaging-dev`，它其中包含

- `gnupg`，即 Ubuntu 隐私守护器（Ubuntu Privacy Guard），包含了你在将包上传到 Launchpad 时对它们进行签名所需的加密工具。
- `pbuilder`，它在干净、隔离的环境中创建包的可重复构建。
- `bzr-builddeb`，它包含`bzr`；它们共同作为你的版本控制和包管理系统。
- `apt-file`，它可以帮助你找到包含所需的二进制包。

### 设置 GPG

生成你的 G 密钥以便对包进行签名。包在被接受上传到 Ubuntu 软件仓库之前必须经过签名。这允许跟踪谁创建了什么，并最大限度地减少恶意软件行为的风险。

```text
matthew@seymour:-$ gpg -gen-key
```
