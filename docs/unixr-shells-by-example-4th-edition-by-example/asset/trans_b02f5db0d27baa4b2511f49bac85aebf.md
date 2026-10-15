

## 第 13 章：交互式 Bash Shell

![](img/60a0b5d254bd6007403850f972cbfad8_790_0.png)

### 13.1 引言

在交互式 shell 中，标准输入、标准输出和标准错误都与终端绑定。交互式使用 Bourne Again shell（Bash）时，你可以在 bash 提示符下输入 UNIX/Linux 命令，然后等待响应。bash 为你提供了大量内置命令和命令行快捷方式，例如历史记录、别名、文件补全和命令补全、命令行编辑等等。其中一些特性在标准 UNIX Bourne shell 和 Korn shell 中已经存在，但 GNU 项目扩展了该 shell，不仅增加了许多新特性，还加入了 POSIX 兼容性。随着 Bash 2.x 的发布，bash shell 已包含 UNIX Korn shell 和 C shell 的众多特性，使其在交互层面和编程层面都是功能完备的 shell，同时向上兼容标准 Bourne shell。对于 UNIX 用户，bash 为标准的 sh、csh 和 ksh shell 提供了一种替代选择。

本章重点介绍如何在命令行中与 bash 交互，以及如何自定义你的工作环境。你将学习如何利用所有快捷方式和内置功能，以创建一个高效且有趣的工作环境。第 14 章将在此基础上更进一步。届时，你将能够编写 bash shell 脚本，通过自动化日常任务和开发复杂的脚本，为自己进一步定制工作环境；如果你是管理员，还可以不仅为自己，也为整个用户群体实现同样的定制。

#### 13.1.1 bash 的版本

Bourne Again shell 于 1988 年 1 月 10 日诞生（摩羯座），由 Brian Fox 创立，后来由 Chet Ramey 接手，他现在正式负责维护 bash、增强其功能并修复 bug。bash 的第一个版本是 0.99。当前版本（截至本书写作时）是 2.05。版本 2.0 中完成了重大增强，但有些操作系统仍在使用 1.14.7 版本。所有版本都可以在 GNU 公共许可证² 下免费获取。甚至还有适用于 Windows 的 bash！要查看你正在使用的版本，可以使用 bash 的 `--version` 选项，或者打印 `BASH_VERSION` 环境变量的值。

> 1. 尽管 bash 历来是 Linux 平台的默认 shell，但现在它也随 Solaris 8 捆绑提供。
> 2. 要获取 bash 的最新版本，请访问 www.delorie.com/gnu/。

#### 示例 13.1

```
(UNIX)
$ bash --version
GNU bash, version 2.05.0(1)-release (sparc-sun-solaris)
Copyright 2000 Free Software Foundation, Inc.

$ echo $BASH_VERSION
2.05.0(1)-release
```

#### 示例 13.2

```
(Linux)
$ bash --version
GNU bash, version 2.05.0(1)-release (i386-redhat-linux-gnu)
Copyright 2000 Free Software Foundation, Inc.
```

#### 13.1.2 启动

如果 bash shell 是你的登录 shell，那么在看到 shell 提示符之前，它会经历一系列启动过程。见图 13.1。

当系统启动时，运行的第一个进程称为 init（PID #1）。它会生成一个 getty 进程。该进程打开终端端口，提供标准输入来源以及标准输出和错误输出的去向，并在屏幕上显示登录提示符。随后执行 `/bin/login` 程序。登录程序会提示输入密码，对密码进行加密并验证，设置初始环境，然后启动登录 shell `/bin/bash`，即 passwd 文件中的最后一个条目。bash 进程会查找系统级初始化文件 `/etc/profile`，并执行其中的命令。然后，它会在用户的主目录中查找名为 `.bash_profile` 的初始化文件。执行完 `.bash_profile`³ 中的命令后，它还会执行用户初始化文件（通常称为 `.bashrc`）中的命令，最后，默认的美元符号 ($) 提示符会出现在你的屏幕上，shell 等待命令输入。（有关初始化文件的更多信息，请参阅第 756 页的“环境”部分。）

> 3. bash 会使用多种不同的初始化文件；后续页面会讨论这些文件。

