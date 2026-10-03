
## STEP BY STEP

## 5.5 验证和更改用户环境

以下示例说明如何验证用户环境设置以及如何更改它们：

1. 以用户身份登录。此步骤可让您以用户所见的方式查看用户环境。

2. 编辑用户的初始化文件。以下步骤建议了一些更改并显示应使用的 shell 特定语法。

3. 将用户的默认路径设置为包含主目录以及用户窗口环境和应用程序的目录或挂载点。要更改路径设置，请按如下方式添加或修改 PATH 行：

对于 Bourne 或 Korn shell，语法如下：

```
PATH=/dirname1:/dirname2:/dirname3:.; export PATH
```

例如，在用户 $HOME/.profile 文件中输入以下行：

```
PATH=$PATH:/usr/bin:$HOME/bin:/net/glrr/files1/bin:.;export PATH
```

对于 C shell，语法如下：

```
set path =(/dirname1 /dirname2 /dirname3 .)
```

例如，在用户 $HOME/.cshrc 文件中输入以下行：

```
set path=($path /usr/bin $HOME/bin /net/glrr/files1/bin .)
```

4. 检查环境变量是否设置为用户窗口环境和第三方应用程序的正确目录。输入 env 并按 Enter：

```
$ env
```

```
HOME=/home/ncalkins
HZ=100
LOGNAME=ncalkins
MAIL=/var/mail/ncalkins
PATH=/usr/bin
SHELL=/bin/sh
TERM=sun
TZ=EST5EDT
$
```

### NOTE
在 $PATH（Korn shell）或 $path（C shell）前加上前缀会将更改附加到站点初始化文件已设置的用户路径设置。当您使用此过程设置 PATH 变量时，初始路径设置不会被覆盖和丢失。另请注意列表末尾的“点” (.) 以表示当前工作目录。正如第 8 章所述，点应始终位于路径的末尾。

5. 通过输入以下任一行来添加或更改环境变量的设置：

对于 Bourne 或 Korn shell，语法如下：

```
VARIABLE=value;export VARIABLE
```

以下示例设置用户的默认邮件目录：

```
MAIL=/var/mail/ncalkins;export MAIL
```

对于 C shell，语法如下：

```
setenv VARIABLE value
```

以下示例将历史记录设置为记录最后 100 个命令：

```
setenv HISTORY 100
```

## 主目录

主目录是分配给用户用于存储私有文件的文件系统的一部分。您为家庭目录分配的空间量取决于用户创建的文件类型和执行的工作类型。通常会专门分配整个文件系统用于家庭目录，并且用户共享此空间。系统管理员需要监控用户主目录，以防止一个用户使用超过其公平份额的空间。磁盘配额用于控制用户可以占用的磁盘空间量。它们在第 6 章“文件系统简介”中进行了讨论。

主目录可以位于用户的本地系统上，也可以位于远程文件服务器上。虽然可以使用任何目录名，但无论哪种情况，主目录按惯例都是 /export/home/<username>。当您将主目录放在 /export/home 中时，如果用户从多个不同的工作站登录，它将在网络上可用。对于大型站点，您应该将主目录存储在服务器上。

无论主目录位于何处，用户通常都通过名为 /home/<username> 的挂载点访问它。当使用 Autofs 挂载主目录时，您不允许在任何系统上在 /home 挂载点下创建任何目录。当 Autofs 处于活动状态时，系统会识别 /home 的特殊状态。有关 Autofs 和自动挂载主目录的更多信息，请参阅第 17 章“ NFS 环境”。

要在网络上的任何位置访问主目录，您应始终将其引用为 $HOME，而不是 /export/home/<username>。后者是特定于机器的，应予以避免。此外，在用户主目录中创建的任何符号链接都应使用相对路径（例如 ../../x/y/x），以便无论主目录挂载在何处，链接都有效。用户主目录的位置可能会发生变化。通过不使用特定于机器的名称，您可以保持一致性并减少系统管理。

## 名称服务

如果您为大型站点管理用户帐户，您可能需要考虑使用名称服务，例如 NIS 或 NIS+。名称服务可让您以集中方式存储用户帐户信息，而不是在每个系统的 /etc 文件中存储。当使用名称服务进行用户帐户时，用户可以使用相同的用户帐户在系统之间移动，而无需在每个系统的 /etc 文件中重复站点范围的用户帐户信息。使用名称服务还有助于促进集中和一致的用户帐户信息。NIS 和 NIS+ 在第 18 章“名称服务”中进行了讨论。

## 章节摘要

### 关键术语

- Admintool
- 用户 ID (UID)
- 组
- 组 ID (GID)
- 主组
- 次要组
- 登录 Shell
- 密码老化
- 主目录
- 用户初始化文件
- Shell 变量

这结束了有关如何向系统添加用户登录帐户的讨论。我描述了如何使用 Admintool 和命令行添加、修改和删除用户帐户。Admintool 的图形用户界面使管理用户帐户比命令行方法容易得多。

其次，我描述了用户 shell 初始化文件。我描述了如何使用这些文件来自定义用户工作环境。此外，还描述了许多控制用户 shell 环境的默认 shell 环境变量。

最后，我描述了主目录——分配给用户用于存储私有文件的文件系统的一部分。

本章描述了管理用户帐户相关的任务。由于大多数用户将使用 Common Desktop Environment (CDE) 窗口界面，作为系统管理员，您还需要熟悉 CDE 的设置和定制。截至本文撰写时，这是一个在任一考试中均未涵盖的主题，但在附录 B“ CDE 的管理和配置”中稍后进行了描述。

下一章将稍微转换一下思路，向您介绍 Solaris 文件系统。

## 应用你的知识

### 练习

## 5.1 管理用户帐户

在以下练习中，您将使用 Admintool 向系统添加新用户、锁定用户帐户并设置密码老化。

预计时间：20 分钟

1. Admintool GUI 出现后，使用 Admintool 添加以下用户列表：

| login | password | shell | UID | Pri GID | Secondary GID |
|---|---|---|---|---|---|
| user3 | trng | Korn | 1003 | 10 | 14 |
| user4 | trng | C | 1004 | 10 | 14 |
| user5 | trng | Bourne | 1005 | 10 |  |
| locked1 | (lock accnt) | Korn | 1006 | 10 |  |
| cleared1 | (cleared until 1st login) | Bourne | 1007 | 10 |  |
| nopass1 | (no password) | Korn | 1008 | 10 |  |

2. 注销。
3. 您能否以用户 locked1 登录？
尝试以 cleared1 登录——会发生什么？
root 能否 su 成为用户 cleared1？

## 5.2 用户初始化文件

在以下练习中，您将使用用户初始化文件。

预计时间：20 分钟

1. 使用 vi 编辑器编辑 /etc/skel/local.profile，并添加以下条目以设置以下变量：

```
EDITOR=/usr/bin/vi; export EDITOR
PATH=$PATH:/usr/lib/lp; export EDITOR
```

2. 使用 Admintool 创建一个名为 user9 的新用户，该用户使用 Korn shell。以 user9 登录，并通过输入以下内容验证 /etc/skel/local.profile 中设置的变量是否已正确设置在用户的环境中：
env

3. 为 user9 创建一个 .profile 文件，其中包含两个别名并将主提示设置为显示当前工作目录。使用 vi 编辑器将以下三行添加到位于 user9 主目录中的 .profile 文件中：

```
alias del='rm -i'
alias hi='echo hello'
PS1='\$PWD' '$'
```

4. 注销并以同一用户重新登录以验证 .profile 是否有效。您是否有新的 shell 提示？
