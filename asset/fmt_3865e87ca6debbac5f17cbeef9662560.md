
这些测试可以根据当前模式、终端类型和你正在使用的应用程序来定制 `Readline` 库。它们在与 `bash` 和其他程序一起使用 `Readline` 库时赋予了你极大的力量和灵活性。

## Readline 定制

`.inputrc` 中的以下命令使 `CONTROL-y` 无论 `bash` 处于 `vi` 还是 `emacs` 模式，都将光标移动到下一个单词的开头：

```
$ cat ~/.inputrc
  set editing-mode vi
  if mode=vi
    "\C-y": vi-next-word
  else
    "\C-y": forward-word
  endif
```

因为 `bash` 在启动时读取上述条件结构，所以你必须将编辑模式设置在 `.inputrc` 中。使用 `set` 交互式更改模式不会改变 `CONTROL-y` 的绑定。

有关 `Readline` 库的更多信息，请打开 `bash` 手册页并输入命令 ` / ^READLINE `，该命令搜索行首的单词 `READLINE`。

## 如果 Readline 命令不起作用，请注销并重新登录

`Bourne Again Shell` 在你登录时读取 `~/.inputrc`。在对这个文件进行修改后，你应该在测试更改之前先注销并重新登录。

## 别名

`别名` 是 `Shell` 将其转换为另一个（通常更长的）名称或（复杂的）命令的（通常较短）名称。别名允许你通过用字符串替换简单命令的第一个标记来定义新命令。它们通常放置在 `~/.bashrc` 启动文件中，以便对交互式子 `Shell` 可用。

`alias` 内建的语法是

```
alias [name=value]
```

等号周围不允许有空格。如果 `value` 包含空格或制表符，你必须用引号将 `value` 括起来。别名不接受来自 `命令行` 的 `value` 中的参数。当需要使用参数时，请使用函数（第 335 页）。

别名不会替换自身，这避免了对如下的别名进行无限递归处理的可能性：

```
$ alias ls='ls -F'
```

你可以嵌套别名。在非交互式 `Shell`（即 `Shell` 脚本）中，别名是被禁用的。要查看当前别名的列表，请键入命令 `alias`。要查看特定名称的别名，请输入 `alias` 后跟该名称且没有其他内容。你可以使用 `unalias` 内建命令删除别名。

当你执行不带任何参数的 `alias` 内置命令时，`shell` 会显示所有已定义的别名列表：

```
$ alias
alias ll='ls -l'
alias ls='ls -ltr'
alias ls='ls -F'
alias zap='rm -i'
```

`Fedora/RHEL` 定义了某些别名。运行 `alias` 命令可查看当前生效的别名。你可以从相应的启动文件中删除不需要的别名。

## 别名中的单引号与双引号

当别名中包含变量时，在 `alias` 语法中选择使用单引号还是双引号至关重要。如果用双引号包裹 `value`，则 `value` 中出现的任何变量都会在创建别名时被展开。如果用单引号包裹 `value`，则变量直到使用该别名时才会展开。以下示例说明了这种区别。

`PWD` 关键字变量保存工作目录的路径名。`Alex` 在他的家目录工作时创建了两个别名。因为他在创建 `dirA` 别名时使用了双引号，所以在创建该别名时，`shell` 替换了工作目录的值。`alias dirA` 命令显示 `dirA` 别名，并表明替换已经发生：

```
$ echo $PWD
/home/alex
$ alias dirA="echo Working directory is $PWD"
$ alias dirA
alias dirA='echo Working directory is /home/alex'
```

当 `Alex` 创建 `dirB` 别名时，他使用了单引号，这阻止了 `shell` 展开 `$PWD` 变量。`alias dirB` 命令显示 `dirB` 别名仍然保持未展开的 `$PWD` 变量：

```
$ alias dirB='echo Working directory is $PWD'
$ alias dirB
alias dirB='echo Working directory is $PWD'
```

在创建 `dirA` 和 `dirB` 别名后，`Alex` 使用 `cd` 将 `cars` 设为工作目录，并将每个别名作为命令执行。用双引号创建的 `dirA` 别名显示创建工作目录的名称作为当前工作目录（这是错误的），而 `dirB` 别名则显示正确的工作目录名称：

```
$ cd cars
$ dirA
Working directory is /home/alex
$ dirB
Working directory is /home/alex/cars
```

## 如何防止 shell 调用别名

> `shell` 只检查简单的、未加引号的命令以判断它们是否为别名。作为相对或绝对路径名给出的命令以及加引号的命令不会被检查。当你要执行一个有别名但你不想使用该别名时，请在命令前加反斜杠，指定命令的绝对路径名，或将命令作为 `command` 给出。

## 别名示例

以下别名允许你输入 `r` 来重复上一条命令，或输入 `r abc` 来重复以 `abc` 开头的最后一条命令行：

```
$ alias r='fc -s'
```

如果你经常使用 `ls -ltr` 命令，可以创建一个别名，使得当你输入命令 `l` 时替换为 `ls -ltr`：

```
$ alias l='ls -ltr'
$ l
total 41
-rw-r---  1 alex  group  30015 Mar  1 2007 flute.ps
-rw-------  1 alex  group  3089 Feb 11 2008 XTerm.ad
-rw-r---  1 alex  group   641 Apr  1 2008 fixtax.icn
-rw-r---  2 alex  group   484 Apr  9 2008 maptax.icn
drwxrwxr-x  2 alex  group  1024 Aug  9 17:41 Tiger
drwxrwxr-x  2 alex  group  1024 Sep 10 11:32 testdir
-rwxr-xr-x  1 alex  group   485 Oct 21 08:03 floor*
drwxrwxr-x  2 alex  group  1024 Oct 27 20:19 Test_Emacs
```

别名的另一个常见用途是保护你免于犯错。以下示例在你输入命令 `zap` 时替换为 `rm` 工具的交互版本：

```
$ alias zap='rm -i'
$ zap f*
rm: remove 'fixtax.icn'? n
rm: remove 'flute.ps'? n
rm: remove 'floor'? n
```

`-i` 选项使 `rm` 询问你验证每个将被删除的文件，从而帮助你避免意外删除错误的文件。你还可以通过 `rm -i` 命令为 `rm` 设置别名：`alias rm='rm -i'`。

下一个示例中的别名使得每次你输入 `l` 命令时，`shell` 都会替换为 `ls -l`，而当使用 `ls` 时替换为 `ls -F`：

```
$ alias ls='ls -F'
$ alias ll='ls -l'
$ ll
total 41
drwxrwxr-x  2 alex  group  1024 Oct 27 20:19 Test_Emacs/
drwxrwxr-x  2 alex  group  1024 Aug  9 17:41 Tiger/
-rw-------  1 alex  group  3089 Feb 11 2008 XTerm.ad
-rw-r---  1 alex  group   641 Apr  1 2008 fixtax.icn
-rw-r---  1 alex  group  30015 Mar  1 2007 flute.ps
-rwxr-xr-x  1 alex  group   485 Oct 21 08:03 floor*
-rw-r---  2 alex  group   484 Apr  9 2008 maptax.icn
drwxrwxr-x  2 alex  group  1024 Sep 10 11:32 testdir/
```

`ls -F` 选项使 `ls` 在目录名末尾打印斜杠（`/`），在可执行文件名末尾打印星号（`*`）。在此示例中，替换别名 `ll`（`ls -l`）的字符串本身包含一个别名（`ls`）。当用其值替换别名时，`shell` 会查看替换字符串的第一个单词以判断它是否为别名。在前面的示例中，替换字符串包含别名 `ls`，因此会发生第二次替换以产生最终命令 `ll -F -l`。（为了避免递归陷阱，替换文本中的 `ls` 虽然是别名，但不会第二次展开。）
