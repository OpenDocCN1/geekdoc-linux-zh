

# 示例 10.34

（脚本）

```
#!/bin/csh -f
# Scriptname: systype
# Program to determine the type of system you are on.
echo "Your system type is:"
1 set release = (`uname -r`)
2 switch (`uname -s`)
3 case SunOS:
4   switch "$release"
5   case 4:;
      echo "SunOS $release"
      breaksw
6   case [5-9]:;
      echo "Solaris $release"
      breaksw
7   endsw
      breaksw
case HP-UX:
    echo HP-UX
    breaksw
case Linux:
    echo Linux
    breaksw
8 endsw
```

（输出）

Your system type:
SunOS 4.1.2

# 解释

+   1 变量 release 被赋值为 uname -r 的输出，即操作系统的发行版本号。
+   2 switch 命令评估 uname -s 的输出，即操作系统的名称。
+   3 如果系统类型是 SunOS，则执行第 3 行的 case 命令。
+   4 变量 release 的值在每个 case 中进行匹配。
+   5 测试所有发行版本为 4 的情况。
+   6 测试所有发行版本为 5-9 的情况。
+   7 内部 switch 语句终止。
+   8 外部 switch 语句终止。

# 10.6.22 here 文档和菜单

here 文档（在第 433 页“here 文档”中讨论过）用于在 shell 脚本中生成菜单。它通常与 switch 语句一起使用。用户看到菜单后，选择一个项目，然后该选择在 switch 语句中与对应选择的 case 进行匹配。here 文档减少了原本需要的 echo 语句数量，并使程序更易于阅读。

# 示例 10.33

```
(The Script)
#!/bin/tcsh
1 echo "Select from the following menu:"
2 cat << EOF
1) Red
2) Green
3) Blue
4) Exit
3 EOF
4 set choice = $<
5 switch ("$choice")
6 case 1:
    echo Red is stop.
    breaksw
7 case 2:
    echo Green is go!\!
    breaksw
case 3:
    echo Blue is a feeling...
    breaksw
case 4:
    exit
    breaksw
default:
    echo Not a choice\!\!
endsw
8 echo Good-bye
```

（输出）
Select from the following menu:
1) Red
2) Green
3) Blue
4) Exit

2
Green is go!
Good-bye

# 解释

+   1 用户被要求从第 2 行 here 文档生成的菜单中进行选择。
+   2 here 文档用于显示颜色选择列表。
+   3 EOF 标记 here 文档的结束。
+   4 用户输入被赋给变量 choice。
+   5 switch 语句评估变量 choice 并将用户的选择与其中一个 case 进行匹配。
+   6 如果用户选择了 1，则显示 Red is stop，并且第 7 行的 breaksw 命令导致程序退出 switch 并跳转到第 8 行。如果用户没有选择 1，则程序从 case 2 开始，依此类推。

# 10.7 循环命令

循环结构允许你多次执行相同的语句。C shell 支持两种类型的循环：foreach 和 while。foreach 循环用于在列表的每个项目上执行命令，例如文件列表或用户名列表。while 循环用于在满足特定条件之前持续执行命令。

# 10.7.1 foreach 循环

foreach 命令后面跟着一个变量和用括号括起来的词表。第一次进入循环时，列表中的第一个词被赋给变量。列表向左移动一位并进入循环体。循环体中的每个命令执行到遇到 end 语句为止。控制返回到循环顶部。列表中的下一个词被赋给变量，foreach 行之后的命令被执行，遇到 end，控制返回到 foreach 循环顶部，处理词表中的下一个词，以此类推。当词表为空时，循环结束。

# 格式

```
foreach variable (wordlist)
    commands
end
```

# 示例 10.36

```
1  foreach person (bob sam sue fred)
2      mail $person < letter
3  end
```

