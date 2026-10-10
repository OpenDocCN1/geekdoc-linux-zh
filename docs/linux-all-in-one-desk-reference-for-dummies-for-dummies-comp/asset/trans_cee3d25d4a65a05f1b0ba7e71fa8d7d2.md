
# 提醒

你可以使用 `userdel` 命令删除用户账户。只需在命令提示符下输入 `/usr/sbin/userdel username` 即可删除用户账户。若同时希望清除该用户的家目录，请输入 `/usr/sbin/userdel -r username`。

要修改用户账户中的任何信息，请使用 `usermod` 命令。例如，如果我希望我的用户名 `naba` 的主要组为 `root`，我将输入以下命令：

```
usermod -g root naba
```

# 提示

要了解关于 `useradd`、`userdel` 和 `usermod` 命令的更多信息，请在终端窗口中输入 `man useradd`、`man userdel` 或 `man usermod`。

## 理解 /etc/passwd 文件

`/etc/passwd` 文件是用户账户的列表。它是一个文本文件，任何用户都可以读取——无需特殊权限。`/etc/passwd` 中的每一行包含七个字段，由冒号（`:`）分隔。

以下是 `/etc/passwd` 文件中的一个典型条目：

```
naba:x:500:10:Naba Barkakati:/home/naba:/bin/bash
```

**图 2-3：** 这个典型的 `/etc/passwd` 条目展示了各个字段的含义。

![](img/11709a8f88c8cd03868a929dc94c0e2b_442_0.png)

正如示例所示，`/etc/passwd` 中每行的格式如下：
`username:password:UID:GID:GECOS:home dir:shell`

表 2-1 解释了 `/etc/passwd` 条目中七个字段的含义。

**表 2-1** */etc/passwd 文件中字段的含义*

| 此字段 | 包含内容 |
| :--- | :--- |
| username | 字母数字用户名，通常为 8 个字符长且唯一（Linux 允许用户名长于 8 个字符，但某些其他操作系统不允许。） |
| password | 若存在，为 13 位加密密码。（空字段表示访问该账户无需密码。若为 x，则表示密码存储在 `/etc/shadow` 文件中，这样更安全。） |
| UID | 用作用户标识符的唯一数字。（`root` 的 UID 为 0，通常 1 到 100 之间的 UID 保留给非人类用户（如服务器服务）；最好将 UID 保持在 32,767 以下。） |
| GID | 用户所属组的默认组 ID（`GID` 0 对应组 `root`，其他组定义在 `/etc/group` 中，用户通常可以同时属于一个或多个组。） |
| GECOS | 关于用户的可选个人信息。（`The finger` 命令使用此字段，GECOS 代表 General Electric Comprehensive Operating System，这是一个早已被遗忘的操作系统，但其名称因 `/etc/passwd` 中该字段而得名而永存。） |
| home dir | 用户家目录的名称 |
| shell | 用户登录时执行的命令解释器（shell），例如 `bash`（`/bin/bash`） |

## 管理用户组

组是用户所属的集合。组具有名称和标识号（ID）。组定义完成后，用户可以属于这些组中的一个或多个。

你可以在 `/etc/group` 中找到所有现有组的列表。例如，定义名为 `wheel` 的组的那一行如下：
`wheel:x:10:root,naba`

如本例所示，/etc/group 中的每一行具有以下格式，由四个字段组成，以冒号分隔：

```
groupname:password:GID:membership
```

表 2-2 解释了组定义中四个字段的含义。

**表 2-2**

*/etc/group 文件中字段的含义*

| 字段名称 | 含义 |
| :--- | :--- |
| groupname | 组名称（例如，wheel） |
| password | 组密码（x 表示密码存储在 /etc/shadow 文件中） |
| GID | 数字组 ID（例如，10） |
| membership | 属于此组的逗号分隔的用户名列表（例如，root, naba） |

若要创建新组，只需使用 groupadd 命令。例如，若要添加一个名为 class 的新组，并自动选择组 ID，只需在终端窗口中输入以下命令（必须以 root 身份登录）：

```
groupadd class
```

然后，你可以使用 usermod 命令将用户添加到该组。例如，要将用户 naba 和 ashley 添加到名为 class 的组中，请输入以下命令：

```
usermod -G class naba
usermod -G class ashley
```

就这样。现在检查 /etc/group，发现其中包含 class 的以下定义：

```
class:x:502:naba,ashley
```

就是这么简单！

若要删除组，请使用 groupdel 命令。例如，若要删除名为 class 的组，请输入

```
groupdel class
```

# 探索用户环境

当你以用户身份登录时，你会获得一组控制你在 Linux 系统中所见所做许多方面的环境变量。若想看当前的环境，请在终端窗口中输入以下命令：

```
env
```

（顺便说一句，`printenv` 命令也能显示环境，但 `env` 更简短。）

`env` 命令会打印出一长串行。这一整集合行构成了当前环境，而每一行定义一个环境变量。例如，`env` 命令显示如下典型的一行：

```
HOSTNAME=localhost.localdomain
```

该行定义了环境变量 `HOSTNAME`，其值为 `localhost.localdomain`。

*环境变量* 不过是与字符串关联的名称。例如，名为 `PATH` 的环境变量通常这样为普通用户定义：

```
PATH=/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin
```

等号（`=`）右侧的字符串是 `PATH` 环境变量的 *值*。按照惯例，`PATH` 环境变量是一系列目录名，每个名称与前一个名称之间用冒号（`:`）分隔。

每个环境变量都有特定用途。例如，当 shell 需要搜索文件时，它只在 `PATH` 环境变量中列出的目录中搜索。shell 按照出现顺序搜索 `PATH` 中的目录。因此，如果两个程序具有相同的名称，shell 将执行它首先找到的那个。

与 shell 使用 `PATH` 环境变量类似，编辑器（如 `vi`）使用 `TERM` 环境变量的值来确定如何显示你用 `vi` 编辑的文件。要在 shell 提示符下查看 `TERM` 的当前设置，请输入以下命令：

```
echo $TERM
```

如果在终端窗口中输入此命令，输出如下：

```
xterm
```

要在 *bash* 中定义环境变量，请使用以下语法：

```
export NAME=Value
```

这里，*NAME* 表示环境变量的名称，*Value* 是代表其值的字符串。因此，使用以下命令可将 *TERM* 设置为值 *xterm*：

```
export TERM=xterm
```

定义环境变量后，你可以通过指定新值来更改其值，语法为 NAME=new-value。例如，要将 *TERM* 的定义更改为 *vt100*，请在 shell 提示符下输入 **TERM=vt100**。

对于 *PATH* 这样的环境变量，你通常希望向现有定义追加新的目录名，而不是从头定义 *PATH*。例如，如果你下载并安装了 Java 2 开发工具包（可从 http://java.sun.com/j2ee/1.5.0/download.jsp 获取），你就必须将 Java 二进制文件的位置添加到 *PATH* 中。以下是完成此任务的方法：

```
export PATH=$PATH:/usr/java/jdk1.5.0/bin
```

该命令将字符串 `:/usr/java/jdk1.5.0/bin` 追加到 *PATH* 环境变量的当前定义中。最终效果是将 `/usr/java/jdk1.5.0/bin` 添加到 *PATH* 的目录列表中。

**注意：** 你也可将这条导出命令写成如下形式：

```
export PATH=$(PATH):/usr/java/jdk1.5.0/bin
```

输入该命令后，你就可以访问 `/usr/java/jdk1.5.0/bin` 目录中的程序，例如 `javac`，这是将 Java 源代码转换为 Java 解释器可执行形式的 Java 编译器。

*PATH* 和 *TERM* 只是少数常见环境变量中的两个。表 2-3 列出了典型 Linux 用户的部分环境变量。

