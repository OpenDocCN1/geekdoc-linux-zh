
每个文件和目录都分配了所有者、所属组和权限设置。权限决定了用户是否获得访问特定文件或目录的权限。当 `ls` 命令后加上 `-l` 选项时，左侧出现的由 `r`、`w`、`x` 和 `-` 组成的九字符序列就是权限信息。这就是该文件或目录的模式。该序列由从左到右排列的三组 `rwx` 组成。`r`、`w` 或 `x` 表示允许相应的访问类型。连字符 (`-`) 表示不允许相应的访问类型。从左到右的这三组分别表示所有者、所属组和其他人的访问权限。

```
drwx-xr-x 12 root      1024 Jul 12 1999 local
```

```
drwx-xr-x 12 root      root
```

| 目录 | 访问权限 | 组的访问权限 | 其他人的访问权限 | 所有者 | 组 |
|---|---|---|---|---|---|

| | r | 读取权限 | 只能查看文件和目录的内容。 | | |
| | W | 写入权限 | | 可以修改文件和目录的内容。 | | |
| | X | 执行权限 | | 可以访问（执行）文件和目录。 | | |

## 目录的 rwxr-xr-x（所有者 root, 组 root）

### rwxr-xr-x 12 root root

初始的 `d` 表示这是一个目录。

- 如果用户是 root，该用户可以列出 (`r`) 文件和目录、修改 (`w`) 这些文件和目录，并访问或执行 (`x`) 这些文件和目录。
- 如果用户属于 root 组，该用户可以列出 (`r`) 文件和目录，并访问或执行 (`x`) 这些文件和目录。
- 如果用户不是 root 且不属于 root 目录，该用户可以列出 (`r`) 文件和目录，并访问或执行 (`x`) 这些文件和目录。

## 文件的 rwxr-xr-x（所有者 root, 组 root）

### rwxr-xr-x 1 root root

初始的连字符 (`-`) 表示这是一个普通文件。

- 如果用户是 root，该用户可以读取文件内容、写入文件并执行文件。
- 如果用户属于 root 组，该用户可以读取文件内容并执行文件。
- 如果用户不是 root 且不属于 root 目录，该用户可以读取文件内容并执行文件。

## 如何设置权限

每个 `rwx` 字符字符串由一个数字表示，整组九位权限使用三个数字表示。其值是允许的访问权限对应的数字之和（`r=4`，`w=2`，且 `x=1`）。例如，`rwx` 由数字 7 表示。

| r w x | | |
|---|---|---|

| r w x | 4+2+1 | 7 |
| r - x | 4+0+1 | 5 |
| r w - | 4+2+0 | 6 |
| r - - | 4+0+0 | 4 |

因为 `rwx` 取值为 7，而 `r-x` 取值为 5，权限 `rwxr-xr-x` 由数字 755 表示。

| r w x | r - x | r - - |
|---|---|---|

| 4+2+1 | 4+0+1 | 4+0+1 |
| 7 | 5 | 5 |

此数字在更改或设置文件或目录的权限时使用。

## 创建用户

### useradd

在 Linux 中创建用户是为了不仅可以登录，还能识别是谁在使用系统。所有操作都以单个用户的形式管理。用户是处理工作区域、文件访问权限以及 Linux 其他方面的基本单位。

你应该以用户身份登录，然后使用 `su` 命令切换到 root。使用 `useradd` 命令在 Linux 中创建新用户。

即使是系统管理员也不应直接以 root 身份登录。相反，系统管理员-

### 以 root 身份登录。

Red Hat Linux release 6.0 Publisher's Edition (Hedwig)

Kernel 2.2.5-15 on an i686

```
server login: root
Password:
Last login: Sun Jul 11 22:51:36 on tty1
[root@server /]:
```

> 输入 "root"，并输入 root 密码。

![](img/17f00f03278f20a01f42454f91fb48b8_109_0.png)

## 创建新用户。

创建一个名为 bob 属于 users 组的用户。

输入命令。

Red Hat Linux release 6.0 Publisher's Edition (Hedwig)

Kernel 2.2.5-15 on an i686

```
server login: root
Password:
Last login: Sun Jul 11 22:51:36 on tty1
[root@server /]: useradd -g users -p '' bob
[root@server /]:
```

> 如果指定密码，使用单引号。

### useradd 命令

`useradd` 添加了名为 foo 的用户。

### useradd 命令

- `-g` 将新用户加入组。
- `p` 设置新用户的密码。

## 修改密码

### 修改密码。

输入 `passwd` 命令。

用户应该更改自己的密码。

红帽 Linux 版本 6.0 发行版 (Hedwig)

内核 2.2.5-15 运行在 i686 上

```
server login: bob
[bob@server bob~$ passwd ✎]
New UNIX password:
```

输入新密码。

再次输入相同的新密码。

```
[bob@server bob$] passwd
New UNIX password:
Retype new UNIX password:
passwd: all authentication token updated successfully
[bob@server bob$]
```

出现一条消息

密码已成功更新

## 密码是重要的密钥

密码是保护每个用户信息的唯一密钥。任何知道你密码的人都可以用你的用户名登录 Linux。即使你们处于同一个网络中，你无法确切知道冒充者正在做什么。请务必谨慎管理你的密码，特别是在连接互联网时，因为人们可以从世界上任何地方访问你的 Linux 机器。此外，如果你的密码被盗，认为只有你个人会受到负面影响是错误的。你必须考虑冒充者可能会给他人带来麻烦的可能性。

## 忘记密码

如果用户忘记了密码，切换到 root 用户并用新密码覆盖用户的密码。如果你执行 `passwd` 命令并将用户名作为参数，就可以设置该用户的密码。设置一个简单的密码以便用户登录，然后让用户设置一个新密码。

```
[root@server /root]# passwd ✎
Changing password for user bob
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully
[root@server /root]#
```

## 编辑文本配置文件

### vi 文本编辑器

为了配置 Internet 服务器，本书使用了 `vi`（这是 Linux 自带的标准编辑器）来编辑配置文件。

`vi` 文本编辑器有命令模式和输入模式。在输入模式下，你输入字符；在命令模式下，你输入命令。起初，`vi` 文本编辑器用起来可能很难用，但在反复使用后，你就会熟悉它的操作。本节解释了 `vi` 文本编辑器的基础，并列出了特别实用的编辑命令。你还可以使用 `vi` 的两个特殊版本来编辑密码文件 (`viwp`) 以及设置组文件 (`vigr`)。`vigr` 是编辑组文件的最佳选择，而 `viwp` 用于编辑密码文件。

### 熟悉命令模式和输入模式

`vi` 文本编辑器有命令模式和输入模式。虽然在命令模式下无法输入文本，但你可以轻松切换到输入模式来输入文本。从输入模式返回命令模式，按下 `[Esc]`。

| 命令模式 | 输入模式 |
| --- | | |
| 执行基本操作（如删除或复制文本或保存文件）的模式。 | 输入文本的模式。 |
| 按 `[Esc]` 切换到命令模式。 | |

### 输入文本

- `i` 在当前光标位置之前立即插入文本。

  按下 "i" 并输入 "word"。

  wordword tango

- `a` 在光标右侧立即追加文本。

  按下 "a" 并输入 "word"。

  wordword tango

  wordord tango

- `o` 在当前行下方直接开启新行。

  按下 "o" 并输入 "word"。

  wordword tango

  wordword_ tango

## 编辑配置文件

### 删除文本

- `x` 删除当前字符。

| wordord tango | 按一次 “x”。 | wordord tango |

### 搜索文本

- `/word` 搜索文本 “word”

| wordord tango | 指定 /word | wordord tango |
| | 搜索从当前光标位置后开始，光标移动到下一个匹配项的开头 |
