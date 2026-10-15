
```
Hi <USERNAME> how's your day going?
"No, <USERNAME> you can't use the car tonight!", she cried.
The time is [ date ] [ time ] PST 2004
The name of this machine is [ hostname ] and the time is [ date ] [ time ]
```

5. 创建一个包含用户名列表的文件。现在创建一个名为 `nlist` 的变量，其中包含通过使用命令替换提取的用户名列表。

a. 打印该变量的值。命令替换如何影响列表的格式？

b. 通过将变量设置为 `ps -eaf` 命令的输出来测试这一点。

c. 格式发生了什么变化？

# LAB 38: 重定向

1. 进入编辑器并创建以下两行文本文件，命名为 `ex6`：

Last time I went to the beach I found a sea shell.

While in Kansas I found a corn shell.

2. 现在将此行追加到你的 `ex6` 文件中：

The National Enquirer says someone gave birth to a shell, called the born shell.

3. 将 `ex6` 文件邮件发送给自己。

4. 使用管道，统计 `ex6` 文件中的行数（`wc -l`）。

5. 要列出所有已设置选项，输入以下内容：

`set -o`

你是否设置了 `noclobber` 变量？如果没有，输入以下内容：

`set -o noclobber`

发生了什么？

6. 在命令行输入以下内容：

```
cat << FINIS

How are you $LOGNAME

The time is `date`Bye!!

FINIS
```

打印了什么？

7. 现在尝试使用制表符：

```
cat << END

hello there

how are you

END
```

打印了什么？

8. 在命令行输入以下内容：

`kat file 2> error || print kat failed`

发生了什么？为什么？

9. 现在在命令行输入以下内容：

`cat zombie > errorfile || print cat failed`

发生了什么？为什么？`||` 运算符如何工作？尝试自己的命令来测试它。

10. 使用 `find` 命令打印从根目录向下开始的所有以 `a` 开头的文件。将标准输出放入名为 `foundit` 的文件中，并将错误发送到 `/dev/null`。

# LAB 39: 作业控制

1. 在命令行输入以下内容：

`mail <user>` 按 Ctrl-z

现在输入：

`jobs`

方括号中的数字是什么？

2. 现在输入：

`sleep 300`

`jobs`

`bg`

`bg` 有什么作用？`+` 和 `–` 符号表示什么？

3. 使用作业控制杀死 `mail` 作业。

4. 进入编辑器。输入 ^Z 来停止作业。现在将停止的 `vi` 作业带回前台。你输入了什么命令？

5. 输入以下命令：

`jobs -l`

输出是什么？

6. `TMOUT` 变量有什么用途？

7. 执行以下命令时内核花费了多少时间：

`(sleep 5 ; ps -eaf )`

# LAB 40: 编写 info Shell 脚本

1. 编写一个名为 `info` 的程序。在尝试执行它之前，确保使用 `chmod` 命令使程序可执行。

2. 程序应包含注释。

3. 程序在执行时应执行以下操作：

a. 输出已登录用户的数量。

b. 输出时间和日期。

c. 输出当前工作目录。

d. 列出父目录中的所有目录文件。

e. 打印正在使用的 shell 的名称。

f. 打印包含你的登录名的密码文件中的一行。

g. 打印你的用户 ID。

h. 打印此机器的名称。

i. 打印你的磁盘使用情况。

j. 打印本月的日历。

k. 向用户告别并以非军用时间打印小时。

# LAB 41: VARIABLE EXPANSION OF SUBSTRINGS

1. 编写一个脚本执行以下操作：

a. 设置一个名为 `mypath` 的变量为你的主目录。

b. 打印 `mypath` 的值。

c. 仅打印 `mypath` 中路径的最后一个元素。

d. 打印 `mypath` 中路径的第一个元素。

e. 打印变量 `mypath` 中除最后一个元素外的所有内容。

# LAB 42: THE lookup SCRIPT

1. 如果 CD 上未为你提供，请创建一个名为 `datafile` 的文件。它将由冒号分隔的字段组成：

a. 名字和姓氏

b. 电话号码

c. 地址（街道、城市、州和邮政编码）

d. 出生日期（04/12/66）

e. 薪资

2. 在你的文件中放入十个条目。编写一个名为 `lookup` 的脚本执行以下操作：

a. 欢迎用户。

b. 打印 `datafile` 中所有用户的姓名和电话号码。

c. 打印 `datafile` 中的行数。

d. 向用户告别。

# LAB 43: USING typset

1. 编写一个脚本执行以下操作：

a. 提示用户输入他的或她的名字和姓氏。

b. 将答案存储在两个变量中。

c. 使用新的 `ksh read` 命令。

2. 使用 `setenv` 命令将名字和姓氏变量转换为全小写字母。

3. 测试此人的姓名是否为 Tom Jones。如果是，打印 Welcome, Tom Jones；如果不是，打印，Are you happy today, `$FIRSTNAME $LASTNAME`？（用户的名字和姓氏转换为大写字母。）

4. 让用户输入对该问题的回答，并使用新的 `ksh test` 命令查看答案是否为 yes 或 no。如果是，让你的脚本对他或她说些好听的话，如果不是，告诉用户回家并给出当前时间。

5. 重写 `lookup` 脚本。

a. 脚本将询问用户是否希望向 `datafile` 添加一个条目。

b. 如果用户回答 yes 或 y，请要求以下输入：

Name

Phone number

Address

Birth date

Salary

每个项目的变量将被分配用户输入。

### EXAMPLE

```
print -n "What is the name of the person you are adding to the file?"
read name The information will be appended to the datafile.
```

# LAB 44: THE if/else CONSTRUCT AND THE let COMMAND

1. 编写一个名为 `grades` 的脚本，它将询问用户他在测试中的数字成绩。

a. 脚本将测试成绩是否在可能的成绩范围内，0 到 100。

b. 脚本将告诉用户他或她是否获得 A、B、C、D 或 F。

2. 编写一个名为 `calc` 的脚本，它将执行简单计算器的功能。脚本将提供一个简单的菜单：

[a] Add

[s] Subtract

[m] Multiply

# LAB 47: AUTOLOADING FUNCTIONS

Steps for autoloading a function:

1. 创建一个名为 `myfunctions` 的目录。

2. 更改目录到 `myfunctions` 并使用编辑器创建一个名为 `good-bye` 的文件。

3. 在 `good-bye` 文件中插入一个名为 `good-bye` 的函数，拼写与文件名完全相同。

4. `good-bye` 函数包含：

5. 编写并退出编辑器。你现在有一个包含与文件名相同名称的函数的文件。

6. 进入你的主目录。通过键入以下行在编辑器中修改 `.kshrc` 文件：

7. 退出编辑器，并使用点命令在当前环境中执行 `.kshrc`。

8. 在你在 Lab 45 中编写的 `timegreet` 脚本中，包含以下行：

9. 运行 `timegreet` 脚本。`good-bye` 函数输出将会出现。

10. 为 `lookup` 脚本中的每个菜单项创建函数。将函数存储在名为 `lookup_functions` 的文件中，该文件位于名为 `myfunctions` 的目录中。

11. 在你的 `lookup` 脚本中自动加载函数并为相应的 case 做出函数调用。
