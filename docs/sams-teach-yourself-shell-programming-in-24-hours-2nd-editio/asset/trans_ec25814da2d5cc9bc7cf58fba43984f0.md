
生成以下输出：

```
8      18      219 fruits
```

第一个数字，在本例中为 8，是文件中的行数。第二个数字，在本例中为 18，是文件中的单词数。第三个数字，在本例中为 219，是文件中的字符数。行末列出了文件名。当指定多个文件时，文件名有助于识别与特定文件关联的信息。

如果指定多个文件，我们会给出每个文件的计数以及总计。例如，命令

```
$ wc fruits users
```

生成输出类似于以下内容：

```
8      18      219 fruits
3      3       19 users
11     21      237 total
```

您系统上的输出可能略有不同。

## 计数行数

要计数行数，可以使用 -l（即 lines）选项。例如，命令

```
$ wc -l fruits
```

生成输出

```
8 fruits
```

第一个数字，在本例中为 8，是文件中的行数。文件名列在行末。

当指定多个文件时，每个文件的行数会列出，同时列出所有指定文件的总行数。例如，命令

```
$ wc -l fruits users
```

生成输出

```
8 fruits
3 users
11 total
```

## 计数单词

要计数文件中单词数，可以使用 -w（即 words）选项。例如，命令

```
$ wc -w fruits
```

生成输出

18 fruits

第一个数字，在本例中为 18，是文件中的单词数。文件名列在行末。

当指定多个文件时，每个文件的单词数会列出，同时列出所有指定文件的总单词数。例如，命令

```
$ wc -w fruits users
```

生成输出

18 fruits
3 users
21 total

## 计数字符

要计数字符数，需要使用 -m 或 -c 选项。-m 选项在 Mac OS X、OpenBSD、Solaris 和 HP-UX 上可用。在 FreeBSD 和 Linux 系统上，应改用 -c 选项。

例如，在 Solaris 上命令

```
$ wc -m fruits
```

生成输出

219 fruits

生成输出

```
219 fruits
18 users
237 total
```

## 组合选项

wc 的选项可以组合在一起并按任意顺序指定。例如，要获取文件 fruits 的行数和单词数计数，可以使用以下任意命令：

```
$ wc -w -l fruits
$ wc -l -w fruits
$ wc -lw fruits
$ wc -lw fruits
```

这些命令的输出完全相同：

```
8 18 fruits
```

输出列出了文件中的行数，其后是文件中的单词数。文件名指定在行末。当指定多个文件时，每个文件的信息会列出，同时列出相应的总值。

## 操作文件

在前面的章节中，您查看了列出文件和查看其内容。在本节中，您将使用 cp、mv 和 rm 命令查看复制、重命名和删除文件。

### 复制文件 (cp)

cp 命令（copy 的缩写）用于复制文件。命令的基本语法是

```
cp src dest
```

也可以为 cp 指定多个源文件，前提是目标 dest 是一个目录。复制多个文件的语法是

```
$ cp src1 ... srcn dest
```

这里 src1 ... srcn 是源文件，dest 是目标目录。例如，以下命令

```
$ cp fruits users Documents/
```

在 Documents 目录中创建文件 fruits 和 users 的副本。

### 交互模式

cp 的默认行为是如果目标文件存在则自动覆盖。这种行为可能导致问题。可以使用 -i 选项（interactive 的缩写）来防止此类问题。在交互模式下，cp 会在覆盖任何文件之前提示确认。

假设文件 fruits.sav 存在，以下命令

```
$ cp -i fruits fruits.sav
```

会产生类似以下的提示：

```
overwrite fruits.sav? (y/n)
```

如果选择 y（yes），文件 fruits.sav 将被覆盖；否则文件保持不变。实际提示在不同版本的 UNIX 中有所不同。

### 常见错误

当遇到错误时，cp 会生成一条消息。以下是一些常见的错误条件：

- 源文件 src 是一个目录。
- 源文件 src 不存在。
- 当指定多个源文件 src1 ... srcn 时，目标 dest 不是一个目录。
- 与多个源文件 src1 ... srcn 一起指定了不存在的目标 dest。
- src1 ... srcn 中的某个源不是文件。

第一种错误类型由以下命令说明：

```
$ cp Downloads/ fruits
```

因为 src（本例中为 Downloads）是一个目录，所以会生成类似以下的错误消息：

```
cp: Downloads: is a directory
```

在本例中，dest 是文件 fruits；如果 dest 是一个目录，也会生成相同的错误。

第二种错误类型由以下命令说明：

```
$ cp fruits.sav
```

```
cp: cannot access fruits: No such file or directory
```

这里文件名 fruits 被拼错为 fruits，导致错误。在本例中 dest 是文件 fruits.sav；如果 dest 是一个目录，也会生成相同的错误。

第三种错误类型由以下命令说明：

```
$ cp fruits users fruits.sav
```

```
usage: cp [R -H | -L | -P] [-f | -i | -n] [-p] src target
cp [R -H | -L | -P] [-f | -i | -n] [-p] src ... srcN directory
```

因为 dest，本例中为 fruits.sav，不是目录，所以会显示突出 cp 命令正确语法的用法说明。输出在您的系统上可能不同，因为某些版本的 cp 不显示用法信息。

如果文件 fruits.sav 不存在，错误消息为

```
cp: fruits.sav: No such file or directory
```

这说明了第四种错误类型。

第五种错误类型由以下命令说明：

```
$ cp fruits Downloads/ users Documents/
```

```
cp: Downloads is a directory (not copied).
```

尽管 cp 对目录 Downloads 报告错误，其他文件仍正确复制到目录 Documents。

### 重命名文件 (mv)

mv 命令（move 的缩写）可用于更改文件名。基本语法是

```
mv src dest
```

这里 src 是文件的原始名称，dest 是文件的新名称。例如，命令

```
$ mv fruits fruits.sav
```

将文件 fruits 的名称更改为 fruits.sav。如果重命名成功，mv 没有输出。

如果 src 不存在，将生成错误。例如，

```
$ mv op fritus fruits.sav
mv: fritus: cannot access: No such file or directory
```

与 cp 类似，如果 dest 已存在，mv 不会报告错误。旧文件会被自动覆盖。可以通过指定 -i 选项（interactive 的缩写）来避免此问题。在交互模式下，mv 会在覆盖任何文件之前提示确认。

假设文件 fruits.sav 已存在，命令

```
$ mv -i fruits fruits.sav
```

会产生类似以下的确认提示：

```
overwrite fruits.sav?
```

如果选择 y（yes），文件 fruits.sav 将被覆盖；否则文件保持不变。实际提示在不同版本的 UNIX 中有所不同。

### 删除文件 (rm)

rm 命令（remove 的缩写）可用于删除文件。其语法是

```
rm file1 ... fileN
```

这里 file1 ... fileN 是要删除的一个或多个文件的列表。例如，命令

```
$ rm fruits users
```

删除文件 fruits 和 users。

因为使用 rm 删除的文件无法恢复，您应确保只指定真正要删除的文件。确保的一种方法是指定 -i 选项（interactive 的缩写）。在交互模式下，rm 在删除每个文件之前都会提示。例如，命令

```
$ rm -i fruits users
```

会产生类似以下的确认提示：

```
fruits: ? (n/y) y
users: ? (n/y) n
```

在这种情况下，您回答 y（yes）删除 fruits，n（no）不删除 users。因此，文件 fruits 被删除，但文件 users 保持不变。
