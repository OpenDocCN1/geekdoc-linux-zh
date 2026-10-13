
```
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# User specific environment
PATH="$HOME/.local/bin:$HOME/bin:$PATH"
export PATH

# Uncomment the following line if you don’t like systemctl’s auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
export DATAPATH=/data/files
alias l="ls -lt"
```

## 8.13 编写 Shell 脚本

到目前为止，我们完全专注于 Bash shell 的交互性。交互性是指手动逐个输入命令并在提示符下执行它们。事实上，这只是 shell 能力的一小部分。毫无疑问，shell 最强大的方面之一是创建 shell 脚本的能力。Shell 脚本是包含可在 shell 环境中执行以执行任务的语句序列的文本文件。除了执行命令的能力外，shell 还提供了许多编程结构，例如 `for` 和 `do` 循环以及 `if` 语句，这些都是您在脚本语言中合理期望找到的。

不幸的是，shell 脚本的详细概述超出了本章的范围。然而，许多专门介绍 shell 脚本的书籍和网络资源对该主题的阐述比我们在这里所能达到的要好得多。因此，在本节中，我们只提供 shell 脚本的一点点介绍。

创建 shell 脚本的第一步是创建一个文件（对于本示例，我们将其命名为 `simple.sh`）并将以下内容作为第一行添加：

```
#!/bin/sh
```

`#!` 称为“shebang”，它是一组特殊字符，表示执行脚本所需的解释器的路径是该行上的下一项（在本例中为 `sh`

## 在 RHEL 9 上使用 Bash Shell

可执行文件位于 `/bin`)。这同样可以是，例如 `/bin/csh` 或 `/bin/ksh`，如果你想使用的解释器是其中之一。

下一步是编写一个简单的脚本：

```bash
#!/bin/sh
for i in *
do
    echo $i
done
```

该脚本所做的一切就是遍历当前目录中的所有文件并显示每个文件的名称。可以通过将脚本名称作为参数传递给 `sh` 来执行此脚本：

```
$ sh simple.sh
```

要使文件可执行（从而无需将其传递给 `sh` 命令），可以使用 `chmod` 命令：

```
$ chmod +x simple.sh
```

一旦在文件的权限上设置了执行位，它就可以直接执行。例如：

```
$ ./simple.sh
```

### 8.14 摘要

我们在本章《Red Hat Enterprise Linux 9 Essentials》中简要介绍了 Bash Shell 环境。在图形桌面环境的世界里，很容易忘记操作系统的真正功能和灵活性通常只能通过跳到用户友好的桌面界面之下并使用 Shell 环境来实现。此外，熟悉 Shell 对于管理维护未安装桌面的基于服务器的系统，或在尝试修复损坏到桌面或 Cockpit 界面无法再启动的系统时是必要的。

Shell 的功能远超本章所涵盖的内容。如果你是 Shell 新手，我们强烈建议你寻求额外的资源。一旦熟悉这些概念，你会很快发现，使用终端窗口中的 Shell 执行许多任务比在桌面上浏览菜单和对话框更快。

## 第 9 章

## 9. 管理 RHEL 9 用户和组

在安装 RHEL 9 期间，安装程序创建了 `root` 或超级用户账户并要求配置密码。安装程序还提供了为系统创建用户账户的机会。我们应该记住，RHEL 9 是一个企业级、多用户和多任务操作系统。因此，要充分利用 RHEL 9 的功能，很可能需要向系统授予多个用户的访问权限。每个用户都应拥有自己的用户账户登录名、密码、主目录和权限。

为了便于管理，用户进一步划分为组，这些组可以具有不同的权限级别。例如，你可能有一组在会计部门工作的用户。在这种环境中，你可以创建一个 `accounts` 组并将所有会计部门用户分配到该组。

本章将介绍在 RHEL 9 系统上添加、删除和管理用户和组的步骤。RHEL 9 上的用户和组可以使用命令行工具、Cockpit Web 界面和桌面设置应用程序进行管理。在本章中，我们将介绍这些用户管理方法的每一种。

### 9.1 从命令行管理用户

可以使用 `adduser` 实用程序通过命令行向 RHEL 9 系统添加新用户。要创建新用户账户，请输入类似以下命令：

```
# useradd john
```

默认情况下，这将在 `/home` 目录为用户创建主目录（在本例中为 `/home/john`）。要指定不同的主目录，请在创建账户时使用 `-d` 命令行选项：

```
# useradd -d /users/johnsmith john
```

创建账户后，需要使用 `passwd` 工具为其分配密码，用户才能登录系统：

```
# passwd john
Changing password for user john.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

可以使用 `userdel` 实用程序通过命令行删除现有用户。虽然这会删除账户，但用户的文件和数据仍会保留在系统上：

```
# userdel john
```

在删除过程中也可以删除用户的主目录和邮件 spool：

```
# userdel --remove john
```

RHEL 9 系统上的所有用户都是一个或多个组的成员。默认情况下，新用户会被添加到与用户名相同的私有组中（在上面的示例中，为用户 `john` 创建的账户是名为 `john` 的私有组的成员）。然而，作为管理员，将用户组织到更合乎逻辑的组中是有意义的。例如，所有销售人员可能属于 `sales` 组，会计人员可能属于 `accounts` 组，等等。可以使用 `groupadd` 命令行工具从命令行添加新组，例如：

```
# groupadd accounts
```

使用 `usermod` 工具从命令行将现有用户添加到现有组：

```
# usermod -G accounts john
```

要将现有用户添加到多个现有组，请使用 `-G` 选项运行 `usermod` 命令：

```
# usermod -G accounts,sales,support john
```

请注意，上述命令会将用户从 `-G` 之后未列出的补充组中移除，但用户当前是这些组的成员。要保留任何当前组成员身份，请使用 `-a` 标志追加新的组成员身份：

```
# usermod -aG accounts,sales,support john
```

可以使用 `groupdel` 实用程序从系统中删除现有组：

```
# groupdel accounts
```

请注意，如果要删除的组是任何用户的首要或初始组，则无法删除。在删除组之前，必须先删除该用户或使用 `usermod` 命令为其分配新的主要组。可以使用 `usermod -g` 选项将用户分配到新的主要组：

```
# usermod -g sales john
```

```
# groupdel accounts
```

运行 `groups` 命令以查找用户所属的组。例如：

```
$ groups john
john : accounts support
```

默认情况下，用户账户无法执行需要超级用户（`root`）权限的任务，除非他们知道 `root` 密码。然而，可以配置用户账户以便使用 `sudo` 命令执行特权任务。这涉及将用户账户添加为 `wheel` 组的成员，例如：

```
# usermod -aG wheel john
```

一旦添加到 `wheel` 组，用户将能够使用 `sudo` 执行以下受限任务：

```
$ sudo dnf update
[sudo] password for demo:
Updating Subscription Management repositories.
.
.
```

可以通过编辑 `/etc/sudoers` 文件并找到以下部分来修改 `wheel` 组的 `sudo` 能力：

```
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL
```

```
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL
```

要禁用所有 `wheel` 组成员的 `sudo`，请按如下方式注释掉第二行：

```
## Allows people in group wheel to run all commands
# %wheel  ALL=(ALL)       ALL
```
