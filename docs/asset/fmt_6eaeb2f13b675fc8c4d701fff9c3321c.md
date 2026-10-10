
5. 查询数据库时，以下语句从名为 `users` 的表中检索所有数据？

-   A. `SELECT ALL FROM users;`
-   B. `QUERY ALL FROM users;`
-   C. `SELECT * FROM Users;`
-   D. `SELECT * FROM users;`

6. 以下哪项对 `PS1` 变量的描述最准确？

-   A. `PS1` 用于设置命令的位置。
-   B. `PS1` 用于定义 `Bash` 的默认 shell提示符。
-   C. `PS1` 作为系统变量使用。
-   D. `PS1` 是用户定义的没有默认值。

7. 以下哪个命令在执行 `ls` 命令时不带选项时确保使用了 `-la` 选项？

-   A. `alias ls="ls -la"`
-   B. `ln -s ls -la`
-   C. `alias "ls -la"=ls`
-   D. `set ls`

8. 登录 `Bash` shell 时配置文件的顺序是什么？

-   A. `.bash_login`, `.profile`, `/etc/profile`
-   B. `.bash_profile`, `.profile`, `.bash_login`
-   C. `.profile`, `.bash_login`, `.bash_profile`
-   D. `.bash_login`, `.bash_profile`, `.profile`

9. `Bash` 脚本中的哪个变量用于访问第一个参数？

-   A. `$ARG`
-   B. `$0`
-   C. `$1`
-   D. `$@`

10. 以下哪个符号为 `Bash` 脚本中的 `if` 条件提供结束标志？

-   A. `ex`
-   B. `}`
-   C. `]`
-   D. `fi`

11. 以下哪个命令将删除 `MySQL` 中名为 `virtualusers` 的表的所有数据？

-   A. `DELETE FROM VIRTUAL;`
-   B. `DELETE FROM virtualusers;`
-   C. `DELETE * FROM virtualusers;`
-   D. `DELETE ALL FROM virtualusers;`

12. 以下哪个命令显示指定表的列和列类型？

-   A. `DESC`
-   B. `ASK`
-   C. `SELECT`
-   D. `DISPLAY`

# 第一部分 CompTIA Linux+/LPIC-1

13. 以下哪个命令将打印从 0 开始的六个数列表？

-   A. `list 0-5`
-   B. `seq 1 5`
-   C. `echo 0-5`
-   D. `seq 1 6`

14. 创建脚本时，使用哪个命令显示变量的内容？

-   A. `var_dump`
-   B. `echo`
-   C. `ls`
-   D. `env`

15. 一个命令通过 `ls -la` 获取了如下列表：

```
-rwsr-xr-x 1 user user 21 Nov 2 13:53 script.sh
```

列表中用户权限中的 `s` 表示什么？

-   A. 该程序设置了 `SUID` 标志位。
-   B. 这是一个符号链接。
-   C. 该文件将不可执行。
-   D. 该文件是一个特殊的系统文件。

16. 以下哪个命令将在执行脚本后退出 shell？

-   A. `run`
-   B. `source`
-   C. `./`
-   D. `exec`

17. 哪种字符序列只有在第一个命令成功退出时执行两个命令？

-   A. `&*`
-   B. `&&`
-   C. `;`
-   D. `&`

18. Shell 脚本中的哪个命令等待用户输入并将输入放入变量中？

-   A. `exec`
-   B. `get`
-   C. `read`
-   D. `prompt`

# 第 5 章 使用 Shell、脚本和数据管理 (领域 105)

19. 使用什么字符在 shell 脚本中将命令序列标记为函数？

-   A. 使用括号声明函数（可选），使用花括号包含命令
-   B. 使用花括号声明函数，使用括号包含命令
-   C. 使用方括号声明函数，使用花括号包含命令
-   D. 使用引号表示函数

20. 假设你从 `MySQL` 数据库检索数据，并根据名为“`id`”的列按数字升序显示。在 `SELECT` 语句中添加以下哪个命令可以完成任务？

-   A. `ORDER BY id ASC;`
-   B. `ORDER BY id;`
-   C. `GROUP BY id;`
-   D. `GROUP BY ASC;`

21. 字符字符表示在前一个命令未成功退出时执行替代命令？

-   A. `&&`
-   B. `--`
-   C. `||`
-   D. `EL`

22. 哪个关键词用于启动 `Bash` 脚本中的备选条件？

-   A. `if`
-   B. `else if`
-   C. `elif`
-   D. `elsif`

23. 以下哪个命令移除当前定义的别名命令？

-   A. `remove`
-   B. `rm`
-   C. `unalias`
-   D. `delete`

24. 在 `Bash` 中 `source` 文件时，假设你的当前用户拥有该文件，哪个 `chmod` 命令将提供最小权限以确保文件被正确 `source`？

-   A. `chmod 600`
-   B. `chmod 755`
-   C. `chmod 777`
-   D. `chmod 400`

25. 假设一个用空格分隔的数值列表定义为 `LIST="one two three four"`，以下哪种 `for` 循环结构将遍历列表中的元素？

-   A. `for LIST`
-   B. `for VAR in LIST`
-   C. `for VAR in $LIST`
-   D. `for $LIST -> $VAR`

26. 在 `SQL` 中看到类似 `table1.id = table2.id` 的语句时，将使用哪种类型的连接（`join`）？

-   A. 内连接 (Inner)
-   B. 外连接 (Outer)
-   C. 左外连接 (Left outer)
-   D. 右外连接 (Right outer)

27. Shell 脚本循环中的哪种测试将检查一个值是否小于另一个值？

-   A. `-less`
-   B. `-lessThan`
-   C. `-lt`
-   D. `-than`

28. 下列哪个测试可以判断 shell 脚本上下文中文件是否存在？

-   A. `-a`
-   B. `-e`
-   C. `-m`
-   D. `-i`

29. 应该将文件放在哪个目录下，以便在创建用户时将这些文件自动复制到用户的家目录？

-   A. `/etc/userhome`
-   B. `/etc/templateuser`
-   C. `/etc/skel`
-   D. `/home/skel`

30. 下列哪项代表 `SQL` `UPDATE` 语句的正确语法？

-   A. `UPDATE <table> SET <column> = <newvalue> WHERE <column> = <value>`
-   B. `UPDATE <table> WHERE <column> = <newvalue>`
-   C. `UPDATE WHERE <column> = <newvalue>`
-   D. `UPDATE FROM <table> VALUE (<value>)`

# 第 5 章 使用 Shell、脚本编写和数据管理（领域 105）

31. 假设一个名为 `AUTHENTICATION` 的 `MySQL` 表有三列（`id`, `username`, `password`）。下列哪条语句向表中插入一行数据？

-   A. `INSERT id,username,password INTO AUTHENTICATION;`
-   B. `INSERT INTO AUTHENTICATION VALUES ('user','pass');`
-   C. `INSERT INTO AUTHENTICATION ('','user','pass');`
-   D. `INSERT INTO AUTHENTICATION (username,password) VALUES ('user','pass');`

32. `Bash` 的哪个选项将导致 shell 在不读取初始化文件的情况下执行？

-   A. `--no-rc`
-   B. `--no-init`
-   C. `--norc`
-   D. `--rc-none`

33. 下列哪项在 `bash` 脚本中用于创建一个数组？

-   A. `ARRAY=(val1 val2)`
-   B. `ARRAY="val1 val2"`
-   C. `ARRAY_PUSH($ARRAY,"val1","val2");`
-   D. `ARRAY{} = "val1"`

34. `declare` 语句的哪个选项以一种可以作为另一个命令输入的方式显示输出？

-   A. `-o`
-   B. `-n`
-   C. `-p`
-   D. `-m`

35. 你需要创建一个函数，该函数在每次登录系统时都可用。该函数应该放在哪个文件中？

-   A. `.bash_profile`
-   B. `.rc`
-   C. `/etc/profile`
-   D. `.bash_run`

36. 哪个 shell 内置命令用于显示只读变量列表？

-   A. `ro`
-   B. `readonly`
-   C. `env-ro`
-   D. `ro-env`

37. 下列哪个 `SQL` 关键字可以与 `GROUP BY` 子句一起使用？

-   A. `SELECT`
-   B. `INSERT`
-   C. `UPDATE`
-   D. `DELETE`

38. 使用哪些字符来表示 shell 脚本中 `while` 循环测试部分的开始和结束？

-   A. 括号 `( )`
-   B. 花括号 `{ }`
-   C. 方括号 `[ ]`
-   D. 双引号 `""`

39. 当使用带有一个参数的 `test` 内置命令时，如果其参数不为空，则返回值将是什么？

-   A. `false`
-   B. `true`
-   C. `unknown`
-   D. `-1`

40. 当使用波浪号字符切换目录（如 `cd ~`）时，使用的是哪个环境变量？

-   A. `HOMEDIR`
-   B. `HOMEPATH`
-   C. `HOME`
-   D. `MAILPATH`

41. 如果你想在用户一段时间未活动后自动将其注销 shell，可以设置哪个环境变量？

-   A. `TIMEOUT`
-   B. `TMOUT`
-   C. `TO`
-   D. `IDLETIME`

42. 在 shell 脚本中使用 `case` 语句时，哪种序列表示 `case/switch` 语句的结束？

-   A. `caseend`
-   B. `esac`
-   C. `endcase`
-   D. `}`
