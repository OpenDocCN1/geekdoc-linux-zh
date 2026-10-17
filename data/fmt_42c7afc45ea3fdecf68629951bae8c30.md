
## 将 `ls` 的输出写入文件

将`ls`的输出写入文件但也显示出来。如果你不想输出，让非特权将输出重定向到`/dev/null`（第 489 页）。下一个示例使用这种技术消除屏幕输出，并使用`-a`选项追加到文件而不是覆盖：

```bash
$ ls | sudo tee -a /root/ls > /dev/null
```

## `sudo` 选项

你可以使用命令行选项来控制`sudo`如何运行命令。`sudo`命令的语法为`sudo [options] [command]`，其中`options`是一个或多个选项，`command`是你想执行的命令。在没有`-u`选项的情况下，`sudo`以`root`权限运行命令。以下是一些更常用的选项；完整列表请查看`sudo` man 页面。

- `b` (background) 在后台运行命令。
- `e` (edit) 使用此选项时，`command`是文件名而不是命令。此选项导致`sudo`以`root`权限使用由`SUDO_EDITOR`、`VISUAL`或`EDITOR`环境变量指定的编辑器编辑名为`command`的文件。它默认使用`nano`编辑器。或者使用带有任何选项的`sudoedit`工具。
- `i` (initial login environment) 启动`/etc/passwd`中为`root`（或通过`-u`指定的其他用户）指定的`shell`，运行`root`（或其他用户）的启动文件，但有某些例外（例如`TERM`未设置）。不接受命令参数。
- `k` (kill) 重置运行命令的用户的时间戳（第 423 页），这意味着用户下次运行`sudo`时必须输入密码。
- `l` (list defaults) 列出可以在`sudoers`文件的`Defaults`行（第 429 页）上设置的参数。不接受命令参数。
- `L` (list commands) 列出运行`sudo`的用户在本地系统上运行的用户。不接受命令参数。
- `-s` (shell) 根据`/etc/passwd`文件中的指定启动一个新的`root`（或通过`-u`指定的另一个用户）`shell`。与`-i`类似，但不会更改环境。不接受命令。
- `-user` 以用户的权限运行命令。在不使用此选项的情况下，`sudo`将以`root`权限运行。

## `sudoers`：配置 `sudo`

根据需要，如果不进行完全配置，`sudo`的安全性和健壮性可能无法达到本应达到的水平。`sudo`配置文件为`/etc/sudoers`。编辑`sudoers`的最佳方法是使用此命令：`sudo visudo`。`visudo`实用程序锁定、编辑并检查`sudoers`文件的语法。默认情况下，`visudo`调用`nano`编辑器。你可以通过设置环境变量`SUDO_EDITOR`、`VISUAL`或`EDITOR`来让`visudo`调用以下命令：

```bash
$ export VISUAL=vi
```

将其替换为您选择的文本编辑器。将此命令放入启动文件（第 293 页）以便在每次登录时都设置此变量。

### 始终使用 `visudo` 编辑 `sudoers`

`sudoers`文件中的语法错误可能会阻止你使用`sudo`获取权限。如果你直接编辑此文件（不使用`visudo`），你将在无法使用`sudo`之前并不知道自己引入了语法错误。`visudo`实用程序在允许你之前会检查`sudoers`的语法。如果发现错误，它将为你提供选择：修复错误、不更改文件退出，或保存更改并退出。最后一种选择通常是糟糕的，因此`visudo`将其标记为 (DANGER!)。

在`sudoers`文件中，以井号（`#`）开头的注释可以出现在一行。除了注释外，此文件还包含两种条目：别名（aliases）和用户权限规范。每个条目都占据一行，可以通过以反斜杠（`\`）结束该行来换行。

## 用户权限规范

指定用户权限的行格式如下（等号周围的空格是可选的）：

```
user_list host_list = [(runas_list)] command_list
```

- `user_list` 指定该规范行所适的用户。此列表可以包含用户名、组（以`%`前缀）和用户别名（见下一节）。
- `host_list` 指定该规范行所适的主机。此列表可以包含一个或多个主机名、`IP`地址或主机别名（见下一节）。你可以使用内置别名`ALL`使该行适用于引用此`sudoers`文件的所有系统。

## 以 `root` 权限运行命令

- `runas_list` 指定了在使用`-u`选项调用`sudo`（第 426 页）时，可以运行`command_list`中命令的用户。此列表可以包含用户名、组（以`%`前缀）和`runas`别名（见下一节）。它必须被括在括号内。如果没有`runas_list`，`sudo`假设为`root`。
- `command_list` 指定该规范行所适的工具。此列表可以包含工具名称、存放工具的目录名称以及命令别名（见下一节）。所有名称必须是绝对路径；目录名称必须以斜杠（`/`）结尾。

如果你在名称后紧跟两个相邻的双双引号（`""`），则用户将无法指定任何命令行参数（包括选项）。或者，你可以指定参数（包括通配符），以限制用户允许使用的参数。

示例：以下用户权限规范允许`Sam`使用`sudo`在所有引用包含此规范的`sudoers`系统（由`ALL`指定）上挂载和卸载文件系统（以`root`权限挂载和卸载）：

```
sam ALL=(root) /bin/mount, /bin/unmount
```

`(root)` `runas_list` 是可选的。如果你省略它，`sudo`将允许用户以`root`权限运行`command_list`中的命令。在以下示例中，`Sam`利用了这些权限。他无法直接运行；相反，他必须调用`sudo`来运行。

```bash
$ whoami
sam
$ mount /music
mount only root can mount /dev/sdb7 from /music
$ sudo mount /music
[sudo] password for sam:
$
```

将上述`sudoers`中的行替换为下行，`Sam`将不允许挂载`/p03`，尽管他仍然可以挂载任何其他文件系统并挂载任何文件系统：

```
sam ALL=(root) /bin/mount, /bin/unmount, !/bin/unmount /p03
```

上述`sudoers`中前一行的结果如下所示。`sudo`工具不会提示密码，因为`Sam`在过去的 15 分钟内输入过密码。

```bash
$ sudo umount /p03
Sorry, user sam is not allowed to execute '/bin/mount /p03' as root on localhost.
```

下一行限制`Sam`只能挂载和卸载挂载在`/p01`、`/p02`、`/p03`和`/p04`上的文件系统：

```
sam ALL=/bin/mount /p0[1-4], /bin/unmount /p0[1-4]
```

以下命令显示了结果：

```bash
$ sudo umount /music
Sorry, user sam is not allowed to execute '/bin/umount /music' as root on localhost.
$ sudo umount /p03
```

### 默认权限

`sudoers`文件包含以下行：

`fqdn` (完全限定域名名) 在`sudoers`文件中对`FQDN`（第 1149 页）执行`DNS`查找。当设置此标志时，你可以在`sudoers`文件中使用`FQDN`，但这样做可能会对`sudo`的性能产生负面影响，特别是在`DNS`无法工作的情况下。如果设置了此标志，你必须使用本地主机的`DNS`名称，而不是别名。如果`host`返回的是`FQDN`，则你不需要设置此标志。默认是关闭。

`insults` 当用户输入错误密码时，显示轻微的、具有伤害性的侮辱。默认也是关闭的。参见`passed_tries`。

`lecture=freq` 控制`sudo`在密码提示之前显示提醒消息机。`freq`的可能值为`never`（默认值）、`once`（一次）和`always`（总是）。指定`!lecture`等同于指定`freq`为`never`。

`mail_always` 每次用户运行`sudo`时，都会发送到`mailto`指定的地址。默认是关闭。

`mail_badpass` 当用户在运行`sudo`时输入错误的密码时，发送到`mailto`指定的用户。默认是关闭。

`mail_no_host` 当在`sudoers`文件中的用户名没有权限在本地主机上运行命令并运行`sudo`时，发送到`mailto`指定的用户。默认是关闭。

`mail_no_perms` 当在`sudoers`文件中的用户名没有权限运行请求的命令并运行`sudo`时，发送到`mailto`指定的用户。默认是关闭。

`mail_no_user` 当不在`sudoers`文件中的用户名运行`sudo`时，发送到`mailto`指定的用户。默认是关闭。

`mailsub=subj` (邮件主题) 更改警告和错误消息的默认邮件主题，将其从默认的 `*** SECURITY information for %sh ***` `subj` 进行更改。该程序会将`subj`内的`%sh`扩展为本地系统的主机名。如果`subj`包含特殊字符，请将其放在双引号之间（第 160 页）。

`mailto=eadd` 将`sudo`警告和错误消息发送到`eadd`（一个电子邮件地址）；默认是`root`）。如果`eadd`包含特殊字符，请将其放在双引号之间。

`passwd_tries=num` 指定用户在`sudo`退出之前响应`sudo`密码提示可以输入错误密码的次数。默认是 3。参见`insults`和`lecture`。

## 使用 `root` 密码代替你的密码

*tip* 如果你设置了`root`密码（第 431 页），你可以通过运行`rootpw`来使用需要密码的图形化程序来恢复`root`密码，而不是运行程序的用户的密码。这些程序会询问你的密码，但只会接受`root`密码。此更改将使`Ubuntu`系统以类似于其他发行版使用该密码的方式使用`root`密码。

`rootpw` 使`sudo`在响应提示时仅接受`root`密码。因为`sudo`在询问你的密码或`root`密码时都会发出相同的提示，因此开启此标志可能会误导用户。`*尚未解锁 root 账户，请勿开启此标志*`（第 431 页），否则你将无法使用`sudo`。要解决此问题，请以恢复模式（第 245 页）启动系统并关闭（删除）此标志。默认是关闭，导致`sudo`提示运行`sudo`的用户的密码。参见前面的`tip`。

`shell_noargs` 在不带任何参数的情况下调用`sudo`时，它将在不改变环境的情况下生成`root` shell。默认是关闭。此选项与`sudo -s`选项相同。

`timestamp_timeout=mins` `mins`是`sudo`时间戳（第 423 页）有效的分钟数。默认是 15；将`mins`设置为`-1`可使时间戳永久有效。

`tty_tickets` 使用`sudo`基于`tty`（终端）验证用户身份，而不是基于用户。

`umask=val` `Val`使用`sudo`运行用户指定的命令的`umask`（第 459 页）。将`val`设置为`0777`以保留用户的`umask`值。默认是`0022`。

## 解锁 `root` 账户（为 `root` 分配密码）

除了少数情况外，`Ubuntu`系统上并不需要解锁`root`账户；事实上，`Ubuntu`建议你不要这样做。以下命令通过为`root`分配密码来解锁`root`账户：

```bash
$ sudo passwd root
Enter new UNIX password:
Retype new UNIX password:
password: password updated successfully
```

重新锁定`root` 如果你决定在解锁后想重新锁定`root`账户，请执行命令`sudo passwd -l root`。你可以使用前面的命令再次解锁它。

## `su`: 赋予另一个用户的权限

要使用`sudo`获得`root`权限，你必须解锁`root`账户（如前一节所述）。

`su`（切换用户）工具可以以指定用户的身份和权限生成`shell`或执行程序。在命令行中`su`后面跟用户名；如果你正以`root`权限工作或知道该用户的密码，你将获得该用户的身份。当你给出一个没有参数的命令时，`su`默认生成具有`root`权限的`shell`（你必须知道`root`密码）。

当你给出一个作为`root`的命令时，它会产生一个新的`shell`，显示`#`提示符。你可以通过终止此`shell`回到正常状态（以及之前的`shell`和提示符）：按下`CTRL-D`或给出`exit`命令。单独给出命令会更改你的用户`ID`和组`ID`，但对环境的更改极小。例如，`PATH`的值与给出`su`命令之前相同。当你给出命令`su -l`或`--login`（注意有连字符）时，你将获得一个`root`登录`shell`：就像你登录为`root`一样。不仅`shell`的用户`ID`和组`ID`与`root`匹配，环境也与`root`完全相同。登录`shell`在显示提示符之前会执行相应的启动文件（第 293 页）。

`id`工具显示你在关联组中用户`ID`和组`ID`的变化：

```bash
$ id
uid=1002(sam) gid=1002(sam) groups=117(admin),1002(sam)
$ 
# id
uid=0(root) gid=0(root) groups=0(root)
```

你可以使用`su`的`-c`选项用`root`身份运行命令，并在命令执行完毕后返回原始`shell`。以下示例显示用户未允许杀死（第 455 页）一个进程。然而，通过使用`su -c`和`root`密码，用户被允许杀死该进程。双引号是必要的，因为`su -c`将其命令视为单个参数。

```bash
$ kill -15 4982
-bash: kill: (4982): Operation not permitted
$ su -c "kill -15 4982"
```

## `Upstart` 事件守护进程

`Upstart`守护进程是基于事件的，并在系统变化时运行指定的程序。与其只在运行级别更改时启动和停止服务，不如`Upstart`在从`udev`（页 502）得知文件、打印机或其他设备添加或移除时启动和停止服务。这种变化被称为事件。例如，`Upstart`可以在系统启动、关机或`job`改变时启动和停止服务。

从`Sysinit`切换到`Upstart`涉及`Linux`系统的许多部分。为了平滑过渡并尽可能减少错误，`Upstart`团队选择在多个版本中进行此转换。

`Ubuntu`一直从`Sysinit`配置转向更灵活的`Upstart`配置。随着越来越多的服务由`Upstart`控制，`init`目录（见第 440 页的`tip`）中的项将取代`/etc/init.d`和`/etc/rc`目录。运行级别将不再是`Ubuntu`的正式功能，但为了兼容性将予以维护。`Upstart`将响应`cron`。

### 软件包

`Upstart`系统包含在一个软件包中，该包默认安装：

- `upstart`—提供`Upstart`守护进程和`initctl`工具。

### 定义

事件是可以传递给`init`的状态变化。系统的任何内部或外部状态变化都可以触发一个事件。例如，引导加载程序触发启动事件（`startup` 手页），而`tell`命令（第 444 页）触发运行级别事件（第 444 页）。移除和插入热插（页 502）或`USB`设备（如打印机）也可以触发事件。你也可以通过给出`initctl`命令（第 436 页）手动触发事件。更多信息请参阅第 437 页的“事件”。

`Job`是`init`读取的一系列指令。这些指令通常包括一个程序（二进制文件或脚本）和一个事件名称。当被触发时，`Upstart`守护进程会运行该程序。你可以通过分别给出`initctl start`和`stop`命令手动运行和停止`job`（第 436 页）。

## 434 第 11 章 系统管理：核心概念

作业分为任务（tasks）和服务（services）。在默认情况下，一个作业是一个服务；你必须显式地将其指定为任务，它才能作为任务运行。

任务是一个执行其工作并在完成后返回等待状态的作业。任务会阻塞触发其事件的程序/进程，直到其指定的程序运行完毕。第 438 页描述的`rc`就是一个任务的示例。

服务是一个通常不会自动终止的作业。例如，日志守护进程（log daemon）和`getty`进程（第 439 页）被实现为服务。`init`守护进程监控每个状态，如果服务失败则重启服务，如果手动或通过事件停止则杀死服务。服务会阻塞触发其事件的程序/进程，直到其运行完成。

`init`目录存放作业文件（定义`Upstart init`守护进程运行的作业的文件）。起初，该目录由`Upstart`软件包填充。某些服务的安装会向此目录添加文件以控制该服务，并替换之前放置在`/etc/rc.d`和`/etc/init.d`目录中的文件（服务之前安装的位置）。

`Upstart`守护进程的核心是一个状态机。它跟踪作业的状态，并在事件触发时跟踪作业状态的变化。当`init`跟踪一个作业从一个状态转换到另一个状态时，它可能会执行作业的命令或终止该作业。

`init`守护进程利用运行级别（runlevels，第 443 页）的变化来决定何时启动和停止进程。依赖`Upstart init`守护进程的`Ubuntu`系统没有运行级别的的概念。为了从基于运行级别的系统向基于事件的系统的迁移，并为其他发行版的软件提供兼容性，`Ubuntu`使用`Upstart`模拟了运行级别。
