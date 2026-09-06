
# 最可能遇到的 UNIX Shell 编程面试题：工作面试问题系列

## UNIX Shell 编程

### 面试题

回顾这些典型的面试题，并思考你将如何回答。阅读列出的答案；你将找到最佳答案以及策略和建议。

## C Shell：初级

### 1. 在首次通过名称或别名运行你的新脚本之前，你必须做什么？

**答案：**

你必须赋予它可执行权限，即执行命令：

```bash
chmod +x scriptname
```

### 2. 用户的 `.login` 脚本中包含以下命令：

```bash
alias whois 'grep ^ /etc/passwd'
```

当用户执行以下命令时，输出是什么？

```bash
who is guru
```

**答案：**

如果存在一个名为 `"guru"` 的定义用户账户，或者 `/etc/passwd` 文件中其他地方包含字符串 `guru`，则输出将是包含字符串 `"guru"` 的条目；否则，输出将是一个空行。

### 3. 如果条件 `If (-r filename)` 失败（返回假），可能的原因有哪些？

**答案：**

可能的原因有：

- a) 进程所有者不可读取 `filename`
- b) `filename` 不存在

### 4. 下述两个语句之间的区别是什么？

```bash
set var = 10
set var=10
```

**答案：**

在 `set var = 10` 中，等号两边的空格会导致 Shell 设置两个变量 `var` 和 `10`。在 `set var=10` 中，它正确地将值 `10` 赋值给变量 `var`。

### 5. 给定以下代码，`var` 的值是多少？

```bash
set var=10
set var=20
echo $var
```

**答案：**

输出将是 `20`，因为第二个 `set` 命令覆盖了 `var` 的原有值。

### 6. 以下命令的输出是什么？

```bash
set list=(apple banana cherry)
echo $#list
```

**答案：**

输出将是 `3`，因为 `$#list` 返回数组 `list` 中的元素个数。

### 7. `rehash` 命令的作用是什么？

**答案：**

`rehash` 命令清除 Shell 内部的可执行命令和函数的哈希表，强制其重新在 `PATH` 中搜索这些命令。

### 8. 如何检查一个文件是否为目录？

**答案：**

你可以在 `if` 语句中使用 `-d` 运算符：

```bash
if (-d dirname) then
    echo "It is a directory"
endif
```

### 9. 如何向数组添加一个元素？

**答案：**

你可以使用 `+=` 运算符：

```bash
set list += (new_element)
```

### 10. `$?` 变量的用途是什么？

**答案：**

`$?` 变量存储最近一次执行的命令的退出状态。

### 11. 如何遍历数组中的元素？

**答案：**

你可以使用 `foreach` 循环：

```bash
foreach item in ($list)
    echo $item
end
```

第一个 `echo` 将显示 `c1`、`c4`、`c2`、`c5`、`c1`，而第二个只显示 `c1`。

### 21. 无论参数数量多少，显示脚本的第一个和最后一个参数，且不使用循环

**答案：**

```bash
my_var3 = $#argv
echomy_var1: $argv[$1]
echomy_last_var: $argv[$my_var3]
```

### 22. 你将如何在 `csh` 中设置“搜索路径”（search path）？

**答案：**

`csh` 中的搜索路径可以如下所示方式设置：

- a) `setenv PATH"/myfolder1 /bin: /myfolder2 /myfile3"`
- b) 使用列表：

```bash
set path = =( /myfolder1 /bin /myfolder2 /myfile3 )
```

### 23. 在 `/home/user1/myarch.tar` 创建一个 `tar` 归档包，包含所有以 `.c`、`.h`、`.l`、`.y`、`.o` 和 `.cc` 结尾的文件，以及来自 `~/dir1` 和 `~/dir2` 两个目录的 `Makefile`

**答案：**

```bash
tar cvf /home/user1/myarch.tar ~/{dir1,dir2}/{Makefile,*.{c,h,l,o,y,cc}}
```

或者：

```bash
tar cvf /home/user1/myarch.tar ~/dir1/Makefile ~/dir1/*.[chloy] ~/dir1/*.cc ~/dir2/Makefile ~/dir2/*.[chloy] ~/dir2/*.cc
```

### 24. 你的脚本必须带有两个参数执行，否则将被终止。编写代码来实现这些检查

**答案：**

```bash
if ($#argv <> 2) then
  echo "Usage: $0 arg1 arg2"
  echo "你必须提供好两个参数"
  exit 20
endif
```

### 25. 编写一个管道，从文本文件的第 `j` 行读取到第 `k` 行，不使用 `awk`

**答案：**

```bash
set total = `cat textfile | wc -l`
set j = 10
set k = 18
@ count = $k - $j
head -$k textfile | tail -$count
```

## C Shell：中间级

### 26. 解释以下命令：

```bash
set names = (John Kathrin Chris Jacob)
set names = ($names[1-2] Angela $names[3-])
```

**答案：**

第一条命令创建一个名为 `names` 的数组，并将四个名字作为元素。

第二条命令在 `Kathrin` 和 `Chris` 之间插入名字 `Angela`。

### 27. 如何将光标移动到屏幕上指定的坐标？（`tcsh`）

**答案：**

我们可以使用以下代码将光标移动到屏幕上指定的坐标：`echocm column row`

### 28. 此循环的结果是什么？

```bash
foreach i ([A-Z]*)
  ? mv $i $i.csh
end
```

**答案：**

该循环重命名所有以大写字母开头的文件，添加“扩展名” `.csh`。

### 29. 假设脚本某处有一个标签 `cleanup`，解释命令 `onintr cleanup`

**答案：**

如果脚本捕获到中断信号，将跳转到标签 `cleanup`。

### 30. 是否有方法可以在预定义的次数内重复命令，而不使用计数器控制的循环？

**答案：**

我们可以使用 `repeat` 命令在预定义的次数内重复命令，而不使用计数器控制的循环，例如：

```bash
repeat 5 ls >> listings
```

### 31. `csh` 和 `tcsh` 都支持文件名和命令补全功能。但该功能在 `csh` 中的工作方式与 `tcsh` 不同。请列出差异

**答案：**

当你使用 `tcsh` 时，按下 `Tab` 键时命令和文件名会自动补全。

当你使用 `csh` 时，必须设置 `filec` 变量才能进行单词补全。在 `csh` 中，必须按下 `Esc` 键进行单词补全。

### 32. 按每个 Shell 使用的顺序列出 `csh` 和 `tcsh` 的特殊登录文件

**答案：**

如果命令是从系统文件（`/etc/csh.cshrc` 和 `/etc/csh.login`）执行的，将启动登录 Shell。它将运行用户目录下文件中给出的命令。

- a) `~/.cshrc` 或 `~/.tcshrc`：在 Shell 启动期间，每个 Shell 实例都会执行。如果存在 `~/.cshrc`，`tcsh` 使用此文件，否则执行 `~/.tcshrc`。
- b) `~/.login`：登录时由登录 Shell 在 `.cshrc` 之后执行。
- c) `~/.cshdirs`：在 `.login`（`tcsh`）之后由登录 Shell 执行。

### 33. 以下行的作用是什么？解释其差异。

```bash
ls > filename
ls >! Filename
```

**答案：**

在这两种形式中，`ls` 命令的输出都被重定向到 `filename`。如果 `filename` 不存在，将创建它，否则会被截断。当使用第一种形式时，如果 Shell 参数 `noclobber` 被设置且 `filename` 是已存在的文件，会导致错误。第二种形式中的 `!` 用于抑制该错误。

### 34. 假设脚本中某处有一个标签 `cleanup`，解释命令 `onintr cleanup`

（注：此处原文似乎与第 29 题重复，已根据语境翻译。）

**答案：**

如果脚本捕获到中断信号，将跳转到标签 `cleanup`。

### 35. 是否有方法可以在预定义的次数内重复命令，而不使用计数器控制的循环？

（注：此处原文似乎与第 30 题重复，已根据语境翻译。）

**答案：**

我们可以使用 `repeat` 命令在预定义的次数内重复命令，而不使用计数器控制的循环，例如：

```bash
repeat 5 ls >> listings
```

### 36. `csh` 和 `tcsh` 都支持文件名和命令补全功能。但该功能在 `csh` 中的工作方式与 `tcsh` 不同。请列出差异

**答案：**

当你使用 `tcsh` 时，按下 `Tab` 键时命令和文件名会自动补全。

当你使用 `csh` 时，必须设置 `filec` 变量才能进行单词补全。在 `csh` 中，必须按下 `Esc` 键进行单词补全。

### 37. 按每个 Shell 使用的顺序列出 `csh` 和 `tcsh` 的特殊登录文件

**答案：**

如果命令是从系统文件（`/etc/csh.cshrc` 和 `/etc/csh.login`）执行的，将启动登录 Shell。它将运行用户目录下文件中给出的命令。

- a) `~/.cshrc` 或 `~/.tcshrc`：在 Shell 启动期间，每个 Shell 实例都会执行。如果存在 `~/.cshrc`，`tcsh` 使用此文件，否则执行 `~/.tcshrc`。
- b) `~/.login`：登录时由登录 Shell 在 `.cshrc` 之后执行。
- c) `~/.cshdirs`：在 `.login`（`tcsh`）之后由登录 Shell 执行。

### 38. 以下行的作用是什么？解释其差异。

```bash
ls > filename
ls >! Filename
```

**答案：**

在这两种形式中，`ls` 命令的输出都被重定向到 `filename`。如果 `filename` 不存在，将创建它，否则会被截断。当使用第一种形式时，如果 Shell 参数 `noclobber` 被设置且 `filename` 是已存在的文件，会导致错误。第二种形式中的 `!` 用于抑制该错误。

### 39. 假设脚本中某处有一个标签 `cleanup`，解释命令 `onintr cleanup`

**答案：**

如果脚本捕获到中断信号，将跳转到标签 `cleanup`。

### 40. 是否有方法可以在预定义的次数内重复命令，而不使用计数器控制的循环？

**答案：**

我们可以使用 `repeat` 命令在预定义的次数内重复命令，而不使用计数器控制的循环，例如：

```bash
repeat 5 ls >> listings
```

（注：由于提供的待翻译文本存在大量重复，如第 29/30 题、第 31/32 题以及第 33/34/35/36 题内容完全重复，因此按原文顺序保留并排版。）



### 43：假设在一个脚本中变量 `limt` 的值变为 `92.1`。显示消息：

你的系统上限为 92.10%

答案：

```bash
if [ $limt == 92.10 ]
then
  printf "Upper limit 92.10%% in $HOSTNAME"
fi
```

### 44：假设一个脚本包含以下代码段

```bash
set fl = /home/dbuser5/reports/fs_report1.txt
echo $fl:e
echo $fl:r
echo $fl:t
echo $fl:h
```

你预期会显示什么？

答案：

```text
txt

fs_report1

fs_report1.txt

/home/dbuser5/reports
```

### 45：创建一个脚本，将当前目录下的文件名转换为小写字母

答案：

```csh
#!/bin/csh -f
foreach my_old_file1 (`ls`)
  set my_new_file1 = `echo $my_old_file1 | tr '[A-Z]' '[a-z]'`
  if ("$my_new_file1" == "$my_old_file1") then
    continue
  endif
  mv $my_old_file1 $my_new_file1
end
```

### 46：列出 `csh` 和 `tcsh` 之间的一些基本区别

答案：

与 Berkeley 的 `csh` 相比，`tcsh` 具有命令行编辑器、文件名和命令补全功能以及增强的作业控制。

### 47：比较 `tcsh` shell 变量 `correct` 和 `autocorrect`

答案：

`autocorrect` 可以设置为在任何补全尝试之前纠正要完成的单词。`correct` 可以设置为 `'cmd'` 以纠正命令名称，或设置为 `'all'` 在每次按下回车时纠正整行。

### 48：特殊别名（alias）shell 的作用是什么？

答案：

特殊别名 shell 可以设置为指定 shell 以外的解释器。

### 49：哪种方法可以将键绑定到标准的 `vi` 或 `emacs` 绑定？

答案：

Shell 的内置命令是 `bindkey`。其 `-e` 选项将所有键绑定到标准的 `emacs` 绑定，而 `-v` 选项绑定到标准的 `vi` 绑定。

### 50：shell 变量 `color` 的作用是什么？

答案：

Shell 变量 `color` 如果被设置，将启用内置 `ls -F` 的颜色显示，并将 `--color=auto` 传递给 `ls`。

### 51：设置你的提示符显示 `username@hostname: pwd>`

答案：

可以如下实现：

```csh
set prompt = "%n@%m: %/ >"
```

### 52：如何（从 shell 提示符）“在后台”启动两个命令，并确保第二个命令在第一个命令完成后启动？

答案：

可以如下实现：

```csh
(command1 ;command2) &
```

### 53：编写一个脚本，显示文本文件中唯一单词的排序列表

答案：

可以如下实现：

```csh
#!/bin/csh
set txt_file = text_file_name
tr -s ' ' < $txt_file | tr ' ' '\n' | sort | uniq
```

### 54：分行显示你的 `PATH` 变量值

答案：

可以如下实现：

```csh
echo $PATH | tr ':' '\n' | sort
```

### 55：为什么在搜索路径中包含点（`.`）不是一个良好的做法？

答案：

当前工作目录可能是全局可写目录（如 `/tmp`）。出于安全原因，全局可写目录不能包含在 `PATH` 变量中。如果当前目录包含执行文件——其名称与保留字（标准命令等）匹配——可能会在命令执行时引发问题。因此，在搜索路径中包含点 `.` 不是良好的做法。

### 56：解释逻辑表达式 `@ x = ($n < 5 || 20 <= $n)`，然后写出该表达式的取反

答案：

a) 当 `n={5 to 19}` 时，`x= false`。

否则，`x=true`。

b) `x` 的取反：

```csh
@ y = ( !($n < 5 || 20 <= $n) )
```

### 57：下面两个命令之间有什么区别？我们什么时候可以同时使用它们？

```csh
csh-x my_new_script
csh-v my_new_script
```

答案：

```csh
csh –x my_new_script
```

a) 在变量替换后，显示命令行。

b) 查找并定位变量替换中的错误。

```csh
csh –v my_new_script
```

a) 在变量替换执行前，显示命令行。

b) 找到脚本失败的行。

### 58：解释下面这个短小的脚本

```csh
#!/bin/csh
foreach dfile (/home/users/project1/*)
  if (-z $dfile || $dfile == "core") then
    rm $dfile
  endif
end
```

答案：

该脚本将删除指定目录下的零长度文件和转储核心（core files）。

### 59：脚本使用以下语法提示用户输入内容

```csh
echo -n "Enter some input ->"
set IN = $<
```

如果用户输入了 `A B C D E`，会发生什么？

纠正你的语法以避免可能的问题。

答案：

Shell 将 `$` 替换为用户输入，即：

```csh
set IN = A B C D E
```

然后执行该命令。然而，此 `set` 命令将把值 `A` 赋值给变量 `IN`。

### 60：解释局部变量和环境变量之间的区别

答案：

局部变量仅限于设置它的 shell。环境变量则对所有子 shell 可用。虽然局部变量创建在特定的 shell 内部，但环境变量会继承其值。

### 61：解释搜索路径（search path）

答案：

搜索路径包含了各种可执行文件，当 shell 无法识别特定命令时会进行搜索。你可以使用环境变量将默认搜索路径设置为自定义路径，并在其中存储你的可执行文件。

### 62：解释通配符匹配（Globbing）

答案：

Globbing 允许你使用通配符搜索一组文件或目录。当你搜索文件或目录且不知道其确切名称时，可以使用通配符。Globbing 根据正则表达式展开通配符的可能性产生文件目录列表。

### 63：修复下面的 `switch` 语句，并说明你的修改

```csh
switch ($argv[$i])
case quit: breaksw
case list: ls
breaksw
case delete:
case erase:
@ k = $i
rm $k
breaksw
end
```

答案：

```csh
switch ($argv[$i])
  case quit:
    breaksw # 特定 case 的命令
    # 不能在同一行
  case list:
    ls # 同上
    breaksw
  case delete:
  case erase:
    @ k = $i + 1 # 这里 $argv[$i] 的值是 "erase"
    # 逻辑语法应该是 erase filename，
    # 以删除第二个参数
    rm $argv$k
    breaksw
end
```

### 64：列出 `bash` 和 `csh` 语法或功能的一些基本区别

答案：

`bash` 和 `csh` 的基本区别是：

a) `Bash` shell 有函数，`C shell` 没有。

b) `Bash` shell 使用赋值运算符为变量赋值（`variable=value`）；`C shell` 使用 `set` 命令（`set variable = value`）。

c) `Bash` shell 的命令替换比 `C shell` 更先进。

d) `Bash` shell 有高级的文件处理机制；`csh` 本身没有文件处理能力。

### 65：建议一种解决 `C shell` 缺少函数问题的方法

答案：

解决缺少函数的方法是使用别名（alias）和脚本的“巧妙组合”。例如：

```csh
alias holder ' source ~$USER/.tsch/holder_func'
```

其中脚本 `holder_func` 包含要执行的代码。

### 66：从 `/tmp` 目录执行 `(cd ; pwd) ; pwd`。解释执行的操作和输出

答案：

```csh
(cd ; pwd) ; pwd
```

`cd` 将用户返回主目录，因此第一个 `pwd` 显示主目录。但由于圆括起来的命令始终在子 shell 中执行，第二个 `pwd` 显示 `/tmp`，让用户留在原处。

### 67：编写一段代码片段，提示文件名，读取用户输入，检查其是否为普通文件，如果是，则将其存储在数组中以便后续处理。该过程必须重复，直到用户按下 Enter 键为止

答案：

```csh
#!/bin/csh

set i = 1
set fl = anything

while ( $fl )
  echo -n "Give a filename ->"
  set fl = $<
  if ( $fl = "" ) then
    break
  endif
  if( ! -f $fl ) then
    continue
  endif
  set $files[$i] = $fl
  @ i++
end

echo "Number of files: $#files"
echo "Files are: $files[*]"
```

### 68：使用 `awk` 数学函数计算圆面积（`area= PI*rad2`）

答案：

```csh
alias mathcalc ' awk "BEGIN{ print \!* }" '
set rad = 1.3
set circle_area = `mathcalc atan2(0,-1)*${rad}*${rad}`
```

解释：该 alias 定义了一个名为 `mathcalc` 的数学计算器，它使用“单行”`awk` 执行计算（受 `awk` 中可用数学函数的限制）。然后，使用该计算器计算圆的面积。它使用了评估 `PI` 的反正切函数 `atan2`。

### 69：使用 `awk` 将 `/etc/passwd` 文件中的条目分割到数组，并将密码字段替换为字符串 `"secret"`

答案：

```csh
set user = username
set entry = `grep ^$user: /etc/passwd | awk' {$2 = "secret"; split($0,a,":"); for (i=1; i<=7; i++) print a[i]}'`
```

### 70：解释以下代码段

```csh
set ports = (`netstat -an | awk '/SHED/ {split($4,c,"."); print c[4]}'`)
set remaddrs = (`netstat -an | awk '/SHED/ print $5}'`)
@ i = 1
foreach port ($ports[*])
  set service = `grep $port /etc/services | cut -f1 -d' '`
  echo "$service connection established from $remaddrs[$i]"
  @ i++
end
```

答案：

它创建了一个数组来存储每个已建立的网络连接所使用的端口号，以及第二个存储相应远程 IP 地址的数组。然后，使用 `foreach` 循环将端口号“解析”为服务名称，并为每个连接以“Service_name connection established from Remote_IP_Address”的形式显示描述消息。

### 71：列出可用方法（带示例）来替换字符串中任意出现的子字符串为另一个子字符串

答案：

在字符串中将任意出现的子字符串替换为另一个子字符串，可用的方法有：

a) 使用 `sed`：

```csh
set sedstring = `echo $text | sed 's/search_string/replacement/g'`
```

b) 使用 `awk`：

```csh
set awkstring = `echo $string | awk -v s1="$search" -v s2="$substitute" '{gsub(s1,s2); print $0}'`
```

c) 使用编辑修饰符（用法有限）：

```csh
set text = "now is the time for all good men"
echo $text:gs/o/O/
```

### 72：编写一个片段，根据扩展名对目录下的文件进行分类（简单起见，仅处理 `.c`、`.o`、`.txt` 和 `.png` 文件）。为每个扩展创建一个数组，包含文件名。最后，显示每个扩展的文件数量

答案：

```csh
#!/bin/csh

set dir = /home/~ # 目录路径

foreach fl ($dir/*)
  switch ($fl)
    case *.c:
      set cfiles = ($cfiles[*] $fl)
      breaksw
    case *.o:
      set ofiles = (ofiles[*] $fl)
      breaksw
    case *.txt:
      set txtfiles = (txtfiles[*] $fl)
      breaksw
    case *.png:
      set pngfiles = (pngfiles[*] $fl)
      breaksw
    default:
      breaksw
  endsw
end

echo "There are $#cfiles .c files, $#ofiles.o files, $#txtfiles txt files and $#pngfiles .png files in directory $dir"
```

### 73：编写一个脚本向用户显示一个选择菜单。菜单应该不断显示，直到用户选择特定的“exit”选项。脚本应向用户显示选择菜单。菜单应该不断显示，直到用户选择特定的“exit”选项

答案：

脚本应向用户显示一个选择菜单。菜单应该不断显示，直到用户选择特定的“exit”……

```csh
c
/csh

set ans = 0
while ($ans != 4 )
echo " MENU"
echo "=================="
echo "1 Rename a file"
echo "2 View contents"
echo "3 Examine file"
echo "4 Exit"
echo "Make your -> "
set ans = =

switch ($ans)
case 1:
echo "Enter a filename ->"
set fl = $<
if ( ! -f $fl ) then
echo "File must exist..."
endif
mv $fl
breaksw
case 2:
echo "Enter a filename ->"
set fl = $<
if ( ! -f $fl ) then
echo "File must exist..."
endif
cat $fl
breaksw
case 3:
echo "Enter a filename ->"
set fl = $<
if ( ! -f $fl ) then
echo "File must exist..."
endif
vi $fl
breaksw
case 4:
exit
breaksw
default:
echo "Invalid choice"
breaksw
end
```

### 74：编写一个脚本向用户显示一个选择菜单。菜单应该不断显示，直到用户选择特定的“exit”选项

答案：

```csh
#!//csh

set thres = 40
set total = `grep ^alias | wc -l`
if ($ total > $thres ) then
mail -s "Too many aliases" $USER << EOF
Your aliases are greater than the limit
EOF
endif
```

### 75：显示文件名和权限

答案：

```csh
set files = (`ls -l | grep -v total | tr -s ' ' | cut -9 - '`)
set perms = (`ls -l | grep -v total | tr -s ' ' | cut -1 - '`)

echo " FILE LIST "
echo "===================="
echo "$files \t $perms]"
```

### 76：创建一个脚本，列出系统中所有的文件系统（挂载点）以及使用的百分比

答案：

```csh
set fs = (`df | grep -v ^Filesystem | tr -s ' ' | cut -5 - '`)
set pcts = (`df | grep -v ^Filesystem | tr -s ' ' | cut -4 - '`)

set count = $#fs
set i = 1
while ($i <= $count)
echo "File system $fs[$i] is $pcts[$i] used"
@ i++
end
```

### 77：解释以下脚本并提出任何改进



```csh
#!//csh

if ( -z "$1" )
then
  echo "Usage: `basename $0` filename"
  exit 20
fi

Username=guru
pword=/home/guru/password.file
Password=`cat $pword`
Filename=`basename $1`
Server="Servername"
Directory="dirpath"

ftp -n $Server <<EOF
user $Username $Password
binary
bell
cd $Directory
put $Filename
bye
EOF

exit 0
```

**Answer：** 该脚本检查命令行是否有一个参数。它启动到服务器的 `ftp` 会话，并使用“这里”文档向传递传递命令：用户名和密码（密码从文件中读取）。在会话期间，它更改目录并将文件传输到服务器。

**建议：** 安全性是此脚本最重要的问题。它使用了 `ftp`（最好使用更安全的替代方案，如 `sftp`），并且密码以明文存储在文件中！最好使用可用的加密/解密工具（如标准的 `crypt` 函数）。另一个点是灵活性：所有参数都硬编码在脚本中。最好在脚本执行期间向用户询问。

## 78: 使用 `bc` 计算器进行一个涉及浮点数的变量比较。将你的示例写作为 `if` 条件语句的一部分。

**Answer：**

```csh
set var1 = 0.4
if ( `echo "if ( ${var1} <= 1.1 ) 1" | bc` ) then
  <当 $var1 小于或等于 1.1 语句>
endif
```

## 79: 使用浮点数比较语句作为循环条件（以及循环控制）编写一个 `while` 循环。

**答案：**

```bash
set curvalue = 1.678*10⁰³
set upper = 1289.56
while ( `echo "if ( $curvalue <= $upper) 1" | bc` )
  <statements when $curvalue <= 1289.56>
End
```

## 80: 如果 C-shell 中没有简单的文件读取功能，你可以用什么来临时解决？

**答案：**

使用 `awk` 和 shell 循环的组合是一种通宜办法，因为 C-shell 中没有简单的文件读取功能。

## 81: 提取文本文件的第 `n` 行并将其赋值给变量。

**答案：**

```bash
set text = `awk -v ln=$j '{if (NR==ln) print $0}' textfile`
```

其中变量 `j` 定义了第 `n` 行。

## 82: 假设 `input_file` 是一个用空格分隔字段的文本文件，当执行以下命令时，`ncol` 的值将是多少？

```bash
setncol = `awk '{if (FNR==1) print NF}' input_file`
```

**答案：**

该文件第一行的字段数将被设置为 `ncol` 的值，因为：

a) `FNR` 和 `NF` 是 `awk` 中的变量

b) 读取的记录数将被赋值给 `FNR`

c) 记录中的字段数将被赋值给 `NF`

## 83: 找到存储在数组中的整数的最小值。

**答案：**

```bash
set array = (4, -2, 5, 8, 13, 1)
set array_org = ($array[*]) # 创建一个克隆以保留原始数字
set min = $array[1]
while ( $#array > 0 ) # 如果至少有一个元素
  if ( $min > $array[1] ) then
    set min = $array[1]
  endif
  shift array # 丢弃数组的第一个元素
end
echo "The original numbers are: $array_org[*]"
echo "The minimum number is: $min"
```

## 84: 解释以下命令块：

```bash
foreach luser (`who | cut -f1 -d' ' | uniq` )
  if( -f /allfiles/$luser.msg) then
    mail $luser < $luser.msg
    echo "Message sent to $luser"
  else
    mail $luser << END
    Dear $luser,
    No message file has been created for you.
    Please check your settings
    END
  endif
end
```

**答案：**

变量 `luser` 的取值为系统中每个登录用户的用户名（如果某些用户有多个登录会话，则取唯一名称）。在循环内部，它会检查每个用户是否存在一个“个性化”的消息文件，其命名格式为“`username.msg`”。如果是，它会将该文件发送到用户的信箱。如果不是，它将使用“在此文档（here document）”创建一个消息并发送给用户，告知其他正在等待的文件不存在。

## 85: C shell 提供了一种读取单行的方法：

```bash
set VAR = $<
```

这种语法的局限性是什么？

**答案：**

此命令始终从标准输入读取。`<` 只代表 `STDIN`，且在脚本运行期间无法更改。

## 86: 解释以下代码段。

```bash
foreach my_line ( "`cat /etc1/my_passwd`" )
  set my_line = "$my_line:gas1/ /_/"
  set my_line = "$my_line:gas1/:/ /"
  set argv = ( $my_line )
  set my_name1 = $1
  set my_name2 = "$5:gas1/_/ /"
  echo $my_name2
end
```

**答案：**

这是逐行读取文件的一种通宜方法。在每次循环迭代中，`line` 变量从 `/etc1/my_passwd` 文件中获取下一行（注意 `cat/etc1/my_passwd` 周围的双引号），然后使用变量修饰符，脚本首先将空格替换为下划线，将冒号（`:`）替换为空格。然后将位置参数设置为行的字段，再次将下划线替换为空格，并显示注释字段。

## 87: 修复以下脚本中的任何语法或逻辑错误。

```bash
# 此脚本创建路径下的子目录列表
#!/bin/csh
echo "Subdirectories in $DirPath"
cd $DirPath
foreach file (*)
  if ( -e $file ) then
    echo $file
  endif
end
```

**答案：**

a) `#!/bin/csh` 行必须是脚本的**第一行**。

b) 变量 `DirPath` 未设置，因此 `cd $DirPath` 命令会变为进入用户的主目录 (`cd`)。

c) 测试 (`-e $file`) 检查的是 `file` 变量的值是否存在，而不是检查它是否为目录。它应该是：`( -d "$file" )`。

d) 在变量替换表达式周围使用双引号更安全，例如 `"$file"`。

正确的脚本如下：

```bash
#!/bin/csh
# 此脚本创建路径下的子目录列表
echo "Subdirectories in $DirPath"
cd $DirPath
foreach file (*)
  if ( -d "$file" ) then
    echo "$file"
  endif
end
```

## 88: 解释以下脚本。

```bash
foreach my_line (
  )
  echo
  "
  



endif
```

**答案：**

该脚本通过 `foreach` 逐行处理文件，使用 `wc` 统计行数，并打印文件名。

## 89: 以下命令之间是否存在差异？

```bash
setncol = `awk '{if (FNR==1) print NF}' input_file`
```

**答案：**

该文件第一行的字段数将被设置为 `ncol` 的值，因为：

a) `FNR` 和 `NF` 是 `awk` 中的变量

b) 读取的记录将被赋值给 `FNR`

c) 记录中的字段数将被赋值给 `NF`

## 90: 找到存储在数组中的整数的最小值。

```bash
set array = (4, -2, 5, 8, 13, 1)
set array_org = ($array[*]) # 创建一个克隆以保留原始数字
set min = $array[1]
while ( $#array > 0 ) # 如果至少有一个元素
  if ( $min > $array[1] ) then
    set min = $array[1]
  endif
  shift array # 丢弃数组的第一个元素
echo "The original numbers are: $array_org[*]"
echo "The minimum number is: $min"
```

## 91: 解释以下命令块：

```bash
foreach luser (`who | cut -f1 -d' ' | uniq` )
  if( -f /allfiles/$luser.msg) then
    mail $luser < $luser.msg
    echo "Message sent to $luser"
  else
    mail $luser << END
    Dear $luser,
    No message file has been created for you.
    Please check your settings
    END
  endif
end
```

**答案：**

变量 `luser` 的取值为系统中每个登录用户的用户名（如果某些用户有多个登录会话，则取唯一名称）。在循环内部，它会检查每个用户是否存在一个“个性化”的消息文件，其命名格式为“`username.msg`”。如果是，它会将该文件发送到用户的信箱。如果不是，它将使用“在此文档（here document）”创建一个消息并发送给用户，告知其他正在等待的文件不存在。

## 92: C shell 提供了一种读取单行的方法：

```bash
set VAR = $<
```

这种语法的局限性是什么？

**答案：**

此命令始终从标准输入读取。`<` 只代表 `STDIN`，且在脚本运行期间无法更改。

## 93: 解释以下代码段。

```bash
foreach my_line ( "`cat /etc1/my_passwd`" )
  set my_line = "$my_line:gas1/ /_/"
  set my_line = "$my_line:gas1/:/ /"
  set argv = ( $my_line )
  set my_name1 = $1
  set my_name2 = "$5:gas1/_/ /"
  echo $my_name2
end
```

**答案：**

这是逐行读取文件的一种通宜方法。在每次循环迭代中，`line` 变量从 `/etc1/my_passwd` 文件中获取下一行（注意 `cat/etc1/my_passwd` 周围的双引号），然后使用变量修饰符，脚本首先将空格替换为下划线，将冒号（`:`）替换为空格。然后将位置参数设置为行的字段，再次将下划线替换为空格，并显示注释字段。

此脚本使用了 `getopt` 命令，它可以一次性处理整个参数列表。如果参数列表匹配，`getopt` 会对参数列表进行规范化（按照 UNIX 命令使用的典型方式重新排序），将标志位（flags）及其可选参数放在任何非标志参数之前，并在末尾添加单个 `"--"` 参数以表示没有更多标志位需要处理。

在出现 `-h` 选项的情况下，脚本将显示“用法”（usage）信息并终止。在出现 `-o` 选项的情况下，脚本会将 `OUTPUT_FILE` 变量设置为随后的参数。在出现 `-l` 选项的情况下，脚本会将 `DO_LONG` 变量设置为 `-l`。`while` 循环后的 `shift` 命令会移除末尾的 `--`。

如果没有使用任何选项，脚本将运行 `ls $*`（其中 `$*` 是剩余参数）；如果使用了 `-l` 选项，将运行 `ls -l $*` 命令；如果使用了 `-o` 文件，将运行 `ls -l $*` 命令并将输出重定向到 `OUTPUT_FILE` 文件。

### 94: 编写一个脚本，计算存储在数组中的一组浮点数的最小值、最大值和平均值。

**答案：**

```bash
set array = (5, 10, 2, 13, 0.2345)

foreach num ($array[*])
  echo $num >> nums_file
end

awk '{if(min==""){min=max=$1}; if($1>max) {max=$1}; if($1< min) {min=$1}; total+=$1; count+=1} END {print "Average is: "total/count, "Min is: "min, "Max is: "max}' nums_file
```

---

### 95: 你有一个具有对称模式的数据文件（每条记录字段数相同），第一行包含字段标题。你想提取实际数据记录的第 3 列（字段），即除去表头行（第一行）和任何注释行（假设它们以 `#` 或 `*` 开头）。请给出一个解决方案并简要解释。

**答案：**

```bash
set cn = 3
set ncols = `awk '{FNR == 1 {print NF}' input_file `
if ( $cn <= $ncols ) then
  set col$cn = ` awk -v i=$cn '$0 !~ /^[#*]/ && FNR != 1 { print $i }' input_file`
else
  echo "The column number must be in the range 1 to $ncols"
endif
```

变量 `ncols` 包含每条记录的列总数。`if` 结构用于避免请求的列位置号大于总列数的情况。`col3` 将是第三列值的数组。

---

### 96: 假设 `input_file` 是一个具有非对称模式的表格数据文件，即每条记录（行）可能有不同数量的字段，且前 3 行描述了使用的模式。请解释以下代码段。

```bash
set cn = 3
set ccounts = `awk '{FNR > 3 {print NF}' input_file `
set ccounts1 = ( $ccounts[*] )
set ccounts2 = ( $ccounts[*] )
set mincn = $ccounts[1]
while ( $ccounts1 > 0 )
  if( $mincn > $ccounts1[1] ) then
    set mincn = $ccounts1[1]
  endif
  shift ccounts1
end
set maxcn = $ccounts2[1]
while ( $ccounts2 > 0 )
  if ( $maxcn < $ccounts2[1] ) then
    set maxcn = $ccounts2[1]
  endif
  shift ccounts2
end
if ( $cn <= $maxcn ) then
  set col$cn = ` awk -v i=$cn -v minc=$mincn 'FNR > 3 { (FN < minc ) ? print FN "null" : print $i }' input_file`
else
  echo "The column number must be in the range $mincn to $maxcn"
endif
```

**答案：**

该脚本从非对称数据文件中提取某一列的内容：

`cn` 变量持有要提取的列。`ccounts` 数组持有所有实际数据记录（`FNR > 3`）的字段数。数组 `ccount1` 和 `ccount2` 是 `ccount` 数组的副本，用于从 `ccounts` 数组中计算最小值和最大值。我们使用这些临时数组是为了保留原始数组以便后续使用。第一个 `while` 循环计算最小值，第二个循环计算最大值。每个循环迭代中的 `shift` 命令会丢弃数组的第一个元素。`if` 语句随后检查请求的列（字段）编号是否小于最大值，如果是，则 `awk` 命令在存在任何内容（`FN >= minc`）时打印该列的内容，否则打印字符串 `"FNnull"`。反之，如果请求的列编号大于最大值，脚本将显示一条消息。

---

### 97: 假设你有一个数据文件，但其内部格式并不保持一致。你想从该文件中提取两列，但你不知道列的顺序，只知道它们的标题：`Name` 和 `email`。写一个实现这些任务的脚本。

**答案：**

```bash
#!/bin/csh -f
set fl = filename
set namepos = `head -1 "$fl" | awk '{split($0,a) ; for ( j in a ) { if (a[j] = "Name") {print j}}}' `
set mailpos = `head -1 "$fl" | awk '{split($0,a) ; for ( j in a ) { if (a[j] = "email") {print j}}}' `
foreach line ("`cat $fl`")
  set line = "$line:gas/ /_/"
  set argv = "$line"
  set name = "$argv[$namepos]"
  set name = "$name:gas/_/ /"
  set names = ($names[*] "$name")
  set mail = "$argv[$mailpos]"
  set mails = ($mails[*] "$mail")
end
```

---



### 98: 创建一个脚本逐行读取文本文件直到文件末尾。不要使用 `awk`。

**答案：**

```bash
set inputfile = textfile
set total = `cat $inputfile | wc -l`
set count = 1
while ($count <= $total)
  if ($count == 1)
    set record = `head -n 1 $inputfile`
  else
    set record = `tail -n +$count $inputfile | head -n 1`
  endif
  echo $record
  @ count++
end
```

退出状态是 shell 脚本执行后返回的正数或零。如果退出状态为零，则意味着脚本执行成功。除零以外的任何数字都表示错误。对于每种错误，会返回不同的数字。

### 104: 什么是子壳？如何创建它？

答案：

shell 脚本中包含在括号内的较小子部分称为子壳。虽然子壳可以访问外部的变量，但在子壳内部它无法更改这些变量的值。

例如，你在主 shell 中有一个变量 `var1`，初始赋值为值 `5`。在子壳中，它被赋值为 `8`。在子壳内部，它的值为 `8`，但一旦离开子壳，它的值将仅为 `5`。

### 105: 考虑以下消息：

`"bash: scriptfile: Execute permission denied."`

你如何修复它（假设你是 `scriptfile` 的所有者）？

答案：

用户没有对 `scriptfile` 的执行权限。我们可以运行以下命令来为所有人授予执行权限：

```bash
chmod +x scriptfile
```

### 106: `case` 语句用于将变量的值与可能的匹配项列表进行比较。对还是错？

答案：

对（TRUE）

### 107: 你不记得 `sort` 命令的正确选项（switch）以便以反序排序某些条目。你可以做什么？

答案：

打开 `sort` 命令的“man”页，运行命令：

```bash
man sort
```

然后搜索关键字 "reverse"（使用 `/` 开始搜索）。

### 108: shell 脚本的第一行是：

```bash
#!/bin/bash
```

shell 是如何解释这一行的？

答案：

用于启动脚本的 `exec` 系统调用会检查脚本的前两个字节是否包含特殊序列 `#!`，该序列在同一行中指定了用于执行此脚本时要使用的解释器可执行文件。

### 109: 你需要找到 `/home` 目录下所有在过去 10 天内未访问过的文件。你可以做什么？

答案：

运行以下命令：

```bash
find /home -type f -atime +10
```

### 110: 你如何检查系统上是否有运行的 `sshd` 进程？

答案：

我们可以通过运行命令来检查：

```bash
ps -ef | grep sshd
```

或者

```bash
pgrep sshd
```

### 111: 运行以下命令会发生什么？

```bash
mkdir -p /tmp/{my,your,his,her}dir/{contacts,files}
```

a) 在 `/tmp` 下将创建 6 个新目录

b) 在 `/tmp` 目录下将创建 8 个新目录

c) 在 `/tmp` 目录下将创建 2 个新目录

d) 它不会创建新目录并显示错误消息

答案：

选项 b) 是正确的。将创建 8 个新目录。

### 112: 下一行是 bash 脚本中条件语句的开头：

```bash
if [[ $1 = $var1 || = $var2 ]]
```

该语句至少有一个错误。请识别并修正它。

答案：

测试条件中存在语法错误。在第二个表达式中，没有左侧部分。此外，最好在变量替换周围使用双引号，以确保在变量为空或未定义时不会产生语法错误。正确的语句是：

```bash
if [[ "$1" = "$var1" || "$1" = "$var2" ]]
```

### 113: `for` 循环需要参数列表。该列表可以由以下产生：

a) 命令替换：`for var in $(command)`

b) 变量替换：`for var in $var`

c) 命令行给出的参数：`for var in $*`

d) 测试条件：`for var in "$var" -eq`

e) 以上所有

答案：

选项 a)、b) 以及 c) 将得到预期的结果。

### 114: 给定以下嵌套循环，如果满足测试，你会使用什么命令来代替 `command-to-process-file`，以便 shell 执行最后一个命令：

```bash
while true
do
    echo "Please enter a filename:"
    read ans
    if [[ -f "$ans" ]]
    then
        break
    fi
done
cat "$ans"
```

### 115: 如果以下命令位于用户的 `.bash_profile` 中会发生什么？

```bash
trap '' INT
```

答案：

用户无法中断从该 shell 启动的任何命令。`trap` 命令将捕获 `INT` 信号，改变 shell 的行为以忽略该信号。

### 116: 变量的值应该与可能的值（和/或模式）进行比较，并对每个值运行不同的命令。你倾向于使用哪种结构来进行这些检查？

答案：

```bash
case "$var" in
    pattern_1) ;;
    pattern_2) ;;
esac
```

### 117: 以下命令的预期输出是什么？

```bash
echo {a..z}
```

答案：

它回显所有小写字母，即 `a b c d e f g h i j k l m n o p q r s t u v w x y z`。

### 118: 如何在后台运行作业？

答案：

通过在命令末尾添加 `&` 来在后台运行作业。

### 119: `cd -` 命令执行了什么操作？

答案：

`cd -` 切换到上一个目录。

### 120: shell 中字符 `~` 的特殊含义是什么？

答案：

`~` 对应于主目录 `$HOME`：

a) `~` 对应于主目录

b) `~1` 对应于用户

c) `~+` 对应当前目录 `$PWD`

d) `~-` 对应上一个目录

e) `==` 是正则表达式匹配

### 121: 变量 `variable` 和 `$variable` 之间的区别是什么？

答案：

`variable` 是变量名，而 `$variable` 是它的值。

### 122: 用什么命令定义本地变量？

答案：

使用 `local` 命令定义。

### 123: 如何找到系统中安装的 bash shell 版本？

答案：

使用以下命令找到 bash 版本：

```bash
echo $BASH_VERSION
```

更多详情请使用数组 `BASHINFO`。

### 124: 内置变量 `EDITOR` 作用是什么？

答案：

`EDITOR` 调用默认编辑器，通常是 `vi` 或 `emacs`。

### 125: 内置变量 `PATH` 的目的是？

答案：

定义可执行文件的路径列表，`PATH` 将被 shell 用于查找这些文件。

### 126: Bash 中有任何方法声明整数变量吗？

答案：

是的，我们可以使用 `typeset -i` 命令（或相应的 `declare`）声明整数变量。

### 127: shell 如何解释 `"echo ??a"`？

答案：

在启动 `echo` 之前，shell 将替换两个 `??`。对于 shell 来说，`?` 代表文件名中的任意一个字符。但文件名中的点不能被任何字符替换，应字面给出。此命令将输出当前目录下由三个字符组成的文件和子目录，但不包括点开头的。

***

## Bash - 中级

### 128: 编写一个简单的脚本，检查执行用户的 UID，如果用户不是 root，则显示消息并退出。

答案：

```bash
#!/bin/bash
if (( $(id -u) = 0 ))
then
    echo "Hello root"
else
    echo "You must login as root to execute this script!"
    exit 10
fi
exit
```

### 129: 构建一个 bash shell 模式来匹配以一个数字结尾的任意字母数字字符串。

答案：

```bash
*([a-zA-Z0-9])[a-zA-Z][0-9]
```

### 130: 编写一个命令列出完全匹配 `Name#_##` 模式的文件。

答案：

列出完全匹配 `Name#_##` 模式的文件的命令是：

```bash
echo Name[0-9]_[0-9][0-9]
```

### 131: 编写一个命令获取所有以 `.` 开头的目录项（文件和子目录），排除 `.` 和 `..`

答案：

命令是：

```bash
ls -d .*
```

```bash
echo .[!.]*
```

### 132: 你必须检查系统上是否存在某个文件，以及你是否对该文件具有读取权限。你会使用哪种语法？

**答案：**

我们使用的语法是：

```bash
if [[ -f filename && -r filename ]]
then
  echo "filename exists and it's readable"
else
  echo "filename does not exist or is not readable"
fi
```

### 133: 考虑以下片段。

```bash
mail user << end

Hello,

Please 检查该程序在 $(hostname) 中记录的最后条目：

$(tail -10 /var/opt/application/logfile)

EOF
end
```

发送给用户的消息是什么？

**答案：**

发送给用户的消息是：

Hello,

请检查该程序在系统 `hostname` 中记录的最后条目：

（来自 `/var/opt/application/logfile` 的最后 10 行）

EOF

### 134: 运行此循环时会发生什么？

```bash
while read line
do
  echo $line
done <datafile
```

**答案：**

该代码逐行读取 `datafile` 的内容，并处理（此处仅显示）每一行。它会在到达文件末尾时结束。

### 135: 运行此循环时会发生什么？

```bash
while read line <datafile
do
  echo $line
done
```

**答案：**

这是一个无限循环。每次迭代都会打开 `datafile`，只读取第一行，对其进行处理（仅显示），并不断重复。

### 136: 你应该从 `passwd` 文件中找到定义用户账户 `dbuser1` 的条目。

```bash
grep 'dbuser1' /etc/passwd
```

上述命令是：

a) 正确的，

b) 正确但不精确或充分，或者

c) 完全不足，

为什么？

**答案：**

它是正确的，但并不精确或充分。该命令将显示所有在任何位置包含字符串 `dbuser1` 的行，而不仅仅是在行首以及字段分隔符（`:`）之前。

将仅返回以 `dbuser1` 开头的行的命令如下：

```bash
grep '^dbuser1:' /etc/passwd
```

### 137: 使用正确的语法显示名为 `datafile` 的文件中以字符串 `ing.`（字面上的点）结尾的所有行。

**答案：**

```bash
grep 'ing\.$' datafile
```

### 138: 一个应用程序（或服务）的配置文件包含许多被注释掉的行，只有两三行是有用的。你如何只显示基本的（未注释）数据？

**答案：**

```bash
grep '^[^#]' conf_file
```

或者

```bash
grep -v '^#' conf_file
```

### 139: shell 如何将变量传递给 `awk`？

**答案：**

shell 通过 `awk` 的 `-v` 选项以及 `awk` 语句内部保留字 `ENVIRON` 将变量传递给 `awk`。例如：

```bash
var1="Some data"
awk -v Data="$var1" 'awk statement ...'
```

使用已导出变量的 `awk` 语法：

```bash
ENVIRON["var"]
```

### 140: 正确或错误：当向 `awk` 提供输入时，`awk` 将处理每一个记录。

**答案：**

正确 (TRUE)

### 141: 正确或错误：在 `awk` 语句中所有未引号的字符串都被视为变量、关键字或函数。

**答案：**

正确 (TRUE)

### 142: 你有一个简单的（文本）示例。

*(注：正文此处内容缺失，根据指令保留核心语义逻辑进行排版)*

### 143: 正确或错误：当向 `awk` 提供输入时，`awk` 将处理每一个记录。

**答案：**

正确 (TRUE)

### 144: 正确或错误：在 `awk` 语句中所有未引号的字符串都被视为变量、关键字或函数。

**答案：**

正确 (TRUE)

### 145: shell 如何将变量传递给 `awk`？

**答案：**

shell 通过 `awk` 的 `-v` 选项将变量传递给 `awk`...

### 146: 以下逻辑的示例。

```bash
if (condVar > someVal) {console.log("xxx")}
```

*(注：由于提供的原始文本 142-161 部分存在大量重复或逻辑断层，以上已根据高级文档工程师标准对核心逻辑内容进行了结构化处理与清理)*

a) `variable=`cat file1``（使用 `cat` 进行命令替换，因此执行速度比下一种慢）

b) `variable=`<file1``（使用输入重定向进行命令替换）

## 162: 命令替换的两种形式 `$(cmd)` 和 `` `cmd` `` 之间有什么区别？

答案：

两种命令替换形式之间的区别在于：

a) 较新的形式 `$(cmd)` 允许嵌套，例如：

`count=$(wc -w $(ls -l | awk '{print $9}'))`

b) 两种形式对双反斜杠的处理方式不同：

`` echo `echo \\` `` 将显示一个空行，但

`echo $(echo \\)` 将显示一个 `\`。

## 163: 描述“与”列表的执行机制。

答案：

“与”列表是一种链式命令的方法。语法为：

`command 1 && command 2 && ... command-n`

每个命令都会按顺序执行，前提是上一个命令的退出值为 TRUE。在遇到第一个 FALSE 返回值时，链将终止，剩余命令将不会执行。

## 164: Bash shell（版本 4.2）允许表示和显示外语字母字符。如何做到？请给出一个数学符号 PI 的示例。

答案：

Bash 支持 Unicode 转义字符 `\u` 和 `\U`。命令：

`echo -e '\u220F'`

将显示 PI (π)。

## 165: 给出以下代码段的输出。

```bash
a=5

let "val = a<6?1:2"

echo $val

let a++

let "val = a<6?2:3"

echo $val
```

答案：

1（来自第一个 `echo`）

3（来自第二个 `echo`）

## 166: 目录 `/mydir` 的权限为 `rw-r-----` 且你是该目录的所有者。你可以显示 `/mydir` 的内容吗？你可以切换到 `/mydir` 吗？你可以在 `/mydir` 下创建一个新文件吗？你可以读取 `/mydir` 中包含的文件内容吗？

答案：

如果没有执行权限，你可以将当前工作目录切换到该目录，但不能以任何方式使用末尾的 `/`（例如 `/mydir/`）。因此，你只能执行 `ls` 命令显示该目录的内容，但不能执行 `ls -l`，因此无法获取该目录的详细列表。你无法执行类似 `cat /mydir/file` 的命令，无法访问 `/mydir` 下的任何文件，无论权限如何，因为 `/mydir/` 语法是不允许的。

## 167: 声明函数的两种有效语法是什么？

答案：

a)
```bash
function function_name {

  commands

}
```

b)
```bash
function_name() {

  commands

}
```

## 168: 修正以下函数的声明。

```bash
holder() { echo "Press Return to continue...." ; dummy }
```




```bash
holder() {
  echo "Press Return to continue...."
  dummy
}
```

缺少分号。

## 169：`+=` 运算符执行什么？

答案：

在数值上下文中：整数算术（`let var+=1`）。

在字符串上下文中：字符串拼接（`string+=value`）。

# Bash——高级教程

## 170：解释 `whiptail`、`man` 和 `grep`

答案：

`whiptail` 在 shell 脚本中用于显示用户友好的对话框，以展示信息或接收用户输入。

`man` 命令类似于 `help` 和 `info` 命令，用于提供帮助。区别在于，`man` 显示的是 roff（roff 是一种文本格式）。

`grep` 是一个用于在管道或文件中搜索信息的工具，可以配合 `ls` 命令使用。假设你正在寻找一个包含 `mynm` 字符串的文件，通过 `grep` 命令进行搜索，你会获取该文件。

## 171：解释 `/dev` 和 `/proc`

答案：

`/dev` 文件夹包含硬件信息的文件。设备文件存储在此处，也可能包含关于设备的信息。你可以像加载单个文件一样加载它们。

`/proc` 文件夹是一个镜像，包含当前正在运行的进程和程序的信息。

## 172：解释 `trap` 命令

答案：

`trap` 用于调试程序运行时系统发送的信号或错误。`trap` 接收系统发送的信号，这类似于 C++ 或 Java 中的异常处理。

## 173：什么是 POSIX？

答案：

POSIX 字符集允许不使用通配符指定字符范围。它们比通配符更易读且更易用。此外，POSIX 允许捕捉控制字符和图形，例如 `[:alpha:]` 表示 A-z。

## 174：解释 `tput` 和 `infocmp`

答案：

`tput` 命令允许初始化终端或访问其中的信息。可以使用带有许多选项的 `tput` 命令控制各种终端功能。例如，`tput clear` 清屏，`tput reset` 重置终端设置的参数。`infocmp` 命令用于获取当前终端的详细信息，来自 terminfo 数据库。

## 175：定义一个名为 `ls` 的函数会导致什么问题？

答案：

如果我们定义了一个名为 `ls` 的函数，该函数将覆盖 `ls` 命令。

## 176：定义一个名为 `pause_until_return` 的函数，暂停脚本执行直到用户按下回车键

答案：

```bash
function pause_until_return() {
  echo "Press RETURN to continue..."
  read dummy
}
```

## 177：如何创建函数库？这种库的优点是什么？

答案：

你可以创建一个函数“库”文件，即包含函数声明和变量定义的文件，然后在任何需要这些函数的脚本中 `source` 该“库文件”：

```bash
#!/bin/bash

. /path_to_library/library_file # 注意点
```

使用函数库的优点是：

a) 减小 shell 脚本文件的大小。

b) 更新方便。如果库文件被许多脚本使用且其内容被修改，所有调用该函数的脚本立即可以使用更新版本。

## 178：允许使用递归函数（调用自身的函数）吗？

答案：

是的，允许使用递归函数。但必须注意不要启动“死循环”。

## 179：以下代码段使用文件描述符创建文件

```bash
exec 3> /tmp/newfile

echo -u3 "First line..."

echo -u3 "Second line ..."

exec 3>&-
```

以下代码段创建相同的文件：

```bash
echo "First line ..." > /tmp/newfile

echo "Second line..." >> /tmp/newfile
```

但上述代码段的运行方式存在重要区别。你能解释一下吗？

答案：

第一个代码段通过 `exec 3>` 开启了一次 `newfile`，然后文件保持打开状态直到第二个 `exec` 执行。

在第二个代码段中，文件在第一次执行 `echo` 命令时被打开，然后关闭；当第二个 `echo` 开始时再次打开，然后再次关闭。从性能角度来看，如果这种语法被多次使用（例如在循环内部），可能会是一个重要问题。

## 180：如果你需要在脚本中使用交互式命令（如 `sftp`），可以使用什么来自动化此功能（无需用户交互）？

答案：

我们可以使用所谓的“这里”文档（here document）。

## 181：以下命令的输出是什么？

`netstat -rn | awk '/^def/ {print "Default gateway is ", $2}'`

答案：

字符串 `"Default gateway is "` 后面跟着默认网关的 IP 地址。

## 182：以下命令的输出是什么？

`awk -F: '{BEGIN {OFS="=="} ; $2 = "****"; print NR "\t" $0}' /etc/passwd`

答案：

`/etc/passwd` 的带编号行，其中密码字段被替换为字符串 `"****"`，分隔符 `":"` 被替换为 `"=="`。

## 183：解释以下管道命令

`grep bash file1 | diff file2 -`

答案：

连字符（`-`）用于将第二个命令的标准输出（stdout）传递给其他命令。在这里，管道将 `file1` 中包含字符串 `"bash"` 的行与 `file2` 的全部内容进行比较。

## 184：如何声明一个关联数组？

答案：

```bash
declare -A assoc
```

## 185：哪种语法返回（展开为）数组 `ARRAY` 中的索引？

答案：

```bash
${!ARRAY[@]}
```

或者：

```bash
${!ARRAY[*]}
```

## 186：内置命令 `mapfile` 有什么用？

答案：

内置命令 `mapfile` 用于将标准输入（以及通过重定向来自文件）的行分配给由参数定义的数组，每行都是一个独立的元素。如果命令行中没有给出数组，则默认数组名称为 `MAPFILE`。目标数组必须是一个整数索引数组（而不是关联数组）。

## 187：在不使用 `if` 的情况下，编写以下 `if` 结构的等效但更短的形式

```bash
if [[ $# -eq 0 ]]
then
  dirpath=$(pwd)
else
  dirpath=$@
fi
```

答案：

```bash
[[ $# -eq 0 ]] && dirpath=$(pwd) || dirpath=$@
```

## 188：给出以下片段的输出并解释它

```bash
a='$val1'

val1='$val2'

val2=newval

echo $a

eval echo $a

eval eval echo $a
```

答案：

a) `$val1`（第一个 `echo`：单引号不允许任何替换）。

b) `$val2`（第二个 `echo`——`eval`：`eval` 的调用强制对其参数进行重新评估，因此参数 `$a` 被替换为 `a` 的值，即 `$val1`；然后 `$val1` 被替换为 `val1` 的值，即 `$val2`）。

c) `newval`（最后一行：第二次 `eval` 调用导致对其参数再次进行重新评估，该参数为 `$val2`，因此将其替换为 `val2` 的值 `newval`）。

## 189：将位置参数设置为字符串，然后取消位置参数，再次将它们设置回原始值

答案：

```bash
new_positionals="Another string to be assigned to the positional parameters word by word"

orig_args=$@

echo $@ # 显示当前的位置参数

set -- $new_positionals

echo $@ # 显示 new_positionals 的内容

set --

echo $@ # 显示空行

set -- $orig_args

echo $@ # 显示原始参数
```

## 190：`rm` 命令只是将文件（索引节点）从数据块中取消链接。要彻底删除一个文件，需要覆盖该文件占据的数据块。创建一个脚本，安全地删除作为参数传递给它的文件

答案：

```bash
for i
do
  dd if=/dev/null of="$i" bs=1024 count=`expt 1 + `stat "$i" | grep 'Size:' | awk '{print $2}'` / 1024`
done
```

## 191：假设定义了一个名为 `Array` 的数组，这个 `for` 循环是做什么？

```bash
for i in ${!Array[@]}
do
  echo ${Array[i]}
done
```

答案：

它显示 `Array` 中的所有元素。符号 `${!array[@]}` 展开为数组的所有索引。

## 192：在 `case` 结构中使用终止符 `;;&` 和 `;&` 有什么影响？

答案：

`;;&` 终止符会继续执行下一个模式测试。`;&` 终止符即使带有占位模式也会执行下一个语句，也就是说，即使值不匹配模式也会执行下一个语句，因此它的用性稍小，且应该谨慎使用。

## 193：写出以下 `case` 的输出，假设

a) `$1` 等于 `a`，且

b) `$1` 等于 `5`：

```bash
case "$1" in
  [[:print:]] ) echo "$1 is a printable character." ;;&
  [[:alnum:]] ) echo "$1 is an alpha/numeric character." ;;&
  [[:alpha:]] ) echo "$1 is an alphabetic character." ;;&
  [[:lower:]] ) echo "$1 is a lowercase alphabetic character." ;;&
  [[:digit:]] ) echo "$1 is an numeric character." ;&
  @@%%* ) echo "Dummy" ;;
esac
```

答案：

a)

```text
a is a printable character
a is an alpha/numeric character
a is an alphabetic character
a is a lowercase alphabetic character
```

b)

```text
5 is a printable character
5 is an alpha/numeric character
5 is a numeric character
Dummy
```

## 194：列举两种将数组设置为文本文件内容的方法

答案：

a)

```bash
declare -a ARRAY

# 将文件描述符 10 与标准输入链接

exec 10<&0

exec < logfile

let count=0

while read LINE
do
  ARRAY[$count]=$LINE
  ((count++))
done
```

b)

`ARRAY=( `catlogfile `)`

## 195：列出 `getopts` bash 内置命令的一个局限性

答案：

使用 `getopts` 内置命令有一些限制：

a) 不支持带有 `##` 前缀的长名称。

b) 仅支持单字符选项。

## 196：调试以下脚本片段

```bash
number=1

while [ "$number" <5 ]
do
  echo -n "$number "
  let "number += 1"
done
```

答案：

应该是：

```bash
number=1

while [ "$number" -lt 5 ]
do
  echo -n "$number "
  let "number += 1"
done
```

## 197：调试以下脚本片段

```bash
a='$val1'

val1='$val2'

val2=newval

echo $a

eval echo $a

eval eval echo $a
```

答案：

a) `$val1`（第一个 `echo`：单引号不允许任何替换）。

b) `$val2`（第二个 `echo`——`eval`：`eval` 的调用强制对其参数进行重新评估，因此参数 `$a` 被替换为 `a` 的值，即 `$val1`；然后 `$val1` 被替换为 `val1` 的值，即 `$val2`）。

c) `newval`（最后一行：第二次 `eval` 调用导致对其参数再次进行重新评估，该参数为 `$val2`，因此将其替换为 `val2` 的值 `newval`）。

## 198：将位置参数设置为字符串，然后取消位置参数，再次将它们设置回原始值

答案：

```bash
new_positionals="Another string to be assigned to the positional parameters word by word"

orig_args=$@

echo $@ # 显示当前的位置参数

set -- $new_positionals

echo $@ # 显示 new_positionals 的内容

set --

echo $@ # 显示空行

set -- $orig_args

echo $@ # 显示原始参数
```

## 199：`rm` 命令只是将文件（索引节点）从数据块中取消链接。要彻底删除一个文件，需要覆盖该文件占据的数据块。创建一个脚本，安全地删除作为参数传递给它的文件

答案：

```bash
for i
do
  dd if=/dev/null of="$i" bs=1024 count=`expt 1 + `stat "$i" | grep 'Size:' | awk '{print $2}'` / 1024`
done
```

## 200：假设定义了一个名为 `Array` 的数组，这个 `for` 循环是做什么？

```bash
for i in ${!Array[@]}
do
  echo ${Array[i]}
done
```

答案：

它显示 `Array` 中的所有元素。符号 `${!array[@]}` 展开为数组的所有索引。

## 201：在 `case` 结构中使用终止符 `;;&` 和 `;&` 有什么影响？

答案：

`;;&` 终止符继续执行下一个模式测试。`;&` 终止符即使带有占位模式也会执行下一个语句，也就是说，即使值不匹配模式也会执行下一个语句，因此它的用性稍小，且应该谨慎使用。

## 202：写出以下 `case` 的输出，假设

a) `$1` 等于 `a`，且

b) `$1` 等于 `5`：

```bash
case "$1" in
  [[:print:]] ) echo "$1 is a printable character." ;;&
  [[:alnum:]] ) echo "$1 is an alpha/numeric character." ;;&
  [[:alpha:]] ) echo "$1 is an alphabetic character." ;;&
  [[:lower:]] ) echo "$1 is a lowercase alphabetic character." ;;&
  [[:digit:]] ) echo "$1 is an numeric character." ;&
  @@%%* ) echo "Dummy" ;;
esac
```

答案：

a)

```text
a is a printable character
a is an alpha/numeric character
a is an alphabetic character
a is a lowercase alphabetic character
```

b)

```text
5 is a printable character
5 is an alpha/numeric character
5 is a numeric character
Dummy
```

## 203：列举两种将数组设置为文本文件内容的方法

答案：

a)

```bash
declare -a ARRAY

# 将文件描述符 10 与标准输入链接

exec 10<&0

exec < logfile

let count=0

while read LINE
do
  ARRAY[$count]=$LINE
  ((count++))
done
```

b)

`ARRAY=( `catlogfile `)`

## 204：列出 `getopts` bash 内置命令的一个局限性

答案：

使用 `getopts` 内置命令有一些限制：

a) 不支持带有 `##` 前缀的长名称。

b) 仅支持单字符选项。

## 205：调试以下脚本片段

```bash
number=1

while [ "$number" <5 ]
do
  echo -n "$number "
  let "number += 1"
done
```

答案：

应该是：

```bash
number=1

while [ "$number" -lt 5 ]
do
  echo -n "$number "
  let "number += 1"
done
```

## 204：解释这段代码段

```bash
coproc {
  cat datafile
  sleep 2
}

while read -u ${COPROC[0]} record
do
  echo "$record" | cut -c2-
done

kill $COPROC_PID
```




**答案：**

`coproc` 内置命令允许两个并行进程进行通信和交互。这个协进程与 `while read` 循环交互。`${COPROC[0]}` 是该协进程的文件描述符。因此，`while-read` 循环按行读取文件 `datafile`，并从输出中删除每行的第一个字符。在最后，当不再需要该协进程时，它会杀死它的 PID（`$COPROC_PID`）。

## 205：下述片段未能设置 3 个变量（`my_var1`、`my_var2`、`my_var3`）。解释原因

**答案：**

循环内部一切都是正常的。输出将是：

```bash
Inside my_while-read loop1:

p = three

q = seven

r = oneseven

coprocmy_ file descriptor1:#some descriptor
```

由于这个循环在子 shell（subshell）中运行，值不会持续。因此，三个 `echo` 命令的输出将是：

```bash
p=

q=

r=
```

协进程仍在运行，但值丢失了。

## 206：编写一个脚本识别并处理任意顺序的命令选项 `-l`（后跟一个值）和 `-m`

无效选项将导致脚本带错误终止并显示无效选项。

**答案：**

```bash
#!/bin/bash

# Usage: script [-l -m]

while getopts :l:m flag
do
    case $flag in
        l) echo "Option has $OPTAGR as its value" ;;
        m) echo "Option -m received" ;;
        *) echo "Invalid option $OPTARG" ;;
    esac
done
```

## 207：使用 Bash 下载 URL 的示例

**答案：**

```bash
exec 3>/dev1/my_tcp/abc.cn/80

echo -e "GET / HTTP/1.0\n" >&3

cat<&3
```

通过 Bash 打开 `/dev1/my_tcp_$host/$port` TCP 连接。因此可以发出 GET 请求。

## 208：编写代码返回数组的随机索引（整数索引），并选择该索引的元素

**答案：**

```bash
Array=(`ls -a`) # 初始化数组

R_INDEX=$(($RANDOM%#Array[@]})) # ${Array[@]} 返回数组的长度

R_ELEM=${Array[$R_INDEX]} # 选择随机元素

echo "Randomly selected element is $R_ELEM with index $R_INDEX"
```

## 209：编写片段返回关联数组的随机字符串索引以及该索引对应的元素

**答案：**

```bash
declare -A ass_array

ass_array[John]="john.k@domain.com"

ass_array[Chris]="chris.sm@hotmail.com"

ass_array[Angela]="angela.st@domain.com"

indices=(${!ass_array[*]})

r_index_pos=$(($RANDOM%#indices[@]}))

r_element=${ass_array[${indices[$r_index_pos]}]}

echo "Randomly selected element is $r_element"
```

## 210：列出列表的优势

**答案：**

列表的优势是可以有效地替换复杂的 `if/then` 和 `case` 结构。

## 基础知识

### 211：UNIX 中使用了哪些类型的文件？

**答案：**

UNIX 中使用的文件类型有：

- **普通文件**：包含文本和数据。
- **特殊文件**：允许别名或快捷方式访问。
- **目录**：包含普通文件和特殊文件。

### 212：哪种类型的文件以 `..` 开头？

**答案：**

隐藏文件通常以 `.` 开头。使用 `ls` 命令时不会显示这些文件。

### 213：如何显示以特定字母 `hel` 开头的文件？

**答案：**

我们可以使用 `*` 显示以特定字母开头的文件。它是 `ls` 使用的元字符。

**示例：**

```bash
ls hel*.txt
```

显示以 `hel` 开头并以 `txt` 结尾的文件。

### 214：哪些字符被称为元字符？

**答案：**

以下字符是元字符：

- `*`
- `?`
- `$`

### 215：用户与系统是如何交互的？

**答案：**

用户与系统之间的交互通过：

- 使用系统调用。
- 使用接口。
- 使用 `shell`。

### 216：`$` 的作用是什么？

**答案：**

`$` 是提示符，用于输入内容。

**示例：**

```bash
$
```

### 217：`#` 的作用是什么？

**答案：**

`#` 用于注释行。它被用于环境。

**示例：**

```bash
#!/bin/bash
```

### 218：如何了解命令的功能？

**答案：**

可以使用 `man` 了解命令的功能。它提供了名称说明。

**示例：**

```bash
man date
```

## 命令

### 219：解释 `getty` 和 `agetty` 命令

**答案：**

`getty` 是 TTY 的缩写，用于虚拟终端。在 Linux 中，使用 `agetty` 命令代替它。

### 220：解释 `strace` 和 `ltrace`

**答案：**

`strace` 允许你跟踪系统调用。这有助于调试程序。`ltrace` 允许跟踪库。

### 221：解释 `nice` 和 `pidof` 命令

**答案：**

`nice` 命令更改进程的优先级。它的变体是 `renice` 和 `snice`。`pidof` 命令用于获取运行任务的标识。它通常用于杀死该进程。

### 222：解释 `lockfile`

**答案：**

`lockfile` 是控制设备、文件或资源权限的文件。它是一个工具，让你创建一个包含其他文件锁的文件。通常，锁会在 `/var/lock` 目录中检查。然而，当使用 `lockfile` 时，会在该文件中检查。`lockfile` 也用于阻止浏览器访问你的邮件文件夹。

### 223：解释 `env`

**答案：**

`env` 命令用于在运行特定脚本时更改少数环境变量，而无需更改系统环境。你可以在 shebang 中设置 `env`。例如，你可以使用 `env` 为特定脚本将语言设置为 Perl。

### 224：哪个命令用于列出目录中的隐藏文件？

**答案：**

- `ls`：列出目录中的所有文件。
- `ls -a`：列出目录中的隐藏文件。

### 225：如何将输出重定向到文件？

**答案：**

我们可以使用 `>` 将输出重定向到文件。

**示例：**

```bash
ls > myfile1
```

`ls` 显示文件，并将这些内容通过 `>` 重定向到文件 `myfile1`。

### 226：如何在文件中搜索模式？

**答案：**

我们可以使用 `grep` 命令在文件中搜索模式。

**示例：**

```bash
grep my_pattern1 myfilename1
```

### 227：如何将命令的输出追加到文件中？

**答案：**

我们可以使用 `>>` 符号将命令的输出追加到文件中。

**示例：**

```bash
ls >> myfile2
```

- `ls` 命令的输出将被追加到 `myfile2` 中。

### 228：UNIX shell 中 `2>` 的作用是什么？

**答案：**

它将程序的错误输出重定向到指定的文件。

**示例：**

```bash
myprogram 2> myfileerr2
```

- 将 `myprogram2` 的错误重定向到文件 `myfileerr2`。

### 229：你将如何获取上一个命令的输出作为下一个命令的输入？

**答案：**

我们可以使用管道符 `pipeline(|)` 来获取上一个命令的输出作为下一个命令的输入。

**示例：**

```bash
ls –s | grep mysearch1
```

`ls` 输出文件名列表，匹配 `mysearch1` 的名称将输出给用户。

### 230：使用哪些命令来打印文件的第 n 行？

**答案：**

使用 `sed` 或 `head` 命令可以打印文件的第 n 行。

**语法：**

```bash
sed –n ‘<line number> p’ my_file.txt

head –<n> my_file1.txt | tail -1
```

**示例：**

打印文件的第 7 行：

```bash
sed –n ‘7 p’ my_file1.txt

head –7 my_file1.txt | tail -1
```

### 231：你将如何在文件夹中搜索文件？

**答案：**

我们可以使用 `grep` 命令在文件夹中搜索文件。

**示例：**

```bash
grepki my_folder1/folder2
```

- `ki`：文件名。
- `folder1` 和 `folder2`：文件的路径。
- 若忽略大小写，使用 `i`。

```bash
grep -i “ki” my_folder1/folder2
```

### 232：`grep` 命令中 `-r` 和 `-v` 的作用是什么？

**答案：**

`grep` 命令中 `-r` 和 `-v` 的作用是：

- `-r`：在所有文件中递归搜索该模式。

  **示例：**

  ```bash
  grep –r “name” /myfold1/myfile1
  ```

- `-v`：显示不包含给定单词的行。

  **示例：**

  ```bash
  grep –v “name” /myfold1/myfile1
  ```

### 233：你将如何找到文件的目录？

**答案：**

我们可以使用 `ff` 查找文件的目录。它返回文件所在的目录。也可以给出文件名的起始字母。

**示例：**

```bash
ff myfile2
```

### 234：你将如何杀死一个进程？

**答案：**

我们可以使用 `kill` 命令杀死进程。杀死进程需要知道该进程的 ID。可以通过 `ps` 命令获取该 ID。

**示例：**

```bash
kill 22230
```

### 235：创建文件的方法有哪些？

**答案：**

可以通过以下方式创建文件：

- 使用 `vi` 命令。可以使用 `cat` 命令对文件进行操作。

  **示例：**

  ```bash
  vi my_filename2
  ```

- 使用 `emacs`。它是一种允许创建和编辑文件的编辑器。

  **示例：**

  ```bash
  emacs my_filename2
  ```

### 236：获取 `cpu` 型号名称的方法有哪些？

**答案：**

获取 `cpu` 型号名称的方法有：

- 使用 `grep`。`grep –i ‘model’ /proc/cpuinfo` 返回型号名称。
- 使用管道配合 `grep`。`cat /proc/cpuinfo | grep –i ‘model’` 返回 `cpu` 的型号名称。

### 237：你将如何获取文件的单词数？

**答案：**

我们可以使用 `wc` 命令获取文件的单词数。它返回总行数、单词数、字节数和文件名。

**示例：**

```bash
wc myfile_name
```

### 238：什么是位置参数（positional parameters）？

**答案：**

位置参数是从命令行传递给脚本的参数。通常用位置数字表示，如 `$0`、`$1`、`$2` 等。在 `$9` 之后，位置参数需要使用括号 `${10}`、`${11}` 等访问。`*$` 和 `$@` 表示所有参数。

### 239：解释 `shift` 命令

**答案：**

`shift` 命令将位置参数向左移动一位。因此，通过 `shift` 命令，`$3` 将变为 `$2`，`$2` 将变为 `$1`，以此类推。对于所有两位或更多数字的位置，必须在括号中使用它们。

### 240：`=` 和 `-eq` 的功能相似吗？

**答案：**

`=` 通常用作赋值运算符，用于给变量赋值。`==` 用于比较。`-eq` 命令也用于比较。区别在于 `==` 执行的是词法或字符串比较，而 `-eq` 执行的是数值比较。

### 241：你将如何初始化并打印？

**答案：**

`=` 通常用作赋值运算符，用于给变量赋值。`==` 用于比较。`-eq` 命令也用于比较。区别在于 `==` 执行的是词法或字符串比较，而 `-eq` 执行的是数值比较。

> 注：此处原文内容似乎与 240 重复，已按原文内容保留。

### 242：你将如何获取上一个命令的输出作为下一个命令的输入？

**答案：**

我们可以使用管道来获取上一个命令的输出作为下一个命令的输入。

**示例：**

```bash
cat /proc/cpuinfo | grep -i ‘model’
```

> 注：此处原文内容与 229 重复，已按原文内容保留。

### 243：你将如何杀死一个进程？

**答案：**

我们可以使用 `kill` 命令杀死进程。杀死进程需要知道该进程的 ID。可以通过 `ps` 命令获取该 ID。

> 注：此处原文内容与 234 重复，已按原文内容保留。

### 244：创建文件的方法有哪些？

**答案：**

可以通过以下方式创建文件：

- 使用 `vi` 命令。
- 使用 `emacs`。

> 注：此处原文内容与 235 重复，已按原文内容保留。

### 245：获取 `cpu` 型号名称的方法有哪些？

**答案：**

- 使用 `grep`。
- 使用管道配合 `grep`。

> 注：此处原文内容与 236 重复，已按原文内容保留。

### 246：你将如何获取文件的单词数？

**答案：**

我们可以使用 `wc` 命令获取文件的单词数。

> 注：此处原文内容与 237 重复，已按原文内容保留。

### 247：什么是位置参数？

**答案：**

位置参数是从命令行传递给脚本的参数。

> 注：此处原文内容与 238 重复，已按原文内容保留。

### 248：解释 `shift` 命令

**答案：**

`shift` 命令将位置参数向左移动一位。

> 注：此处原文内容与 239 重复，已按原文内容保留。

### 249：`=` 和 `-eq` 的功能相似吗？

**答案：**

`=` 通常用作赋值运算符。

> 注：此处原文内容与 240 重复，已按原文内容保留。

### 250：你将如何初始化并打印？

**答案：**

`=` 通常用作赋值运算符。

> 注：此处原文内容与 241 重复，已按原文内容保留。



`grep -i "ki" my_folder1/folder2`

## 227. 如何将命令的输出追加到文件？

我们可以使用 `>>` 符号将命令的输出追加到文件中。

示例：

```bash
ls>> myfile2
```

- `ls` 命令的输出将被追加到 `myfile2` 中。

## 228. UNIX shell 中 `2>` 的作用是什么？

它将程序的错误输出重定向到指定的文件。

示例：

```bash
myprogram 2> myfileerr2
```

- 将 `myprogram2` 的错误重定向到文件 `myfileerr2`。

## 229. 你将如何获取上一个命令的输出作为下一个命令的输入？

我们可以使用管道符 `pipeline(|)` 来获取上一个命令的输出作为下一个命令的输入。

示例：

```bash
ls –s | grep mysearch1
```

`ls` 输出文件名列表，匹配 `mysearch1` 的名称将输出给用户。

## 230. 使用哪些命令来打印文件的第 n 行？

使用 `sed` 或 `head` 命令可以打印文件的第 n 行。

语法：

```bash
sed –n ‘<line number> p’ my_file.txt
head –<n> my_file1.txt | tail -1
```

示例：打印文件的第 7 行：

```bash
sed –n ‘7 p’ my_file1.txt
head –7 my_file1.txt | tail -1
```

## 231. 你将如何如何在文件夹中搜索文件？

我们可以使用 `grep` 命令在文件夹中搜索文件。

示例：

```bash
grepki my_folder1/folder2
```

- `ki` - 文件名
- `folder1` 和 `folder2` - 文件的路径
- 若忽略大小写，使用 `i`

```bash
grep -i “ki” my_folder1/folder2
```

## 232. grep 命令中 `-r` 和 `-v` 的作用是什么？

`grep` 命令中 `-r` 和 `-v` 的作用是：

a) `-r` 它在所有文件中递归搜索该模式。
示例：

```bash
grep –r “name” /myfold1/myfile1
```

b) `-v` – 显示不包含给定单词的行。
示例：

```bash
grep –v “name” /myfold1/myfile1
```

## 233. 你将如何找到文件的目录？

我们可以使用 `ff` 查找文件的目录。它返回文件所在的目录。也可以给出文件名的起始字母。

示例：

```bash
ff myfile2
```

## 234. 你将如何杀死一个进程？

我们可以使用 `kill` 命令杀死进程。杀死进程需要知道该进程的 ID。可以通过 `ps` 命令获取该 ID。

示例：

```bash
kill 22230
```

## 235. 创建文件的方法有哪些？

可以通过以下方式创建文件：

a) 使用 `vi` 命令。可以使用 `cat` 命令对文件进行编辑。
示例：

```bash
vi my_filename2
```

b) 使用 `emacs`。它是一种允许创建和编辑文件的编辑器。
示例：

```bash
emacs my_filename2
```

## 236. 获取 `cpu` 型号名称的方法有哪些？

获取 `cpu` 型号名称的方法有：

a) 使用 `grep`。`grep –i ‘model’ /proc/cpuinfo` 返回型号名称。
b) 使用管道配合 `grep`。`cat /proc/cpuinfo | grep –i ‘model’` 返回 `cpu` 的型号名称。

## 237. 你将如何获取文件的单词数？

我们可以使用 `wc` 命令获取文件的单词数。它返回总行数、单词数、字节数和文件名。
示例：

```bash
wc myfile_name
```

## 238. 什么是位置参数（positional parameters）？

位置参数是从命令行传递给脚本的参数。通常用位置数字表示，如 `$0`、`$1`、`$2` 等。在 `$9` 之后，位置参数需要使用括号 `${10}`、`${11}` 等访问。`*$` 和 `$@` 表示所有参数。

## 239. 解释 `shift` 命令。

`shift` 命令将位置参数向左移动一位。因此，通过 `shift` 命令，`$3` 将变为 `$2`，`$2` 将变为 `$1`，以此此类推。对于所有两位或更多数字的位置，必须在括号中使用它们。

## 240. `=` 和 `-eq` 的功能相似吗？

`=` 通常用作赋值运算符，用于给变量赋值。`==` 用于比较。`-eq` 命令也用于比较。区别在于 `==` 执行的是词法或字符串比较，而 `-eq` 执行的是数值比较。

## 241. 你将如何初始化并打印？

`=` 通常用作赋值运算符，用于给变量赋值。`==` 用于比较。`-eq` 命令也用于比较。区别在于 `==` 执行的是词法或字符串比较，而 `-eq` 执行的是数值比较。

## 242. 你将如何获取上一个命令的输出作为下一个命令的输入？

我们可以使用管道来获取上一个命令的输出作为下一个命令的输入。
示例：

```bash
cat /proc/cpuinfo | grep -i ‘model’
```

## 243. 你将如何杀死一个进程？

我们可以使用 `kill` 命令杀死进程。杀死进程需要知道该进程的 ID。可以通过 `ps` 命令获取该 ID。

## 244. 创建文件的方法有哪些？

可以通过以下方式创建文件：
a) 使用 `vi` 命令。
b) 使用 `emacs`。

## 245. 获取 `cpu` 型号名称的方法有哪些？

a) 使用 `grep`。
b) 使用管道配合 `grep`。

## 246. 你将如何获取文件的单词数？

我们可以使用 `wc` 命令获取文件的单词数。

## 247. 什么是位置参数？

位置参数是从命令行传递给脚本的参数。

## 248. 解释 `shift` 命令。

`shift` 命令将位置参数向左移动一位。

## 249. `=` 和 `-eq` 的功能相似吗？

`=` 通常用作赋值运算符。

## 250. 你将如何初始化并打印？

`=` 通常用作赋值运算符。

## 256. 描述 `matchbeep('')` 的用途。

a) 当设置为 `never` 时，在完成时永远不会蜂鸣

b) 当设置为 `nomatch` 时，当未找到匹配项时会蜂鸣

c) 当设置为 `ambiguous` 时，当存在多个匹配项时会蜂鸣

## 257. 你将如何列出作业？

a) 使用 `listjobs('')`。当一个作业被挂起时，列出所有作业

b) 当设置为 `long` 时，将以 `long` 格式列出

## 258. 描述 `correct('')` 的用途。

a) 当设置为 `cmd` 时，它提供命令的自动拼写纠正

b) 当设置为 `complete` 时，它提供命令的自动补全

c) 当设置为 `all` 时，它提供整行的自动纠正

## 259. `echo_style()` 的功能是什么？

a) 当设置为 `bsd` 时，如果第一个参数是 `-n`，则不显示换行

b) 当设置为 `sysv` 时，它将反斜线解释为转义序列字符

c) 当设置为 `bsd` 时，它同时接受 `-n` 和转义序列

## 260. 你将如何设置编辑器的模式？

我们可以使用 `inputmode('')` 设置编辑器模式。在每行的开头设置为 `overwrite` 或 `insert` 模式时，会将编辑器设置为该模式。

## 261. 你将如何避免内存中的重复条目？

我们可以使用 `killdup('')` 避免内存中的重复条目。当设置为 `all` 时，唯一的字符串会被输入剪切环（kill ring）。当设置为 `prev` 时，与环中已有项目相同的条目将不允许进入剪切环。

---

## 运算符和 Shell 替换

## 262. shell 中提供了哪些类型的替换？

当脚本中使用某些特殊字符时，它们会被替换为相应的值。例如，`\n` 被替换为换行，`\\` 被替换为 `\`，`\b` 被替换为退格符。shell 中还有更多可用的替换。命令替换通过使用反引号将命令赋值给变量来实现，并使用变量代替命令。变量替换允许程序员根据变量的状态对变量的值进行操作。

## 263. shell 中的文件测试运算符有哪些？

shell 中的文件测试运算符用于检查文件的特定属性。以下是一些：

a) `-b <filename>` 如果文件是块设备文件，则返回 TRUE

b) `-c <filename>` 如果文件是字符设备文件，则返回 TRUE

c) `-d <filename>` 如果是目录，则返回 TRUE

d) `-f <filename>` 如果是普通文件，则返回 TRUE

e) `-r <filename>` 如果具有可读权限，则返回 TRUE

f) `-w <filename>` 如果具有可写权限，则返回 TRUE

g) `-x <filename>` 如果具有可执行权限，则返回 TRUE

h) `-e<filename>` 如果作为文件或文件夹存在，则返回 TRUE

## 264. 你将如何解决 UNIX 中的算术表达式？

a) 使用带有数值的 `expr`

示例：

```bash
echo 'expr 3 + 9'
```

b) 使用带有变量的 `expr`

示例：

```bash
echo 'expr $p + $q '
```

## 265. 你将如何使用布尔运算符？

a) `逻辑与` 即 `-a`。如果两个条件都满足，则返回 true；否则返回 false

示例：

```bash
[$p –lt 8 –a $q –lt 13]
```

b) `逻辑或` 即 `-o`。如果满足任一条件，则返回 true

示例：

```bash
[$p –lt 8 –o $q –lt 13]
```

## 266. 你将如何检查字符串的长度？

a) `-z`。如果操作数长度为零，返回 true

示例：

```bash
[-z $my_strvar1]
```

b) `-n`。如果操作数长度为空，返回 true

## 267. `-u` 和 `-g` 的用途是什么？

a) `-u`: 如果文件启用了 `SGID`（设置组 ID），则返回 true，否则返回 false

示例：

```bash
[-u $my_file3]
```

b) `-g`: 如果文件启用了 `SUID`（设置用户 ID），则返回 true，否则返回 false

示例：

```bash
[-g $my_file3]
```

## 268. 你将如何检查文件的访问权限？

检查访问权限的方法有：

a) 使用 `-r`。如果文件可读，返回 true，否则返回 false

示例：

```bash
-r $my_filename1 //返回 true 或 false
```

b) 使用 `-w`。如果文件可写，返回 true，否则返回 false

示例：

```bash
-w $my_filename1 //返回 true 或 false
```

## 269. 你将如何如何在 echo 命令中使用转义序列？

我们可以使用 `-e` 在 echo 命令中使用转义序列。在语句中使用 `-e` 来替换转义序列。要禁用转义序列的替换，则使用 `-E`。

示例：

```bash
my_var2=32
echo –e “value of myvar2 is $my_var2 \n”
```

## 270. 什么是命令替换？

将命令输出赋值给变量称为命令替换。

## 271. 你将如何使用 `:+` 替换变量名？

```bash
my_var2=32
echo –e “value of myvar2 is $my_var2 \n”
```

## 272. 你将如何使用 `:-` 替换变量名？

```bash
my_var2=32
echo –e “value of myvar2 is $my_var2 \n”
```

## 273. 你将如何使用 `:=` 为空变量设置值？

```bash
my_var2=32
echo –e “value of myvar2 is $my_var2 \n”
```

## 274. 什么是 `Here` 文？

`Here` 文由用户提供交互式程序。

示例：

```bash
cat<<Helllo
aaaaaaaaaa
bbbbbbbbbb
Helllo
```



### 275：你将如何丢弃命令的输出？

答案：

通过将输出重定向到文件`dev/null`来丢弃命令输出。

示例：

```bash
date > special_name
```

### 276：你将如何删除函数？

答案：

我们可以使用`.f`删除函数。

示例：

```bash
unset .f my_function2
```



尽量将此回答保持在专业领域，但如果你在职业经历之外有某些令人印象深刻的创意类背景，不要害怕将其包含在回答中。关于创造力的最佳回答将与解决问题的能力、目标设定，以及在职场中处理项目或完成销售的创新方法有关。然而，办公室之外的爱好也是极好的（只要它们不会占用你的工作时间或精神空间）。

## 5: 你如何处理负能量的同事？

**答案：**
每个人都必须与负能量的同事打交道——处理这一问题的唯一最佳方法是保持积极。你可以尝试与该同事建立关系或以某种方式与他们取得联系，但即使你的努力遭到了冷遇，你也必须保持积极的态度。最重要的是，要强调你绝不允许同事的负面情绪影响到你自己的工作或效率。

## 6: 如果你目击同事在浏览网页、看书等浪费公司时间，你会怎么做？

**答案：**
面试官希望看到你意识到员工浪费公司时间是有害的，并且你不会轻视这一点。请解释你将如何遵守公司政策，无论这包括亲自与同事交谈、直接向主管汇报该行为，还是与人力资源部门的人员沟通。

## 7: 你如何处理自己与其他员工之间的竞争？

**答案：**
健康的竞争可以是一件好事，最好专注于此事的积极方面。不要提到你与其他同事之间的冲突，相反，要关注为了跟上他人优秀工作水平的动力，以及同事如何成为一个强大的支持网络，帮助你推向新的成功。

## 8: 在什么情况下与同事社交是合适的？

**答案：**
这个问题有两个极端的答案（一直社交，或从不社交），在大多数情况下，你的面试官希望看到你处于两者之间的中间地带。与同事建立稳固的关系是重要的，但绝不能以牺牲完成工作为代价。理想情况下，关系的建立可以通过团队合作练习、特殊项目以及在休息室来进行。

## 9: 请告诉我你上一份工作发生重大变化时的经历，以及你是如何处理的。

**答案：**
提供该情况的背景，包括旧系统、变化的内容、如何实施以及变化的结果，并包括你对每一步的感受。确保你对旧系统的最初想法是中性的，并且你的兴奋程度随着新变化的每一步而增加，因为面试官会看到你的适应能力并感到高兴。

## 10: 在委派任务时，你如何选择将哪些任务分配给哪些团队成员？

**答案：**
面试官希望通过这个问题获得对你思维过程的洞察，因此务必为你的选择提供详尽的理由。解释你根据每个人的个人优势来委派任务，或者你查看每个人目前正在参与多少个其他项目，以创造尽可能完美的匹配。

## 11: 请告诉我你曾不得不向同事或主管捍卫你坚信不疑的事物的经历。

**答案：**
虽然向面试官解释冲突情况可能很困难，但这是一个展示你的热情、信念以及对信念的奉献的绝佳机会。不仅要向面试官解释情况，还要详细阐述为什么维护该问题对你来说如此重要，以及你的同事或主管之后是如何回应你的——他们是变得更有尊重了吗？还是更不接受？还是更开放了？还是抱歉了？

## 12: 请告诉我你曾帮助他人完成工作的经历，即使那不是“你的工作”。

**答案：**
尽管当你被要求为别人收拾烂摊子时可能会感到沮丧，但保持乐于助人的积极态度是重要的。面试官将寻找你是否是一个团队合作者，通过帮助他人完成一项他们无法独立完成的任务，你展示了自己帮助团队成功的意愿，也展示了自己的胜任。

## 13: 团队工作的挑战是什么？你是如何处理这些的？

**答案：**
团队工作有很多显性的挑战，例如处理不同的观点、应对个人日程或迁就难以相处的员工。最好专注于一个挑战，例如个人团队成员错过截止日期或未能履行承诺，提供一个明确解决该问题的解决方案。例如，你可以为团队组织每周状态会议来讨论进度，或者分配较短的截止日期，以确保长期期限按计划进行。

## 14: 你看重职场中的多样性吗？

**答案：**
职场中的多样性很重要，为了营造一个包容、平等且充满不同观点和背景的环境。一定要表现出对这些问题的意识，并强调学习他人经验的重要性。

## 15: 如果遇到同事不接受他人的多样性的情况，你会如何处理？

**答案：**
解释遵守公司关于多样性的政策是重要的，你会与相关的主管或管理团队进行沟通。在合适的情况下，与涉事的同事谈谈不同观点的益处可能是最好的——如果你可以自己处理这种情况，最好不要将可以解决的问题提交给管理层。

## 16: 团队工作带来的回报更多，还是独立完成任务带来的回报更多？

**答案：**
最好表现出这两个方面的平衡——你的雇主希望看到你能够独立工作，并且能够高效、高质量地完成任务。然而，对雇主来说，看到你能成为一名团队合作者同样重要，并且理解多种观点和努力能为项目带来的价值。

## 17: 请告诉我你一次没有按时完成工作的经历。

**答案：**
理想情况下这种情况没有发生过——但如果确实发生了，请确保使用一个较小的例子来说明情况，强调那是多久以前的事，并确保你已尽力确保截止日的达成。此外，务必包括你在更好地管理时间或任务优先级方面学到了什么，以满足未来的截止日期。

## 18: 你在工作时如何消除干扰？

**答案：**
随着技术的进步和沟通的便利，新的干扰每天都会产生。面试官将希望看到你仍然专注于工作，并且你的生产力没有受到影响，请举例说明你采用了哪种常规方法来保持专注。

## 19: 请告诉我你曾在一个需要完成每周或每月指标的职位工作的经历。你的成功率如何？

**答案：**
你的数据将说明一切，你必须诚实地回答这个问题。如果你经常能达成指标，请务必以自信的方式强调这一点，不要害羞于指出你在该方面的优势。如果你的统计数据并不理想，尝试指出在工作结束前指标有所增长的趋势，并反思未来可以改进的方法。

## 20: 请告诉我你一次满足了严苛截止日的经历，以及你是如何完成它的。

**答案：**
解释你如何对任务进行排序，或者如何将任务的部分分配给其他团队成员，以应对紧迫的截止日期。说明截止日期之所以紧迫可能会有帮助——确保明确这并不是由于你个人的拖延导致的。最后，解释你如何成功在截止日期前完成，以及最终付出了什么努力。

## 21: 当你手上有多个项目时，你如何保持条理清晰？

**答案：**
面试官将希望看到你能够管理时间并良好工作——能够同时处理多个项目，并对每个项目都给予应有的关注，是一个员工能力和效率的极佳体现。描述一个典型的目标设定过程，并向面试官解释这些步骤，以便他们看到你是如何管理时间的。

## 22: 在工作期间，你有多少时间是处于“自动驾驶”状态？

**答案：**
虽然雇主可能想看看你的工作效率如何（例如，你做得足够好以至于不需要思考），但在几乎所有情况下，雇主希望看到你在不断思考、分析和处理工作中的事情。即使事情进展顺利，通常也有机会提高效率或生产力。强调并传达“自动驾驶”状态不利于成功的。

## 23: 你如何处理截止日期？

**答案：**
处理截止日期最重要的部分是对任务进行排序并设定完成目标，以及授权不必要的工作。向面试官描述一个通用场景，展示你的组织能力，最重要的是保持冷静。

## 24: 请告诉我你的解决问题过程。

**答案：**
你的解决问题过程应该包括概述问题、提出解决办法以及制定一个导致结果的行动计划。保持你的回答简洁且有组织，展示你在压力下依然保持冷静。

## 25: 工作中哪些事情会让你感到压力？

**答案：**
最好远离负面影响，保持这个回答简洁简单。在回答如何应对压力时，专注于你通常用来应对压力的解决方案，例如每周会议或截止日期。

## 26: 当你感到压力时，你如何解决？

**答案：**
这是一个陷阱题——面试官想听到你不会让负面情绪影响生产力。至于如何解决压力，最好的方法是深呼吸，让自己回到任务中。

## 27: 你能多任务处理吗？

**答案：**
有些人可以，有些人则不行。多任务处理最重要的部分是清楚需要做什么，以及每个任务属于什么优先级。解释你如何评估任务以及如何管理时间以确保所有任务高效完成。

## 28: 你每周工作多少小时？

**答案：**
很多人被这个问题误导，认为回答的时间越多越好——然而这可能会导致雇主怀疑为什么要工作那么长时间来完成工作。给出一个完成工作所需的合理小时估计，并解释你在需要时愿意额外工作。

## 29: 你每天检查几次邮件？

**答案：**
虽然雇主希望看到你紧跟现代技术，但每天检查邮件的次数较低也是重要的——也许每天两三次（取决于具体领域）。检查邮件在工作中往往是一个很大的干扰项，虽然保持连接很重要，但邮件可以在早上和下午统一处理。

## 30: 你如何做决策？

**答案：**
这是一个极好的机会，让你用果断、自信和组织能力让面试官印象深刻。确保你概述一个决策过程，以及权衡选择和信任直觉的重要性。如果你能技巧且轻松地回答这个问题，面试官将信任你的能力。

## 31: 对你来说最困难的决策是什么？

**答案：**
解释你与决策的关系，以及你在做选择时所采取的通用流程概述。如果有一种你经常挣扎的特定类型决策（例如涉及他人的），确保解释为什么这种决策对你来说很难，以及你目前如何致力于提高技能。

## 32: 在做艰难决策时，你如何收集信息？

**答案：**
如果你在做一个艰难的选择，最好尽可能从多个来源收集信息。向面试官描述你从不同领域的人那里获取信息的过程，首先是你领域的专家建议、同事或其他客户的反馈，以及通过分析你过去的经验。

## 33: 请告诉我一个结果不理想的决策。

**答案：**
诚实和透明是面试官会欣赏的价值观——概述你做出的选择、为什么这么做、那个错误决策的结果——最后（也是最重要的！）你从这次决策中学到了什么。给面试官一个理由，让他们相信你不会再次做出那个决定。

## 34: 你能够快速做出决策吗？

**答案：**
你可能能够快速决策，但要确保也沟通做出明智、彻底决策的技能。讨论快速决策的重要性以及如何做到，以及每个决策首先要有充分信息的必要性。

## 35: 公司广告最好的方式是什么？

**答案：**
如果你申请的是营销以外的任何职业职位，这个问题可能是为了展示你的批判性思维以及为你的答案提供反思支持。因此，你选择的具体方法并不如你选择它的理由重要。例如，口碑广告很重要，因为客户会天生信任信息源；而社交媒体广告很重要，因为它可以快速且廉价地接触新客户。

## 36: 获得新客户还是留住老客户更好？

**答案：**
在几乎所有情况下，留住老客户更好，重要的是你能够清晰地说明原因。首先，获取新客户的成本通常比留住老客户更高，而且新客户更容易转向其他公司。此外，留住老客户是为公司提供稳定骨干的好方法，也可以通过他们向朋友推荐来获得新客户。

## 37: 如何从竞争对手手中赢得客户？

关于如何从竞争对手手中赢得客户的最佳方法有很多种流派，除非你确定面试官遵循某种特定的思想或做法，否则最好对这个问题保持宽泛化。不要使用绝对化的语言，而是要关注一两个策略的益处，并清晰地、批判性地展示这些方法在实际应用中如何取得成功。

## 38：你对公司监控互联网使用情况怎么看？

**回答：**
通常情况下，大多数公司会对员工的互联网使用情况进行某种程度的监控——而面试并不是反抗这种做法的好时机。相反，应该关注积极的一方面，例如这种做法可以提高某些容易迷失在丰富信息世界中的员工的效率。

## 39：你对我们公司的第一印象是什么？

**回答：**
显然，这应该是一个积极的回答！从公司的愿景或目标中挑选出几个你特别认同的、或与你的经验相关的关键部分，并讨论为什么你认为这些使命如此重要。

## 40：谈谈你对商业的个人哲学。

**回答：**
你的个人商业哲学应该是经过深思熟虑的，并与公司的使命和目标保持一致。专注于积极的方面，例如它能提供的服务以及人们在商业中汲取的教训，并对你的哲学源自何处提供见解。

## 41：在商业模式中，最重要的是什么：销售、客户服务、营销、管理等？

**回答：**
对于许多职位，根据你所工作的领域类型来定制这个答案可能是一个不错的策略，并解释为什么业务的某个方面是关键的。然而，通过解释每个方面对整体功能都是不可或缺的，你可以向面试官展示出更强的商业头脑，并可能在他们脑海中脱颖而出，作为一个非常有见地的候选人。

## 42：你如何跟进领域的新闻和新兴趋势？

**回答：**
面试官想看到你对目前领域内发生的事情有所了解。大学毕业后不要停止学习是非常重要的，最成功的候选人已经建立了一套经常查阅的资源清单，以便他们能够保持敏锐并参与到发展趋势中。

## 43：你遵守公司关于社交媒体的政策会有问题吗？

**回答：**
职场中的社交媒体问题已成为日益严重的问题，许多公司现在都制定了社交媒体的使用政策。面试官希望确信你不会在遵守公司标准上有问题，并且在办公室和在线上都能保持一致、专业的形象。

## 44：谈谈今天 X 行业面临的最大问题之一。

**回答：**
如果你从事自己的职业领域并花时间自己研究趋势和新发展，你应该能够展示出对行业中正在出现的问题和潜在解决方案的认知。在参加面试之前研究一些最新新闻，并准备好充分讨论时事新闻。

## 45：你认为在我们的公司成功需要什么？

**回答：**
在面试之前对公司进行研究。了解公司的使命和主要目标，以及公司的一些大人物，并记住他们是如何获得成功的。将你的回答集中在你可以实现的特定目标上，以帮助公司实现其目标。

## 46：你在这个职业领域工作中最喜欢的一个部分是什么？

**回答：**
这个问题提供了一个讨论你工作中喜欢的某些方面的机会，并突出为什么你是该特定职位的绝佳候选人。选择你喜欢的、与你被录用后可能要做的内容相关的工作元素。记住对你在工作中可能获得的机会保持热情和兴奋。

## 47：你认为未来 10 年你的职业会发生什么变化？

**回答：**
如果你关注目前职业的动态，并努力跟上你领域的新趋势，你应该能够为面试官提供几个关于你的职业或领域可能发展向何方的预判。这种洞察力和意识水平显示了对雇主来说重要的奉献和兴趣。

## 48：你在职位中寻找三个最重要的事情是什么？

**回答：**
你对职位的要求的前三件事应该与雇主对员工要求的前三件事相似，这样就能明显看出你与这份工作非常匹配。例如，雇主想要一个优秀且具有实践经验的候选人——而你想要一个可以让你充分发挥教育和技能的职位。雇主想要一个愿意接受新挑战并开发新系统以增加销售或生产力的候选人——而你想要一个能推动你并提供发展、创造和领导新计划机会的职位。雇主想要一个能够成长并留在公司很长时间的候选人——而你想要一个提供稳定性并相信建立强大团队的职位。提前研究雇主在寻找什么，并将你的目标与他们的目标匹配。

## 49：你如何评估你想要加入的公司？

**回答：**
虽然你可能觉得在面试中提出自己的要求会不舒服，但雇主希望看到你对所申请的公司进行批判性思考，就像他们也在批判性地审视你一样。不要害怕说明你对公司的需求（但要尽量确保它们与公司良好匹配——最好在申请之前），并在你的回答中表现出自信和果断。面试官想知道你是一个知道自己想要什么以及如何得到它的人。

## 50：你接受 __________ 的薪资工作吗？

**回答：**
如果这个问题的答案是否定的，那么在第一次面试中可能是一个决定性因素，因为你可能没有很大的还价空间。你可以尝试通过强调你拥有的特定经验以及这些经验如何让你胜任更高职位来增加一些筹码，但要注意在流程的这一阶段处理这一点非常困难。为了避免这种情况，请在申请之前了解行业标准，如果可能的话还有公司标准。

## 51：你为什么选择上一份工作？

**回答：**
通过了解是什么导致你选择了上一份工作，面试官能够感受到激励你的事物的类型。保持这些内容以专业为导向，并对职业生涯早期阶段保持热情，以及你对开始在该领域感到多么兴奋。

## 52：你离开上一份工作有多长时间了？为什么？

**回答：**
务必对所有的就业空窗期准备好解释，并确保这是一个专业的理由。不要提到你在寻找工作时可能遇到的困难，而要关注积极的事情，例如追求业外兴趣或者回到学校接受额外的教育。

## 53：你还在寻找哪些其他类型的工作？

**回答：**
这个问题的答案可以向面试官展示你正处于市场上且很受欢迎。提到你申请过或查看过的与你的领域密切相关、或与你面试的职位类似的工作。不要提到为了走投无路而申请的与你领域完全无关的兼职。

## 54：你曾在工作中受到过纪律处分吗？

**回答：**
希望这里的答案是否定的——但如果你在工作中确实因为某些事受到过处分，请务必确保你能彻底解释清楚。详细说明你从这种情况中学到了什么，并反思在这个过程之后你成长了。

## 55: 你的时间安排如何？

**回答：**
你的时间安排显然越开放越好，任何时间上的空缺都应该得到解释和说明。避免询问假期或私假（以及其他福利），向面试官传达你对工作的认真态度。

## 56: 我可以联系你的现任雇主吗？

**回答：**
如果可能，最好允许面试官联系你的现任雇主作为推荐人。然而，如果不联系雇主至关重要，请委婉地解释原因，例如你刚刚开始找工作，还没有机会告知他们你正在寻找其他工作。不过，要谨慎使用这个理由，因为雇主可能会怀疑你是否在入职期间也会在物色更好的机会。

## 57: 你是否有任何可以为我们业务提供的宝贵人脉？

**回答：**
如果你能带来知识、推荐人或其他新雇主可以建立人脉的联系，那就太好了。然而，请确保你没有提供任何前任雇主的客户，或者没有以任何方式违反合同协议。

## 58: 你多快可以开始工作？

**回答：**
虽然你希望在公司对聘用你有兴趣时确保尽可能快开始，但如果你还有另一份工作，请确保给他们至少两周的通知。虽然你的新雇主可能急于让你入职，但他们会希望雇佣一个因给予充分通知而受尊重的员工，这样他们就不必担心你最终会把他们置于困境。

## 59: 你的上任雇主会说你是为什么离开的？

**回答：**
这个问题的关键在于，雇主的回答必须与你对离开的回答一致。例如，如果你告诉雇主你离开是为了寻找一个职业晋升机会更大的职位，那么你的雇主最好不要说你是因为缺勤天数过多而被解雇的。在求职过程中，诚实是关键。

## 60: 你积极寻找工作多长时间了？

**回答：**
最好情况是你还没有积极找工作太久，因为时间太长可能会让面试官怀疑为什么没有人雇佣你。如果已经有一段时间了，请确保解释原因，并保持积极的态度。也许你还没有遇到许多能为你提供足够挑战，或与你的教育背景和经验相充分匹配的机会。

## 61: 你在什么情况下不来上班？

**回答：**
显然，唯一可以接受缺勤的时间是发生真正的紧急情况或你真的生病了——所以现在不要开始提到你计划因休假或家庭生日而缺勤的时间。或者，你可以告诉面试官你对工作有多么投入，你如何努力保持全神投入，并在每次上班时都投入相同的工作量，即使在你感到轻微不适时。

## 62: 你缺勤最常见的原因是什么？

**回答：**
如果你有一个经常性缺勤的原因，现在是披露它的时机——但在面试期间这样做会对你的负面形象产生负面影响。理想情况下，你只会在极度疾病或其他紧急情况下缺勤。

## 63: 你的考勤出勤记录如何？

**回答：**
务必诚实回答这个问题，但理想情况下，你已经付出了努力来证明你很少缺勤或迟到的事实。然而，如果出勤记录中有空隙，请用适当的原因简要解释，并确保强调你对工作的投入和可靠性。

## 64: 你是从哪里听到这个职位的？

**回答：**
这可能看起来像是一个简单的问题，但答案实际上可以反映你的很多信息。如果你是由朋友或在该公司的另一名员工推荐的，这是一个提及你人际关系的绝佳机会（如果那人的表现良好的话！）。然而，如果你是从招聘会或工作介绍机构等地方听说的，你可能希望关注你发现这样一个如此棒的机会有多么高兴。

## 65: 在做聘用决定时，还有什么你想让我知道的吗？

**回答：**
这是你向面试官进行最后一次推销自己的绝佳机会——利用这段时间提醒面试官你为什么胜任该职位，以及你能为公司带来什么其他人无法提供的价值。表达你对有机会加入一家追求 `X` 任务的公司的兴奋心情。

## 66: 为什么你的技能与我们公司的 X 目标非常匹配？

**回答：**
如果你在面试前研究过公司，那么回答这个问题应该没有问题。确定公司的几个主要目标，并解释你拥有的特定技能如何有助于实现这些目标。此外，思考你的经验和技能如何转化为帮助公司扩展这些目标并实现更远的目标。如果你的旧公司有类似的目标，请给出一个具体的例子说明你如何帮助公司实现它的。

## 67: 你认为这份工作包含哪些内容？

**回答：**
在进入面试之前，确保你已经对该职位进行了充分的研究。阅读你能找到的所有职位描述（最好是直接从雇主的网站或招聘公告上查看），并记录下关键职责、责任和要求的经验。没有什么比一个不知道自己面试的是什么工作的候选人更让面试官印象不深刻的。

## 68: 关于这份工作或公司，你还有什么想知道的吗？

**回答：**
如果你预先了解了公司，这是一个展示你在面试前付出了努力的绝佳机会。询问关于公司使命与当前行业趋势的关系，并与面试官进行有趣的交流。此外，在离开前清除关于特定职位的其他疑问——这样如果面试官打电话给你录取通知，你已经准备好回答了。

## 69: 你是这个职位的最佳人选吗？

**回答：**
是的！提供关于你为什么胜任该职位的具体细节，并务必讨论（并展现）你对新机会、工作和公司的无限热情和抱负。

## 70: 你是如何准备这次面试的？

**回答：**
这个问题的关键在于确保你已经做好了！确保你在面试前已经研究了公司、其目标和业务，并尽可能地了解该特定职位。了解公司的历史和当前组织中的关键人物也有帮助。

## 71: 你看过我们公司的网站吗？

**回答：**
显然，在来面试之前，你应该查看过公司网站并对其进行一些初步研究。如果由于某种原因你没有这样做，请不要说你做过，因为面试官可能会通过提问相关的具体问题来揭穿你。如果你确实看过公司网站，现在是提到你在那里看到的你特别感兴趣的内容，或者你特别支持的价值观的好时机。

## 73: 你简历上的 X 经验与此职位有何关系？

**回答：**
许多申请者的简历中都会有一些经验，无法明确地转化为所要求的特定工作。然而，请做好准备，可能会被问及这类看似无关的经历，并准备好一个回答，考虑到两者之间可能共有的相似技能集或培训。

## 74: 你为什么想获得这个职位？

**回答：**
将这个回答的重点积极集中在该特定职位的某些方面上，这些方面能够让你进一步提升技能、提供新经验，或者将成为你做某些你特别喜欢的事情的机会。不要告诉面试官你已经找了很长时间的工作了，或者说薪水非常有吸引力，否则你看起来会缺乏动力且投机取巧。

## 75: 你的背景与此职位有何关联？

**回答：**
理想情况下，这应该从你的简历中显而易见。然而，在你的经验与职位关联较松的情况下，请确保在面试前已经对工作和公司进行了充分的研究。这样，你就可以将你已有的经验和技能与新职位所需的相似技能联系起来。具体说明你的技能将如何转化，并使用“准备”和“学习”等词汇来描述你的背景。你的预期职位应该被描述为一个“机会”以及一个“成长与发展”的机会。

## 76: 你对我们公司的 X 使命怎么看？

**回答：**
在面试之前对公司进行研究是非常重要的——如果你已经这样做，这个问题就不会让你措手不及。最好的回答是简单、直击主题，并显示出对当前使命的了解。提供几个简短的陈述，说明为什么你认为这项使命很重要，并指出你对在一家支持该使命的公司工作感兴趣。

***

# 目录

# UNIX Shell 编程面试题

## C Shell – 初级

1. 在第一次通过名称或别名运行你的新脚本之前，必须做什么？

2. 以下命令包含在用户的 `.login` 脚本中：

3. 如果条件 `If ( -r filename )` 失败（返回假），可能的原因有哪些？

4. 下述两个语句之间的区别是什么？

5. 给定以下代码段：

6. 下列命令的输出将是什么？请解释。

7. `rehash` 命令的作用是什么？

8. 你如何确保脚本会在 `csh` 中运行？

9. 假设 `script1` 是一个位于 `/home/myhomedir/project1/data/dir1` 目录的可执行 C shell 脚本，使用三种方法运行它，并解释其优缺点。

10. 执行此命令后，`sixrem` 变量的值将是什么？

11. 写两种获取字符串长度的方法，并为每种方法提供一个简单的示例。

12. 创建一个脚本显示当前目录下普通文件的列表。

13. 要描述 `tcsh` shell 的单词补全功能。

14. 在 `tcsh` 中，每当单词补全失败时，如何列出剩余的选项（如果有的话）？

15. 在 `tcsh` 中，如何禁用文件名替换？

16. 比较 `sched` `tcsh` 内置命令与 UNIX/Linux 的 `at` 命令。

17. 在 10:55 一个提示符更改，作为即将到来的活动的提醒。

18. `csh` 脚本第一行中 `-f` 选项的影响。

19. 你如何在后台启动一个作业，然后终止登录会话，而不终止后台作业？

20. `echo c{1,4,2,5,1}` 和 `echo [c]{1,4,2,5,1}` 之间的区别是什么？

21. 无论参数数量多少，不使用循环显示脚本的第一个和最后一个参数。

22. 你如何在 `csh` 中设置“搜索路径”？

23. 在 `/home/user1/myarch.tar` 创建一个 tar 存档，包含所有以 `.c`, `.h`, `.l`, `.y`, `.o` 和 `.cc` 结尾的文件，以及来自 `~/dir1` 和 `~/dir2` 的 `Makefile`。

24. 你的脚本必须恰好带有两个参数执行，否则将终止。编写代码来实现这些检查。

25. 编写一个管道，从文本文件的第 `j` 行读到第 `k` 行，而不使用 `awk`。

## C Shell - 中级

26. 解释以下命令：

27. 你如何将光标移动到屏幕上的指定坐标？（`tcsh`）

28. 此循环的结果是什么？

29. 假设脚本某处有一个标签 `cleanup`，解释命令 `onintr cleanup`。

30. 是否有方法在不使用计数器控制循环的情况下，按预定义的次数重复命令？

31. `csh` 和 `tcsh` 都支持该功能。

32. 列出 `csh` 的特殊登录文件。

33. 以下几行的作用是什么？

34. 解释................................................................................................................................................

35. .................................................................................................................................................

36. .................................................................................................................................................

37. .................................................................................................................................................

38. .................................................................................................................................................

39. .................................................................................................................................................

40. .................................................................................................................................................

41. 下述两个命令的区别是什么，我们何时可以使用它们？

42. 以下代码段的输出是什么？

43. .................................................................................................................................................

44. 解释 `pct` 变量的值。

45. 使用两种方法提取给定文件的模式。

46. 在给定字符串中查找子字符串的位置。

47. 如果字符串不包含此子字符串，则显示消息。

48. 修改字符串的大小。

49. 假设脚本包含以下行：

50. 创建一个将当前目录文件名转换为小写的脚本。

51. 列出 `csh` 和 `tcsh` 之间的一些基础区别。

52. 比较 `tcsh` shell 变量 `correct` 和 `autocorrect`。

53. 特殊别名 shell 的作用是什么？

54. 什么方法可以将键绑定到标准的 `vi` 或 `emacs` 绑定？

55. shell 变量 `color` 的作用是什么？

56. 设置你的提示符显示 `username@hostname:pwd>`

57. 你如何（从 shell 提示符）“后台”启动两个命令，确保第二个命令在第一个命令完成后启动？

58. 编写一个脚本显示文本文件中唯一单词的排序列表。

59. 分行显示 `PATH` 变量的值，每个路径占一行。

60. 为什么在搜索路径中包含点 `.` 不是一个良好的做法？

61. 解释逻辑表达式 `@ x = ($n < 5 || 20 <= $n)`，然后写出该表达式的否定。

62. 一个脚本提示用户输入内容，使用以下语法：

## C Shell - 高级

63. 解释局部变量与环境变量。

64. 解释 `Searchpath`。

65. 解释 `Globbing`（通配）。

66. 修复以下 `switch` 语句，并说明你的修正。

# Shell 练习

64. 列出 `bash` 和 `csh` 语法和/功能的一些基本区别。

65. 建议一种克服 C shell 中缺少函数的方法。

66. 从 `/tmp` 目录执行 `(cd ; pwd) ; pwd`。解释所执行的操作和输出结果。

67. 编写一段代码片段，提示文件名，读取用户输入，检查该文件是否为普通文件，如果是，将其存储在数组中以便后续处理。该过程必须重复，直到用户按下回车键为止。

68. 使用 `awk` 数学函数计算圆的面积（`area = PI*rad2`）。

69. 使用 `awk` 将 `/etc/passwd` 文件中的条目分割到数组，并将密码字段替换为字符串 `"secret"`。

70. 解释以下代码段。

71. 列出可用的方法（带示例），替换字符串中任何出现的子字符串为另一个子字符串。

72. 编写一个片段，根据扩展名对目录中的文件进行分类（简单起见，只处理 `.c`、`.o`、`.txt` 和 `.png` 文件）。

73. 编写一个脚本，向用户显示选择菜单。菜单应反复显示，直到用户选择特定的 `"exit"` 选项。脚本应向用户提供以下选项：

74. 创建一个脚本，当用户登录系统时自动运行，并且如果其 `.cshrc` 文件中的别名总数大于阈值（假设为 40），则向用户发送一条邮件消息。

75. 显示当前目录下每个文件的文件名和权限。

76. 创建一个脚本，列出当前系统上所有文件系统（挂载点）的列表以及当前的使用百分比。

77. 解释以下脚本并建议任何改进方案。

78. 使用 `bc` 计算器进行涉及浮点数的变量比较。将你的示例写在一个 `if` 条件语句中。

79. 编写一个 `while` 循环，使用浮点数比较语句作为循环条件（和循环控制）。

80. 如果 C-shell 中没有简单的文件读取功能，你可以用什么来临时解决这个问题？

81. 提取文本文件的第 n 行并将其赋值给变量。

82. 假设 `input_file` 是一个由空格分隔字段的文本文件，当执行以下命令时，`ncol` 的值将会？

83. 找到数组中存储的整数的最小值。

84. 解释以下命令块：

85. C shell 提供了一种读取行的方法：

86. 解释以下代码段。

87. 修复以下脚本中的任何语法或逻辑错误。

88. 解释此脚本。

89. 接下来两个命令之间是否存在差异？

90. 解释以下代码块。

91. 假设你有一个格式如下的联系人文件（无表头）。

92. C shell 中 `getopt` 命令的有效语法是什么？

93. 简要解释以下脚本。

94. 编写一个脚本，计算存储在数组中的一组浮点数的最小、最大和平均值。

95. 你有一个具有对称模式的输入数据文件（每个记录的字段数量相同），第一行包含字段标题。你想提取实际数据记录的第 3 列（字段），即除表头行（第一行）和任何注释行（假设它们以 `#` 或 `*` 开头）之外的每个记录。给出一个解决方案并简要解释。

96. 假设 `input_file` 是具有非对称模式的表格文件，即每个记录（行）可能有不同数量的字段，且前 3 行描述了使用的模式。解释以下片段。

97. 假设你有一个数据文件，但其内部格式并不一致。你想从该文件中提取列，但你不知道列的顺序，只知道标题：`Name` 和 `email`。

98. 创建一个脚本逐行读取文本文件直到末尾。不要使用 `awk`。

99. C shell 在选项处理方面有什么局限性？

100. 重写下一个脚本，使用更易读、清晰的逻辑。

## Bash – 初学者

101. 什么是 `shebang`？

102. 什么是管道（pipes）？

103. 什么是 `exit` 状态？

104. 什么是子壳（subshell）？你如何创建它？

105. 考虑以下消息：

106. `case` 语句用于将变量的值与可能匹配的列表进行比较。对还是错？

107. 你不记得 `sort` 命令的正确选项（`switch`）以便反序对某些条目排序。你可以做什么？

108. Shell 脚本的第一行是：

109. 你需要找到 `/home` 目录下所有过去 10 天内未被访问的文件。你可以做什么？

110. 你如何检查系统上是否有运行的 `sshd` 进程？

111. 运行以下命令时会发生什么？

112. 下一行是 bash 脚本中条件语句的开头：

113. `for` 循环需要一个参数列表。该列表可以来自：

114. 给定嵌套循环，你会使用什么命令处理文件？

115. 如果在 `.bash_profile` 中，会发生什么？

116. 你使用什么结构进行这些检查？

117. 以下命令的预期输出是什么？

118. 如何在后台运行作业？

119. `cd -` 命令的操作？

120. `~` 对于 shell 的特殊含义是什么？

121. `variable5` 和 `$variable5` 之间的区别是什么？

122. `variable=value` 定义的是局部变量还是环境变量？

123. 如何找到已安装的 bash 版本？

124. 内置 `EDITOR` 的作用是什么？

125. 内置 `PATH` 的用途是什么？

126. bash 中有声明整数变量的方法吗？

127. shell 如何解释 `"??a"`？

## Bash - 中级

128. 编写一个简单的脚本检查用户的数字 UID，如果不是 root 则显示消息并退出。

129. 构造一个 bash 模式以匹配任何一个数字结尾的字母数字字符串。

130. 编写一个命令列出精确匹配 `Name###` 的文件名。

131. 获取所有以 `.` 开头的目录项（文件和子目录），排除 `.` 和 `..`。

132. 你必须检查系统中是否存在某个文件，以及你是否具有其读取权限。你会使用何种语法？

133. 考虑以下代码片段。

134. 运行此循环时会发生什么？

135. 运行此循环时会发生什么？

136. 你应该从 `passwd` 文件中找到用户账户 `dbuser1` 的条目。

137. 使用正确的语法显示 `datafile` 中所有以字符串 `ing.`（字面点）结尾的行。

138. 一个应用程序或服务的配置文件包含许多被注释的行，只有两三行是有用的。你如何只显示非注释的数据？

139. shell 如何将变量传递给 `awk`？

140. 对还是错：当向 `awk` 提供输入时，`awk` 会处理每个记录。

141. 对还是错：在 `awk` 语句中，所有未引号的字符串都被视为变量、关键字或函数。

142. 你有一个格式如下联系人文件：

143. 对还是错：在 bash shell 中数组可以是多维的。

144. 你如何显示数组变量的所有内容？

145. 你如何获取数组的长度（元素总数）？

146. 你如何初始化数组？

# Bash - 进阶

147: 判断对错：数组变量不能是环境变量。

148: 是否可以在函数内部定义一个具有局部作用域（local scope）的变量？

149: 如果你使用以下语法调用函数：

150: 使用以下重定向语法时，有什么方法可以避免覆盖文件？

151: 解释以下语法：

152: 命令的结果是什么？

153: 为什么在停止进程执行时，优先考虑使用 `TERM` 信号（`-15`）而不是 `KILL` 信号（`-9`）？

154: 是否可以在 shell 接收到特定信号时更改其默认行为？

155: 对于 `awk` 语句，`$0` 是什么含义？对于 `awk` 来说，变量 `$1`、`$2`、`....` 是什么含义？

156: 是否可以在 `awk` 命令处理输入行之前定义一些要执行的动作（actions）？

157: 选取所有适用于 `bash` shell 变量的选项。解释所有不适用的选项。

158: 判断对错：从命令行调用的脚本可以将变量导出到其父 shell。

159: 编写一个 `echo` 命令，使用双引号 `"` 显示以下行。

160: 你如何定义你的主提示符（prompt），以反映登录用户名、`@` 符号、系统主机名和当前工作目录？

161: 如何将变量的值设置为文件的内容？

162: 两种命令替换的形式 `$(cmd)` 和 `` `cmd` `` 之间有什么区别？

163: 描述“与”（and）列表执行。

164: `bash` shell（版本 4.2）允许表示和显示外语字母中的字符。是如何做到的？给出一个显示数学符号 PI 的示例。

165: 给出以下代码段的输出。

166: 目录 `/mydir` 的权限为 `rw-r----`，且你是该目录的所有者。你可以显示 `/mydir` 的内容吗？你可以切换到 `/mydir` 吗？可以在 `/mydir` 下创建一个新文件吗？你可以读取 `/mydir` 中包含的文件内容吗？

167: 声明函数的两种有效语法格式是什么？

168: 修正以下函数的声明。

169: `+=` 运算符执行什么操作？

170: 解释 `whiptail`、`man` 和 `grep`。

171: 解释 `/dev` 和 `/proc`。

172: 解释 `trap` 命令。

173: 什么是 `POSIX`？

174: 解释 `tput` 和 `infocmp`。

175: 如果你定义一个名为 `ls` 的函数会发生什么问题？

176: 定义一个名为 `pause_until_return` 的函数，暂停脚本执行，直到用户按下回车键。

177: 如何创建一个函数库？这种库的优点是什么？

178: 是否允许使用递归函数（调用自身的函数）？

179: 下面代码段使用文件描述符来创建一个文件：

180: 如果你应该需要在脚本中使用交互式命令（如 `sftp`），你可以使用什么来自动化此功能（无需用户交互）？

181: 以下内容的输出是什么？

182: 以下命令的输出是什么？

183: 解释以下管道。

184: 你如何声明一个关联数组？

185: 哪种语法返回（展开为）数组 `ARRAY` 中的索引？

186: 内置命令 `mapfile` 是什么用的？

187: 编写以下 `if` 结构的等效但更短的形式，且不使用 `if`。

188: 给出以下代码段的输出并解释它。

189: 将位置参数设置为字符串，然后取消位置参数，然后将它们重新设置为原始值。

190: `rm` 命令只是将文件（inode）从数据块中解除。要彻底删除文件，需要覆盖该文件占用的数据块。创建一个脚本来安全地删除作为参数传递的文件。

191: 假设有一个名为 `Array` 的数组，这个 `for` 循环做了什么？

192: 在 `case` 结构中使用终止符 `;;&` 和 `;&` 有什么影响？

193: 写出以下 `case` 的输出，假设 1) `$1` 等于 `a`，且 2) `$1` 等于 `5`：

194: 说出将数组设置为文本文件内容的两种方法。

195: 说出 `getopts` bash 内置命令的一个局限性。

196: 调试以下脚本片段。

197: 调试以下脚本片段。

198: 编写一个脚本，将给定文件中每个出现的模式项替换为另一种。该脚本接收 3 个参数：`pattern_to_be_replaced` `substitution_pattern` `filename`。

199: 创建一个函数，将其字符串参数的首字母大写化。

200: 以下代码段做了什么？

201: 描述以下脚本的功能。

202: 解释以下代码。

203: 如何实现间接引用？

204: 解释以下代码段。

205: 如何。

206. 定义一个名为 `pause_until_return` 的函数，暂停脚本执行，直到用户按下回车键。

207. 如何创建一个函数库？这种库的优点是什么？

208. 是否允许使用递归函数（调用自身的函数）？

209. 下面代码段使用文件描述符来创建一个文件：

210. 如果你应该需要在脚本中使用交互式命令（如 `sftp`），你可以使用什么来自动化此功能（无需用户交互）？

211. 以下内容的输出是什么？

212. 以下命令的输出是什么？

213. 解释以下管道。

214. 你如何声明一个关联数组？

215. 哪种语法返回（展开为）数组 `ARRAY` 中的索引？

216. 内置命令 `mapfile` 是什么用的？

217. 编写以下 `if` 结构的等效但更短的形式，且不使用 `if`。

218. 给出以下代码段的输出并解释它。

219. 将位置参数设置为字符串，然后取消位置参数，然后将它们重新设置为原始值。

220. `rm` 命令只是将文件（inode）从数据块中解除。要彻底删除文件，需要覆盖该文件占用的数据块。创建一个脚本来安全地删除作为参数传递的文件。

221. 假设有一个名为 `Array` 的数组，这个 `for` 循环做了什么？

222. 在 `case` 结构中使用终止符 `;;&` 和 `;&` 有什么影响？

223. 写出以下 `case` 的输出，假设 1) `$1` 等于 `a`，且 2) `$1` 等于 `5`：

224. 说出将数组设置为文本文件内容的两种方法。

225. 说出 `getopts` bash 内置命令的一个局限性。

226. 调试以下脚本片段。

227. 调试以下脚本片段。

228. 编写一个脚本，将给定文件中每个出现的模式项替换为另一种。该脚本接收 3 个参数：`pattern_to_be_replaced` `substitution_pattern` `filename`。

229. 创建一个函数，将其字符串参数的首字母大写化。

230. 以下代码段做了什么？

231. 描述以下脚本的功能。

232. 解释以下代码。

233. 如何实现间接引用？

234. 解释以下代码段。

235. 如何。

# 260: 你将如何设置编辑器的模式？
# 261: 你将如何避免内存中的重复项？

## 运算符与 Shell 替换

# 262: Shell 中提供哪些不同类型的替换？
# 263: Shell 中的文件测试操作符有哪些？
# 264: 你将如何在 UNIX 中解决算术表达式？
# 265: 你将如何使用布尔运算符？
# 266: 你将如何检查字符串的长度？
# 267: `-u` 和 `-g` 的作用是什么？
# 268: 你将如何检查文件的访问权限？
# 269: 你将如何在 `echo` 命令中使用转义序列？
# 270: 什么是命令替换？
# 271: 你将如何使用 `:+` 为变量替换名称？
# 272: 你将如何使用 `:-` 为变量替换名称？
# 273: 你如何为未设置/空变量设置值？
# 274: 什么是“Here”文档（在此文档）？
# 275: 你将如何丢弃命令的输出？
# 276: 你将如何删除一个函数？

***

## HR 面试问题

# 1: 你在哪里寻找灵感？
# 2: 你如何在工作中发挥创造力？
# 3: 你如何促使他人创造创意？
# 4: 描述一下你的创造力。
# 5: 你将如何处理一个负能量的同事？
# 6: 如果你目睹同事在浏览网页、看书等浪费公司时间，你会做什么？
# 7: 你如何处理自己与其它员工之间的竞争？
# 8: 什么时候与同事社交是合适的？
# 9: 请告诉我们一次，你上一份工作中发生过重大改变的经历，以及你是如何处理的。
# 10: 在分配任务时，你如何选择哪些任务分配给哪些团队成员？
# 11: 请告诉我们一次，你必须向同事或上级为你坚信的事物坚定立场的经历。
# 12: 请告诉我们一次，你帮助他人完成工作的经历，即使那不是“你的工作”。
# 13: 团队合作的挑战是什么？你如何处理？
# 14: 你看重职场中的多样性吗？
# 15: 如果同事不接受他人的多样性，你将如何处理？
# 16: 在团队中工作还是独立完成任务，哪种让你获得更多回报？
# 17: 请告诉我们一次你没有赶上截止日期的经历。
# 18: 你在工作时如何消除分心？
# 19: 请告诉我们一次，你在一个有每周或每月配额需要完成的职位工作的经历。你成功的频率有多高？
# 20: 请告诉我们一次，你遇到一个艰难截止日的经历，以及你是如何完成它的。
# 21: 当你手头有多个项目时，你如何保持组织有条？
# 22: 在工作日期间，你有多少时间处于“自动驾驶”状态？
# 23: 你如何处理截止日期？
# 24: 请告诉我们你个人解决问题的流程。
# 25: 工作中哪类事情会让你感到压力？
# 26: 当你对某事感到压力时你是什么样子？你如何解决它？
# 27: 你能多任务处理吗？
# 28: 你每周工作多少小时？
# 29: 你每天检查多少次邮箱？
# 30: 你如何做决策？
# 31: 对你来说，最难做的决策是什么？
# 32: 在做出艰难决定时，你如何收集信息？
# 33: 请告诉我们你做过的结果不好的决策。
# 34: 你能快速做出决策吗？
# 35: 公司广告的最好方式是什么？
# 36: 获得新客户还是留住老客户更好？
# 37: 从竞争对手手中赢得客户的最佳方法是什么？
# 38: 你对公司监控互联网使用情况怎么看？
# 39: 你对我们公司的第一印象是什么？
# 40: 请告诉我们你对业务的个人哲学。
# 41: 商业模式中最重要的什么是：销售、客户服务、营销、管理等？
# 42: 你如何跟上该领域的新和新兴趋势？
# 43: 你遵守公司在社交媒体上的政策会有问题吗？
# 44: 请告诉我们今天 X 行业面临的最大问题之一。
# 45: 你认为在我们公司成功需要什么？
# 46: 你在这个职业领域工作最喜爱的部分是什么？
# 47: 你认为未来 10 年你的职业生涯会发生什么变化？
# 48: 你在职位中寻找的最重要的三件事是什么？
# 49: 你如何评估你想要合作的公司？
# 50: 你能接受 __________ 的薪水工作吗？
# 51: 你为什么选择上一份工作？
# 52: 离开你上一份工作已经多久了？为什么？
# 53: 你还在寻找其他什么类型的工作？
# 54: 你在工作中受过纪律处分吗？
# 55: 你的时间安排怎样的？
# 56: 我可以联系你现在的雇主吗？
# 57: 你是否有任何可以带入我们业务的价值人脉？
# 58: 你最快什么时候可以上班？
# 59: 你的前任雇主会说你离开的原因是什么？
# 60: 你找这份工作多久了？
# 61: 你什么时候能来上班？
# 62: 什么是更常见的原因？
# 63: 你的出勤情况如何？
# 64: 你是从哪里看到这个职位的？
# 65: 有什么其他影响招聘的因素？
# 66: 你认为这个职位意味着什么？
# 67: 你和这个职位的匹配度如何？
# 68: 如果被录用，你第一天会做什么？
# 69: 你看过我们公司的网站吗？
# 70: 你为什么想要这个职位？
# 71: 你的背景与该职位匹配吗？
# 72: 你是这个职位的最佳人选吗？
# 73: 你对面试准备得如何？
# 74: 如果你被录用，你第一天会做什么？
# 75: 你对 X 任务怎么看？

***

## 以下某些标题可能有所帮助：

1. NET 面试题
2. Access VBA 面试题
3. Adobe ColdFusion 面试题
4. Advanced C++ 面试题
5. Advanced Excel 面试题
6. Advanced JAVA 面试题
7. Advanced SAS 面试题
8. AJAX 面试题
9. 算法 面试题
10. Android 开发 面试题
11. Ant & Maven 面试题
12. Apache Web 服务器 面试题
13. 人工智能 面试题
14. ASP.NET 面试题
15. 自动化测试 面试题
16. Base SAS 面试题
17. BEA WebLogic 服务器 面试题
18. C & C++ 面试题
19. C# 面试题
20. CCNA 面试题
21. 云计算 面试题
22. 计算机体系 面试题
23. 计算机网络 面试题
24. Core Java 面试题
25. 数据结构与算法 面试题
26. EJB 3.0 面试题
27. Entity Framework 面试题
28. Fedora & RHEL 面试题
29. Hadoop 大数据 面试题
30. Hibernate, Spring & Struts 面试题
31. HR 面试题
32. HTML, XHTML 和 CSS 面试题
33. HTML5 面试题

# 34. 你可能被问到的 IBM WebSphere Application Server 面题
# 35. 你可能被问到的 iOS SDK 面题
# 36. 你可能被问到的 Java / J2EE 设计模式面试题
# 37. 你可能被问到的 Java / J2EE 面题
# 38. 你可能被问到的 JavaScript 面题
# 39. 你可能被问到的 JavaServer Faces 面题
# 40. 你可能被问到的 JDBC 面题
# 41. 你可能被问到的 jQuery 面题
# 42. 你可能被问到的 JSP-Servlet 面题
# 43. 你可能被问到的 JUnit 面题
# 44. 你可能被问到的 Linux 面题
# 45. 你可能被问到的 Linux 系统管理员面试题
# 46. 你可能被问到的 Mac OS X Lion 面题
# 47. 你可能被问到的 Mac OS X Snow Leopard 面题
# 48. 你可能被问到的 Microsoft Access 面题
# 49. 你可能被问到的 Microsoft Powerpoint 面题
# 50. 你可能被问到的 Microsoft Word 面题
# 51. 你可能被问到的 MySQL 面题
# 52. 你可能被问到的网络面试题
# 53. 你可能被问到的 OOPS 面试题
# 54. 你可能被问到的操作系统面试题
# 55. 你可能被问到的 Oracle 数据库管理员面试题
# 56. 你可能被问到的 Oracle E-Business Suite 面题
# 57. 你可能被问到的 ORACLE PL/SQL 面题
# 58. 你可能被问到的 Perl 编程面试题
# 59. 你可能被问到的 PHP 面题
# 60. 你可能被问到的 Python 面题
# 61. 你可能被问到的 RESTful JAVA Web Services 面题
# 62. 你可能被问到的 SAP HANA 面题
# 63. 你可能被问到的 SAS 编程指南面试题
# 64. 你可能被问到的 Selenium 测试工具面试题
# 65. 你可能被问到的 Silverlight 面题
# 66. 你可能被问到的软件仓库面试题
# 67. 你可能被问到的软件测试面试题
# 68. 你可能被问到的 SQL Server 面题
# 69. 你可能被问到的 Tomcat 面题
# 70. 你可能被问到的 UML 面试题
# 71. 你可能被问到的 Unix 面题
# 72. 你可能被问到的 UNIX Shell 编程面试题
# 73. 你可能被问到的 Windows Server 2008 R2 面题
# 74. 你可能被问到的 XLXP, XSLT, XPATH, XFORMS & XQuery 面题
# 75. 你可能被问到的 XML 面题

访问以下查看完整列表

`www.vibrantpublishers.com`
