
这将每隔 60 秒截取一次屏幕，持续 1 小时，创建 60 个较大的 TIFF 文件，每个文件超过 1.5MB，顺序编号为 `capture1.tiff, capture2.tiff, ... capture60.tiff`。这对于训练目的非常有用，或者也许你怀疑在你吃午饭时有人使用了你的电脑：设置好这个后，你就可以回来查看发生过什么，而对方完全毫无察觉。

让我们来看一些更复杂的 Mac OS X 脚本。

## #93 列出 NetInfo 用户

为了开始学习如何使用 NetInfo，这里有一个简单的脚本，允许你通过脚本工具轻松地与 NetInfo 数据库进行交互。

## Code

```bash
#!/bin/sh
```

- `listmacusers` - 用于列出 Mac OS X NetInfo 数据库中用户的简单脚本。

- 注意，Mac OS 也有一个 `/etc/passwd` 文件，但它仅在启动初始阶段和恢复启动时使用。否则，所有数据都在 NetInfo db 中。

```
fields="
while getopts "Aahnprsu" opt ; do
  case $opt in
    A ) fields="$uid passwd name realhome shell" ;;
    a ) fields="$uid name realhome shell" ;;
    h) fields="$fields home" ;;
    n) fields="$fields name" ;;
    p) fields="$fields password" ;;
    r) fields="$fields realname" ;;
    s) fields="$fields shell" ;;
    u) fields="$uid uid" ;;
  ? ) cat << EOF
8
EOF
Usage: $0 [A|ahnprsu]
Where:

- -A 输出所有已知的 NetInfo 字段
-a 仅输出感兴趣的用户字段
-h 显示账户的主目录目录
-n 显示账户名
-p 密码（加密的）
-r 显示真实姓名/全名
-s 显示登录 shell
-u uid
EOF
exit 1
esac
done
"
```

```bash
exec netreport . /users ${fields:=uid name realhome shell}
```

## 工作原理

该脚本几乎大部分部分都用于构建变量`fields`，该字段初始为空。`netreport` 实用工具允许你指定想要查看的字段名称，因此，如果用户指定了`-a`获取所有感兴趣的字段，`netreport` 实际上会输入：

```
fields="uid name realhome shell"
```

这是一个清晰、直观的脚本，应该很容易理解。

## 运行脚本

`listmacusers` 脚本接受几个不同的命令行参数，如用法信息所示。你可以通过`-hnamsu`指定精确的字段和顺序，或者使用`-a`列出除加密密码字段以外的所有字段，或者使用`-A`强制列出所有内容。在不带任何参数的情况下，默认行为是显示所有感兴趣的用户字段(-a)。

## 结果

首先，我们指定想为 NetInfo 数据库中的每个账户使用用户 ID、登录名、真实姓名和登录 shell：

```
$ listmacusers -u -n -s
```

| ID | Name | Real Name | Shell |
| :--- | :--- | :--- | :--- |
| 0 | root | System Administrator | `/bin/sh` |
| 1 | daemon | System Services | `/dev/null` |
| 2 | nobody | Unprivileged User | `/dev/null` |
| 3 | test | | `/bin/tcsh` |
| 4 | | | `/dev/null` |
| 5 | test3 | Mr. Three | `/bin/tcsh` |
| 6 | tintin | Tintin, Reporter | `/bin/tcsh` |
| 7 | gary | Gary | `/bin/bash` |
| 8 | | | `/dev/null` |
| 99 | unknown | Unknown User | `/dev/null` |
| 55 | smmsp | Sendmail User | `/dev/null` |
| 70 | www | World Web Server | `/dev/null` |
| 74 | mysql | MySQL Server | `/dev/null` |
| 75 | sshd | Privilege separation | `/dev/null` |
| 505 | test3 | Mr. Three | `/bin/tcsh` |
| 501 | taylor | Dave Taylor | `/bin/bash` |
| 502 | badguy | Test Account | `/bin/tcsh` |
| 503 | test | | `/bin/tcsh` |
| 506 | tintin | Tintin, Reporter | `/bin/tcsh` |
| 507 | gary | Gary | `/bin/bash` |

注意，这显示了所有管理账户（基本上是所有带有 shell 的账户）。如果我们只想看登录账户，我们需要过滤掉 shell：

```
$ listmacusers -u -n -s | grep -v /dev/null
```

| ID | Name | Real Name | Shell |
| :--- | :--- | :--- | :--- |
| 0 | root | System Administrator | `/bin/sh` |
| 1 | daemon | System Services | `/dev/null` |
| 2 | nobody | Unprivileged User | `/dev/null` |
| 3 | test | | `/bin/tcsh` |
| 4 | | | `/dev/null` |
| 5 | test3 | Mr. Three | `/bin/tcsh` |
| 6 | tintin | Tintin, Reporter | `/bin/tcsh` |
| 7 | gary | Gary | `/bin/bash` |
| 8 | | | `/dev/null` |
| 99 | unknown | Unknown User | `/dev/null` |
| 55 | smmsp | Sendmail User | `/dev/null` |
| 70 | www | World Web Server | `/dev/null` |
| 74 | mysql | MySQL Server | `/dev/null` |
| 75 | sshd | Privilege separation | `/dev/null` |
| 505 | test3 | Mr. Three | `/bin/tcsh` |
| 501 | taylor | Dave Taylor | `/bin/bash` |
| 502 | badguy | Test Account | `/bin/tcsh` |
| 503 of test | | `/bin/tcsh` |
| 506 | tintin | Tintin, Reporter | `/bin/tcsh` |
| 507 | gary | Gary | `/bin/bash` |

那个坏账户不应该在那里的！为了查看那里有什么以及修改 NetInfo 条目，明智的做法是使用苹果提供的 NetInfo 应用，它可以在`Applications/Utilities`中找到或从命令行启动：

```bash
open -a "NetInfo Manager"
```

## #94 为 Mac OS X 添加用户

在书的之前，你看到了向典型的 Unix 或 Linux 系统添加新用户的基本步骤。Mac OS X 版本从根本上非常简单。本质上，是你提示账户名和登录 shell，向`/etc/passwd`和`/etc/shadow`文件追加适当的信息，创建新用户的家目录并设置某种初始密码。在 Mac OS X 上这没那么简单，因为向`/etc/passwd`追加信息不会创建新账户。相反，必须使用`netutil`命令将信息注入 NetInfo。

## Code
