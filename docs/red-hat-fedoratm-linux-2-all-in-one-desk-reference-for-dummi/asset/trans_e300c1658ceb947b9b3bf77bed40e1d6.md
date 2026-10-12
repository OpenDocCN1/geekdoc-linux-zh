
# 了解 /etc/passwd 文件

要修改用户账户中的任何信息，请使用 **usermod** 命令。例如，如果我希望我的用户名 *naba* 的主组为 **root**，我会键入以下命令：

```
usermod -g root naba
```

> 要了解关于 **useradd**、**userdel** 和 **usermod** 命令的更多信息，请在终端窗口中键入 **man useradd**、**man userdel** 或 **man usermod**。

## 了解 /etc/passwd 文件

/etc/passwd 文件列出了所有用户账户。它是一个文本文件，任何用户都可以读取它——无需特殊权限。/etc/passwd 中的每一行都有七个字段，由冒号（ **:** ）分隔。

以下是 /etc/passwd 文件中的一个典型条目：

```
naba:x:500:10:Naba Barkakati:/home/naba:/bin/bash
```

图 2-4 解释了此条目中七个字段的意义。

![](img/9f89727199836b0f871f1745838aa8b2_455_0.png)

如示例所示，/etc/passwd 中每行的格式如下：

```
username:password:UID:GID:GECOS:home dir:shell
```

表 2-1 解释了每个 /etc/passwd 条目中七个字段的意义。

| 表 2-1 | /etc/passwd 文件中各字段的意义 |
|---|---|
| **此字段** | **包含内容** |
| `username` | 一个字母数字用户名，通常长度为 8 个字符且唯一（Linux 允许用户名长于 8 个字符，但某些其他操作系统不允许） |
| `password` | 如果存在，为 13 个字符的加密密码（空字段表示访问该账户不需要密码，x 表示密码存储在 /etc/shadow 文件中，这样更安全） |
| `UID` | 一个唯一的数字，用作用户标识符（root 的 UID 为 0，通常 1 到 100 之间的 UID 保留给非人类用户，如服务器；最好保持 UID 小于 32,767） |
| `GID` | 用户所属组的默认组 ID（GID 0 用于 root 组，其他组定义在 /etc/group 中，用户可以并且通常同时属于多个组） |
| `GECOS` | 关于用户的可选个人信息（finger 命令使用此字段，GECOS 代表 General Electric Comprehensive Operating System，这是一个已被遗忘的操作系统，但通过 /etc/passwd 中此字段的名称而名留青史） |
| `homedir` | 用户主目录的名称 |
| `shell` | 命令解释器（shell），例如 Bash (/bin/bash)，当此用户登录时执行 |

# 管理组

组是用户所属的一种实体。组有一个名称和一个标识号（ID）。组定义后，用户可以属于这些组中的一个或多个。

您可以在 /etc/group 中找到所有现有组的列表。例如，下面是定义名为 wheel 的组的那一行：

```
wheel:x:10:root,naba
```

如此示例所示，/etc/group 中的每行具有以下格式，四个字段由冒号分隔：

```
groupname:password:GID:membership
```

表 2-2 解释了组定义中四个字段的意义。

| 表 2-2 | /etc/group 文件中各字段的意义 |
| --- | --- |
| **字段名称** | **意义** |
| *groupname* | 组的名称（例如，*wheel*） |
| *password* | 组密码（**x** 表示密码存储在 */etc/shadow* 文件中） |
| *GID* | 数字组 ID（例如，10） |
| *membership* | 属于此组的用户名逗号分隔列表（例如 *root,naba*） |

如果您想创建一个新组，只需在用户管理器中单击“添加组”按钮（参见图 2-1）。更快捷的方法是使用 **gpasswd** 命令。例如，要添加一个名为 *class* 的新组并自动选择组 ID，只需在终端窗口中键入以下命令（您必须以 *root* 身份登录）：

```
gpasswd class
```

然后，您可以使用 **usermod** 命令将用户添加到该组。例如，要将用户 *naba* 和 *ashley* 添加到名为 *class* 的组，我会键入以下命令：

```
usermod -G class naba
usermod -G class ashley
```

就这样。现在我检查 */etc/group*，发现它包含 *class* 的以下定义：

```
class:x:502:naba,ashley
```

就是这么简单！

如果您想删除一个组，请使用 **groupdel** 命令。例如，要删除一个名为 *class* 的组，键入：

```
groupdel class
```

# 探索用户环境

当您作为用户登录时，您将获得一组环境变量，这些变量控制着您在 Fedora Core 系统上看到和执行内容的许多方面。如果您想查看当前环境，请在终端窗口中键入以下命令：

```
env
```

（顺便说一下，`printenv` 命令也显示环境，但 `env` 更短。）

`env` 命令打印一长行列表。整个行集合就是当前环境，每一行定义一个环境变量。例如，`env` 命令显示如下典型的一行：

```
HOSTNAME=localhost.localdomain
```

这一行定义了环境变量 `HOSTNAME`，其定义为 `localhost.localdomain`。

*环境变量* 只不过是与其关联的字符串名称。例如，名为 `PATH` 的环境变量通常定义如下：

```
PATH=/usr/local/bin:./bin:/usr/bin:/usr/X11R6/bin
```

等号右边的字符串是 `PATH` 环境变量的值。按照惯例，`PATH` 环境变量是一系列目录名称，每个名称与前一个名称之间由冒号（`:`）分隔。

每个环境变量都有特定的用途。例如，当 shell 需要搜索文件时，它只需搜索列在 `PATH` 环境变量中的目录。shell 按 `PATH` 中目录出现的顺序进行搜索。因此，如果两个程序同名，shell 将执行它首先找到的那个。

类似于 shell 使用 `PATH` 环境变量的方式，像 `vi` 这样的编辑器使用 `TERM` 环境变量的值来确定如何使用 `vi` 显示您正在编辑的文件。要在 shell 提示符下查看 `TERM` 的当前设置，请键入以下命令：

```
echo $TERM
```

如果在终端窗口中键入此命令，输出如下：

```
xterm
```

要在 Bash 中定义环境变量，请使用以下语法：

```
export NAME=Value
```

这里，`NAME` 表示环境变量的名称，`Value` 是表示其值的字符串。因此，您使用以下命令将 `TERM` 设置为值 `xterm`：

```
export TERM=xterm
```

定义环境变量后，您可以通过使用 *NAME=new-value* 语法指定新值来更改其值。例如，要将 *TERM* 的定义更改为 *vt100*，请在 shell 提示符下键入 **TERM=vt100**。

对于像 *PATH* 这样的环境变量，您通常希望将新目录名称追加到现有定义中，而不是从头定义 *PATH*。例如，如果您下载并安装了 Java 2 软件开发工具包（可从 *java.sun.com/j2se/downloads/index.html* 获取），您必须将 Java 二进制文件的位置添加到 *PATH* 中。以下是完成此任务的方法：

```
export PATH=$PATH:/usr/java/j2sdk1.4.2_02/bin
```

此命令将字符串 `:/usr/java/j2sdk1.4.2_02/bin` 追加到 *PATH* 环境变量的当前定义中。净效果是将 `:/usr/java/j2sdk1.4.2_02/bin` 添加到 *PATH* 中的目录列表中。

注意：您也可以将此 *export* 命令编写为如下形式：

```
export PATH=${PATH}:/usr/java/j2sdk1.4.2_02/bin
```

键入该命令后，您可以访问 `/usr/java/j2sdk1.4.2_02/bin` 目录中的程序，例如 *javac*，这是一个将 Java 源代码转换为 Java 解释器可执行形式的 Java 编译器。

*PATH* 和 *TERM* 只是少数常见环境变量中的两个。表 2-3 列出了典型 Fedora Core 用户的一些环境变量。

表 2-3    Fedora Core 中的典型环境变量

| 环境变量 | 内容 |
| :--- | :--- |
| DISPLAY | X Window 系统显示输出的显示器名称（通常设置为 :0.0） |
| HOME | 您的主目录 |
| HOSTNAME | 您的系统主机名 |
| LOGNAME | 您的登录名 |
| MAIL | 您的邮件目录位置 |
| PATH | shell 查找程序的目录列表 |
| SHELL | 您的 shell（Bash 为 SHELL=/bin/bash） |
| TERM | 终端类型 |

