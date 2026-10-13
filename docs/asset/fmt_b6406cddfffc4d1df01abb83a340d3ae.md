
| :--- | :--- |

| 此字段 | 包含 |

| username | 字母数字用户名，通常为 8 个字符且唯一（Red Hat Linux 允许用户名超过 8 个字符，但某些操作系统不允许） |

| password | 存在时，为一个 13 字符的加密密码（空字段表示访问账户不需要密码；x 表示密码存储在 `/etc/shadow` 文件中，更安全） |

| UID | 作为用户标识符的唯一数字（root 的 UID 为 0，1 到 100 之间的 UID 留给作为服务器的非人类用户；最好将 UID 保持在 32,767 之下） |

| GID | 用户所属组的默认组 ID（GID 0 用于 root 组；其他组在 `/etc/group` 中定义，用户通常可以同时属于多个组） |

| GCOS | 关于用户的可选个人信息（`finger` 命令使用此字段表示 General Electric Comprehensive Operating System，这是一个被遗忘的操作系统，其名称已被该字段的名称所固定了） |

| homedir | 主目录名称 |

| shell | 命令解释器（例如 `/bin/bash`） |

## 管理组 433

```
username:password:UID:GID:GECOS:homedir:shell
```

表 2-1 解释了每个 `/etc/passwd` 条目中七个字段的含义。

| 表 2-1 /etc/passwd 文件字段含义 |

| :--- | :--- |

| 此字段 | 包含 |

| username | 字母数字用户名，通常为 8 个字符且唯一（Red Hat Linux 允许用户名超过 8 个字符，但某些操作系统不允许） |

| password | 存在时，为一个 13 字符的加密密码（空字段表示访问账户不需要密码；x 表示密码存储在 `/etc/shadow` 文件中，更安全） |

| UID | 作为用户标识符的唯一数字（root 的 UID 为 0，1 到 100 之间的 UID 留给作为服务器的非人类用户；最好将 UID 保持在 32,767 之下） |

| GID | 用户所属组的默认组 ID（GID 0 用于 root 组；其他组在 `/etc/group` 中定义，用户通常可以同时属于多个组） |

| GCOS | 关于用户的可选个人信息（`finger` 命令使用此字段表示 General Electric Comprehensive Operating System，这是一个被遗忘的操作系统，其名称已被该字段的名称所固定了） |

| homedir | 主目录名称 |

| shell | 命令解释器（例如 `/bin/bash`） |

`/etc/passwd` 文件是所有用户账户的列表。它是一个文本文件，任何用户都可以读取它——不需要特权。`/etc/passwd` 中的每行都有七个字段，用冒号（`:`）分隔。这是 `/etc/passwd` 文件中的一个典型条目：

```
naba:500:10:Naba Barkakati:/home/naba:/bin/bash
```

图 2-4 使用此典型条目来解释字段的含义。

![](img/509edf67e1a0798154916aafeb3f0878_458_0.png)

## 管理组

```
username:password:UID:GID:GECOS:homedir:shell
```

（注：此处后续重复内容已过滤处理）

| 表 2-1 /etc/passwd 文件字段含义 |

| :--- | :--- |

| 此字段 | 包含 |

| username | 字母数字用户名，通常为 8 个字符且唯一（Red Hat Linux 允许用户名超过 8 个字符，但某些操作系统不允许） |

| password | 存在时，为一个 13 字符的加密密码（空字段表示访问账户不需要密码；x 表示密码存储在 `/etc/shadow` 文件中，更安全） |

| UID | 作为用户标识符的唯一数字（root 的 UID 为 0，1 到 100 之间的 UID 留给作为服务器的非人类用户；最好将 UID 保持在 32,767 之下） |

| GID | 用户所属组的默认组 ID（GID 0 用于 root 组；其他组在 `/etc/group` 中定义，用户通常可以同时属于多个组） |

| GCOS | 关于用户的可选个人信息（`finger` 命令使用此字段表示 General Electric Comprehensive Operating System，这是一个被遗忘的操作系统，其名称已被该字段的名称所固定了） |

| homedir | 主目录名称 |

| shell | 命令解释器（例如 `/bin/bash`） |

## 探索用户环境 435

了解如何使用 `vi` 显示你正在编辑的文件。要查看 `TERM` 的当前设置，请在 shell 提示符处输入以下命令：

```
echo TERM
```

如果你在终端窗口输入此命令，输出如下：

```
xterm
```

在 Bash 中定义环境变量，请使用以下语法：

```bash
export NAME=Value
```

在这里，`NAME` 表示环境变量的名称，`Value` 是代表其值的字符串。因此，你可以使用以下命令将 `TERM` 设置为值 xterm：

```bash
export TERM=xterm
```

定义环境变量后，你只需通过 `NAME=new value` 语法指定新值即可更改其值。例如，要将 `TERM` 的定义更改为 vt100，在 shell 提示符处输入 `TERM=vt100`。

对于环境变量 `PATH`，你通常希望向现有定义中添加新目录，而不是从头开始定义 `PATH`。下面的示例展示了如何完成此任务：

```bash
export PATH=$PATH:/usr/games
```

此命令将字符串 `:/usr/games` 追加到 `PATH` 环境变量的当前定义中。最终效果是将 `/usr/games` 添加到 `PATH` 目录列表中。

注意，你也可以如下所示编写此 `export` 命令：

```bash
export PATH=$PATH:/usr/games
```

输入该命令后，你可以访问 `/usr/games` 目录中的程序，例如 `fortune`，这是一个打印简短且通常幽默（有时令人困惑）的格言的程序。如果你好奇，请继续输入以下命令：

```
fortune
```

`fortune` 打印随机的内容，但可能很有趣。结果应该是一个简短、幽默和/或令人困惑的格言。

## 436 更改文件的用户和组所有权

`PATH` 和 `TERM` 只是少数常见环境变量中的两个。表 2-3 列出了典型 Red Hat Linux 用户的一些环境变量。

| 环境变量 | 内容 |

| :--- | :--- |

| DISPLAY | X Window 系统显示输出的显示器（通常设置为 :0） |

| HOME | 你的家目录 |

| HOSTNAME | 你的系统的主机名 |

| LOGNAME | 你的登录名 |

| MAIL | 你的邮件目录位置 |

| PATH | shell 查找程序的目录列表 |

| SHELL | 你的 shell（Bash 对应 `SHELL=/bin/bash`） |

| TERM | 终端类型 |

## 更改文件的用户和组所有权

在 Red Hat Linux 中，每个文件或目录有两个所有者——用户和一个组。用户和组所有权用于控制谁可以访问文件或目录。

要查看文件或目录，使用 `ls -l` 命令查看目录的详细列表。例如，这里有一个典型文件的信息：

```
-rw-rw-rw-- 1 naba naba 40099 07-14 20:37 composer.txt
```

示例中，第一组字符显示文件的权限设置——谁可以读取、写入或执行该文件。第三和第四字段（在此示例中为 naba naba）指示文件的用户和组所有者。每个用户都有一个与用户名同名的私有组。大多数文件的用户和组所有权显示两次用户名。

作为系统管理员，你可能决定将文件的组所有权更改公共组。例如，假设你想将 `composer.txt` 文件的组所有权更改为 组。这样做，请以 root 身份登录并输入以下命令：

```bash
chgrp class composer.txt
```

## 更改文件的用户和组所有权 437

此 `chgrp` 命令将 `composer.txt` 的组所有权更改为 `class`。在我尝试之后，我再次输入 `ls -l` 来验证所有权，结果如下：

```
-rw-rw-r-- 1 naba class 40990 07-14 20:37 composer.txt
```

你可以使用 `chown` 命令更改用户所有者。命令格式如下：

```bash
chown filename
```

例如，将名为 `sample.jpg` 的文件的所有者更改为 `naba`，输入：

```bash
chown naba sample.jpg
```

事实上，`chown` 可以同时更改用户和所有组。例如，将用户所有者更改为 `naba`，组所有者更改为 `class`，输入：
