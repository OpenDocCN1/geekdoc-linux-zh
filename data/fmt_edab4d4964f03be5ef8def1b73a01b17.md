
"Intro_to_UNIX/chap05$ grep Taylor contacts 781,555,0000

Taylor, Joanna Administrative Asst 781,555,2323

Murphy, Taylor Accounting

"Intro_to_UNIX/chap05$

```
图 5.16 使用 grep 搜索名为 Taylor 的文件。
```

要仅匹配 Taylor 匹配姓氏，你必须将模式搜索限制在出现 Taylor 的每行的开头。要使用 grep 实现从每行开始的模式搜索，你需要在模式前加上符号 `^` 符号，如图 5.17 所示。现在，你只得到了想要的匹配项。

```
"Intro_to_UNIX/chap05$ grep ^Taylor contacts

Taylor, Joanna Administrative Asst 781,555,0000

"Intro_to_UNIX/chap05$
```

图 5.17 在行首搜索模式。

## 从行尾开始搜索

同样，假设你想搜索出现在每行末尾的模式。例如，假设你想知道在 `contacts` 文件中哪些人的电话号码最后两位是 `01`。由于电话号码是每行中的最后一条信息，因此你将搜索模式设定为行末尾的 `01`。要实现这一点，你使用带有符号 `$` 符号的模式，如图 5.18 所示。

```
"Intro_to_UNIX/chap05$ grep 01$ contacts

Williams, Troy Systems Administrator 781,555,4001

"Intro_to_UNIX/chap05$
```

图 5.18 在行尾搜索模式。

# 110 UNIX/Linux 简介

## 不区分大小写的搜索

在到目前为止的 `grep` 示例中，你指定的词搜索模式的大写字母和小写字母与它们在被搜索文件中出现的完全一致。除非另有说明，否则 `grep` 执行的是区分大小写的模式搜索，其中大写字母和小写字母是不同的并被视为不同的项目。然而，如果你想用 `grep` 执行不区分大小的搜索（大写和小写字母被视为相同），可以通过 `-i` 选项进行指定。

除非指示，否则许多 UNIX/Linux 特性和命令都以区分大小写的方式运行（大写和小写字母是不同的）。

![](img/e3ac56d195b48617d5ae42cd57458af3_121_0.png)

为了演示不区分大小的搜索，假设你想搜索名字包含“Anna”的联系人，无论是完整还是部分。这意味着“Anna”的第一个字母可能是大写的也可能是小写的，取决于文本出现在名字的开头还是中间。要完成这次特定的搜索，请使用带有 `-i` 选项的 `grep`，如图 5.19 所示。如果你不指定 `-i` 选项，`grep` 只匹配第一个结果，因为“Joanna”中的文本序列“anna”包含了全小写字母。

```
//_to_UNIX/chap05 grep -i anna contacts

Taylor, Anna           Administrative Asst     781,555,0000

Cobb, Anna             Customer Sales        937,555,6777

//_to_UNIX/chap05$ 
```

图 5.19 使用 `grep` 执行不区分大小的搜索。

## 搜索多个文件

在 `grep` 的 man页上（如图 5.6 所示），`FILE` 组件后的省略号表示你可以指定多个文件。此功能允许你使用 `grep` 在多个文件之间进行搜索。你使用通配符模式指定文件名来匹配多个文件，而不是单个文件名。

为了演示多个文件的搜索，考虑 `~/_chap05/output_files` 中的一组文件。多台计算机各负责一个科学应用程序的一部分以解决一个物理问题，实际上生成了这些文件。每台计算机都保存了完成其问题部分所需的时间。要找出每台计算机花费多长时间完成其部分，请查找出现在文本“Compute time”上的消逝时间。要搜索每个文件中的该行文本，你执行一个 `grep` 命令，如图 5.20 所示。如果你不确定任何字母是否大写，请使用 `-i` 不区分大小写的选项。

# 中级文件管理 111

```
$Intro_to_UNIX/chap05$ cd output_files

$Intro_to_UNIX/chap05/output_files$ grep -i "compute time" output

output,10.1:Compute time: 87,278001

output,10.10:Compute time: 87,766712

output,10.2:Compute time: 87,86012

output,10.3:Compute time: 87,2236

output,10.4:Compute time: 87,4816

output,10.5:Compute time: 87,27032

output,10.6:Compute time: 87,6549

output,10.7:Compute time: 87,27645

output,10.8:Compute time: 87,6283

output,10.9:Compute time: 87,27507

Intro_to_UNIX/chap05/output_files$
```

图 5.20 使用 `grep` 搜索文件。

## 搜索文件或目录

有时，你可能会忘记搜索文件或目录。`find` 允许你搜索 UNIX 中的文件和目录。

### 通过名字查找

通过名字查找文件是搜索文件或目录的常用方法。假设你想查找一个名为 `contacts` 的文件。在 `/home/user` 目录中查找，你可以使用 `find` 命令：

```
$ find /home/user -name contacts

/home/user/contacts

/home/user/documents/contacts
```

如果你已经在该目录中，只想在当前目录中查找，可以使用 `.`：

```
$ find . -name contacts

./contacts

./documents/contacts
```

如果你想查找名字包含“Anna”的文件，可以使用通配符 `*`：

```
$ find . -name "*Anna*"

./Anna.txt

./Anna_notes.doc

./my_Anna.txt
```

如果你想查找以“Anna”结尾的文件，可以使用 `*Anna`：

```
$ find . -name "*Anna"

./my_Anna

./backups/old_Anna
```

如果你想查找以“Anna”开头的文件，可以使用 `Anna*`：

```
$ find . -name "Anna*"

./Anna.txt

./Anna_notes.doc
```

如果你想进行不区分大小写的查找，可以使用 `-iname` 选项：

```
$ find . -iname "anna*"

./Anna.txt

./anna_notes.doc

./My_Anna.txt
```

如果你想在特定的目录中查找：

```
$ find /home/user -name "Anna*"

/home/user/Anna.txt

/home/user/Anna/

/home/user/Anna/Anna.txt
```

如果你只想查找目录，可以使用 `-type d` 选项：

```
$ find . -type d

.

./documents

./music

./backup
```

如果你只想查找文件，可以使用 `-type f` 选项：

```
$ find . -type f -name "*.txt"

./notes.txt

./documents/notes.txt
```

如果你想查找在 7 天内修改过的文件，可以使用 `-mtime -7`：

```
$ find . -mtime -7
```

如果你想查找在 7 天前修改的文件，可以使用 `-mtime +7`：

```
$ find . -mtime +7
```

如果你想查找大于 10MB 的文件，可以使用 `-size` 选项：

```
$ find . -size +10M
```

如果你想查找小于 10MB 的文件，可以使用 `-size -10M`：

```
$ find . -size -10M
```

如果你想查找大小恰好为 10MB 的文件，可以使用 `-size 10M`：

```
$ find . -size 10M
```

如果你想查找最近执行过的文件，可以使用 `-atime` 选项：

```
$ find . -atime -1
```

如果你想查找在 1 天前未访问过的文件，可以使用 `-atime +1`：

```
$ find . -atime +1
```

如果你想查找最近更改状态的文件，可以使用 `-ctime` 选项：
