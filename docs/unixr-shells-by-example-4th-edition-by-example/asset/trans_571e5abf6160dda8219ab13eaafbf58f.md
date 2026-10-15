

## 11.10 引用

引号用于保护特殊元字符不被解释。它们会在所有 shell 脚本中造成主要的调试麻烦。单引号必须配对。它们会保护特殊元字符不被 shell 解释。双引号也必须配对。它们会保护大多数字符不被 shell 解释，但允许变量和命令替换字符被处理。单引号会保护双引号，双引号会保护单引号。与 Bourne shell 不同，Korn shell 如果引号不匹配，会向标准错误发送错误信息并指出检测到引号不匹配的行。

### 11.10.1 反斜杠

反斜杠用于保护（或转义）单个字符不被解释。

### EXAMPLE 11.54

```
1 $ print where are you going\?
   where are you going?
2 $ print Start on this line and \
> go to the next line.
   Start on this line and go to the next line.
```

### EXPLANATION

- 1. 特殊元字符 `?` 用反斜杠转义。shell 不会将其解释为文件名扩展。
- 2. 换行符被转义。下一行将成为第一行的组成部分。`>` 是 Korn shell 的二级提示符。

### 11.10.2 单引号

单引号必须配对。它们会保护所有元字符不被解释。要打印单引号，它必须用双引号括起来或用反斜杠转义。

### EXAMPLE 11.55

```
2 $ print 'Do you need $5.00?'
Do you need $5.00?

3 $ print 'Mother yelled, "Time to eat!"'
Mother yelled, "Time to eat!"
```

### EXPLANATION

- 1. 该行的单引号未配对。Korn shell 会产生二级提示符。它正在等待引号被配对。
- 2. 单引号保护所有元字符不被解释。在此示例中，`$` 和 `?` 受 shell 保护，将被视为字面量。
- 3. 单引号保护此字符串中的双引号。这里的双引号是对话引号。

### 11.10.3 双引号

双引号必须配对。它们允许变量和命令替换，并保护其他任何特殊元字符不被 shell 解释。

### EXAMPLE 11.56

```
1 $ name=Jody

2 $ print "Hi $name, I'm glad to meet you!"
Hi Jody, I'm glad to meet you!

3 $ print "Hey $name, the time is `date`"
Hey Jody, the time is Fri Dec 18 14:04:11 PST 2004
```

## 11.11 命令替换

命令替换用于将命令的输出赋给变量，或将命令的输出替换到字符串中。Bourne shell 和 C shell 使用反引号执行命令替换。Korn shell 仍允许反引号格式（称其为“过时”），但将命令放在括号中是首选方法，因为它具有更简单的引用规则并且使嵌套命令更容易。

```
Unix/Linux command # Old method with backquotes
$(Unix/Linux command) # New method
```

```
(Old Way)
1 $ print "The hour is `date +%H`"
The hour is 09
2 $ name=`nawk -F: '{print $1}' database`
$ print $name
Ebenezer Scrooge
3 $ ls -l /etc
shutdown
4 $ set `date`
5 $ print $*
Sat Oct 13 09:35:21 PDT 2004
6 $ print $2 $6
Oct 2004
```

- 1. `date` 命令的输出被替换到字符串中。
- 2. `nawk` 命令的输出被赋给变量 `name`，并显示出来。
- 3. 用反引号括起来的 `ls` 命令的输出，是来自 `/etc` 目录的文件列表。文件名将作为命令中第一个 `$` 的参数。`/etc` 中与当前目录同名且所有文件都被列出。
- 4. `set` 命令将 `date` 命令的输出赋给位置参数。空白字符将单词列表分隔为各自的参数。
- 5. `$*` 变量保存所有参数。`date` 命令的输出被存储在 `$*` 变量中。每个参数由空白字符分隔。
- 6. 第二个和第六个参数被打印。

> 使用反引号进行命令替换是 Bourne shell 和 C shell 中仍在使用的一种旧形式。虽然仍然是合法语法，但 Korn shell 引入了本节所示的新方法。

