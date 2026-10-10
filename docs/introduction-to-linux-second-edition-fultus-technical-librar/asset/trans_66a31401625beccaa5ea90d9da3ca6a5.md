
普通文件。它们的后缀可能是 .desktop 或 .lnk；在 `~/.gnome-desktop` 目录下可以找到示例：

```
[dupont@boulut .gnome-desktop]$ cat La Maison Dupont
[Desktop Entry]
Encoding=Legacy-Mixed
Name=La Maison Dupont
Type=X-Nutilus-home
X-Nutilus-Icon=temp-home
URL=file:///home/dupont
```

这个示例来自一个 KDE 桌面：

```
[lena@venus Desktop]$ cat camera
[Desktop Entry]
Dev=/dev/sda1
FSType=auto
Icon=memory
MountPoint=/mnt/camera
Type=FSType
X-KDE-Dynamic-Device=true
```

使用图形环境的功能来创建这种链接非常简单。如果你需要帮助，系统文档应该是你的首选资源。

在下一节中，我们将研究如何使用命令行创建 UNIX 风格的符号链接。

### 3.3.5.2 创建符号链接

符号链接对初学者特别有用：它们看起来相当直观，而且你不需要担心分区的问题。

创建链接的命令是 `ln`。为了创建符号链接，你需要使用 `-s` 选项：

```
ln -s targetfile linkname
```

在下面的示例中，用户 freddy 在其主目录的一个子目录中创建了一个指向系统其他位置目录的链接：

```
freddy:~/music> ln -s /opt/mp3/Queen/ Queen

freddy:~/music> ls -l
lrwxrwxrwx 1 freddy freddy 17 Jan 22 11:07 Queen -> /opt/mp3/Queen
```

符号链接始终是非常小的文件，而硬链接的大小与原始文件相同。

符号链接的应用非常广泛。它们常用于节省磁盘空间，为了新程序的安装需求（该程序期望文件位于另一个位置）而制作文件的副本，用于修复突然需要在新环境中运行的脚本，并且通常可以节省大量的工作。系统管理员可能会决定将用户的主目录移动到新的位置，例如 disk2，但如果他希望一切像以前一样运行（例如 /etc/passwd 文件），他只需付出最少的努力，从 /home 创建指向新位置 /disk2/home 的符号链接即可。

## 3.4 文件安全

### 3.4.1 访问权限：Linux 的第一道防线

Linux 安全模型基于 UNIX 系统所使用的模型，并且像 UNIX 安全模型一样严格（有时甚至更严格），而这已经相当健壮了。在 Linux 系统中，每个文件都有一个用户和一个组用户拥有它。还有第三类用户，即非文件所有者且不归属于文件所属组的用户。对于每一类用户，可以授予或拒绝读、写和执行权限。

我们之前在使用 `ls -l` 命令列出文件时已经使用过 *长* 选项，尽管当时是为了其他目的。该命令还显示这三类用户的文件权限；它们由文件属性列表开头处（表示文件类型的第一个字符之后的）九个字符表示。如下面的示例所示，这九个字符序列中的前三个字符显示实际拥有该文件的用户的访问权限。接下来的三个字符代表文件的组所有者，最后三个字符代表其他用户。权限的顺序始终相同：用户对文件、组和其他用户的读、写、执行权限。一些示例：

```
marise:~> ls -l To_Do
-rw-rw-r-- 1 marise users     5 Jan 15 12:39 To_Do
marise:~> ls -l /bin/ls
-rwxr-xr-x 1 root   root    45948 Aug  9 15:01 /bin/ls*
```

第一个文件是一个普通文件（第一个短划线）。用户名为 *marise* 的用户或属于 *users* 组的用户可以读取和写入（修改/移动/删除）该文件，但不能执行它（第二个和第三个短划线）。所有其他用户仅允许读取该文件，但不能写入或执行它（第四个和第五个短划线）。

第二个示例是一个可执行文件，区别在于：每个人都可以运行这个程序，但你需要是 *root* 才能修改它。

Info 页面详细解释了 `ls` 命令如何处理访问权限的显示，请参阅 *What information is listed* 部分。

为了方便在命令中使用，访问权限（或模式）和用户组都有代码。参见下表。

| 代码 | 含义 |
| :--- | :--- |
| 0 或 - | 此位置本应授予的访问权限未被授予。 |
| 4 或 r | 此位置定义的用户类别被授予读取访问权限 |
| 2 或 w | 此位置定义的用户类别被授予写入权限 |
| 1 或 x | 此位置定义的用户类别被授予执行权限 |

表 3.7. 访问模式代码

| 代码 | 含义 |
| :--- | :--- |
| u | 用户权限 |
| g | 组权限 |
| o | 其他用户的权限 |

表 3.8. 用户组代码

这种直截了当的方案被非常严格地应用，即使在没有任何网络安全措施的情况下也能提供高水平的安全性。除了其他功能外，该安全方案还负责管理用户对程序的访问，它可以根据“需知”原则提供文件服务，并保护敏感数据，例如主目录和系统配置文件。

你应该知道你的用户名是什么。如果你不知道，可以使用 id 命令显示它，该命令还会显示你所属的默认组以及你可能是成员的其他组：

```
tilly:-> id
uid=504(tilly) gid=504(tilly) groups=504(tilly), 100(users), 2051(org)
```

你的用户名还存储在环境变量 USER 中：

```
tilly:-> echo $USER
tilly
```

### 3.4.2 工具

#### 3.4.2.1 chmod 命令

应用严格的文件权限的一个正常后果（有时是个麻烦）是，出于各种原因，需要更改访问权限。我们使用 chmod 命令来做这件事，最终 chmod 甚至变成了一个几乎被接受的英语动词，意味着更改文件的访问模式。**chmod** 命令可以使用字母数字或数字选项，取决于你更喜欢哪种。

下面的示例使用字母数字选项来解决新用户常遇到的问题：

```
asim:~> ./hello
bash: ./hello: bad interpreter: Permission denied

asim:~> cat hello
#!/bin/bash
echo "Hello, World"

asim:~> ls -l hello
-rw-rw-r-- 1 asim asim 32 Jan 15 16:29 hello

asim:~> chmod u+x hello

asim:~> ./hello
Hello, World

asim:~> ls -l hello
-rwxw-r--- 1 asim asim 32 Jan 15 16:29 hello*
```

+ 和 - 运算符用于授予或拒绝给特定组的特定权限。允许使用逗号分隔的组合。Info 和 man 页面包含有用的示例。这是另一个示例，使前一个示例中的文件成为用户 *asim* 的私有文件：

```
asim:~> chmod u+rxw,go-rwx hello

asim:~> ls -l hello
-rwx----- 1 asim asim 32 Jan 15 16:29 hello*
```

导致某处出现权限拒绝错误消息的问题类型，通常是由访问权限问题引起的。此外，像“昨天还能用”和“当我以 root 身份运行时它可以工作”这样的评论，也很可能是由错误的文件权限引起的。

当使用 **chmod** 配合数字参数时，每个组中授予的每个访问权限值必须累加在一起。因此，我们会得到一个 3 位数，这是 **chmod** 需要设置的符号值。下表列出了最常见的组合：

| 命令 | 含义 |
| :--- | :--- |
| chmod 400 file | 保护文件免受意外覆盖。 |
| chmod 500 | 保护自己意外删除、重命名或移动此目录中的文件。 |
| chmod 600 file | 私有文件，仅输入此命令的用户可以更改。 |
| chmod 644 file | 公共可读文件，仅发起用户可以更改。 |
| chmod 660 file | 属于你组的用户可以更改此文件，其他人完全无法访问。 |
| chmod 700 file | 保护文件免受其他用户的任何访问，而发起用户仍具有完全访问权限。 |
| chmod 755 directory | 用于其他用户应可读取和可执行的目录，但仅由发起用户可更改。 |
| chmod 775 file | 组的标准文件共享模式。 |
| chmod 777 file | 每个人都可以对此文件做任何事。 |

表 3.9. 使用 chmod 保护文件

如果输入的数字位数少于三位作为 **chmod** 的参数，省略的字符将从左侧开始用零替换。实际上，Linux 系统还有一个第四位数字，它位于前三位之前，并设置特殊的访问模式。关于这些以及更多内容的详细信息位于 Info 页面中。

#### 3.4.2.2 登录到另一个组

当你在命令行输入 **id** 时，你会得到一个列表，显示你所有可能所属的组，前面是你的用户名和 ID，以及你当前连接的组名和 ID。然而，在许多 Linux 系统中，你一次只能主动登录到一个组。默认情况下，这个活动的或 *主组* 是你从 `/etc/passwd` 文件中分配的那个。该文件的第四个字段包含用户的主组 ID，这可以在 `/etc/group` 文件中查找。一个示例：

```
asim:~> id
uid=501(asim) gid=501(asim) groups=100(users),501(asim),3400(web)

asim:~> grep asim /etc/passwd
asim:x:501:501:Asim El Baraka:/home/asim:/bin/bash

asim:~> grep 501 /etc/group
asim:x:501:
```

