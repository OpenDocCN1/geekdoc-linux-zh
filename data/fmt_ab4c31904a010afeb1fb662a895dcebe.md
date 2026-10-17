
列表 13.4 显示了编译步骤（第 1 行）以及你如何使用文件 `13LST03.txt` 作为标准输入运行测试程序。关于此示例会话可以得出以下几点：

- 1. 尝试了 `%z` 说明符（第 3 行）。下一行的结果（第 4 行）显示了你当前的区域（locale）配置显示的内容。
- 2. 尝试了缩写的星期几名称 `%a`、非世纪年份格式 `%y` 以及周数 `%W`（第 6 行和第 7 行）。
- 3. 显示了非特殊字符在此情况下被格式化为字符串 `"TIME"`）（第 9 行和第 10 行）。还尝试了特定区域的 `%p`。
- 4. 测试了时区说明符 `%z` 和不缩写的星期几名称 `%A`（第 12 行和第 13 行）。
- 5. 尝试了 12 小时格式 `%I` 和 AM/PM 标识 `%p`（第 21 行和第 22 行）。
- 6. 尝试了一年中的天说明符 `%j`（第 27 行和第 28 行）。

# 理解区域（Locale）的影响

`strftime` 支持的一些格式说明符会根据区域（locale）进行格式化。例如 `%A` 说明符（完整的星期几名称）。

在 Linux 环境中，区域（locale）代表了在特定主机系统上使用的语言和文化规则集。区域定义了用于某些消息的语言、字典约定（如日期和时间格式）以及将使用的字符集。

区域设置决定了你的系统使用星期几英文名称还是法语名称。月份是另一个受区域影响的方面。例如，像 `%X` 说明符这样的字典约定规定了时间应该以 12 小时还是 24 小时格式显示。

关于区域的更多信息，请查看系统上的 `locale(7)` 手册页。然而，检查和配置你系统的区域超出了本书的范围。

## 总结

在本节中，你学习了 Linux 如何使用 `time_t` 数据类型中的自 epoch 值来保留和管理时间。你学习了适用于 Linux 的时区，以及如何为你的会话配置本地时区。

你还检查了许多在不同形式之间转换时间和日期的函数。你学习了如何通过 `mktime()` 函数生成 `time_t` 值。最后，你使用 `strftime()` 函数来格式化自定义日期和时间。

## 问答

- 为什么 `time_t` 值被称为自 epoch 以来的秒数？
- `time_t` 值表示自某个时间点（UTC 时间的 1970 年 1 月 1 日）以来的秒数。
- 为什么我应该始终使用 `time_t` 数据类型而不是传统的长整型？
- 数据类型在将来可能会发生变化，以避免超出 31 位限制的问题。
- 我如何计算两个日期之间的天差？
- 从较后的 `time_t` 值中减去较早 `time_t` 值。结果是秒差。将该差值除以 8600（每天的秒数）。
- 我如何计算从现在五天三小时五分钟后发生的事件的日期和时间？
- 获取当前 `time_t` 数据类型的当前日期和时间。在此值基础上加上 5 倍 86400 以推进五天。加上 3 倍 3600 以推进三小时。最后加上 5 秒以得到最终时间。
- 我如何知道 `mktime()` 无法将 `struct tm` 转换为有效的 `time_t` 值？
- 它会返回一个值 `(-1)`。
- 在使用任何外部变量 `tzname[]`、`timezone` 或 `daylight` 之前必须确保什么？
- 你必须确定这些值已经初始化。当调用诸如需要时区信息的 `localtime()` 等函数时，你就可以确定这一点。如果你有任何疑问，必须调用 `timeset()` 函数。

## 工作坊

鼓励你在进入下一节课程之前完成测验和练习。

## 测验

- 1. 你使用什么函数获取当前的系统日期和时间？
- 2. 你使用什么函数将 `time_t` 值转换为其日期时间组件？
- 3. 什么函数获取日期和时间组件并将其转换回 `time_t` 数据类型？
- 4. 返回 ASCII 字符串的两个函数是什么？
- 5. 你使用什么函数格式化日期字符串？
- 6. 你如何知道系统日期和时间在什么情况下？
- 7. 什么环境变量可以覆盖你的时区？

## 练习

- 1. 写一个新程序，使用 `getopt()` 风格的命令行选项获取当前的系统日期和时间。该程序必须支持 `-t` 选项，其参数是 `time_t` 值。确保在提供该选项时，以十进制格式输出结果。
- 2. 使用第 1 题编写的程序，添加一个新的命令行选项 `-f`。当该选项存在时，使用提供的格式字符串调用 `strftime()`。如果省略了选项 `-f`，输出 `time_t` 值。
- 3. 使用第 2 题编写的程序，添加一个新的命令行选项 `-d days`，其中 `days` 是正负天数。当提供该选项时，将指定的天数加到日期值。确保使用 `strtol()` 将 `-d` 选项参数转换为长型值。

括号中的是组名，但你可能不不信，它们必须在数据库中查询。
在本节中，你将查看 Linux 提供的查询用户和用户组信息的设施。

## 理解用户名和 uid 数字

`id` 命令报告 `student1` 的 uid 为 507。这个数字是从哪里来的？什么是用户 ID（用户标识符）？它和用户名相同吗？我将在下文中回答这些问题。

你在登录系统时提供的名称就是用户名。在给出的示例中，使用的用户名是 `student1`。这个名称是你作为用户的、易于人类识别的身份标识。登录程序在数据库中查找此名称，并在此情况下确定该用户的 uid 为 507。有时，用户名也被直接称为账户（account）或用户（user）。

uid 数字允许 Linux 能够跟踪你是谁以及你拥有哪些权限。用于此值的 C 数据类型是 `uid_t`。它是由系统管理员分配给你的。它是在你创建登录账户时给你的一个唯一数字。

## 使用“用户 ID”术语

“user ID”这一术语在 UNIX 圈中被频繁使用。大多数情况下，它指的是用户的用户名。有时，它被泛泛地描述你作为用户的身份，无论是指你的用户名还是你的 uid 数字。本质上，它们是等价的，尽管它们代表了同一种身份的不同表现。

## 理解用户名 root

uid 数字 0 在 Linux 中是特殊的。它被称为 root 用户名，尽管不一定必须称为 root。该用户账户的另一个术语是超级用户（super user）。uid 数字 0 拥有整个 Linux 系统不受限制的访问权限。这就是为什么该账户被严格保护的原因。

然而，如果你设置并运行自己的 Linux 系统，你可以在需要的时候成为 root。虽然使用 root 可能很有趣，但你应该你应该在非驻留账户中执行更多的非管理性任务。这样，当发生意外事故时，你的系统可以使用权限机制来保护自己免受伤害（而事故是会发生的）。

## 理解组名和 gid 数字

与 uid 类似，gid 数字被 Linux 用于引用一个组。用于此值的 C 数据类型是 `gid_t`。这个数字由创建组的系统管理员定义。

## 用户id、密码和组管理

在外部，像你我这样的用户会称为*组名*（group name）。组名通常被直接称为*组*（group）。这些术语是内部使用的 gid 值的易于用户的等价物。

组数据库允许一个用户成为多个组的成员。这就是为什么在前面的示例中，`id` 命令将最后一个字段列为 `groups=104(user)`。如果 `student1` 是其他组的成员，那些组名和 gid 数字就会列在那里。

## 理解 gid

与 uid 值 0 类似，gid 值 0 授予了组级别资源的不受限制访问权限。虽然这不等同于成为超级用户，但它仍然授予了很多权限。因此，这个组通常只授予 root 账户或特殊的管理账户。

## 身份函数

在进行查询之前，你必须能够确定自己到底是谁。当 `id` 命令运行时，它必须找出它是在什么 uid 数字和 gid 数字下运行。为了获取这些信息，它必须调用一些信息检索函数。

## getuid() 和 getegid() 函数

这里显示的 `getuid()` 和 `getegid()` 函数允许进程分别确定其运行的真实 uid（real uid）以及其运行的有效 uid（effective uid）。这两个函数都返回 `uid_t` 类型的 id 数字。

```c
#include <unistd.h>

uid_t getuid();

uid_t getegid();
```

`getuid()` 返回有效 uid 数字。由于特殊安排， UNIX 进程可以临时切换到另一个用户。例如，邮件程序会临时切换到 mail uid，以便它能够访问只有 mail 用户账户才能访问的目录和文件。`getegid()` 函数返回调用时当前有效的 uid。

另一方面，`getuid()` 函数返回真实的 uid 数字。即使进程临时切换到了像 mail 这样的其他用户，`getuid()` 函数也会返回你真实的 uid 数字。

这些函数没有错误可供测试，因为它们总是执行成功的。

![](img/be1d279b4a141bb2ee2a617a8ff21d0d_290.png)

## getgid() 和 getegid() 函数

命令还必须找出它以什么 gid 数字运行。为了这个目的，提供了两个辅助函数——`getgid()` 和 `getegid()`：

```c
#include <unistd.h>

gid_t getgid(void);

gid_t getegid(void);
```

通过 uid 数字可以获得真实和有效的 gid 值。`getgid()` 函数返回真实的 gid，而 `getegid()` 函数返回有效的 gid。两个函数都返回 `gid_t` 类型的 id 数字。这些函数没有错误可供测试，因为它们总是执行成功的。

uid 和 gid 示例

你可以如下用 C 语言编写 `id` 命令的简单等效实现：

```c
printf("Real user: %ld\n", (long)getuid());
printf("Real groupid: %ld\n", (long)getgid());
```

你还可以通过 `getuid()` 和 `geteuid()` 函数打印有效的 uid 和 gid 数字：

```c
printf("Effective user: %ld\n", (long)geteuid());
printf("Effective groupid: %ld\n", (long)getegid());
```

## 理解 /etc/passwd 文件

对于外部，用户名和密码信息存储在 Linux 系统的 `/etc/passwd` 文件中。该文件是以冒号分隔的文本，格式如下：

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:4:sync:/dev:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lp:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
bin:x:9:9:bin:/bin:/usr/sbin/nologin
u:x:10:10:u:/home/u:/usr/sbin/nologin
proxy:x:33:33:proxy:/bin/bin/nonexistent:/usr/sbin/nologin
news:x:34:38:news:/var/lib/news:/usr/sbin/nologin
irc:x:35:35:irc:/var/run/ircd:/usr/sbin/nologin
up:x:36:36:up:/root/up:/usr/sbin/nologin
list:x:38:38:list:/var/list:/usr/sbin/nologin
gnats:x:41:41:gnats:/var/lib/gnats:/usr/sbin/nologin
www:x:32:32:www:/var/www:/bin/false
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
irc:x:35:35:irc:/var/run:/usr/sbin/nologin
data:x:83:83:data:/root:/usr/sbin/nologin
listd:x:84:84:listd:/var/spool/listd:/usr/sbin/nologin
ubus:x:99:99:ubus:/var/lib/dbus:/usr/sbin/nologin
student1:x:507:507:student1:/home/student1:/bin/bash
```

## 用户id、密码和组管理

外部，像你我这样的用户会称为*组名*（group name）。组名通常被直接称为*组*（group）。这些术语是内部使用的 gid 值的易于用户的等价物。

组数据库允许一个用户成为多个组的成员。这就是为什么在前面的示例中，`id` 命令将最后一个字段列为 `groups=104(user)`。如果 `student1` 是其他组的成员，那些组名和 gid 数字就会列在那里。

## 理解 gid

与 uid 值 0 类似，gid 值 0 授予组级别资源的不受限制访问权限。虽然这不等同于成为超级用户，但它仍然授予了很多权限。因此，这个组通常只授予 root 账户或特殊的管理账户。

## 身份函数

在进行查询之前，你必须能够确定自己到底是谁。当 `id` 命令运行时，它必须找出它是在什么 uid 数字和 gid 数字下运行。为了获取这些信息，它必须调用一些信息检索函数。

## getuid() 和 getegid() 函数

这里显示的 `getuid()` 和 `getegid()` 函数允许进程分别确定其运行的真实 uid（real uid）以及其运行的有效 uid（effective uid）。这两个函数都返回 `uid_t` 类型的 id 数字。

```c
#include <unistd.h>

uid_t getuid();

uid_t getegid();
```

`getuid()` 返回有效 uid 数字。由于特殊安排，UNIX 进程可以临时切换到另一个用户。例如，邮件程序会临时切换到 mail uid，以便它能够访问只有 mail 用户账户才能访问的目录和文件。`getegid()` 函数返回调用时当前有效的 uid。

另一方面，`getuid()` 函数返回真实的 uid 数字。即使进程临时切换到了像 mail 这样的其他用户，`getuid()` 函数也会返回你真实的 uid 数字。

这些函数没有错误可供测试，因为它们总是执行成功的。

![](img/be1d279b4a141bb2ee2a617a8ff21d0d_290.png)

## getgid() 和 getegid() 函数

命令还必须找出它以什么 gid 数字运行。为了这个目的，提供了两个辅助函数——`getgid()` 和 `getegid()`：

```c
#include <unistd.h>

gid_t getgid(void);

gid_t getegid(void);
```

通过 uid 数字可以获得真实和有效的 gid 值。`getgid()` 函数返回真实的 gid，而 `getegid()` 函数返回有效的 gid。两个函数都返回 `gid_t` 类型的 id 数字。这些函数没有错误可供测试，因为它们总是执行成功的。

uid 和 gid 示例

你可以如下用 C 语言编写 `id` 命令的简单等效实现：

```c
printf("Real user: %ld\n", (long)getuid());
printf("Real groupid: %ld\n", (long)getgid());
```

你还可以通过 `getuid()` 和 `geteuid()` 函数打印有效的 uid 和 gid 数字：

```c
printf("Effective user: %ld\n", (long)geteuid());
printf("Effective groupid: %ld\n", (long)getegid());
```

## 理解 /etc/passwd 文件

对于外部，用户名和密码信息存储在 Linux 系统的 `/etc/passwd` 文件中。该文件是以冒号分隔的文本，格式如下：

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:4:sync:/dev:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lp:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
bin:x:9:9:bin:/bin:/usr/sbin/nologin
u:x:10:10:u:/home/u:/usr/sbin/nologin
proxy:x:33:33:proxy:/bin/bin/nonexistent:/usr/sbin/nologin
news:x:34:38:news:/var/lib/news:/usr/sbin/nologin
irc:x:35:35:irc:/var/run/ircd:/usr/sbin/nologin
up:x:36:36:up:/root/up:/usr/sbin/nologin
list:x:38:38:list:/var/list:/usr/sbin/nologin
```
