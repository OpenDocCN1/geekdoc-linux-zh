

passwd 文件可以包含在第一列以加号 (+) 或减号 (-) 开头的条目。这些行用于访问网络信息系统 (Network Information System) 网络数据库。以加号 (+) 开头的行用于引入来自网络信息系统的条目。+ 条目有三种形式：

- **+*+** 在该位置插入网络信息系统 passwd 文件的全部内容。
- **+name** 在该位置插入来自网络信息系统的 name 的条目（如果存在）。
- **+@name** 在该位置插入网络组 name 中所有成员的条目。

如果 + 条目的密码、目录、gecos 或 shell 字段非空，这些字段将覆盖网络信息系统中包含的内容。数值用户 ID 和组 ID 字段不能覆盖。

passwd 文件也可以包含以减号 (-) 开头的行，这禁止来自网络信息系统的条目。- 条目有两种形式：

- **-name** 禁止 name 的后续任何条目（如果存在）。
- **-@name** 禁止网络组 name 中所有成员的后续任何条目。

### 警告

用户 ID (uid) 17 预留给 Pascal 语言操作系统。用户 ID (uid) 18 预留给 BASIC 语言操作系统。这些是 Series 300 和 400 计算机的操作系统，它们可以与 HP-UX 在同一磁盘上共存。将这些 uid 用于其他用途可能会阻碍文件传输和共享。

root 用户 (uid 0) 的登录 shell 必须是 /sbin/sh。其他 shell 如 sh、ksh 和 csh 都位于 /usr 目录下，而在引导过程的早期阶段该目录可能尚未挂载。将 root 用户的登录 shell 更改为 /sbin/sh 以外的值可能导致系统无法正常工作。

pw_gecos 字段中保存的信息可能与该字段不支持或未来的用途冲突。使用 pw_gecos 字段保存用户识别信息在任何行业标准中均未正式化。该字段的当前用法源自其在 Berkeley 软件发行版中的使用。未来标准可能将此字段定义为其他用途。

以下字段如注释所述存在字符限制：

- 登录名字段长度不得超过 8 个字符；
- 初始工作目录字段长度不得超过 63 个字符；
- 程序字段长度不得超过 44 个字符。
- 如果这些字段的长度超过上述指定的限制，结果将不可预测。

以下字段如注释所述存在数值限制：

- 用户 ID 是介于 -2 和 UID_MAX 之间（包含两端）的整数值。
- 组 ID 是介于 0 和 UID_MAX 之间（包含两端）的整数值。
- 如果其中任何一个值超出范围，getpwent(3C) 函数会将 ID 值重置为 (UID_MAX)。

## 示例

### NFS 示例

这里有一个 /etc/passwd 文件的示例：

```text
root:3Km/04Cyg84Xc:0:10:System Administrator::/sbin/sh
joe:r4hRrdr4gJ4CqG:100:50:Joe User, Post 4A, 12345:/home/joe:/usr/bin/ksh
@john:
@bob:
+@documentation:no-login:
-@marketing:
+:::Guest
```

在此示例中，如果网络信息系统发生故障，会有针对用户 root 和 joe 的具体条目。

- 用户 john 在 Network Information System 中的密码条目将被原样引入。
- 用户 bob 的任何后续条目都将被忽略。
- netgroup documentation 中任何人的密码字段都被禁用。
- netgroup marketing 中的用户不会被 getpwent(3C) 返回，因此不允许登录。
- 其他任何人都可以使用其通常的密码、shell 和主目录登录，但 pw_gecos 字段为 Guest。

### NFS 警告

加号 (+) 和减号 (-) 功能是 NFS 功能；因此，如果未安装 NFS，它们将无法工作。此外，这些功能仅适用于 /etc/passwd，而不适用于已转换为可信系统的系统。当系统转换为可信系统时，加密密码只能从受保护的密码数据库 /tcb/files/auth/*/* 中访问。Network Information System 数据库中的任何用户条目也必须在受保护的密码数据库中有一个条目。

uid -2 预留给通过 NFS 进行的远程 root 访问。通常赋予此 uid 的 pw_name 是 nobody。由于 uid 是以有符号值存储的，因此在 <pwd.h> 中包含以下定义以匹配用户 nobody。

```c
UID_NOBODY (-2)
```

## 文件

| 文件 | 描述 |
| :--- | :--- |
| /tcb/files/auth/*/* | 当系统转换为可信系统时使用的受保护密码数据库。 |
| /etc/passwd | HP-UX 使用的标准密码文件。 |

## 另请参见

chfn(1), finger(1), login(1), passwd(1), a641(3C), crypt(3C), getprwent(3), getpwent(3C), authcap(4), limits(5).

## 标准符合性

passwd: SVID2, SVID3, XPG2

![](img/75f39fc91296b889c0653851accdfd46_869_0.png)

# ps - 报告进程状态。

## 名称

ps - 报告进程状态

## 概要

```
ps [-adehflP] [-g grplist] [-P proclist] [-R prmgrglist] [-t termlist] 
   [-u uidlist]
```

## XPG4 概要

```
ps [-AacdefHhjLP] [-C cmdlist] [-g grplist] [-G gidlist] [-n namelist] 
   [-o format] [-P proclist] [-R prmgrglist] [-s sidlist] [-t termlist] 
   [-u uidlist] [-U uoidlist]
```

## 描述

ps 打印关于选定进程的信息。使用选项来指定要选择哪些进程以及关于它们要打印什么信息。

### 进程选择选项

使用以下选项来选择应该选择哪些进程。

> 注意：如果在默认 (标准 HP-UX) 和 XPG4 环境中都使用了某个选项，此处提供的描述记录了默认行为。有关 XPG4 行为的更多信息，请参阅外部影响 (EXTERNAL INFLUENCES) 下的 UNIX95 变量。

- **(none)** 选择与当前终端关联的进程。
- **-A** (仅限 XPG4。) 选择所有进程。（-e 的同义词。）
- **-a** 选择所有进程，但不包括进程组领导者和未与终端关联的进程。
- **-C cmdlist** (仅限 XPG4。) 选择正在执行 cmdlist 中给定的基名命令的进程。
- **-d** 选择所有进程，但不包括进程组领导者。
- **-e** 选择所有进程。
- **-g grplist** 选择进程组领导者在 grplist 中给出的进程。
- **-G gidlist** (仅限 XPG4。) 选择真实组 ID 号或组名在 gidlist 中给出的进程。
- **-n namelist** (仅限 XPG4。) 此选项被忽略；允许其存在以符合标准。
- **-P proclist** 选择进程 ID 号在 proclist 中给出的进程。
- **-R prmgrglist** 选择属于 PRM 进程资源组的进程，其名称或 ID 号在 prmgrglist 中给出。请参阅依赖项 (DEPENDENCIES)。
- **-s sidlist** (仅限 XPG4。) 选择会话领导者在 sidlist 中给出的进程。（-g 的同义词）。
- **-t termlist** 选择与 termlist 中给出的终端关联的进程。终端标识符可以用两种形式之一指定：设备的文件名（例如 tty04）或者如果设备文件名以 tty 开头，则仅指定其余部分（例如 04）。如果设备文件位于 /dev 或 /dev/pty 以外的目录中，则终端标识符必须包含包含该设备文件的 /dev 下目录的名称（例如 pfs/5）。
- **-u uidlist** 选择有效用户 ID 号或登录名在 uidlist 中给出的进程。
- **-U uidlist** (仅限 XPG4。) 选择真实用户 ID 号或登录名在 uidlist 中给出的进程。

如果指定了 -a、-A、-d 或 -e 选项中的任何一个，则 -C、-g、-G、-P、-R、-t、-u 和 -U 选项将被忽略。

如果指定了 -a、-A、-d 和 -e 中的多个，则限制最少的选项生效。

如果指定了 -C、-g、-G、-P、-R、-t、-u 和 -U 选项中的多个，如果进程匹配指定的任何选项，则选择该进程。

用作 -C、-g、-G、-P、-R、-t、-u 和 -U 选项参数的列表可以用两种形式之一指定：

- 由逗号分隔的标识符列表。
- 用引号 (") 包围并由逗号和/或一个或多个空格分隔的标识符列表。

## 输出格式选项

使用以下选项来控制输出列表中包括哪些数据列。选项是累积的。

- **(none)** 默认列是：pid、tty、time 和 comm，按此顺序。
- **-f** 显示列 user、pid、ppid、cpu、stime、tty、time 和 args，按此顺序。
- **-l** 显示列 flags、state、uid、pid、ppid、cpu、intpri、nice、addr、sz、wchan、tty、time 和 comm，按此顺序。
- **-fl** 显示列 flags、state、user、pid、ppid、cpu、intpri、nice、addr、sz、wchan、time、tty、time 和 args，按此顺序。

