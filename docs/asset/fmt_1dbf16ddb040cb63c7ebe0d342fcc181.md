
`echo -e "Please enter the name of the family member --> "`

`read NAME`

`echo -e "Please enter the family member's relation to you\n(i.e. mother) --> "`

`read RELATION`

`echo -e "Please enter the family member's telephone number --> "`

`read PHONE`

`echo "$NAME\t$RELATION\t$PHONE" >> database`

![](img/8fe037bf1ed016dccb79dbd1a27184f2_390_0.png)

4. 在命令提示符下，输入 `chmod u+x myscript2` 并按回车。接下来在命令提示符下输入 `./myscript2` 并按回车。根据你某个家庭成员的信息回答问题。

5. 在命令提示符下，输入 `cat database` 并按回车。步骤4中的条目是否存在？为什么？

6. 多次执行步骤4，以向数据库文件中填充条目。

7. 在命令提示符下，输入 `vi myscript2` 并按回车。编辑 `myscript2` shell 脚本内部的文本：

```bash
#!/bin/bash

echo -e "Would you like to add an entry to the family database
file?"
read ANSWER1

if [ $ANSWER1 = "y" -o $ANSWER1 = "y" ]
then
echo -e "Please enter the name of the family member --> \c"
read NAME
echo -e "Please enter the family member's relation to you
(i.e. mother)-->\c"
read RELATION
echo -e "Please enter the family member's telephone number"
read PHONE
echo "$NAME\t$RELATION\t$PHONE >> database"
fi

echo -e "Would you like to search for an entry in the family
database file?"
read ANSWER2

if [ $ANSWER2 = "y" -o $ANSWER2 = "y" ]
then
echo "What word would you like to look for? --> \c"
read WORD
grep "$WORD"
fi
```

8. 在命令提示符下，输入 `./myscript2` 并按回车。当提示向数据库输入条目时，选择 `y` 并按回车。根据你某个家庭成员的信息回答问题。回答 `y` 并按回车。接下来，当提示搜索数据库时，搜索你几秒钟刚输入的名称。它在那里吗？

9. 在命令提示符下，输入 `./myscript2` 并按回车。当提示向数据库输入条目时，选择 `n` 并按回车。接下来，当提示搜索数据库时，搜索你在步骤6中之前输入的名称。它在那里吗？

10. 在命令提示符下，输入 `vi myscript2` 并按回车。编辑 `myscript2` shell 脚本内部的文本：

## 动手实践项目 375

```bash
#!/bin/bash

echo -e "What would you like to do?
Add an entry (a)
Search an entry (s)
Enter your choice (a/s)-->\c"
read ANSWER

case $ANSWER in
  a|A) echo -e "Please enter the name of the family member\n-->\c"
    read NAME
    echo -e "Please enter the family member's relation to\ny (i.e. mother)-->\c"
    read RELATION
    echo -e "Please enter the family member's telephone\nnumber -->\c"
    read PHONE
    echo "$RELATION\$PHONE" >> database
  s|S) echo "What word would you like to look for? -->\c"
    read WORD
    grep "$WORD" database
*) echo "You must enter either the letter a or s."
esac
```

- 1. 在命令提示符下，输入 `./myscript` 并按**回车**。选择 `y` 并按**回车**。你收到了什么错误信息？为什么？

- 2. 在命令提示符下，输入 `./myscript` 并按**回车**。选择 `a` 并按**回车**。输入另一个家庭成员的信息。在之前的提示符中输入 `a` 还是 `A` 有区别吗？

- 3. 在命令提示符下，输入 `./myscript` 并按**回车**。选择 `s` 并按**回车**。搜索步骤12中之前输入的家庭成员。在之前的提示符中输入 `s` 还是 `S` 有区别吗？为什么？

- 4. 在命令提示符下，`vi myscript3` 并按**回车**，在主目录下创建一个名为 `myscript3` 的新文件。

- 5. 将以下文本输入 `myscript3` 文件。完成后，保存并退出编辑器。

- 6. 在命令提示符下，输入 `chmod +x myscript3` 并按**回车**。接下来在命令提示符下输入 `./myscript3` 并按**回车**。当提示文件名时，输入 `/etc/hosts` 并按**回车**。`stuff` 目录是否成功创建？为什么？`/etc/hosts` 文件是否成功复制到 `stuff` 目录？为什么？

# 第8章 使用 Shell

17. 在命令提示符下，输入 `./myscript3` 并按回车。当提示向数据库输入条目时，选择 `y` 并按回车。根据你某个家庭成员的信息回答问题。回答 `y` 并按回车。接下来，当提示搜索数据库时，搜索你几秒钟刚输入的名称。它在那里吗？

18. 在命令提示符下，输入 `./myscript3` 并按回车。当提示向数据库输入条目时，选择 `n` 并按回车。接下来，当提示搜索数据库时，搜索你在步骤6中之前输入的名称。它在那里吗？

# 发现练习

- 1. 在命令提示符下，输入 `./myscript` 并按回车。选择 `y` 并按**回车**。你收到了什么错误信息？为什么？

- 2. 在命令提示符下，输入 `./myscript` 并按回车。选择 `a` 并按**回车**。输入另一个家庭成员的信息。在之前的提示符中输入 `a` 还是 `A` 有区别吗？

- 3. 在命令提示符下，输入 `./myscript` 并按回车。选择 `s` 并按**回车**。搜索步骤12中之前输入的家庭成员。在之前的提示符中输入 `s` 还是 `S` 有区别吗？为什么？

- 4. 在命令提示符下，`vi myscript3` 并按**回车**，在主目录下创建一个名为 `myscript3` 的新文件。

- 5. 将以下文本输入 `myscript3` 文件。完成后，保存并退出编辑器。

- 6. 在命令提示符下，输入 `chmod +x myscript3` 并按**回车**。接下来在命令提示符下输入 `./myscript3` 并按**回车**。当提示文件名时，输入 `/etc/hosts` 并按**回车**。`stuff` 目录是否成功创建？为什么？`/etc/hosts` 文件是否成功复制到 `stuff` 目录？为什么？

5. 检查显示的 `/root/.bash_profile` 文件。根据本章介绍的信息，描述每行代码的作用。

```bash
# .bash_profile

# 获取别名和函数

if [ -f ~/.bashrc ]; then
  source ~/.bashrc
fi

# 用户特定环境和启动程序

PATH=$PATH:$HOME/bin
BASH_ENV=$HOME/.bashrc
USERNAME="root"
```

6. 编写一个包含注释的 shell 脚本。它应该执行以下任务：

   a. 显示当前登录的用户列表
   b. 显示系统主机名
   c. 显示时间和日期
   d. 显示磁盘占用
   e. 显示当前工作目录
   f. 显示 BASH shell 的路径

7. 编写一个 shell 脚本提示用户输入 0 到 100 之间的成绩。该脚本应根据以下标准计算该成绩对应的字母：

```
0–49 = F
50–59 = D
60–69 = C
70–79 = B
```
