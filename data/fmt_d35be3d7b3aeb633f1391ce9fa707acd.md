
# password Joe

Changing password for user Joe.

New UNIX password: ******\*\*

Retype UNIX password: ******\*\*

passwd: all authentication tokens updated successfully.

在这里，`password` 命令提示你为 `joe` 输入新密码。在这种情况下，它没有提示你输入他的旧密码。这允许 `root` 在用户忘记密码时重置其密码（即使这种情况发生得很频繁）。

### 注意

许多 Linux 系统使用可插拔认证模块（PAM）来控制身份验证。通过修改 `/etc/pam.system-auth` 文件，你可以更改系统上的实用程序验证用户的方式。例如，你可以更改允许的失败尝试次数，以及在达到该数字时的操作。（不过，修改 PAM 文件时要小心，因为配置错误可能会导致所有用户无法登录）。■

## 使用影子密码文件

在 UNIX 的早期版本中，所有账户和密码信息都存储在一个所有用户都可以读写（`root` 除外）的文件中。这通常不是问题，因为密码信息是加密的。密码使用陷门算法（`trapdoor algorithm`）加密，未编码的密码可以编码成杂乱的字符字符串，但该字符串无法翻译回未编码的密码。换句话说，陷门意味着加密是单向的，因此加密后的密码无法还原为未编码的密码。

在这种情况下，系统如何检查你的密码？当你登录时，系统会编码你输入的密码，将生成的杂乱字符串与密码文件中存储的杂乱字符串进行比较，只有当两者匹配时才授予访问权限。你是否曾经问过系统管理员你的账户的密码，结果得到的回答是“我不知道”？如果是这样，原因如下：管理员确实没有密码，只有加密后的版本。

## 破解加密密码

在一种情况下，系统如何检查你的密码？当你登录时，系统编码你输入的密码。破解加密密码的问题在于，任何用户都能看到密码文件，这比尝试每个用户的密码要高效得多。破解者有更大的机会进入系统。

幸运的是，Linux 和所有 UNIX 系统都支持影子密码文件。影子文件是 `passwd` 文件的特殊版本，只有 `root` 可以读取。

### 检查影子文件

密码文件名为 `passwd`，位于 `/etc` 目录。影子文件名为 `shadow`，也位于 `/etc`。如果你的 `/etc/shadow` 缺失，可能是你的 Linux 将密码信息存储在 `/etc/passwd` 中。通过使用 `less` 命令显示该文件来验证这一点

```
$ less /etc/passwd
```

类似于显示的内容：

```
root:Dks6uke7Q:0:0:root:/root:/bin/bash
bin:x:1:1::/bin
daemon:x2:daemon:/sbin/sh
mary:KRpRu20yZM5TA:500:100:Smith:/home/mary:/bin/bash
je:0esXrvznOaki:501:100:John:/home/joe:/bin/bash
jane:ptNoieYEJW_:502:100:Anderson:/home/jane:/bin/bash
bob:ju2VY7AK0Kzw:503:100:Reynolds:/home/bob:/bin/bash
```

列表中的每一行对应一个用户账户。每行由冒号分隔的字段组成。从左到右，字段分别是登录名、密码、用户 ID、组 ID、主目录和默认 shell。查看第一行，你可以看到 `root` 账户，其加密密码为 `Dks6uke7Q`。你也可以看到 `root` 的用户 ID 为零，组 ID 为零，主目录为 `/root`，且其默认 shell 为 `/bin/bash`。

这些对于 `root` 账户来说都是正常的，但看到那个加密密码会让你引起警觉。这确认了系统没有使用影子密码文件。此时，你应该立即转换你的密码文件，这通过使用 `pwshadow` 命令完成的。

在提示符后。它不会打印任何消息，但当你的 shell 提示符返回时，你应该拥有一个 `/etc/shadow` 文件，并且你的 `/root/passwd` 文件现在看起来应该是这样：

```
root:x:0:0:root:/bin/bash
bin:x:1:1::/bin:
dnemon:x:2:2::daemon:/sbin
.
mary:x:500:100:Mary Smith:/home/mary:/bash
je:x:501:100:John Johnson:/home/joe:/bash
jane:x:502:100:Jane Anderson:/home/jane:/bash
bob:x:503:100:Bob Reynolds:/home/bob:/bash
```
