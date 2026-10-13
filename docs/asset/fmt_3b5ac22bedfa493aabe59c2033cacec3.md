
## 2. 使用 `smbpasswd` 程序为每个用户创建加密的 Samba 密码
例如，要为名为 `sheila` 的用户创建加密的 Samba 密码，请运行以下命令：
```
smbpasswd sheila
```

## 3. 修改 `/etc/samba/smb.conf` 文件
使以下行出现在 `[global]` 配置部分：
```
encrypt passwords = yes
```

## 4. 测试并重启服务
通过运行 `testparm` 程序测试新配置；如果测试成功，重新启动 Samba 服务。另一方面，如果 `testparm` 显示错误，请根据需要检查并修改配置。

从您的 Windows 系统测试 Samba 服务。如果您已修改 Windows 注册表以使用明文密码，请删除您创建的注册表项，以便可以使用加密密码。

# 第四部分

## 附录

附录将向您介绍最常用的命令行 Linux 命令、IP 网络基础知识以及可用于 Linux 的 USENET 新闻组、网站和邮件列表等 Internet 资源。我还将向您展示如何使用 Red Hat Linux CD-ROM 从系统崩溃中恢复。

- 附录 A 常用 Linux 命令
- 附录 B IP 网络基础
- 附录 C Linux 的 Internet 资源
- 附录 D 从系统崩溃中恢复

# 附录 A

## 常用 Linux 命令

Red Hat Linux 在命令行工具和图形工具方面非常丰富。然而，与其他 Unix 或 Unix 类系统一样，Red Hat Linux 的强大之处仍然在于命令行工具。在本附录中，我将向您展示许多您可以经常使用的命令行工具的常见用法。

在学习工具之前，您应该知道如何从 Red Hat Linux 获取有关任何工具的在线帮助信息。Red Hat Linux 系统附带在线手册页（简称为 `man pages`），您可以使用 `man` 命令访问。手册页分为不同的章节，如表 A-1 所示。

表 A-1 手册页的章节

| Section | Topic |
|---|---|
| 1 | Executable programs or shell commands |
| 2 | System calls (functions the kernel provides) |
| 3 | Library calls (functions within system libraries) |
| 4 | Special files (usually in /dev) |
| 5 | File formats (that is, /etc/passwd) |
| 6 | Games |
| 7 | Miscellaneous information |
| 8 | Maintenance commands |

The `man` command allows you to view the online manuals. The syntax for this command is as follows:
```
man [-k] [section] keyword
```

The `keyword` is usually the name of the program, utility, or function. The default action is to search in all of the available sections following a predefined order and to show only the first page found, even if the keyword exists in several sections.

Because commands may appear in several sections, the first page found might not be the man page you are looking for. The command `printf` is a good example.

Say you are writing a program and would like to know more about the ANSI C library function `printf()`. Just by typing
```
man printf
```
you get information about `printf`. However, the man pages for this `printf` are for the shell command `printf`. Obviously, this is the wrong information. A reasonable solution is to list all of the sections covering `printf` (if it exists in multiple sections) and to select the correct one. You can search the keywords of the man pages with the `-k` option:
```
man -k printf
fprintf    printf (3)    - formatted output conversion
fprintf    printf (3)    - print formatted output
printf     printf (1)    - write formatted output
printf     printf (3)    - formatted output conversion
printf     printf (3)    - print formatted output
```

The `printf` you are interested in this example is a library function that can be found in section 3 (from Table B-4) or, more specifically, in section 3b or 3s (as you can see from the preceding output). To specify a particular section of a man page, you pass it to `man` at the command line to find the correct information you are looking for:
```
man 3b printf
```

## 通用文件和目录命令

在本节中，你将学习有关文件和目录特定命令的知识，这些命令你很可能会在日常使用中用到。

### cat

**语法：** `cat file [> | >>] [destination_file]`

`cat` 命令将文件的内容显示到标准输出，使你能够检查文件的内容。你传递给 `cat` 的参数是你想要查看的文件。要查看名为 `name` 的文件的全部内容，你可以使用以下命令（命令下方显示示例输出）：
```
cat name
Kiwee
Joe
Ricardo
Charmaine
```

`cat` 也可以将多个现有文件合并为一个：
```
cat name1 name2 name3 > allnames
```

此示例将文件 `name1`、`name2` 和 `name3` 合并以生成最终文件 `allnames`。你通过在命令行输入文件的顺序来确定合并的顺序。

使用 `cat`，你可以将一个文件追加到另一个文件。例如，如果你在上一个命令中忘记添加文件 `name4`，你可以通过执行以下命令将其添加到 `allnames` 文件中：
```
cat name4 >> allnames
```

### chmod

**语法：** `chmod [-R] permission_mode file_or_directory`

使用此命令更改文件或目录的权限模式。权限模式指定为三位或四位八进制数。例如：
```
chmod 755 myscript.pl
```

上述命令将 `myscript.pl` 脚本的权限更改为 `755` (`rwxr-xr-x`)，这允许文件所有者读取、写入和执行，而其他人只有读取和执行权限。以下是另一个示例：
```
chmod -R 744 public_html
```

上述命令将 `public_html` 目录及其所有内容（文件和子目录）的权限更改为 `744` (`rwxr--r--`)，这是在使用 Apache 服务器通过 `http://server/~username` URL 访问个人 Web 目录时典型的权限设置。`-R` 选项告诉 `chmod` 递归地更改指定目录下所有文件和目录的权限。

### chown

```
Syntax: chown [ -f h R ] owner [ :group ] { file . . . | directory . . . }
```
