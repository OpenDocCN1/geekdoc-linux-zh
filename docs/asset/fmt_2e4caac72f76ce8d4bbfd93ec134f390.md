
```bash
# chmod 660 MyFile
# ls -l MyFile
-rw-rw---- 1 root sales 23 2009-05-27 22:31 MyFile
```

示例 2：模式 `755` 将为所有者提供完全访问权限，并为组和其他人提供读/执行访问权限。

```bash
# chmod 755 MyProgram.sh
# ls -l MyProgram.sh
-rwxr-xr-x 1 root sales 23 2009-05-27 22:31 MyProgram.sh
```

示例 3：模式 `600` 将为所有者提供读写访问权限，而为其他人不提供任何访问权限。

```bash
# chmod 600 MyFile
# ls -l MyFile
-rw------- 1 root sales 23 2009-05-27 22:31 MyFile
```

示例 4：应用于目录的模式 `775` 将为所有者和组提供读/写/执行访问权限，并为其他人提供只读访问权限。

```bash
$ chmod 775 MyDirectory
$ ls -ld MyDirectory
drwxrwxr-x 2 root sales 4096 2009-05-27 16:04 MyDirectory
```

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `chmod [MODE] [FILE]` | 更改指定文件的权限 |
| `chmod [MODE] -R [DIR]` | 递归更改所有文件的权限 |

### chown

**用途：** 更改文件或目录的所有者。

**语法用法：** `chown [OPTIONS] [USER:GROUP] [DIRECTORY/FILE]`

```bash
# ls -l ShoppingList.txt
-rw-r--r-- 1 nick nick 23 2009-05-27 22:31 ShoppingList.txt
# chown root ShoppingList.txt
# ls -l ShoppingList.txt
-rw-r--r-- 1 root nick 23 2009-05-27 22:31 ShoppingList.txt
```

*使用 `chown` 命令更改文件的所有者*

`chown` 命令用于更改文件或目录的所有者。在上面的示例中，`ShoppingList.txt` 文件的所有者从 `nick` 更改为 `root`。

下一个示例演示了如何使用 `chown` 命令同时更改文件的所有者和组。

```bash
# ls -l ShoppingList.txt
-rw-r--r-- 1 root nick 23 2009-05-27 22:31 ShoppingList.txt
# chown nick:sales ShoppingList.txt
# ls -l ShoppingList.txt
-rw-r--r-- 1 nick sales 23 2009-05-27 22:31 ShoppingList.txt
```

*使用 `chown` 命令更改文件的所有者和组*

执行 `chown nick:sales ShoppingList.txt` 命令后，`ShoppingList.txt` 文件的所有者更新为 `nick`，组更新为 `sales`。

> **提示**
>
> 如果只需更改文件的组，可以使用 `chgrp` 命令（在第 88 页中有讨论）。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `chown [USER] [FILE]` | 更改文件的所有者 |
| `chown [USER]:[GROUP] [FILE]` | 更改文件的所有者和组 |
| `chown -R [USER] [DIR]` | 递归更改指定目录中所有文件的所有者 |

### chgrp

**用途：** 更改文件和目录的组。

**语法用法：** `chgrp [OPTIONS] [GROUP] [DIRECTORY/FILE]`

```bash
# ls -l ShoppingList.txt
-rw-r--r-- 1 root root 23 2009-05-27 22:31 ShoppingList.txt
# chgrp sales ShoppingList.txt
# ls -l ShoppingList.txt
-rw-r--r-- 1 root sales 23 2009-05-27 22:31 ShoppingList.txt
```

*使用 `chgrp` 命令更改文件的组*

`chgrp` 命令用于更改文件或目录的组。在上面的示例中，使用 `chgrp` 命令将 `ShoppingList.txt` 文件的组从 `root` 更改为 `sales`。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `chgrp [GROUP] [FILE]` | 将文件的组更改为指定的组 |
| `chgrp -R [DIR]` | 递归更改所有文件的组 |

### umask

**用途：** 显示/设置用户默认的文件创建掩码。

**语法用法：** `umask [OPTIONS] [MODE]`

```bash
$ umask
022
```

*显示当前用户的 `umask`*

`umask` 控制用户默认的文件创建掩码。这决定了新创建的文件和目录将被分配的权限。要确定文件/目录创建模式，`umask` 值从目录的 `777` 和文件的 `666` 中减去。例如，`umask` 为 `022` 将为文件创建有效权限 `644`（`rw-r-x--`），为目录创建 `755`（`rwxr-xr-x`）。

在某些系统中，可以使用 `-S` 选项以更友好的符号形式显示 `umask` 值，如下一个示例所示。

```bash
$ umask -S
u=rwx,g=rx,o=rx
```

*以符号表示法显示 `umask`*

`umask` 命令还可以用于更改 `umask` 值，如下一个示例所示。

```bash
$ umask 077
```

*设置 `umask` 值*

在此示例中，`umask` 值为 `077` 将为文件创建有效权限 `600`（`rw-------`），为目录创建 `700`（`rwx------`）。

> **注意**
>
> 在命令行上指定的 `umask` 值在您注销时会被重置。若要使 `umask` 永久生效，必须将其添加到用户主目录中的 `.*profile` 文件或 `/etc/profile`（针对所有用户）。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `umask` | 以八进制格式显示 `umask` |
| `umask -S` | 以符号格式显示 `umask` |
| `umask [MODE]` | 将 `umask` 设置为指定值 |

### su

**用途：** 切换用户账户。

**语法用法：** `su [OPTIONS] [USER]`

```bash
$ whoami
nick
$ su
Password: ******
### whoami
root
```

*使用 `su` 命令从普通用户切换到 `root` 用户*

`su` 命令（`Switch User` 的缩写）允许您登录为另一个用户，而无需先注销系统。在上面的示例中，普通用户使用 `su` 切换到 `root` 用户账户。请注意，当您变成 `root` 用户时，您的 shell 提示符从 `$` 变为 `#`。作为 `root` 用户，您现在可以运行需要提升权限的命令。

> **提示**
>
> 您应始终限制以 `root` 用户登录的时间。这是一个良好的实践，可以帮助减少事故。

默认情况下，不带参数执行 `su` 会切换到 `root` 用户账户。可以使用 `su` 指定用户名以变成不同的用户，如下一个示例所示。

```bash
$ whoami
nick
$ su steve
Password: ******
$ whoami
steve
```

*使用 `su` 切换到另一个用户*

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `su` | 切换到 `root` 用户账户 |
| `su -` | 切换到 `root` 用户账户并加载 `root` 的配置文件 |
| `su [USERNAME]` | 切换到指定的用户名 |

### sudo

**用途：** 以不同用户身份运行单个命令。

**语法用法：** `sudo [OPTIONS] [COMMAND]`

```bash
$ whoami
nick
$ sudo whoami
[sudo] password for nick: ******
root
$ whoami
nick
```

*使用 `sudo` 以 `root` 用户身份运行命令*

`sudo` 命令允许您以另一个用户身份运行单个命令。它通常用于执行需要 `root` 权限的命令。在此示例中，通过 `sudo` 命令以 `root` 身份执行 `whoami`。
