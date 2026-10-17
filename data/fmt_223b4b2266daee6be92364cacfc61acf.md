
- 39. `users` 组成员无法访问多少个文件？
- a. 4
- b. 4
- c. 2
- d. 全部

- 40. 有多少文件或目录对所有者可执行？
- a. 4
- b. 7
- c. 5
- d. 全部

- 41. 哪个命令更改 `time.status` 文件的权限，使得只有你可以读取或写入？
- a. `set [rw,] time.status`
- b. `chmod g-rw,w time.status`
- c. `chmod g-rw,o time.status`
- d. `chmod u+rw time.status`

- 42. 哪个命令给用户读、写、执行权限，给组读和执行权限，给其他人无权限的文件 `a.out`？
- a. `chmod 660 a.out`
- b. `chmod 730 a.out`
- c. `chmod 430 a.out`
- d. `chmod 750 a.out`

### 测试 18-35

- 43. 从主目录执行的哪个命令将 `/usr/users/personal/misc/phones` 和 `/usr/users/personal/misc/resume` 移动到 `/usr/users/personal` 目录？
- a. `mv personal/misc/phones personal`
- b. `mv resume personal`
- c. `mv personal/misc/phones resume`
- d. `mv phones personal`

- 44. 你的当前工作目录是 `/usr/users/you/database/code`。哪个命令将 `/usr/users/you/database/doc/design.detail` 文件复制到名为 `design` 的当前目录？
- a. `cp /usr/users/you/database/doc/design.detail design`
- b. `cp /usr/users/you/database/doc/design.detail detail`
- c. `cp /database/doc/design.detail /database/code/design`
- d. `cp design.detail design/code`

- 45. 哪个命令删除名为 `work1` 的文件？
- a. `delete work1`
- b. `del work1`
- c. `rm work1`
- d. `remove work1`

- 46. 从主目录执行的哪个命令删除 `/usr/users/you/personal` 目录及其所有文件？
- a. `rmdir /usr/users/you/personal`
- b. `rmdir -r personal`
- c. `rm -r personal`
- d. `rmdir /personal`

- 47. 假设你的工作目录是 `/usr/users/you/work`，且工作目录下有一个名为 `projects` 的空目录。哪个命令删除该空目录？
- a. `rm projects`
- b. `rmdir projects`
- c. `rm /usr/users/you/projects`
- d. `rmdir work/projects`

- 48. 关于硬链接，哪个说法是正确的？
- a. 可以指向目录
- b. 与原始文件不可区分
- c. 可以跨越文件系统
- d. 不共享 inode

- 49. 关于符号链接，哪个说法是正确的？
- a. 在原始文件删除后仍可以通过符号链接访问
- b. 不可以跨文件系统创建
- c. 可以指向目录
- d. 每个符号链接的创建会导致链接计数增加

- 50. 你可以从哪些日历视图创建预约条目？
- a. 日、周、年
- b. 周、月、年
- c. 日、周、月
- d. 日、周

- 51. 使用文本编辑器你可以通过以下方式向文件添加新文本：
- a. 从一个窗口复制并粘贴到另一个窗口
- b. 使用文本编辑器的拖放功能
- c. 输入信息
- d. 以上所有

- 52. 使用 CDE 时，输入命令应点击哪个控件？
- a. 日历
- b. 邮件服务器
- c. 终端
- d. 桌面应用程序

- 53. 系统管理员将经常使用的应用程序放在哪个系统文件夹？
- a. 个人文件夹
- b. 用户文件夹
- c. 系统管理员文件夹
- d. 应用程序管理器

- 54. 下列哪项可以被认为是 shell 的目的？
- a. UNIX 系统的用户界面
- b. 命令语言解释器
- c. 一种编程语言
- d. 以上所有

- 55. 哪些 shell 提供命令历史缓冲区？
- a. Bourne shell
- b. C shell
- c. Korn shell
- d. C shell 和 Korn shell

- 56. 什么不是 Tru64 UNIX shell 的文件名？
- a. `/bin/sh`
- b. `/bin/bsh`
- c. `/bin/ksh`

- 57. Korn 通配符 `?` 可以匹配：
- a. 零或一个任意字符
- b. 任意一个字符
- c. 一个或多个字符
- d. 仅限数字字符

- 58. 要列出当前工作目录下所有 `.txt` 扩展的文件，使用命令：
- a. `ls .txt?`
- b. `ls ?txt`
- c. `ls *.txt`
- d. `ls .txt`

- 59. 用哪个命令验证所有 Bourne、C 和 Korn shell 变量的设置？
- a. `show variables`
- b. `set`
- c. `set variables`
- d. `show -all`

- 60. 用哪个命令可以在 Bourne、C 和 Korn shell 中显示特定变量的值？
- a. `print variable_name`
- b. `variable_name =`
- c. `echo $variable_name`
- d. `print $variable_name`

- 61. 用 Korn shell 设置变量 `myname` 的正确方法是：
- a. `set myname='Charlie Brown'`
- b. `set myname = "Charlie Brown"`
- c. `myname = 'Charlie Brown'`
- d. `myname="Charlie Brown"`

- 62. 使用哪个命令可以显示所有的 Korn shell 选项？
- a. `set -o {option}`
- b. `set -o`
- c. `set +o {option}`
- d. `set +o`

- 63. 哪个命令将 emacs 开启为 Korn shell 的行编辑器？
- a. `set -o emacs`
- b. `set +o emacs`
- c. `set emacs`
- d. `set emacs on`

- 64. 哪一个不是默认的 shell 登录脚本？
- a. `.login`
- b. `.cshrc`
- c. `.profile`
- d. `.kshrc`

- 65. Korn shell 登录脚本文件之一的文件名是基于哪个变量扩展的？
- a. `ENV`
- b. `LOGIN`
- c. `KSHSTART`
- d. `SHELL`

- 66. 如果你使用 C shell 并且启动了一个子 shell，会执行哪一个启动文件？
- a. `.login`
- b. `.profile`
- c. `.kshrc`
- d. `.cshrc`

- 67. 哪个选项描述了 Korn shell 环境脚本文件的目的？
- a. 定义适用于交互式使用以及从 ksh 调脚本的别名和函数
- b. 设置你想应用到所有 ksh 调用的默认选项
- c. 设置你想应用到当前会话的变量
- d. 以上所有

- 68. 在单用户模式下可以使用哪个编辑器？
- a. emacs
- b. ed
- c. vi
- d. ex

- 69. 下列中哪一个是 vi 编辑器的只读版本？
- a. ed
- b. ex
- c. sed
- d. view

- 70. 哪个编辑器允许你同时编辑多个缓冲区和多个窗口？
- a. ed
- b. vi
- c. emacs
- d. sed

- 71. 如果你使用 vi 编辑器编辑名为 junk 的现有文件，并使用 `:wq` 命令将其保存为同名文件，编辑器会给文件的之前的（未编辑）版本起什么名字？
- a. `junk~`
- b. `junk.bak`
- c. `junk;1`
- d. 文件的之前的版本不会保留

- 72. 哪个答案最能描述 vi 编辑器的模式？
- a. 命令模式；编辑模式；文本输入模式
- b. 命令模式；文本输入模式；末行模式
- c. 光标模式；文本输入模式；末行模式
- d. 命令模式；文本输入模式；退出模式

- 73. 哪种 vi 模式用于编辑另一个文件、执行 shell 命令或执行 ex 命令？
- a. 命令模式
- b. 文本输入模式
- c. 末行模式
- d. 退出模式

- 74. 应该使用哪种控制序列从 vi 文本输入模式切换到命令模式？
- a. Eof (Ctrl/D)
- b. Escape (Ctrl/[])
- c. Stop (Ctrl/S)
- d. Suspend (Ctrl/Z)

- 75. 哪个答案不是离开 vi 命令模式并返回 shell 提示符的有效命令？
- a. Q
- b. ZZ
- c. :q
- d. :q!

- 76. 哪个命令将名为 test 的文件追加到名为 output 的末结尾？
- a. `cat output >> test`
- b. `append output > test`
- c. `write output > test`
- d. `cat test >> output`

- 77. 命令 `ls -l > listing` 实现了什么？
- a. 将 `ls -l` 的输出存到一个名为 listing 的文件中
- b. 使用 listing 的内容作为 `ls -l` 命令的输入
- c. 使用 `ls -l` 命令的输出作为 listing 命令的输入
- d. 使用名为 listing 的文件的内容

- 78. `<` 重定向符号的作用是什么？
- a. 重定向标准输出
- b. 重定向标准输入
- c. 将输出添加到文件末尾
- d. 重定向标准输入和标准输出

- 79. 哪个命令显示名为 flowers 的文件中有多少行？
- a. `sort -l flowers`
- b. `sort -w flowers`
- c. `wc -l flowers`
- d. `lines flowers`

- 80. 哪个命令按忽略字母大小写的方式对 flowers 文件进行反字母顺序排序？
- a. `sort -f flowers`
- b. `sort -f flowers`
- c. `sort -r flowers`
- d. `sort -r -m flowers`

- 81. dates 文件包含三个字段：名字、姓和生日，顺序如下。哪个命令创建一个名为 dates.new 的新文件，其中包含 dates 文件中的数据按字母顺序排序，先按姓排序，再按名排序？
- a. `sort +1 -2 dates > dates.new`
- b. `sort -o dates +1 -2`
- c. `sort dates +1 -2 > dates.new`
- d. `sort -o dates.new +1`

- 82. sort 的 `-m` 选项实现了什么？
- a. 合并时消除重复项
- b. 合并两个或多个已排序的文件
- c. 排序并合并大于 500 行的文件
- d. 排序并合并多个文件

使用以下示例回答问题：
1) go.c
2) date
3) go.bin
4) go.lst
5) a.out
6) bodyguard
7) glob.in
8) layout.c
9) layout.h
10) totals

- 83. 正则表达式 `t$` 匹配哪些字符串？
- a. 10
- b. 4, 5
- c. 4, 5, 8, 9
- d. 2, 4, 5, 9

- 84. 正则表达式 `...` 匹配哪些字符串？
- a. 2
- b. 2, 5
- c. 1, 2
- d. 所有字符串

- 85. 正则表达式 `^[la` 不匹配哪个字符串？
- a. `.login`
- b. `layout.c`
- c. `a.out`
- d. `bodyguard`

- 86. 正则表达式 `...$` 匹配哪些字符串？
- a. `a.out`
- b. `go.bin`
- c. `layout.c`
- d. `lifeguard`

- 87. 输入哪个字符可以将一个命令的输出作为另一个命令的输入：
- a. 问号 (?)
- b. 竖线 (|)
- c. 星号 (*)
- d. 符号 (@)
- e. 斜杠 (/)

- 88. 哪个命令创建一个文件列表，然后按反字母顺序并将结果放入名为 sortedlist 的文件中？
- a. `ls | sort -r > sortedlist`
- b. `ls > sort`
- c. `ls > sort -r sortedlist`
- d. (选项缺失)

- 89. 哪个命令可以显示系统中所有登录 shell 为 ksh 的账户列表，按字母排序并一次显示一屏？
- a. `more /etc/passwd | grep "usr/ksh"`
- b. `grep 'ksh' /etc/passwd ; sort; more`
- c. `sort /etc/passwd > grep "ksh" > more`
- d. `cat /etc/passwd | grep "ksh" | sort | more`

- 90. 哪个命令可以创建一个名为 phonenums 的文件，其中包含来自名为 phones 的文件的电话号码，如果电话号码是第三字段？
- a. `awk phones [3] > phonenums`
- b. `awk "print $3" phones > phonenums`
- c. `awk '{print $3}' phones > phonenums`
- d. `awk -o phones phonenums > $3`

- 91. 哪个命令运行名为 sum2.awk 的 awk 文件来处理 weekly.sum 文件？
- a. `awk -F sum2.awk weekly.sum`
- b. `awk -f weekly.sum sum2.awk`
- c. `awk '{sum2.awk}' weekly.sum`
- d. `awk -f sum2.awk weekly.sum`

- 92. awk 命令源自：
- a. 创建者名字的首字母
- b. 创建者姓的首字母
- c. 该命令语法奇怪的能力
- d. 一种南美鸟

- 93. 哪个命令显示用户 pmj 的真实名和扩展？
- a. `who pmj`
- b. `whoami pmj`
- c. `users pmj`
- d. `finger pmj`

- 94. 哪个命令可以查看缓冲区中的命令？
- a. `show history`
- b. `history`
- c. `cat history`
- d. `view commands`

- 95. Korn shell 有一个默认的历史文件和默认的保留命令数。这些默认值是：
- a. `.history, 128`
- b. `.sh_history, 128`
- c. `.ksh_history, 64`
- d. `history, 64`

- 96. 开启 Korn shell 内置命令编辑器有很多方法。如果进行了以下三个选项/变量赋值，使用哪个内置编辑器作为 Korn shell 命令编辑器？

```
EDITOR=emacs
VISUAL=gmacs
set -o vi
```
