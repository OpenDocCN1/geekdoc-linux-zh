
### 39. 有多少个文件组成员无法访问？
- a. 1
- b. 4

### 40. 有多少个文件或目录是所有者可以执行的？
- a. 4
- b. 7

### 41. 哪个命令使得你的当前目录（主目录）对组用户可读？
- a. `chmod g+rw`
- b. `chmod g-w`
- c. `chmod g-r`
- d. `chmod u+rw`

### 42. 哪个命令赋予用户读、写、执行权限，赋予组读执行权限，赋予其他无权限？
- a. `chmod 660`
- b. `chmod 730`
- c. `chmod 430`
- d. `chmod 750`

### 43. 哪个命令从主目录执行时，将 `/users/you/personal` 移动到 `misc` 目录？
- a. `mv /users/you/personal misc`
- b. `mv personal`
- c. `mv misc`
- d. `mv /`

### 44. 你的当前工作目录是 `/usr/users/you/book`。哪个命令将该目录中名为 `design` 的文件复制到 `database` 目录？
- a. `cp design /usr/users/you/book/database`
- b. `cp design /database`
- c. `cp database /usr/users/you/book`
- d. `cp design.detail /usr/users/you/book`

### 45. 哪个命令删除名为 `work1` 的文件？
- a. `delete work1`
- b. `del work1`
- c. `rm work1`
- d. `remove work1`

### 46. 哪个命令从主目录执行删除 `/users/you/personal` 目录及其所有文件？
- a. `rmdir /users/you/personal`
- b. `rmdir -r`
- c. `rm -r personal`
- d. `rmdir`

### 47. 假设你的工作目录是 `/usr/users/you/work`，工作目录下有一个名为 `projects` 的空子目录。哪个命令删除该空目录？
- a. `rm projects`
- b. `rmdir projects`
- c. `rm /usr/users/you/projects`
- d. `mkdir`

### 48. 关于硬链接，哪项描述是正确的？
- a. 可以指向目录
- b. 与原始文件无法区分
- c. 可以跨文件系统
- d. 不共享 inode

### 49. 关于符号链接，哪项描述是正确的？
- a. 在原始文件被删除后仍可以通过符号链接访问
- b. 不能跨文件系统创建
- c. 可以指向目录
- d. 每个符号链接的创建会导致计数增加

### 50. 你可以在哪些日历视图创建预约条目？
- a. 天、周、年
- b. 周、月、年
- c. 天、周、月
- d. 天、周

### 51. 使用文本编辑器你可以通过以下方式向文件添加新文本：
- a. 从一个窗口复制并粘贴到另一个窗口
- b. 使用文本编辑器的拖放功能
- c. 输入信息
- d. 以上所有

### 52. 使用 CDE 时，点击哪个控件输入命令？
- a. 日历 (Calendar)
- b. 邮件服务器 (Mailer)
- c. 终端 (Terminal)
- d. 桌面应用 (Desktop_Apps)

### 53. 系统管理员将常用的应用程序放在哪个系统文件夹中？
- a. 个人应用程序文件夹
- b. 用户文件夹
- c. 系统管理员文件夹
- d. 应用程序文件夹

### 54. 下列哪项可以被认为是 shell 的目的？
- a. UNIX 操作系统的用户界面
- b. 命令语言解释器
- c. 编程语言
- d. 以上所有

### 55. 哪个 shell(s) 提供命令历史缓冲区？
- a. Bourne shell
- b. C shell
- c. Korn shell
- d. C shell 和 Korn shell

### 56. 哪一个不是 Tru64 UNIX shell 的文件名？
- a. `/bin/sh`
- b. `/bin/bsh`
- c. `/bin/ksh`

### 57. Korn shell 通配符运算符 `?` 可用于匹配：
- a. 零或一个任意字符
- b. 恰好一个字符
- c. 一个或多个字符
- d. 仅限数字字符

### 58. 列出当前工作目录下所有以 `.txt` 结尾的文件，使用以下命令：
- a. `ls .txt?`
- b. `ls ?.txt`
- c. `ls *.txt`
- d. `ls .txt`

### 59. 使用哪个命令可以验证所有 Bourne、C 和 Korn shell 变量的设置？
- a. `show variables`
- b. `set`
- c. `set variables`
- d. `show -all`

### 60. 使用哪个命令可以在 Bourne 和 Korn shell 中显示任何特定 shell 变量的值？
- a. `print variable_name`
- b. `variable_name =`
- c. `echo $variable_name`
- d. `print $variable_name`

### 61. 使用 Korn shell 设置变量 `myname` 的正确方法是：
- a. `set myname = 'Charlie Brown'`
- b. `set myname = "Charlie Brown"`
- c. `myname = 'Charlie Brown'`
- d. `myname="Charlie Brown"`

### 62. 使用哪个命令可以显示所有的 Korn shell 选项？
- a. `set -o {option}`
- b. `set -o`
- c. `set +o {option}`
- d. `set +o`

### 63. 哪个命令将 emacs 开启为 Korn shell 命令编辑器？
- a. `set -o emacs`
- b. `set +o emacs`
- c. `set emacs`
- d. `set emacs on`

### 64. 哪一个不是默认的 shell 登录脚本？
- a. `.login`
- b. `.cshrc`
- c. `.profile`
- d. `.kshrc`

### 65. Korn shell 登录脚本文件之一的文件名是基于哪个变量的扩展的？
- a. `ENV`
- b. `LOGIN`
- c. `KSHSTART`
- d. `SHELL`

### 66. 如果你正在使用 C shell 并启动了一个子 shell，将执行哪个启动文件？
- a. `.login`
- b. `.profile`
- c. `.kshrc`
- d. `.kshrc`

### 67. 哪个语句描述了 Korn shell 环境脚本文件的用途？
- a. 定义适用于交互式使用以及从 ksh 用的脚本的别名和函数
- b. 设置你想应用到所有 ksh 调用的默认选项
- c. 设置你想应用到当前会话变量
- d. 以上所有

### 68. 在单用户模式下可以使用哪个编辑器？
- a. `emacs`
- b. `ed`
- c. `vi`
- d. `ex`

### 69. 下列中哪项是 vi 编辑器的只读版本？
- a. `ed`
- b. `ex`
- c. `sed`
- d. `view`

### 70. 哪个编辑器允许你同时编辑多个缓冲区和多个窗口？
- a. `ed`
- b. `vi`
- c. `emacs`
- d. `sed`

### 71. 如果你使用 vi 编辑器编辑一个现有文件 `junk`，并将其保存为与 `:wq` 命令同名的文件，编辑器会给文件的之前的（未编辑的）版本起什么什么名字？
- a. `junk~`
- b. `junk.bak`
- c. `junk;`
- d. 不保留文件的之前的版本

### 72. 哪个答案最能描述 vi 编辑器的模式？
- a. 命令模式；编辑模式；文本输入模式
- b. 命令模式；文本输入模式；末行模式
- c. 标标模式；文本输入模式；末行模式
- d. 命令模式；文本输入模式；退出模式

### 73. 哪个 vi 模式用于编辑另一个文件、执行 shell 命令或执行 ex 命令？
- a. 命令模式
- b. 文本输入模式
- c. 末行模式
- d. 退出模式

### 74. 应该使用哪个控制序列从 vi 文本输入模式跳转到命令模式？
- a. Eof (Ctrl/D)
- b. Escape (Ctrl/I)
- c. Stop (Ctrl/S)
- d. Suspend (Ctrl/Z)

### 75. 哪个答案不是离开 vi 命令模式并返回 shell 提示符的有效命令？
- a. `Q`
- b. `ZZ`
- c. `:q`
- d. `:q!`

### 76. 哪个命令将名为 `test` 的文件追加到名为 `output` 的文件的末尾？
- a. `cat output >> test`
- b. `append output > test`
- c. `write output > test`
- d. `cat test >> output`

### 77. 命令 `ls -l > listing` 实现了什么？
- a. 将 `ls -l` 的输出放入名为 `listing` 的文件中
- b. 使用 `listing` 的内容作为 `-l` 命令的输入
- c. 将 `-l` 命令的输出作为文件的输入
- d. 列出 `listing` 文件的内容

### 78. 符号 `<` 的作用是什么？
- a. 重定向标准输出
- b. 重定向标准输入
- c. 添加到文件的末尾
- d. 重定向标准输出

### 79. 哪个命令显示文件中有多少行？
- a. `sort -l`
- b. `sort -w`
- c. `wc -l`
- d. `sort`

### 80. 哪个命令在不考虑大小的情况下对 `flowers` 文件进行排序？
- a. `sort -f`
- b. `sort -r`
- c. `sort`
- d. `sort`

### 81. 创建包含姓名、生日并按字母顺序排列的 `dates` 文件的命令是：
- a. `sort +1 > dates`
- b. `sort -2`
- c. `sort +1 -2`
- d. `sort -r dates`

### 82. `-m` 选项实现了什么？
- a. 合并重复项
- b. 合并两个文件
- c. 排序大于 500 的文件
- d. 合并文件

使用以下示例回答问题：

```
1) go.c
2) date
3) list
4) go
5) out
6) glob
7) in
8) h
9) totals
10) login
```

### 83. 哪些命令匹配正则表达式 `$` 的字符串？
- a. 10
- b. 4, 5
- c. 4, 9
- d. 2

### 84. 哪些命令匹配正则表达式 `.*'` 的字符串？
- a. 2
- b. 5
- c. 4, 9
- d. All strings

### 85. 哪个字符串不匹配正则表达式 `[la]$`？
- a. `.login`
- b. `layout.c`
- c. `a.out`
- d. `bodyguard`

### 86. 哪个字符串匹配正则表达式 `.*$`？
- a. `a.out`
- b. `go.bin`
- c. `layout.c`
- d. `bodyguard`

### 87. 将命令输出作为另一个输入的单个字符是：
- a. 问号 (?)
- b. 竖线 (|)
- c. 星号 (*)
- d. At 符号 (@)
- e. 斜杠 (/)

### 88. 哪个命令创建文件列表，反向排序并将结果放入名为 `sortedlist` 的文件中？
- a. `ls | sort -r`
- b. `ls > sort`
- c. `ls > sort -r`
- d. `ls > sortedlist`

### 89. 哪个命令可以列出系统中登录 shell 为 ksh 的账户，按登录名字母顺序排序并显示屏幕？
- a. `more /etc/password | grep "/users/ksh" | sort`
- b. `grep 'ksh' /etc/password ; sort`
- c. `sort /etc/password > grep "ksh"`
- d. `cat /etc/password | grep "ksh" | sort`

### 90. 哪个命令可以创建一个名为 `phonenames` 的文件，其中包含 `phones` 文件的电话号码列表，如果电话号码是第三字段？
- a. `awk [3] >! phonenames`
- b. `awk "print $3" phones | phonenames`
- c. `awk '{print $3}' phones > phonenames`
- d. `awk -o phones phonenames > $3`

### 91. 哪个命令运行名为 `sum2.awk` 的 awk 文件来处理名为 `weekly.sum` 文件？
- a. `awk -F sum2.awk weekly.sum`
- b. `-f weekly.sum sum2.awk`
- c. `awk '{sum2.awk}' weekly.sum`
- d. `awk -f sum2.awk weekly.sum`

### 95. Korn shell 有默认的历史文件和默认的保留已执行命令数量。这些默认值是：
- a. `.history, 128`
- b. `.sh_history, 128`
- c. `.ksh_history, 64`
- d. `history, 64`

### 96. 开启 Korn shell 内置命令编辑器有多种方法。如果执行了以下三个选项/变量赋值，将使用哪一个内置命令作为 Korn shell 的命令编辑器？

```
EDITOR=emacs
VISUAL=emacs
set -o vi
```
