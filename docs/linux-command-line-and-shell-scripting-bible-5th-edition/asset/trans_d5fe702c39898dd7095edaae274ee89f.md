
## **第三部分：高级 Shell 脚本**

  管理员组会议将举行。  
  所有系统管理员都应参加。  
  感谢您的配合。

```
$ sed 's/System Admin/DevOps Engineer/' data3.txt
```

  周二，Linux 系统  
  管理员组会议将举行。  
  所有 DevOps 工程师都应参加。  
  感谢您的配合。

替换（s）命令正在文本文件中查找特定的两词短语“System Admin”。在短语出现的单行中，一切正常；替换命令可以替换文本。但在短语被拆分到两行之间的情况下，替换命令无法识别匹配的模式。

N 命令有助于解决此问题：

```
$ sed 'N ; s/System.Admin/DevOps Engineer/' data3.txt
```

  周二，Linux DevOps 工程师组会议将举行。  
  所有 DevOps 工程师都应参加。  
  感谢您的配合。

通过使用多行（N）命令将下一行与找到第一个单词的行合并，您可以检测到短语中发生行拆分的情况。

请注意，替换（s）命令在“System”一词和“Admin”一词之间使用通配符模式（.）来匹配空格和换行情况。然而，当它匹配到换行符时，它会将其从字符串中移除，导致两行合并为一行。这可能不是您确切想要的结果。

为了解决这个问题，您可以在 sed 编辑器脚本中使用两个替换命令，一个用于匹配多行出现的情况，另一个用于匹配单行出现的情况：

```
$ sed 'N  
> s/System\nAdmin/DevOps\nEngineer/  
> s/System Admin/DevOps Engineer/'  
> ' data3.txt
```

  周二，Linux DevOps  
  工程师组会议将举行。  
  所有 DevOps 工程师都应参加。  
  感谢您的配合。

第一个替换命令专门查找两个搜索词之间的换行符，并将其包含在替换字符串中。这允许您在新文本的相同位置添加换行符。

然而，该脚本中仍有一个细微的问题。脚本总是先读取**下一个**文本行到模式空间，然后执行 sed 编辑器命令。当它到达文本的最后一行时，没有下一个文本行可供读取，因此 **N** 命令会导致 sed 编辑器**停止**。如果匹配的文本位于数据流中的最后一行，命令将不会捕获匹配的数据：

```
$ cat data4.txt
On Tuesday, the Linux System
Admin group meeting will be held.
All System Admins should attend.
$
$ sed 'N
> s/System\nAdmin/DevOps Engineer/
> s/System Admin/DevOps Engineer/
> ' data4.txt
On Tuesday, the Linux DevOps
Engineer group meeting will be held.
All System Admins should attend.
$
```

因为“System Admin”文本出现在数据流中的最后一行，多行（N）命令会错过它，因为没有另一行可以读取到模式空间以进行合并。您可以轻松通过解决此问题，将单行编辑命令移到多行命令之前，并只让用于多行的编辑命令出现在 N 之后，如下所示：

```
$ sed '
> s/System Admin/DevOps Engineer/
> N
> s/System\nAdmin/DevOps Engineer/
> ' data4.txt
On Tuesday, the Linux DevOps
Engineer group meeting will be held.
All DevOps Engineers should attend.
$
```

现在，查找单行短语的替换（s）命令在数据流中的最后一行上工作得非常好，而多行（N）命令之后的替换命令涵盖了数据流中间的出现情况。

## 导航多行删除命令

第 19 章涉及了单行删除（d）命令的主题。sed 编辑器使用它来删除模式空间中的当前行。然而，如果您正在使用 N 命令，在使用单行删除命令时必须小心：

```
$ sed 'N ; /System\nAdmin/d' data4.txt
All System Admins should attend.
$
```

删除（d）命令查找位于不同行的单词“System”和“Admin”，并删除了模式空间中的这两行。这可能与您的意图相符，也可能不符。

sed 编辑器提供了多行删除（D）命令，它只删除模式空间中的第一行。它会移除所有字符，包括换行符在内：

```
$ sed 'N; /System\nAdmin/D' data4.txt

Admin group meeting will be held.

All System Admins should attend.
$
```

由 N 命令添加到模式空间中的第二行文本保持完整。如果您需要删除出现在您找到数据字符串的那一行之前的一行文本，这将很有用。

以下是删除数据流中第一行之前出现的空行的示例：

```
$ cat data5.txt

Header Line

First Data Line



End of Data Lines
$
```

```
$ sed '/^$/N; /Header/D' data5.txt

Header Line

First Data Line



End of Data Lines
$
```

这个 sed 编辑器脚本查找空行，然后使用 N 命令将下一行文本添加到模式空间。如果新的模式空间内容包含单词“Header”，D 命令会移除模式空间中的第一行。如果没有 N 和 D 命令的组合，将无法在不删除所有其他空行的情况下删除第一个空行。

## 导航多行打印命令

到目前为止，您可能已经注意到了单行和多行版本命令之间的区别。多行打印命令（P）遵循相同的技术。它只打印多行模式空间中的第一行。这包括模式空间中直到换行符的所有字符。当您使用 -n 选项抑制脚本的输出以显示文本时，其用途与单行 p 命令非常相似。

```
$ sed -n 'N; /System\nAdmin/P' data3.txt

On Tuesday, the Linux System
$
```

![](img/0798d50a0e5dbf1265fbda3832b3e015_538_0.png)

当发生多行匹配时，`P` 命令只打印模式空间中的第一行。多行 `P` 命令的强大之处在于与 `N` 和 `D` 多行命令结合使用时的表现。

`D` 命令具有一个独特功能，即在从模式空间中删除第一行后，它会强制 `sed` 编辑器返回到脚本的开头，并对当前模式空间重复命令（它不会从数据流中读取新的文本行）。通过在命令脚本中包含 `N` 命令，您可以有效地在模式空间中单步执行，同时匹配多行。

接下来，通过使用 `P` 命令，您可以打印第一行，然后使用 `D` 命令删除第一行并循环回脚本的开头。当您回到脚本开头时，`N` 命令读取下一行文本并重新开始整个过程。该循环一直持续到数据流结束，如下所示，在此文件中移除数据损坏：

```
$ cat corruptData.txt
Header Line#
@
Data Line #1
Data Line #2#
@
End of Data Lines#
@n
$
$ sed -n 'n
> N
> s/#\n@//
> P
> D
> ' corruptData.txt
Header Line
Data Line #1
Data Line #2
End of Data Lines
$
```

数据文件在某些行的末尾被 `#` 损坏，且下一行接着是 `@`。要修复此问题，使用 `sed` 将“Header Line#”行加载到模式空间中，然后多行下一个（n）命令加载第二行（@），并将其追加到空间中的第一行内。替换（s）命令通过将违规数据（#\n@）替换为空来移除这些数据。接下来，`P` 命令只打印模式空间中现在已清理的第一行。删除（D）命令从空间中移除这一行，并返回脚本开头，在那里下一个 `N` 命令将第三行文本（Data Line #1）读取到模式空间中，编辑循环继续。

