
我们在这里将讨论的配置文件位于`/etc/pam.d`目录。如果你希望更改适用于`/etc/security`目录中特定模块的配置文件，你应该咨询该模块自带的文档。（记住 PAM 只是一个框架。任何人都可以编写特定的模块。）

PAM 配置文件的性质很有趣，因为它具有“可堆叠”的特性。也就是说，在身份验证文件的每一行都会被评估（后续所示例外）。每行指定一个执行某些身份验证任务的模块，并返回成功标志或失败标志。结果摘要将返回给调用 PAM 的应用程序。

> 注意：我们所说的“失败”，并不是指程序没有运行。然而，我们的意思是当执行某些过程以验证用户是否可以执行某操作时，返回值为“否”。PAM 使用“成功”和“失败”术语来表示传递回调用应用程序的信息。

`/etc/pam.d/`目录中的每个 PAM 配置文件由具有以下语法/格式的行组成：`control_flag module_path arguments`，其中`module_type`代表四种模块之一：auth、account、session 或 password。注释必须以井号`#`字符开头。表 5-4 列出了这些类型及其功能。

### 模块类型 功能

| 模块类型 | 功能 |
| --- | --- |
| auth | 指示应用程序提示用户输入密码，然后授予用户和组权限。它用于身份验证。 |
| account | 不执行身份验证，但根据其他因素（如用户的时间或地理位置）决定访问权限。它用于授权。例如，可以通过这种方式仅为 root 登录提供控制台访问权限。 |
| session | 指定在用户登录之前或之后需要执行哪些操作（例如记录连接）。 |
| password | 指定允许用户更改密码（如果适用）的模块。 |

**表 5-4** PAM 模块类型

`control_flag`（控制标志）允许你指定如何处理特定身份验证模块的成功或失败。表 5-5 描述了一些常见的控制标志。

**required**（必须的）

如果指定了此标志，模块必须成功验证该个人。如果失败，则返回的摘要值必须为失败。

**requisite**（要求的）

此标志与 required 类似；但是，如果 requisite 身份验证失败，配置文件中列出的后续模块将不再调用，并立即向应用程序返回失败。这允许你要求在接受登录尝试之前确保某些条件成立（例如，用户必须在局域网内，且不能尝试通过互联网登录）。

**sufficient**（充分的）

如果一个 sufficient 模块返回成功，且配置文件中没有更多 required 或 sufficient 控制标志，PAM 将向调用应用程序返回成功。

**optional**（可选的）

此标志允许 PAM 即使在此模块失败也继续检查其他模块。换句话说，该模块的结果被忽略。例如，当在特定模块失败时仍允许用户登录时，你可以使用此标志。

**include**（包含）

此标志用于包含作为参数指定的另一个配置文件的所有行或指令。它被用作链接或堆叠不同 PAM 配置文件中指令的方法。

**substack**（子栈）

这用于从指定的 PAM 配置文件中包含给定类型的所有行（堆栈）。它与 include 控制标志不同，因为指定的子栈中的失败并不意味着会自动跳过对模块栈其余部分的检查。对当前模块栈的评估将继续。

### 表 5-5 PAM 控制标志

`module_path`（模块路径）指定执行身份验证任务的模块的相对文件名或完整路径。模块通常存储在`/lib64/security/`/（或`/lib/security/`）目录下。

PAM 配置行的最后一项是`arguments`（参数），代表传递给身份验证模块的参数。虽然参数特定于每个模块，但某些通用选项可以适用于所有模块。这些参数在表 5-6 中描述。

### 表 5-6 PAM 参数

| 参数 |  |
| --- | --- |
| debug | 向系统发送调试信息。 |
| no_warn | 不向应用程序给出警告。 |
| use_firstpass | 此选项与 use_firstpass 类似，因为如果失败则返回失败。 |
| try_first_pass | 此参数允许模块返回密码。 |
| use_account | 此参数允许该模块用于账户。 |
| expose | 此参数允许模块返回账户信息。 |
| blankok | 此参数允许模块返回空值。 |

## 示例 PAM 配置文件

让我们查看一个示例配置文件`/etc/pam.d/login`：

#1.0

2. auth system-auth

3. auth include postlogin

4. account required pam_nlogin.so

5. account include system-auth

6. password include system-auth

7. session required pam_inux.close

8. session required system-auth

9. session required pam_uid

请注意，已添加行号以提高可读性。第一行以井号开头，因此是一个注释。

在第 6 行中，`module_type`设置为`password`。这将包含`/etc/pam.d/system-auth`配置文件中所有类型为 password 的行。该行没有参数。

# pam_selinux.so close 应该是第一个会话规则

第 7 行被注释掉了。我们可以忽略它。

```
session                required        pam_selinux.so close
```

在第 8 行中，`module_type`设置为`session`，用于指定在用户登录后需要执行哪些操作（如果有的话）。`control_flag`设置为`required`。`pam_selinux.so (/lib64/security/pam_selinux.so)`是要调用的实际 PAM 模块名称。`pam_selinux.so`模块用于设置默认安全上下文。它在基于 Red Hat 的发行版中最为流行。在这种情况下，`close`参数被传递给`pam_selinux.so`模块。

```
session                required        pam_loginuid.so
```

在第 9 行中，`module_type`设置为`session`。`control_flag`设置为`required`。`pam_loginuid.so`是要调用的实际 PAM 模块名称。相同的概念适用于`/etc/pam.d`目录下的其他配置文件。如果你需要更多关于特定 PAM 模块功能或其接受的参数的信息，可以查询该模块的 man 页。例如，要了解更多关于`pam_loginuid.so`模块的信息，你可以执行此命令：

```
# man pam_loginuid
```

### “Other”文件

如前所述，如果 PAM 无法找到特定应用程序的配置文件，它将使用一个通用配置文件。这个通用配置文件被称为`/etc/pam.d/other`。默认情况下，“other”配置被设置为谨慎（paranoid）设置，这样所有身份验证尝试都会被记录并立即拒绝。建议你保持这种状态。

### 噢！我无法登录了！

不要担心——在 PAM 配置文件中搞错设置是每个人都会遇到的。将其视为学习过程的一部分吧。不要恐慌：像 Linux 下大多数配置错误一样，你可以通过引导到单用户模式（见第 7 章）并修复`err`文件来解决问题。如果你搞乱了登录配置文件并需要将其恢复到正常状态，这里有一个你可以使用的安全设置：

```
auth                required        pam_unix.so
account             required        pam_unix.so
password            required        pam_unix.so
session             required        pam_unix.so
```

这将赋予 Linux 默认行为，即简单的查看`/etc/passwd`或`/etc/shadow`密码。这应该足够让你重新进入，并在那里进行你想做的更改！

> 注意：`pam_unix.so`模块是一个标准的 Linux/UNIX 身份验证模块。根据模块页面，它使用系统库的标准调用来检索和设置账户信息以及身份验证。通常，这些是从`/etc/passwd`文件和`/etc/shadow`文件（如果启用了 shadow）获取的。

## 调试 PAM

与其他 Linux 服务一样，PAM 充分利用了系统日志文件（你可以在第 8 章阅读更多信息）。如果运行结果不符合预期，请从查看日志末尾开始，看看 PAM 是否说明了发生了什么。很可能是这样。你应该利用这些信息来更改设置并修复问题。

在类 Red Hat 发行版中，要监控的主系统日志文件是`/var/log/messages`，而在类 Debian 发行版中，等效日志文件是`/var/log/syslog`。

# 概览

查看本章讨论的许多工具如何相互作用的最佳方法是让它们实际运行。在本节中，我们将采取逐步方法来创建、修改、删除用户和组。我们还将介绍并使用一些未提及但在管理系统用户时有用且相关的新命令。

## 使用 useradd 创建用户

在我们的 Fedora 服务器上，我们将使用`useradd passwd`命令添加新用户账户并分配密码。

- 1. 创建一个全名为 "Ying Yang"，登录名（账户名）为 yyang 的新用户。输入以下内容：

```bash
[root@server ~]# useradd -c "Ying Yang" yyang
```

yyang:x:1001:1001:Ying Yang:/home/yyang:/bin/bash

从此条目中，你可以了解到关于 Fedora（以及 RHEL）默认用户值的信息：

- UID 号与 GID 号相同。在本例中，值为 1001。
- 新用户的默认 shell 是 Bash (/bin/bash)。
- 为所有新用户自动创建主目录（例如 /home/yyang）。

使用`password`命令为用户名 yyang 创建新密码。将密码设置为 19gan19，并在提示时重复相同操作。输入以下内容：

```bash
root@server ~]# password yyang
Changing password for user yyang
...<输出省略>...
```

> 注意：`pam_unix.so`模块是一个标准的 Linux/UNIX 身份验证模块。根据模块页面，它使用系统库的标准调用来检索和设置账户信息以及身份验证。通常，这些是从`/etc/passwd`文件和`/etc/shadow`文件（如果启用了 shadow）获取的。

```bash
root@server ~# chage -1 master
Last password change : Oct 26, 2017
Password expires : never
Password inactive : never
Account expires : Dec 12, 2019
Minimum number of days between password change : 0
Maximum number of days between password change : 99999
Number of days of warning before password expires : 7
```

**提示** 在像 Fedora、CentOS 和 RHEL 这样的 Red Hat 发版中，你可以通过将普通用户添加到 wheel 组来授予他们超级用户权限（root）或 sudo 权限。在经过适当的身份验证后，这允许具有 sudo 权限的用户根据系统安全策略指定的，以超级用户或其他用户的身份执行命令。例如，要将 master 用户添加到 wheel 组并授予其 sudo 权限，你需要运行：

```bash
# usermod master -a -G wheel
```

在初始操作系统安装期间（第 2 章），要求你允许新创建的用户管理系统的复选框本质上是将该用户添加到了 wheel 组！

## 使用 groupmod 修改组属性

现在使用`groupmod`命令：

- 1. 使用`groupmod`命令将伪组 bogus 重命名为 bogusgroup：

```bash
root@server ~# groupmod -n bogusgroup bogus
```

2. 使用`groupmod`命令将新命名的 bogusgroup 的 GID 更改为 1600：

```bash
root@server ~# groupmod -g 1600 bogusgroup
```

3. 在`/etc/group`文件中查看你对 bogusgroup 的修改：

```bash
root@server ~# grep bogusgroup /etc/group
bogusgroup:x:1600:
```

## 使用 userdel 和 groupdel 删除用户和组

尝试使用`userdel`和`groupdel`命令分别删除用户和组。

- 1. 使用`userdel`命令删除你之前创建的用户 bogususer。在 shell 提示符下，输入以下内容：

```bash
root@server ~# userdel -r bogususer
```

2. 使用`groupdel`命令删除伪组：

```bash
root@server ~# groupdel bogusgroup
```

注意`/etc/group`文件中的 bogusroup 条目已被移除。

> 注意：当你在命令行上仅指定用户登录名运行 userdel 命令（例如 userdel bogususer）时，etc/passwd 和 /etc/shadow 文件中的所有条目以及 /etc/group 文件中的引用都会自动删除。但如果你使用可选的 -r 参数（例如 userdel -r bogususer），则用户主目录下所有该用户的所有的文件也将被删除。

## 总结

本章记录了 Linux 下用户和组管理的方方面面。你在这里阅读的大部分内容也适用于 UNIX 的其他变体，这使得在不同的 *NIX 种类* 中在异构环境中管理用户变得各不相同。

此外，本章涵盖了以下要点：

- 每个用户都有一个唯一的 UID。
- 每个组都获得一个唯一的 GID。
- `/etc/passwd`文件将 UID 映射到用户名。
- Linux 以多种方式处理加密密码。
- Linux 包含了帮助你管理用户的工具。
- Linux 可以将用户和组信息存储在具有标准格式和结构的各种数据库中。
- PAM（可插身份模块）是 Linux 处理多种身份验证机制的通用方法。

这些概念对于来自 Microsoft Windows 环境的管理员来说可能非常陌生，起初可能会有点棘手。不过，不用担心——Linux/UNIX 安全模型非常直观，因此你会很快熟悉它的运行机制。

如果你对构建自己的工具来管理用户的想法感兴趣，请务必查看关于 Perl 或 Python 脚本语言的书籍。它们非常适合处理表格化数据（例如`/etc/passwd`文件）。如果你对这些感兴趣，可以花些时间在当地书店翻阅几本 Perl 或 Python 编程书籍。

# 第 6 章

启动与关闭

现代操作系统的复杂性已经增加，启动和关闭过程的复杂性也之增加。任何经历过从基于 DOS 的系统到基于 Microsoft Windows 的系统的人都亲身经历过这种转变。不仅是操作系统的启动和关闭，像 Windows 一样，还有一系列令人叹的服务和服务（某些是关键的，另一些不是）也必须启动和停止。

在本章中，我们讨论了使用 GRUB 和 Linux Loader (LILO) 进行 Linux 系统的引导。然后，我们逐步介绍 Linux 环境的启动和关闭过程。我们讨论了自动化这些过程某些部分的脚本，以及有时在脚本中可能需要的修改。最后，我们涵盖了与启动和关闭有关的一些杂项。

> 注意：在真实/生产系统上遵循本章的实践练习时，请充分运用常识……可能会导致你的系统进入无法通过重启恢复的非功能状态。不要弄乱生产系统；如果你必须这样做，请确保已备份了所有想要更改的文件，最重要的是，有一个可启动的救援系统。

## 引导程序

对于任何在 PC 上启动的操作系统，都需要一个引导程序。如果你只处理过 Windows，你可能从未直接与引导程序交互。引导程序通常位于磁盘的 MBR 或分区的扇区。引导程序可以通过网络（使用引导协议 BOOT、动态主机配置协议 DHCP、预启动执行环境 PXE、以太网等）来引导系统。引导程序的第一阶段可以加载 Stage 1.5 或 Stage 2。大多数 Linux 发行版使用 GRUB 作为默认引导程序，因为它比 LILO 提供了更多功能。GRUB 遵循 Multiboot 规范并在 Fedora、RHEL、openSUSE、Debian、Ubuntu 等发行版中使用。LILO 的提及仅出于历史原因。

## GRUB

大多数现代 发行版在安装期间使用 GRUB。GRUB 允许访问文件系统。在基于 RPM 的系统中，你可以通过以下命令检查 GRUB 版本：

```bash
## rpm -qa | grep -i
```

在基于 Debian 的系统中，你可以通过以下命令检查 GRUB 版本：

```bash
## dpkg -l | grep -i
```

## Stage 1
