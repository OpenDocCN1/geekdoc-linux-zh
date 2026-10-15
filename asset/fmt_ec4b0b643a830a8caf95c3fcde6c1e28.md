
在示例中，用户 `cathy` 显示了 `/etc/passwd` 中包含字符串 `root` 的行。

然后她显示了包含此搜索字符串的行号。

通过第三个命令，她检查了哪些用户没有使用 `bash`，但使用 `noglogin` shell 的账户没有被显示。

然后她统计了以 `/bin/false` 为 shell 的账户数量。

最后一个命令显示了她家目录中所有以 `~/.bash` 开头的文件，排除了包含 `history` 的匹配项。

### 行和词锚点

在示例中，用户 `cathy` 显示了 `/etc/passwd` 中包含字符串 `root` 的行。

```
cathy > grep -c false /etc/passwd?
```

### 字符类

在括号表达式中，范围表达式由两个用连字符连接的字符组成。它匹配排序位于两个字符之间的任意单个字符（包含边界）。例如，在默认的 C 语言中，`"[a-d]"` 等于 `"[abcd]"`。许多语言按字典顺序排序，在这些语言中，它可能等于 `"[AbCc]"`。要获得传统的括号表达式解释，你可以通过将环境变量 `LC_ALL` 设置为 `"C"`。

最后，某些命名的字符类在括号表达式中是预定义的。查看 `grep` 的 `man` 或 `info` 页面以获取有关这些预定义表达式的信息。

## 第4章：正则表达式

```
cathy > grep [yf] /etc/group
sys:x:root,bin,adm
tty:x:5:
mail:x:12:
tftp:x:50:
nobody:x:99:
floppy:x:19:
fs:x:43:
nfbody:x:65534:
postfix:x:89:
```

```
cathy > ls *[1-9].xml
app.xml chap1.xml chap2.xml chap3.xml chap4.xml
```

在示例中，显示了包含 `"y"` 或 `"f"` 字符的所有行，随后是 `ls` 命令的范围示例。

### 通配符

```
cathy > grep '\<c...h\>' /usr/share/dict/words
catch
clash
cloth
coach
couch
cough
crash
crush
```

如果你想显示包含字面点字符的行，请对 `grep` 使用 `-F` 选项。

匹配多个字符请使用星号。此示例从系统字典中选择了所有以 `"c"` 开头并以 `"h"` 结尾的单词：

```
cathy > grep '\<c.*\h\>' /usr/share/dict/words
caliph
cash
catch
cheesecloth
cheetah
--省略--
```

如果你想在文件或输出中查找字面星号字符，请使用 `grep -F`:

## 4.3 使用 Bash 特性进行模式匹配

```
cathy > grep /etc/profile

cathy > grep -F '*' /etc/profile
for i in /etc/profile.d/*.sh; do
```

## 4.3 使用 Bash 特性进行模式匹配

除了 `grep` 和正则表达式外，还有很多模式匹配可以直接在 `shell` 中完成，而无需使用外部程序。

### 4.3.1 字符范围

如你所知，星号（`*`）和问号（`?`）分别匹配任何字符串或任何单个字符。对这些特殊字符加上引号可以对其进行字面匹配。

```
cathy > touch ***
cathy > ls **
.
```

但你也可以使用方括号来匹配任何括在内的字符或字符范围，前提是字符对之间由连字符分隔。例如：

```
cathy > ls -ld [a-cx-z]*
drwx-xr-x 2 cathy cathy 4096 Jul 20 2002 app-defaults/
drwx-xr-x 4 cathy cathy 4096 May 25 2002 arabic/
drwx-xr-x 2 cathy cathy 4096 Mar 4 18:30 bin/
drwx-xr-x 7 cathy cathy 4096 Sep 2 2001 crossover/
drwx-xr-x 3 cathy cathy 4096 Mar 22 2002 xml/
```

这列出了 `cathy` 家目录下所有以 `"a"`、`b"`、`c"`、x"`、y"` 或 `z"` 开头的文件。

如果括号内的第一个字符是 `"!"` 或 `"-"`，则会匹配任何未被括在内的字符。要匹配连字符（`-`），请将其作为集合中的第一个或最后一个字符。排序取决于当前的区域设置（`locale`）以及 `LC-COLLATE` 变量的值（如果已设置）。请注意，如果按照字典顺序进行排序，其他区域设置会将 `"[a-cx-z]"` 解释为 `"[aBbCcXxYyZz]"`。如果你想确保按照范围的传统解释，请通过将 `LC_COLLATE` 和 `LCALL` 设置为 `"C"` 来强制执行此行为。

### 4.3.2 字符类

可以在方括号内指定字符类，语法为 `[:CLASS:]`，其中 `CLASS` 由 `POSIX` 标准定义，其值为 `"alnum"`, `"alpha"`, `"ascii"`, `"blank"`, `"ctrl"`, `"digit"`, `"graph"`, `"lower"`, `"print"`, `"punct"`, `"space"`, `"upper"`, `"word"` 或 `"xdigit"` 之一。

部分示例：

```
cathy > ls -1d [[digit:]]*
drwxrxr-x  2 cathy cathy  4096 Apr 20 13:45 2/
n
cathy > ls -1d [[upper:]]*
drwxrxr-x  3 cathy cathy  4096 Sep 30 2001 Nautilus/
drwxrxr-x  4 cathy cathy  4096 Jul 11 2002 OpenOffice.org/0/
-rw-r--w--  1 cathy cathy  997376 Apr 18 15:33 Schedule.sed
```

当启用 `extglob` `shell` 选项时（使用内置命令 `shopt`），将能够识别多个扩展模式匹配操作符。更多信息请参阅 `Bash` 页面中的 `Basic shell features → Shell Expansions → Filename Expansion → Pattern Matching` 章节。

## 4.4 总结

正则表达式是从文件或输出中选择特定行的强大工具。许多 `UNIX` 命令都使用了正则表达式：`vim`、`perl`、`PostgreSQL` 数据库等。它们可以通过外部库在任何语言或应用程序中使用，甚至被引入了非 `UNIX` 系统。例如，正则表达式用于 `Microsoft Windows Office` 套件中的 `Excel` 表格中。在本章中，我们接触了 `grep` 命令，它在任何 `UNIX` 环境中都是不可或缺的。

注意

`grep` 命令可以完成比我们这里讨论的几个任务要多得多；我们仅将其作为正则表达式的示例。`GNU grep` 版本提供了大量的文档，强烈建议阅读！

`Bash` 具有匹配模式的内置功能，并识别字符类和范围。

## 4.5 练习

这些练习将帮助你掌握正则表达式。

- 1. 显示系统中所有以 `Bash` shell 作为默认登录壳的用户列表。
- 2. 从 `/etc/group` 目录列出所有以字符串 `"daemon"` 开头的行。
- 3. 打印示例文件中所有不包含该字符串的行。
- 4. 从 `/etc/hosts` 文件显示 `localhost` 信息，显示匹配搜索字符串的行号，并统计该字符串出现的次数。
- 5. 显示 `/usr/share/doc` 中包含 `shell` 信息的子目录列表。
- 6. 这些子目录包含多少个 `README` 文件？不要统计任何 `"README.a"` 形式的内容。
- 7. 使用 `grep` 列出你家目录下修改少于 10 小时的文件列表，但排除目录。
- 8. 将这些命令放入一个 `shell` 脚本中，生成易读的输出。
- 9. 你能使用 `grep` 找到 `wc -l` 的替代方案吗？
- 10. 使用文件系统表（例如 `/etc/fstab`），列出本地磁盘设备。
- 11. 编写一个脚本，检查用户是否存在。
- 12. 列出 `/etc/passwd` 中包含特定数字的行。

## 第 5 章：GNU sed 流编辑器编辑器

```
sandy > sed -n '/errors/p' example
It is a text with errors.
Lots of errors.
Much erors, all these erors are making me sick.

sandy >
```

## 5.2.2 删除包含模式的输入行

我们使用相同的示例文件。现在我们只想看到不包含搜索字符串的行：

```
sandy > sed '/errors/d' example
This is the first line of an example text.
This is a line not containing any errors.
This is the last line.

sandy >
```

`d` 命令的结果是排除某些行不显示。
