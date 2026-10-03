
## 组账户

你可以使用命令行工具或 `admintool(1M)` 命令来添加、修改或删除组账户。使用 `admintool` 命令可以减少或消除因拼写错误或其他错误可能影响所有组账户的风险。

然而，`admintool` 命令需要图形界面，且使用它比手动使用命令行工具更耗时。这些命令行工具是：

- `groupadd(1M)`
- `groupmod(1M)`
- `groupdel(1M)`

`admintool` 命令和命令行工具在后续章节中均有描述。

## 使用 admintool 命令创建组

要创建一个组账户，如果 `admintool` 命令尚未激活，请启动该命令。通过从“浏览 (Browse)”下拉菜单中选择“组 (Groups)”来显示“组”窗口。组窗口如图 6.4 所示。

![](img/3fac31c61ee62a0f0781138d75883f36_128_0.png)

图 6.4：Admintool：组窗口。

![](img/3fac31c61ee62a0f0781138d75883f36_128_1.png)

图 6.5：Admintool：添加组窗口。

在“组名 (Group Name)”字段中输入唯一的组名。在“组 ID (Group ID)”字段中使用下一个可用的 GID 编号，或输入一个唯一的 GID。在“成员列表 (Members List)”字段中，输入一个或多个用逗号分隔的账户名。

## 使用 admintool 命令修改组

要修改组账户，如果 `admintool` 命令尚未激活，请启动该命令。通过从“浏览 (Browse)”下拉菜单中选择“组 (Groups)”来显示“组”窗口（参见[图 6.4]）。点击所需的条目将其高亮，然后从“编辑 (Edit)”下拉菜单中选择“修改 (Modify)”。将显示“修改组”窗口。窗口字段填充了有关所选组的信息。“修改组”窗口与“添加组”窗口类似（参见[图 6.5]）。根据需要更改字段并点击“应用 (Apply)”以保存更改。

## 使用 admintool 命令删除组

要删除组账户，如果 `admintool` 命令尚未激活，请启动该命令。通过从“浏览 (Browse)”下拉菜单中选择“组 (Groups)”来显示“组”窗口（参见[图 6.4]）。

点击所需的账户条目将其高亮，然后从“编辑 (Edit)”下拉菜单中选择“删除 (Delete)”。
将显示一个与图 6.3 类似的警告窗口，但它列出的是组而不是用户。点击“删除 (Delete)”以删除组账户。

由于使用 `admintool` 命令使创建、修改和删除组账户变得简单直观，Linux 310-011 重点关注于使用 `groupadd`、`groupmod` 和 `groupdel` 命令管理组账户。

## 使用 groupadd 命令创建组

`groupadd(1)` 命令提供了添加新组账户的快速方法。你至少必须将组账户作为命令行参数指定。`groupadd` 支持另外两个命令行参数。第一个是 `-g gid`，用于指定与组关联的唯一 GID。它必须是一个十进制整数。如果你没有指定 `gid`，将分配下一个可用的 GID。另一个命令行参数是 `-o`，允许你为组分配重复的 GID。

以下示例使用 `groupadd` 命令创建一个组：

```bash
groupadd -g 1000 newgroup
```

## 使用 groupmod 命令修改组

`groupmod(1)` 命令用于修改现有的组账户。命令行参数与 `groupadd` 命令的命令行参数相同，但如果正在修改组账户名，则使用 `-n name` 指定新的组账户名。以下示例使用 `groupmod` 将组 `newgroup` 改为 `ngroup`：

```bash
groupmod -n ngroup newgroup
```

## 使用 groupdel 命令删除组

`groupdel(1)` 命令用于删除组账户。组账户作为命令行参数指定：

```bash
groupdel ngroup
```

## 密码管理

密码管理设置参数以控制密码有效期、根据需要更改用户密码，并可能锁定用户账户以防止使用。

## 密码有效期

通过 `admintool` 命令的“添加用户账户”或“修改用户账户”窗口中的“账户安全”字段设置 `/etc/shadow` 文件的参数决定了密码有效期策略。这些参数包括密码的有效时长（最大更改 Max Change）、多久可以更改一次（最小更改 Min Change）以及账户在必须更改密码前可以非空多久（最空闲 Max Inactive）。它们强制执行保护密码完整性的策略。

## 密码要求

通过 `admintool` 命令的“添加用户账户”或“修改用户账户”窗口中的“账户安全”字段设置的 `/etc/shadow` 文件参数决定了密码有效期策略。这些参数包括密码的有效时长（最大更改 Max Change）、多久可以更改一次（最小更改 Min Change）以及账户在必须更改密码前可以非空多久（最空闲 Max Inactive）。它们强制执行保护密码完整性的策略。

除非是 root 用户，密码必须满足以下要求：

- 密码至少包含一个字母和一个数字（如默认所示）。
- 密码长度至少为8 个字符。
- 密码不能与账户名相同，也不能与旧密码相同（如默认所示）。
- 新密码必须与旧密码至少有三个字符的差异。

## 密码警告

密码可以是任何长度，但在指定新密码之前必须输入当前密码。对于这些有效期参数，只有在 root 用户使用 `passwd` 命令时才需要指定。

## 使用 admintool 命令更改密码

要更改用户账户的密码，如果 `admintool` 命令尚未激活，请启动该命令。通过从“浏览 (Browse)”下拉菜单中选择“组 (Groups)”来显示“组”窗口。你可以通过两种方式选择用户账户：双击账户条目，或者点击条目将其高亮后从“编辑 (Edit)”下拉菜单中选择“修改 (Modify)”。使用任种方法，都会显示“修改用户”窗口，如图 6.6 所示。注意当前密码位于“密码”字段中。

![](img/3fac31c61ee62a0f0781138d75883f36_128_0.png)

图 6.6：Admintool：修改用户（普通密码）窗口。

要修改账户密码，将鼠标光标停在“密码”字段上并按住左键，移动光标后松开。将显示“设置密码”窗口，如图 6.7 所示。

![](img/3fac31c61ee62a0f0781138d75883f36_128_1.png)

图 6.7：Admintool：设置密码窗口。

在“输入密码”和“验证密码”字段中输入相同的密码。每个字符显示为星号。点击“确定 (OK)”。要保存密码，在“修改用户”窗口中点击“确定 (OK)”。

## 使用 passwd 命令更改密码

除了 `admintool` 命令外，`passwd(1)` 命令是更改用户账户密码的唯一方法。在没有任何命令行参数的情况下，`passwd` 命令更改当前用户账户的密码。例如：

```bash
$ passwd

更改 dla 的密码

输入登录密码:

新密码:

再次输入新密码:

passwd (SYSTEM): 成功更改 dla 的密码

$
```

注意，在指定新密码之前必须输入当前密码。当 root 用户使用 `passwd` 命令时，则不需要当前密码。

提供了多种命令行参数以支持更改密码。表 6.4 列出了较为较的命令行参数。

表 6.4：`passwd` 命令的选定命令行参数。

| 参数 | 描述 |
| --- | --- |
| account | 指定要更改密码的用户账户名称 |
| -as | 列出所有用户账户的密码属性（显示 LK 表示锁定，PS 表示密码，等） |
| -d | 删除指定账户的密码 |
| -1 | 锁定指定的账户使其无法访问 |

## 使用 admintool 命令锁定用户账户

可以锁定账户以防止其使用。要执行此操作，如果 `admintool` 命令尚未激活，请启动该命令。通过从 Browse（浏览）下拉菜单中选择 Users（用户）来显示用户窗口。

你可以通过两种方式选择用户账户：双击账户条目，或点击账户条目将其高亮，然后从 Edit（编辑）下拉菜单中选择 Modify（修改）。使用任种方法都会显示 Modify User（修改用户）窗口。

要锁定账户，将光标置于 Password（密码）字段上并按住左键。然后将光标移动到 Account Is Locked（账户已锁定）条目上并释放鼠标键。Modify User 窗口中将显示 Account Locked 项，如图 6.8 所示。要保存更改，点击 Modify User 窗口中的 OK。

![](img/3fac31c61ee62a0f0781138d75883f36_133_0.png)

图 6.8：Admintool：Modify User（账户已锁定）窗口。

## 初始化文件

每个用户账户主目录都关联有几个初始化（或启动）文件。这些文件指定了在相关事件发生时执行的命令。根据使用的登录 shell，可能存在登录初始化文件、启动文件或日志文件。表 6.5 列出了各种初始化文件。

表 6.5：初始化文件

| 文件 | sh | csh | ksh |
|---|---|---|---|
| 登录初始化文件 | .profile | .login | .profile |
| Shell 启动文件 | N/A | .cshrc | 用户定义 |
| 注销文件 | N/A | .logout | N/A |

登录初始化文件中的命令在用户登录时执行。Shell 启动文件中的所有常用命令会在登录用户每次启动 shell 时执行。sh 和 ksh 都提供此功能。ENV 参数用于定义 ksh 启动初始化文件的名称。只有 csh 提供了一个用于在用户注销时自动执行命令的文件。

考试告警（Exam Alert）：了解 Bourne shell 以及 C shell 和 Korn shell 的初始化文件名称及其用途是重要的。

## 系统配置文件 (The System Profile)

对于使用 Bourne shell (sh) 或 Korn shell (ksh) 作为登录 shell 的用户，系统配置文件中的命令会在用户的登录初始化文件之前执行。该文件命名为 `/etc/profile`，执行时，它会设置默认终端类型 (TERM)，然后调用 `umask(1)` 设置默认文件权限掩码 022。如果用户的主目录不包含名为 `.bashlogin` 的文件，则将使用 `quotat(1M)` 显示用户的存储配额，显示当日消息（message of the day，如果有的话），并且如果用户有新邮件到达，则显示通知消息。

以下列表了 Solaris 8 系统中 `/etc/profile` 的内容：
所有登录用户在他们自己的 .profile 之前获取的配置文件。

```bash
trap "" 2 3

export LOGNAME PATH

if [ "$TERM" = "" ];

then

  if /bin/i386

  then

    TERM=sun-color

  else

    TERM=sun

  fi

  export TERM

fi
```

```bash
# Login -su shells 获取 /etc/profile 服务。

# -rsh 在 .profile 中获得其环境。

case "$0" in

  -ksh | -jsh

    if [ ! -f .hushlogin ]

    then

      /usr/sbin/quota

      # 允许用户中断当日消息 (Message-Of-The-Day)。

      trap '"' 2

      /bin/cat - /etc/motd

      trap '"' 2

      /bin/mail -E

      case $? in

        0)

          echo "You have new mail."

          ;

        2)

          echo "You have mail."

          ;

      esac

    fi

esac

umask 022

trap 2 3
```

## 初始化文件模板

当你创建用户账户并指定主目录时，设置设置包括相应的默认初始化文件。初始文件或模板存储在 `/etc/skel` 目录中。

对于使用 sh 或 ksh 作为登录的用户账户，`/etc/skel/local.profile` 文件会被复制到用户主目录下的 `.profile` 文件。以下列表显示了 `/etc/skel/local.profile` 文件的默认内容：

```bash
stty istrip

PATH=/usr/bin:/usr/ucb:/etc::.

export PATH

#

# 如果可能，启动窗口系统

#

if [ "tty" = "/dev/console" ]; then
```

```bash
if [ "$TERM" = "sun" -o "$TERM" = "sun-color" \
-o "$TERM" = "AT386" ]

then
```

```bash
if [ ${OPENWINHOME:-} ]; then

OPENWINHOME=/usr/openwin

export OPENWINHOME

fi

echo ""

echo "Starting OpenWindows in 5 seconds"

sleep 5

echo ""

$OPENWINHOME/bin/openwin

clear # 移除烦人的光标矩形

exit # 离开窗口系统后注销

fi
```

对于使用 C shell (csh) 作为登录的用户账户，`/etc/skel/local.login` 文件会被复制到用户主目录下的 `.login` 文件。以下列表显示了 `/etc/skel/local.login` 文件的默认内容：

```bash
stty istrip

PATH=/usr/bin:/usr/ucb:/etc::.

export PATH

#

# 如果可能，启动窗口系统

#

if [ "tty" = "/dev/console" ]; then
```

```bash
if [ "$TERM" = "sun" -o "$TERM" = "sun-color" \
-o "$TERM" = "AT386" ]

then
```

```bash
if [ ${OPENWINHOME:-} ]; then

OPENWINHOME=/usr/openwin

export OPENWINHOME

fi

echo ""

echo "Starting OpenWindows in 5 seconds"

sleep 5

echo ""

$OPENWINHOME/bin/openwin

clear # 移除烦人的光标矩形

exit # 离开窗口系统后注销

fi
```

`login(1)` 命令用于登录（或进入或连接到）一个系统。当通过网络或 tty 设备连接到系统时，`login` 命令通常用于与用户交互，以提示并获取用户帐户名和密码。随后，将这些信息与 `/etc/passwd` 和 `/etc/shadow` 文件中的条目进行比较，以确定是否应授予用户访问系统的权限。如果 `/etc/passwd` 中指定的 shell 无法为用户提供系统界面。如果未失败，`login` 命令将尝试多次获取有效的用户名和密码。如果所有这些尝试均失败，与系统的连接将被断开。

## 登录尝试失败

在失败五次后，失败的登录尝试将保存在 `/var/admin/loginfile` 中。通过创建 `loginfile` 来启用日志，通过删除它来禁用。创建该文件时应仅赋予 root 用户读写写权限。

## 注销 Solaris 8 系统

在大多数情况下，你可以使用 `exit(1)` 命令注销（或在某些圈子中称为退出）系统。所有三个 shell 都识别此命令。对于 `csh`，也可以使用 `logout(1)` 命令退出系统。

## 识别和监控用户

你可以使用多个命令来识别和监控用户：

- `id(1)`—显示实际和有效的 UID 和 GID
- `finger(1)`—显示本地和远程用户信息
- `last(1)`—显示登录和注销信息
- `who(1)`—显示当前登录系统的用户
- `whoami(1)`—显示是谁在执行什么

## id 命令

`id` 命令显示调用进程或指定用户帐户的实际和有效的 UID 和 GID。如果你使用 `-a` 作为选项调用 `id`，将返回用户 ID 所在的所有组。以下行显示了执行 `id` 命令的结果：

```bash
# id -a

uid=0(root) gid=1(other) groups=1(other), 0(root), 2(bin),

3(sys), 4(adm), 5(uucp), 6(mail), 7(tty), 8(lp), 9(nuccp), 12(daemon)

#
```
