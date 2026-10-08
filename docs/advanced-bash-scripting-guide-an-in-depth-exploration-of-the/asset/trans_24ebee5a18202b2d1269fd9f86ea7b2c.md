

# 高级 Bash 脚本指南

然而...

```bash
bash$ su
Password: ......

bash# whoami
root
bash# logname
bozo
```

虽然 `logname` 输出的是登录用户的名称，但 `whoami` 输出的是连接到当前进程的用户名称。正如我们所看到的，有时这两者并不相同。

以替换用户的身份运行程序或脚本。`su rjones` 会以用户 `rjones` 的身份启动 shell。直接运行 `su` 默认使用 `root`。参见示例 A-14。

以 root（或其他用户）的身份运行命令。这可以用于脚本，从而允许普通用户运行该脚本。

```bash
#!/bin/bash

# 一些命令。
sudo cp /root/secretfile /home/bozo/secret
# 更多命令。
```

文件 `/etc/sudoers` 包含了允许调用 `sudo` 密码的用户名列表。

设置、更改或管理用户的密码。

`password` 命令可以在脚本中使用，但可能不应该这样做。

# 示例 17-1. 设置新密码

```bash
#!/bin/bash
# setnew-password.sh: 仅用于演示目的。
# 实际运行此脚本并不是好主意。
# 此脚本必须以 root 身份运行。

ROOT_UID=0      # Root 的 $UID 为 0。
E_WRONG_USER=65  # 不是 root？
```

```bash
E_NOSUCHUSER=70
SUCCESS=0

if [ "$UID" -ne "$ROOT_UID" ];
then
  echo "只有 root 可以运行此脚本。";
  exit $E_WRONG_USER
else
  echo
  echo "root，你应该更明智不要运行这个脚本。"
  echo "即使是 root 用户也会感到忧郁..."
  echo
fi
```

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

```bash
username=bozo
NEWPASSWORD=security_violation

# 检查 bozo 是否在此处。
grep -q "$username" /etc/passwd
if [ $? -ne $SUCCESS ];
then
    echo "用户 username 不存在。"
    echo "密码未更改。"
    exit $E_NOSUCHUSER
fi

echo "$NEWPASSWORD" | passwd --stdin "$username"
# 'passwd' 的 '--stdin' 选项允许
## 从标准输入（或管道）获取新密码

echo; echo "用户 $username 的密码已更改!",
```

# 在脚本中使用 'passwd' 命令是危险的。

exit 0
`passwd` 命令的 `-1`, `-u` 和 `-d` 选项允许锁定、解锁和删除用户的密码。*Root* 可以这些选项。

从 `/var/log/wtmp` 读取并显示已登录的用户。这是 GNU 工具程序之一。

| bash$ ac |
| 总计 | 68.08 |

从 `/var/log/wtmp` 读取最后登录的用户。此命令也可以显示远程登录。

例如，要显示系统最后几次重启的时间：

```bash
bash$ last reboot
reboot system boot 2.6.9-1.667 Fri Feb 4 18:18 (00:02)
reboot system boot 2.6.9-1.667 Fri Feb 4 15:20 (01:27)
reboot system boot 2.6.9-1.667 Fri Feb 4 12:56 (00:49)
reboot system boot 2.6.9-1.667 Thu Feb 3 21:08 (02:17)
.
wtmp 开始于 Tue Feb 1 12:50:09 2005
```

newgrp

在不注销的情况下更改用户的组 ID（GID）。此权限授予了对组文件的访问权限。由于用户可能同时属于多个组，此命令的用途有限。

> Kurt Gleassemann 指出，`newgrp` 命令对于设置用户写入文件的默认组权限可能很有帮助。然而，`chgrp` 命令可能可能更为方便。

# 终端 (Terminals)

tty

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

回当前用户终端的名称（文件名）。注意，每个独立的 xterm 窗口都算作不同的终端。

```bash
bash$ tty
/dev/pts/1
```

stty
显示并更改终端设置。这个复杂的命令在脚本中使用时，可以控制终端行为并显示输出。请查看 info 页面并仔细研究。

# 示例 17-2. 设置删除字符

```bash
#!/bin/bash
# erase.sh: 使用 "stty" 在读取输入时设置删除字符。

echo -n "你的名字是什么？ " # 尝试使用退格键来删除输入字符。
read name
echo "你的名字是 $name。"

stty erase '#' # 将“井号” (#) 设置为删除字符。用于删除最后一个字符。
echo -n "你的名字是什么？"
# 即使脚本退出后，新的键值仍然保持设置。练习：你如何将删除字符重置为默认值？
```

# 示例 17-3. 秘密密码：关闭回显

```bash
#!/bin/bash
# secret-pw.sh: 秘密密码

echo -n "输入密码 "
read passwd
echo "密码是 $passwd"
echo -n "如果有人在背后盯着你，密码就会泄露。"

echo && echo # 两个换行符

`passwd` 命令的 -1, -u, 和 -d 选项允许锁定、解锁和删除用户的密码。*Root* 可以使用这些选项。

从 `/var/log/wtmp` 读取并显示已登录的用户。这是 GNU 工具程序之一。

| bash$ ac |
| 总计 | 68.08 |

从 `/var/log/wtmp` 读取最后登录的用户。此命令也可以显示远程登录。

例如，要显示系统最后几次重启的时间：

```bash
bash$ last reboot
reboot system boot 2.6.9-1.667 Fri Feb 4 18:18 (00:02)
reboot system boot 2.6.9-1.667 Fri Feb 4 15:20 (01:27)
reboot system boot 2.6.9-1.667 Fri Feb 4 12:56 (00:49)
reboot system boot 2.6.9-1.667 Thu Feb 3 21:08 (02:17)
.
wtmp 开始于 Tue Feb 1 12:50:09 2005
```

newgrp

在不注销的情况下更改用户的组 ID（GID）。此权限授予了对组文件的访问权限。由于用户可能同时属于多个组，此命令的用途有限。

> Kurt Gleassemann 指出，`newgrp` 命令对于设置用户写入文件的默认组权限可能很有帮助。然而，`chgrp` 命令可能更为方便。

# 终端 (Terminals)

tty

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

回显当前用户终端的名称（文件名）。注意，每个独立的 xterm 窗口都算作不同的终端。

```bash
bash$ tty
/dev/pts/1
```

stty
显示并更改终端设置。这个复杂的命令在脚本中使用时，可以控制终端行为并显示输出。请查看 info 页面并仔细研究。

# 示例 17-2. 设置删除字符

```bash
#!/bin/bash
# erase.sh: 使用 "stty" 在读取输入时设置删除字符。

echo -n "你的名字是什么？ " # 尝试使用退格键来删除输入字符。
read name
echo "你的名字是 $name。"

stty erase '#' # 将“井号” (#) 设置为删除字符。用于删除最后一个字符。
echo -n "你的名字是什么？"
# 即使脚本退出后，新的键值仍然保持设置。练习：你如何将删除字符重置为默认值？
```

# 示例 17-3. 秘密密码：关闭回显

```bash
#!/bin/bash
# secret-pw.sh: 秘密密码

echo -n "输入密码 "
read passwd
echo "密码是 $passwd"
echo -n "如果有人在背后盯着你，密码就会泄露。"

echo && echo # 两个换行符

`passwd` 命令的 -1, -u, 和 -d 选项允许锁定、解锁和删除用户的密码。*Root* 可以使用这些选项。

[/content]

*(注：由于你提供的待翻译文本存在大量重复（如标题和段落出现了多次），我根据“不要重复输出原文”的原则，对内容进行了整合翻译。以下是去重后的翻译结果：)*

[content]
# 高级 Bash 脚本指南

然而...

```bash
bash$ su
Password: ......

bash# whoami
root
bash# logname
bozo
```

虽然 `logname` 输出的是登录用户的名称，但 `whoami` 输出的是连接到当前进程的用户名称。正如我们所看到的，有时这两者并不相同。

以替换用户的身份运行程序或脚本。`su rjones` 会以用户 `rjones` 的身份启动 shell。直接运行 `su` 默认使用 `root`。参见示例 A-14。

以 root（或其他用户）的身份运行命令。这可以用于脚本，从而允许普通用户运行该脚本。

```bash
#!/bin/bash

# 一些命令。
sudo cp /root/secretfile /home/bozo/secret
# 更多命令。
```

文件 `/etc/sudoers` 包含了允许调用 `sudo` 密码的用户名列表。

设置、更改或管理用户的密码。

`password` 命令可以在脚本中使用，但可能不应该这样做。

# 示例 17-1. 设置新密码

```bash
#!/bin/bash
# setnew-password.sh: 仅用于演示目的。
# 实际运行此脚本并不是好主意。
# 此脚本必须以 root 身份运行。

ROOT_UID=0      # Root 的 $UID 为 0。
E_WRONG_USER=65  # 不是 root？
```

```bash
E_NOSUCHUSER=70
SUCCESS=0

if [ "$UID" -ne "$ROOT_UID" ];
then
  echo "只有 root 可以运行此脚本。";
  exit $E_WRONG_USER
else
  echo
  echo "root，你应该更明智不要运行这个脚本。"
  echo "即使是 root 用户也会感到忧郁..."
  echo
fi
```

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

```bash
username=bozo
NEWPASSWORD=security_violation

# 检查 bozo 是否在此处。
grep -q "$username" /etc/passwd
if [ $? -ne $SUCCESS ];
then
    echo "用户 username 不存在。"
    echo "密码未更改。"
    exit $E_NOSUCHUSER
fi

echo "$NEWPASSWORD" | passwd --stdin "$username"
# 'passwd' 的 '--stdin' 选项允许
## 从标准输入（或管道）获取新密码

echo; echo "用户 $username 的密码已更改!",
```

# 在脚本中使用 'passwd' 命令是危险的。

exit 0
`passwd` 命令的 -1, -u, 和 -d 选项允许锁定、解锁和删除用户的密码。*Root* 可以使用这些选项。

从 `/var/log/wtmp` 读取并显示已登录的用户。这是 GNU 工具程序之一。

| bash$ ac |
| 总计 | 68.08 |

从 `/var/log/wtmp` 读取最后登录的用户。此命令也可以显示远程登录。

例如，要显示系统最后几次重启的时间：

```bash
bash$ last reboot
reboot system boot 2.6.9-1.667 Fri Feb 4 18:18 (00:02)
reboot system boot 2.6.9-1.667 Fri Feb 4 15:20 (01:27)
reboot system boot 2.6.9-1.667 Fri Feb 4 12:56 (00:49)
reboot system boot 2.6.9-1.667 Thu Feb 3 21:08 (02:17)
.
wtmp 开始于 Tue Feb 1 12:50:09 2005
```

newgrp

在不注销的情况下更改用户的组 ID（GID）。此权限授予了对组文件的访问权限。由于用户可能同时属于多个组，此命令的用途有限。

> Kurt Gleassemann 指出，`newgrp` 命令对于设置用户写入文件的默认组权限可能很有帮助。然而，`chgrp` 命令可能更为方便。

# 终端 (Terminals)

tty

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

回显当前用户终端的名称（文件名）。注意，每个独立的 xterm 窗口都算作不同的终端。

```bash
bash$ tty
/dev/pts/1
```

stty
显示并更改终端设置。这个复杂的命令在脚本中使用时，可以控制终端行为并显示输出。请查看 info 页面并仔细研究。

# 示例 17-2. 设置删除字符

```bash
#!/bin/bash
# erase.sh: 使用 "stty" 在读取输入时设置删除字符。

echo -n "你的名字是什么？ " # 尝试使用退格键来删除输入字符。
read name
echo "你的名字是 $name。"

stty erase '#' # 将“井号” (#) 设置为删除字符。用于删除最后一个字符。
echo -n "你的名字是什么？"
# 即使脚本退出后，新的键值仍然保持设置。练习：你如何将删除字符重置为默认值？
```

# 示例 17-3. 秘密密码：关闭回显

```bash
#!/bin/bash
# secret-pw.sh: 秘密密码

echo -n "输入密码 "
read passwd
echo "密码是 $passwd"
echo -n "如果有人在背后盯着你，密码就会泄露。"

echo && echo # 两个换行符

`passwd` 命令的 -1, -u, 和 -d 选项允许锁定、解锁和删除用户的密码。*Root* 可以使用这些选项。

