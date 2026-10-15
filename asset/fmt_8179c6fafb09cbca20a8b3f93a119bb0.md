
# 第 8 章

## 创建用户账户

这七个字段是：
* 用户名——必须是唯一的。
* 密码的哈希值——如果未定义密码，则使用星号 (`*`)。对于功能用户。
* 上次更改密码的日期——自 1970 年 1 月 1 日以来的天数。
* 最小密码年龄——用户两次更改密码之间必须的天数。
* 最大密码年龄——用户允许保留密码的天数。
* 密码过期——匹配 `/etc` 文件。空字段表示没有限制。
* 密码过期前的警告——在密码过期前显示警告的天数。
* 密码过期后的宽限期——密码过期后禁用账户前的等待天数。

修改您的密码，现在只有几天时间可以继续使用该账户直到它被禁用。

- 密码过期日期——自 1970 年 1 月 1 日以来的天数。

你可以手动创建新用户，也可以使用程序。要手动操作，只需向 `/etc/passwd` 文件末尾添加条目即可。（强烈建议在更改文件之前对该文件进行备份。）你可以将密码字段留空，然后使用 `passwd` 工具分配密码。如果你留空它，它是一个没有密码的有效账户：

```bash
$ cat /etc/passwd

evan::504:100:EvanD:/home/evan:/bin/bash

(Press Ctrl+D)

$

$ passwd evan

New user password: (Enter password)

Retype new user password: (Enter password again)

passwd: all authentication tokens updated successfully

$

$ tail -1 /etc/passwd

evan:$6$...:504:100:/home/evan:/bin/bash

$
```

> 任何用户都可以使用 `passwd` 工具更改 `/etc/passwd` 文件中自己的密码。然而，只有 root 用户可以使用它更改其他用户的密码。

请注意，这种方法将加密后的密码放置在 `/etc/passwd` 文件本身，而不利用 `/etc/shadow` 文件。只要主目录存在且用户是其所有者（参见本章稍后关于 `chown` 的讨论），该用户就会成为经过验证的用户。

Linux 提供了一个工具（大多数供应商也有自己的工具）来简化此过程，即 `useradd`。你必须使用该工具的选项；其中关键键是 `-D` 用于显示默认设置：

```bash
$ useradd -D

GROUP=100

HOME=/home/%s

SHELL=/bin/bash

SKEL=/etc/skel

PASS_MIN_DAYS=0

PASS_MAX_DAYS--1

PASS_WARN_DAYS--7

PASS_INACTIVE--1

PASS_EXPIRE--1
```

你使用这些默认值通过该工具创建一个新用户。默认值来自文本文件 `/etc/login.defs`。因此，以下序列是可能的：

```bash
$ useradd kerby

$ tail -1 /etc/passwd

kerby:x508:100:Caldera Linux User:/home/kerby:/bin/bash

$ tail -1 /etc/shadow

kerby:*:not set*:11213:0:-1:-7:-1:

$ password kerby

New user password: (Enter password)

Retype new password: (Enter password again)

passwd: all authentication tokens updated successfully

$ tail -1 /etc/shadow

kerby:M3cMnQDwHJrd6:11213:0:-1:-7:-1:
```
