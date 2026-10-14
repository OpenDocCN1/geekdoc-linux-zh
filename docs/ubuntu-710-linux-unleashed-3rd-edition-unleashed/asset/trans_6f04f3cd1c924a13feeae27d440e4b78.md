

## 相关 Ubuntu 命令

您将使用这些命令在 Ubuntu 中管理用户账户：

- ac—用户账户统计命令
- change—设置或修改用户密码过期策略
- chfn—在 /etc/passwd 中创建或修改用户 finger 信息
- chgrp—修改组 membership
- chmod—更改文件权限
- chown—更改文件所有权
- chpasswd—批量修改用户密码命令
- chsh—修改用户的 shell
- groups—显示现有组 membership
- logname—显示用户的登录名
- newusers—批量用户管理命令
- passwd—创建或修改用户密码
- su—以另一用户身份执行 shell 或命令
- sudo—管理选定用户执行权限
- useradd—创建、修改或管理用户
- usermod—编辑用户的登录配置文件

## 参考

- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/_User-Authentication-HOWTO.html—《用户认证 HOWTO》描述了用户和组信息如何存储以及用于认证。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Shadow-Password-HOWTO.html—《Shadow 密码 HOWTO》深入探讨了 shadow 密码的模糊深处，甚至讨论了为什么你可能不想使用它们。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/_Security-HOWTO.html—必读的 HOWTO，《安全 HOWTO》是对安全问题的良好概述。尤其是本章适用的部分包括创建账户、文件权限和密码安全。
- http://www.securinf.net/unix_security/Linux_Administrators_Security_Guide/—一份通用指南，《Linux 系统管理员安全指南》对限制和监控用户有有趣的章节。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Config-HOWTO.html—如何自定义某些用户特定设置？《Config HOWTO 软件配置》提供了一些建议。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Path.html—如何知道真正的路径？《Path HOWTO》阐明了这个问题。如果你想引导用户访问其数据和应用程序，你需要理解路径。
- http://www.courtesan.com/sudo/—Superuser DO 命令是向普通用户授予特定命令权限的一种强大而优雅的方式。
- http://www.kernel.org/pub/linux/libs/pam/index.html—可插拔认证模块套件包含复杂且非常有用的应用程序，可为密码提供额外的安全性和日志记录。PAM 在 Ubuntu 中默认安装。有效使用它不需要理解 PAM 的复杂细节。

## 第 11 章

## 自动化任务

### 本章内容

- 启动时运行服务
- 手动启动和停止服务
- 调度任务
- 基础 Shell 控制
- 编写和执行 Shell 脚本
- 参考

在本章中，你将学习在系统上自动化任务的五种方法：使它们成为随系统启动而运行的服务，使它们成为你手动启动和停止的服务，安排它们在特定时间运行，在 shell 上将多个命令连接在一起，以及编写自定义脚本将所有内容组合在一条命令下。

在打开电源开关后，启动过程从计算机执行存储在称为 BIOS 的芯片中的代码开始；无论安装了什么操作系统，此过程都会发生。Linux 启动过程始于称为引导加载程序的代码开始加载 Linux 内核，并在登录提示符出现时结束。

作为系统管理员，你将使用本章中学到的技能来控制系统的服务并管理计算机上的运行级别。理解系统服务和状态的管理对于理解 Linux 的工作原理至关重要（尤其是在多用户环境中），并将有助于解开 Ubuntu 系统中一些配置文件之谜。此外，对处理任务调度的 cron 守护进程的良好了解对于所有技能水平的管理员都是必不可少的。

本章也是创建 shell 脚本基础的介绍，shell 脚本是可执行文本文件，编写时符合 shell 语法。Shell 脚本在 Linux 下像任何其他命令一样运行，可以包含复杂的逻辑或一系列简单的 Linux 命令行指令。你也可以在 shell 程序内部运行其他 shell 脚本。本章在简短介绍从
