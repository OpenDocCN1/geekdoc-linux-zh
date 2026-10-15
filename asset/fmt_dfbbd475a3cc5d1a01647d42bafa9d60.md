
通过添加解释复杂命令并描述脚本工作原理的注释，你可以编写出更容易理解和维护的脚本。注释是脚本中的行，系统在运行时会忽略它们。注释的作用是向他人解释你的脚本。

通过 `source` 命令赋值一个变量的值。这在 `  

 `

` 运行 脚本。

- 1 输入 `source` 后面加空格。
- 2 输入脚本文件名并按回车。
- `shell` 会逐行读取并执行指定脚本中的命令。
- 3 输入 `chmod` 后面加空格。
- 4 输入 `a+x` 后面加空格。
- 5 输入脚本文件名并按回车。`chmod` 命令为所有用户添加执行权限。

## 自动化 shell 任务

### 额外

虽然 `source` 命令非常方便，特别是对于运行没有执行权限的脚本，但有一个重要的限制。脚本中的命令必须与你正在使用的 `shell` 兼容。如果脚本包含任何 `shell` 特有的语法，例如在“Shell 条件”节中讨论的循环，只有当你运行接受该语法的 `shell` 时，才能成功执行该文件。请记住，这就像在当前 `shell` 中手动输入命令一样，如果你的 `shell` 不支持该语法，你也无法使用 `source` 命令运行包含该命令的脚本。例如，`source` 命令在 `tsh` 中为变量赋值。这个 `tsh` 特有的命令内置命令对 `sh` 和 `zsh` 来说没有意义。如果你是 `tuser`，你可以 `source` 包含 `set` 命令的文件来建立变量的值；这在 Bourne shell 中不起作用。

将以下行输入到名为 `macosx` 的文件中。注意不同的 `shell` 处理文件的方式不同。

| 输入： |
| --- |
| macosx |

结果：

我爱 Mac OS X

| 输入： |
| --- |
| /bin/sh sh-2.05a$ macosx |

结果：

sh-2.05a$ i love

示例：

```bash
set OS = "Mac OS X"
echo love $0
```

# 编写循环 Shell 脚本

你可以通过在 `shell` 脚本中放置循环来多次执行某条命令或命令列表。添加循环可以避免你为目录中的每个文件或列表中的每个值都运行一次脚本。

当你想要通过一系列文件、数字或其他值运行脚本时，可以使用循环结构。为了确保脚本运行正确，请在脚本顶部添加一行以 `#!` 开头的行，后面紧跟该特定脚本的完整路径。编写在 `tcsh` 中运行的脚本应该以 `#!/bin/tcsh` 开头。

对于 `tcsh`，你可以使用 `foreach` 命令来遍历一组值。命令 `foreach (4 5 6)` 会运行三次，对应列出的每一个值。循环每执行一次，下一个数字就会被赋值给变量 `$number`。在 `foreach` 命令之后，你可以输入你想要对每个 `$number` 执行的任何内容。通过单独的一行输入单词 `end` 来结束你的循环。

对于某些任务，你想要循环一组命令的次数取决于某个变量的值或其他条件。例如，如果你想写一个相两个数字的脚本，你可以让它一直相加直到运行脚本的人停止输入数字。在这种情况下，你使用 `while` 循环。只要指定的测试条件为真，`while` 循环就会继续执行。

# 循环 Shell 脚本

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_123_0.png)

# 使用 FOREACH 命令

1. 启动 Pico 创建名为 `work2day` 的文件。
2. 输入 `#!/bin/tcsh` 并按两次回车。
3. 输入 `foreach workday ( Mon Tue Wed Fri )` 并按回车。
4. 输入 `echo go to work on Friday` 并按回车。
5. 输入 `end`，按回车，然后输入 `echo today is $(date +%A)`。
你的脚本完成了。
6. 保存你的脚本并退出 Pico。
7. 输入 `chmod a+x work2day` 并按回车。
8. 输入 `./work2day` 并按回车。脚本开始执行。

# 自动化 Shell 任务

# 实践

你通常可以通过将重复的命令放在循环中来减少脚本的行数。你可以使用 Mac OS 提供的任何 `shell` 进行循环。`foreach` 和 `while` 命令是每个 `shell` 内置的。如果你在 `bash`、`zsh` 或 `sh` 中编写脚本，必须使用不同的语法。这些 `shell` 的 `for` 命令语法使用单词 `for`，后面跟着变量名和单词 `in`，然后是值列表。`do` 和 `done` 单词构成了循环中执行的命令的开始和结束。确保你在运行练习时使用了 `/bin/bash`、`/bin/zsh` 或 `/bin/tcsh`。

输入以下：

```bash
for weekday in Mon Tue Wed Thu Fri
do
  echo Go to work on $weekday
done
```

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_124_0.png)

结果：

Go to work on Mon

Go to work on Tue

Go to work on Wed

Go to work on Thu

Go to work on Fri

| 终端 | 文件 | 编辑 | 滚动条 | 字体 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| UR PICO(tcsh) 2.5 | File: addoploop | Modified | | | | |
| 终端 | 文件 | 编辑 | 滚动条 | 字体 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| UR PICO(tcsh) 2.5 | File: addloop | Modified | | | | |

```bash
#!/bin/bash
sum=0
while [ $sum -lt 10 ]; do
  sum=$(expr $sum + 1)
done
```

```tcsh
#!/bin/tcsh
set sum = 0
while ($sum < 10
  echo "number"
  set sum = $sum + 1
end
```

```
Get Help WriteOut Read Prv Pg Cut Text Cur Pos
Exit Justify Where is Next Pg Uncut Ter To Spell
```

```
File Name to write : addloop
Go Get Help To Files
Cancel
```

# 使用 WHILE 命令

1. 启动 Pico 编辑器创建一个名为 `addloop` 的文件。
2. 输入 `#!/bin/tcsh` 并按回车。
3. 输入 `set sum = 0` 并按两次回车。
4. 输入 `set num = ""` 并按回车。
5. 输入 `set sum=$(expr $sum + $num)` 并按回车。
注意：在第 5 步中使用单反引号。
6. 输入 `echo -n "number: "` 并按回车。
7. 输入 `echo $sum` 并按回车。
8. 输入 `end` 并按两次回车。
9. 输入 `echo $sum`。
10. 保存你的文件并退出 Pico。

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_124_1.png)

# 编写条件 Shell 脚本

条件语句让脚本更有用。你可以使用 `if` 命令来测试 `shell` 脚本中的条件。这种操作被称为条件逻辑。所有的 `shell` 都提供了条件逻辑。然而，与循环不同，语法是内置的，所以如果你在终端输入命令时可以找到它。

当你输入在条件为真时执行的命令列表时，为了可读性，脚本编写者通常会缩进这些行。在这些命令之后，你应该用 `end` 结束你的条件语句。

在 `bash` 中，`if` 语句有不同的形式。你在 `if` 单词后面跟着一组包含测试条件的方括号。括号后面跟着分号 `;` 和单词 `then`。你也可以喜欢将 `then` 写在下一行。用 `fi` 终止执行命令列表。

对于 `tcsh` 和 `csh`，你使用 `if` 将要测试的命令括在括号内，后面跟着单词 `then`。测试数字是否等于 0，例如命令为 `if ($number == 0 ) then`。测试变量是否包含特定字符串，将字符串括在引号中：`if ($day == "yes") ) then`。你还可以指定在未满足指定条件运行时的命令列表。在两种 `if` 形式中，你使用单词 `else` 开始这个列表。`else` 分支必须与之相关。

# 编写条件 Shell 脚本

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_125_0.png)

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_125_1.png)

1. 启动 Pico 编辑器创建一个命名文件。
2. 输入 `#!/bin/tcsh` 并按回车。
3. 输入 `set day=$(date +%A)` 并按回车。
4. 输入 `if ($day == "Saturday") then` 并按回车。
5. 输入 `echo "It is the weekend"` 并按回车。
6. 输入 `else` 并按回车。
7. 输入 `echo "It is a weekday"` 并按回车。
8. 输入 `end` 并按两次回车。
9. 保存你的文件并退出 Pico。

## 自动化 shell 任务

### 运用

`awk` 语言的某些特性使其外观与 `shell` 脚本有很大不同。例如，`awk` 中的变量名不以 `$` 开头。变量 `$1,$2` 等表示正在处理的文本中的字段。你可以使用一个没有取值的变量名，`awk` 会会忽略该命令并继续处理。

在 `awk` 中，显示文本行的命令是 `print` 而不是 `echo`。你必须在单引号内包含文本行。`awk` 使用 `(` 和 `)` 标记来开始和结束代码块。

# 输入以下内容：

```bash
[file:-] cat work2day | awk '(print NF)'
```

# 输入以下内容：

```bash
[file:-] cat work2day | awk '(print $NF)'
```

## 结果：

```
#/bin/tcsh

Weekday
end
+*
```

## 在脚本中使用 AWK

- 1 启动 PICO 编辑器，创建一个名为 `count_users` 的文件。
- 2 输入 `#/bin/tcsh` 并按两次回车。
- 3 输入 `set USERCOUNT = awk '(print $4)'` 并按两次回车。
- 4 输入 `if ($USERCOUNT - 10) then echo USERCOUNT users logged in` 并按回车，然后输入 `endif`。
- 5 保存文件并退出 Pico。
- 6 输入 `chmod +x count_users` 并按回车。
- 7 输入 `./count_users` 并按回车。
- 你的脚本运行了。

## 使用 SED 扩展脚本

`sed` 命令允许你修改 Unix 命令的输入或输出或文件的内容，而无需使用文本编辑器。`sed` 是一种特殊的编辑器，可以更改文件内容或其他命令的输出。它可以更改通过管道传递给它的文件的行，并从修改后的文件中输出内容。管道的形状代表了你指定的一系列编辑命令，它决定了哪些文本发生变化以及如何变化。

命令 `sed "s/a/z/g"` 将其输入中字母 `a` 的所有出现情况更改为输出中的字母 `z`。

如果你想同时更改多个字符串，请创建一个包含所有替换规则的文件。命令 `sed -f infile > output` 会在 `subs` 文件中查找一系列请求，在处理 `infile` 文件时应用这些更改，并将修改后的文本写入 `output`。

最简单的 `sed` 命令是用一个字符串替换另一个。命令 `echo please go to work today | sed "s/go to work/stay home/"` 的结果是：

`Please go stay home today.`

如果你想让文本更改一个正斜杠 `/`，`sed` 可能会混淆要更改哪些文本。你可以指定不同的分隔符来替换旧文本和新文本。命令 `sed "s:old:new/"` 的效果与 `sed "s/old/new/"` 相同。无论使用哪种分隔符，只要使用三个相同的即可。

`sed` 在每行中更改第一个字符串的一个实例。如果你想在文本每次出现在行中时都进行更改，请在末尾添加字母 `g`。

## 在命令行上使用 SED

- 1 启动 `sed` 编辑器，创建一个名为 `message` 的文件。
- 2 输入 `Please go to work today` 并按回车。
- 3 输入 `Don't to take your lunch.`。
- 4 保存文件并退出 Pico。
- 5 输入 `cat message` 后加一个空格。
- 6 输入后加一个空格。
- 7 输入 `sed "s/go to work/stay/"` 来用一段文本替换另一段并按回车。
屏幕显示了要求你今天留在家的文本。

## Extra

与 `awk` 一样，你可以使用 `sed` 创建相当复杂的脚本，但你通常使用该命令来扩展 `shell` 脚本。完全用 `sed` 编写的脚本可以是简单的，也可以非常有挑战性。尝试一个像名为 `oneline` 的文件所示的简单 `sed` 脚本并使其具有可执行性。它通过删除换行符将文件中的行合并为单行。

### 在文件中输入以下内容：

```bash
[file:-] cat work2day | awk '(print NF)'
```

- 4 输入 `if ($USERCOUNT - 10) then echo USERCOUNT users logged in` 并按回车，然后输入 `endif`。
- 5 保存你的文件并退出 Pico。
- 6 输入 `chmod +x count_users` 并按回车。
- 7 输入 `./count_users` 并按回车。
- 你的脚本运行了。

# 从终端打开 Aqua 应用程序

你可以使用 `shell` 命令 `open` 来通过 Aqua 应用程序（如 EditText、Preview、Photoshop 或 Microsoft Word）打开文件。如果你在 Mac OS X 的 Finder 中双击文件，它也会以这种方式打开。使用 `open` 命令有三种方式：

- `open filename`
- `open -e filename`
- `open -a Application-name filename`

该命令的第一种版本会启动 Aqua 应用程序来打开指定的文件名。Mac OS X 将每个文档与称为元数据的信息关联。这些元数据包含此类信息，例如哪个 Aqua 应用程序创建了该文件。`open` 命令从目录 `.` 启动应用程序。例如，`filename-dog.jpg` 的扩展名是 `.jpg`。Mac OS X 使用默认应用程序来打开 JPG 文件。这与 Mac OS X Finder 在你双击图标时确定使用哪种应用程序的方法相同。

并不是所有的文本文件都有 `.txt` 扩展名。一个 HTML 文件可能名为 `-cat.html`。如果你使用 `open`，文件将在 浏览器中打开，但如果你想编辑它，可以使用 EditText。`open` 命令的第二个版本带有 `-e` 选项，会在 EditText 中打开文件，让你编辑不是以 `.txt` 扩展结尾的文本文件，例如 HTML 或配置文件。

该命令的第三种版本允许你指定使用哪个应用程序。你可以命名位于 `/Applications` 目录或其子目录下的任何应用程序。你可以通过省略文件名来带空文件启动应用程序。

如果你创建的应用程序没有列在元数据中，Mac OS X 将查看文件的扩展名。扩展名是文件中出现的最后部分。

## 打开图像文件

输入图像文件名并按回车键。

输入 `open` 和一个空格。

Aqua 会启动相应的查看器程序并显示图像。

# 附加

`open` 命令不仅限于打开文件。如果你提供了其他参数，`open` 命令尝试在适当的查看器或编辑器中显示这些参数。

使用 `open` 最有用的方法之一是在 Mac OS X Finder 中打开目录。此命令会创建一个 Finder 文件夹窗口来打开当前目录。

```
open ~/Pictures
```

`open` 命令还可以通过你在“系统偏好设置”互联网面板中指定的默认浏览器打开 Web URL。要打开它，请将你的 URL 作为参数输入。

```
open http://cssin24hours.com/
```

你可能需要将 Web URL 包在引号中，以防止 `shell` 解释问号和其他特殊字符。
