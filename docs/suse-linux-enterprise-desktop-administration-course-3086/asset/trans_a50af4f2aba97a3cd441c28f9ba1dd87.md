
## find 命令

要在命令行上搜索文件，可以使用 `find` 命令。以下是 find 命令的语法：

```
find path criterion action
```

该命令有大量选项，其中一些在此解释。你可以使用以下参数与该命令一起使用：

- *path*—要搜索的文件系统部分（指定的目录及其所有子目录）。如果未指定，则搜索当前目录下的文件系统。
- *criterion*—文件应具有的属性如表 7-19 所示。

| Option | Description |
|---|---|
| `--ctime [+/-]days` | 搜索最后更改时间不超过（不早于）指定天数的文件。 |
| `--gid number` | 搜索具有 GID（组 ID）编号的文件。 |
| `--group name` | 搜索由组名拥有 的文件。也可以使用数字 GID 代替名称。 |
| `--name pattern` | 搜索名称包含给定模式的文件。如果模式包含元字符（例如 `$` 或通配符），它们必须用引号括起来。否则，它将被 shell 而不是 find 命令解释。 |
| `--size [+/-]size` | 匹配大于或小于特定大小的文件。作为参数，给出大小（以 512 字节块为单位）。后缀 `c` 切换到字节，`k` 切换到 1024 字节块。前面加 `+` 表示所有更大的文件，`-` 表示所有更小的文件。 |
| `--type file_type` | 搜索文件类型。文件类型可以是以下之一：`d` 表示目录，`f` 表示文件，或 `l` 表示符号链接。 |
| `--uid number` | 搜索具有 UID（用户 ID）编号的文件。 |
| `--user name` | 搜索由用户名拥有 的文件。也可以使用数字 UID 代替名称。 |

Table 7-19

- *action*—影响以下条件或控制整个搜索的选项，例如以下：
  - `print` (default)
  - `exec command`

使用 `-exec` 选项，你可以调用另一个命令。此选项经常用于将 `find` 和 `grep` 链接起来，如下所示：

```text
geeko@da10:~ > find ~ -name 'letter*' -type f -exec grep appointment {} \;
appointment for next meeting: 23.08.
/home/geeko/letters/letter_Smith
geeko@da10:~ >
```

在此示例中，`find` 命令搜索名称以“letter”开头的文件。找到的文件名由 `-exec` 传递给以下命令（在本例中为 `grep appointment {}`）。

两个大括号 `{}` 用作文件名占位符，这些文件名被找到并传递给 `grep` 命令。分号关闭 `-exec` 指令。由于这是一个特殊字符，因此通过在其前面放置反斜杠来屏蔽它。

当单独使用 `grep` 时，它会在文件系统位置已知的文件中搜索特定表达式。当与 `find` 结合使用时，搜索的是包含特定表达式但位置未知的文件。

## which 命令

`which` 命令搜索变量 PATH 中列出的所有路径以查找指定的命令并返回该命令的完整路径。PATH 变量包含 shell 查找可执行文件的目录。

![](img/9129877170834ca9d5fdac5319bf5f12_242_0.png)

要查看变量的内容，请使用 `echo` 命令并在变量名称前加上“$”。要查看变量 PATH 的内容，请输入 `echo $PATH`。

如果不同目录中存在多个版本的命令，`which` 命令尤其有用。如果你想知道在不指定路径的情况下输入命令时执行哪个程序，则使用 `which`。

以下是使用 `which` 命令的示例：

```text
geeko@da10:~ > which find
/usr/bin/find
geeko@da10:~ > which cp
/bin/cp
geeko@da10:~ > which grep
/usr/bin/grep
geeko@da10:~ >
```

有关 which 的更多信息，请输入 `man which`。

## type 命令

*type* 命令可用于查找在输入 *command* 时执行的是哪种类型的命令——shell 内置（硬编码在 shell 中的基本命令）、外部命令（由 shell 调用）、别名或函数。选项 -a 显示文件系统中具有此名称的命令的所有实例。

以下是使用 type 命令的示例：

```text
geeko@da10:~ > type type
type is a shell built in
geeko@da10:~ > type grep
grep is /usr/bin/grep
geeko@da10:~ > type -a grep
grep is /usr/bin/grep
grep is /bin/grep
geeko@da10:~ >
```

![](img/9129877170834ca9d5fdac5319bf5f12_243_0.png)

## 练习 7-6： 在 Linux 上查找文件

在此练习中，使用 **whereis**、**which** 和 **find** 命令以及 GNOME 搜索工具查找文件。

## 完成此练习的详细步骤

- 第一部分：使用 whereis 和 which 命令
- 第二部分：使用 GNOME 搜索工具
- 第三部分：使用 find 命令

## 第一部分：使用 whereis 和 which 命令

要使用 whereis 和 which 命令，请执行以下操作：

1. 打开一个终端窗口。
2. 通过输入以下内容查找 ll 命令的类型
   ```text
   type ll
   ```
3. 通过输入以下内容查找 find 命令的手册页
   ```text
   whereis -m find
   ```
4. 通过输入以下内容查找 Firefox 程序的路径
   ```text
   which firefox
   ```

## 第二部分：使用 GNOME 搜索工具

要使用 GNOME 搜索工具，请执行以下操作：

1. 启动 GNOME 搜索工具（计算机 > 更多应用程序 > 系统 > GNOME 搜索工具）。
2. 通过执行以下操作查找主目录中名称以 my 开头的所有文件：
   a. 在“名称包含”字段中输入 `my*`。
   b. 选择 **Find**。
3. 通过执行以下操作查找 `/bin/` 目录中名称由两个字符组成的所有文件：
   a. 在“名称包含”字段中输入 `??`。
   b. 仅在 `/bin` 目录中搜索，打开 **Look in Folder** 菜单；然后选择 **Other**。
   c. 从对话框中选择 **bin**；然后选择 **Open**。
   d. 选择 **Find** 开始搜索。
4. 通过执行以下操作查找 `/tmp/` 目录中在过去 24 小时内更改或创建的所有文件：
   a. 在“名称包含”字段中输入 `*`。
   b. 仅在 `/tmp` 目录中搜索，打开 **Look in Folder** 菜单。从菜单中选择 **Other**。
   c. 从对话框中选择 **tmp**；然后选择 **Open**。
   d. 选择 **Select More Options**。
   e. 从 **Available Options** 菜单中选择 **Date Modified Less Than**；然后选择 **Add**。
   f. 在 **Date Modified Less Than** 文本框中输入 `1`。
   g. 选择 **Find**。
5. 关闭搜索对话框。

## 第三部分：使用 find 命令

要使用 find 命令，请执行以下操作：

1. 启动一个终端窗口。
2. 通过输入以下内容查找主目录中名称以 my 开头的所有文件

   `find ~ -name 'my*'`

3. 通过输入以下内容查找 `/tmp` 目录中在过去 24 小时内更改或创建的所有文件

   `find /tmp -ctime -1`

4. 通过输入 `exit` 关闭终端窗口。

## 摘要

- Linux 文件系统使用一系列目录层次结构来存储文件。
- 无论文件系统数量多少，Linux 中只有一个根目录，用“/”字符表示。
- Linux 目录和文件遵循文件系统层次标准（FHS），其位置可以使用绝对或相对路径名描述。你可以使用 pwd 命令查看当前目录，或使用 cd 命令更改目录。
- /bin 和 /sbin 目录包含可执行二进制程序。文件系统中有许多其他目录名称为 bin 和 sbin。
- /boot 目录包含用于加载 Linux 内核的信息。
- /dev 目录包含字符和块设备文件，用于标识 Linux 系统上大多数硬件设备。每个设备文件包含一个主号，用于标识 Linux 内核中的设备驱动程序，以及一个次号，用于标识特定设备的实例。你可以使用 mknod 命令创建设备文件。
- 大多数系统配置信息存储在 /etc 目录下的文本文件中，共享库存储在 /lib 目录下。
- 主目录通常位于 /home 目录下，并以其用户帐户命名（例如，/home/gecko）。root 用户的主目录始终为 /root。
- /media 和 /mnt 目录通常包含挂载点子目录，用于挂载和访问诸如 CD-ROM、CD-RW、DVD 和软盘等可移动媒体。系统通常会自动挂载这些设备，但你可以使用 mount 和 umount 命令手动将设备挂载和卸载到这些目录。
- 非 Linux 分区通常挂载到以 /data 或 /windows 开头的目录。
- /usr 和 /opt 目录存储大多数系统和用户应用程序。此外，许多应用程序将应用程序数据存储在 /srv 目录中，并将临时文件存储在 /tmp 目录中。
- 日志文件、 spool 目录和特定于应用程序的文件通常存储在 /var 目录下。
- /proc 和 /sys 目录是系统内存中的虚拟目录，包含由 Linux 内核公开的信息，包括进程、硬件、网络和版本信息。因此，这些目录中的文件通常用于系统故障排除。
- Linux 文件系统上可以存在许多类型的文件，例如普通文件（文本文件、数据文件、可执行程序）、目录、设备文件、链接文件、套接字和命名管道（FIFO）。你可以使用 ls 命令的各种选项查看文件名信息。
- touch 命令可以创建新文件或更新现有文件的时间戳。

