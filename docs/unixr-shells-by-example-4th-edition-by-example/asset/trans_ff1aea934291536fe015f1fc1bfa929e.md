

4. 尝试使用 echo 和 verbose 命令来调试你的脚本。你是如何使用这些命令的？

## LAB 29: 命令行参数

- 1. 编写一个名为 rename 的脚本，其功能如下：
  - a. 将两个文件名作为命令行参数接收；第一个文件是旧文件，第二个文件是新文件。
  - b. 将旧文件名重命名为新文件名。
  - c. 列出目录中的文件以显示更改。

- 2. 编写一个名为 checking 的脚本，其功能如下：
  - a. 接收一个命令行参数，即用户的登录名。
  - b. 测试是否提供了命令行参数。
  - c. 检查用户是否在 /etc/passwd 文件中。如果是，打印以下内容：
    Found <user> in the /etc/passwd file.
    否则，打印以下内容：
    No such user on our system.

## LAB 30: 条件语句和文件测试

- 1. 在 lookup 脚本中，询问用户是否希望向 datafile 添加一个条目。如果回答是或 y：
  - a. 提示用户输入新的姓名、电话、地址、出生日期和薪水。每个项目将存储在单独的变量中。你将在字段之间提供冒号并将信息追加到 datafile。
  - b. 按姓氏对文件进行排序。告诉用户你已添加该条目，并显示添加的行，其前面加上行号。

- 2. 重写 Lab 29 中的 checking。 在检查指定用户是否在 /etc/passwd 文件中之后，程序将检查他或她是否已登录。如果是，程序将打印正在运行的所有进程；否则将向用户显示以下信息：
  <user> is not logged on.

- 3. lookup 脚本依赖 datafile 才能运行。在 lookup 脚本中，检查 datafile 是否存在且可读可写。

- 4. 为 lookup 脚本添加一个菜单，使其类似于以下内容：
  [1] Add entry
  [2] Delete entry
  [3] View entry
  [4] Exit

- 5. 你已经编写了脚本的 Add entry 部分。Add entry 例程现在应包含代码来检查姓名是否已存在于 datafile 中，如果存在，则通知用户。如果姓名不存在，则添加新条目。

- 6. 现在编写 Delete entry、View entry 和 Exit 函数的代码。

- 7. Delete entry 部分的脚本应首先检查条目是否存在，然后再尝试删除它。如果条目不存在，请通知用户；否则，删除条目并告诉用户你已删除它。在 Exit 时，确保使用数字表示适当的退出状态。

- 8. 你如何从命令行检查退出状态？

## LAB 31: switch 语句

- 1. 使用 switch 语句重写以下脚本：

```
#!/bin/csh -f
# Grades program
echo -n "What was your grade on the test? "
set score = $<
if ( $grade >= 90 && $grade <= 100 ) then
echo You got an A!
else if ( $grade >= 80 && $grade <= 89 ) then
echo You got a B.
else if ( $grade >= 70 && $grade <= 79 ) then
echo You're average.
else if ( $grade >= 60 && $grade <= 69 ) then
echo Better study harder
else
echo Better luck next time.
endif
```

- 2. 使用 switch 语句为每个菜单项重写 lookup 脚本。

## LAB 32: 循环

- 1. 编写一个名为 picnic 的程序，该程序将逐一向用户列表发送野餐邀请。用户列表将位于名为 friends 的文件中。friends 文件中列出的用户之一将是 Popeye。

Bonus: 如果你有时间，可以自定义你的邀请文件，以便每个用户收到包含其姓名的信件。例如，消息可能以以下内容开头：

```
Dear John,
I hope you can make it to our picnic....
```

为此，你的邀请文件可以这样写：

```
Dear XXX,
I hope you can make it to our picnic....
```

然后使用 sed 或 awk 将 XXX 替换为用户名。 （将用户名中的大写字母放入其中可能很棘手，因为用户名始终为小写。）

- 2. 在 lookup 脚本中添加一个新菜单项，使其类似于以下内容：
  [1] Add entry
  [2] Delete entry
  [3] Change entry
  [4] View entry
  [5] Exit

用户选择有效条目后，函数完成后，询问用户是否希望再次查看菜单。如果输入无效条目，程序应打印以下内容：

```
Invalid entry, try again.
```

菜单将被重新显示。

- 3. 在 lookup 脚本的 View entry 下创建一个子菜单。用户将被询问是否希望查看所选个人的特定信息：
  + a) Phone
  + b) Address
  + c) Birth date
  + d) Salary

- 4. 使用标签向你的脚本添加 onintr 命令。当程序在标签处开始执行时，任何临时文件都将被删除，用户将被告知 Good-bye，并且程序将退出。

