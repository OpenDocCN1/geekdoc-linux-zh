
该地址将你连接到全面 Perl 归档网络 (`CPAN`)—实际上，它连接到离你最近的 `CPAN` 站点，你可以下载包含 Perl 内置函数概述的页面。点击函数名称查看有关该函数的详细信息。

| 表 24-3 Perl 函数快速参考指南 |
| 函数调用 | 描述 |
| --- | --- |
| `abs(VALUE)` | 返回参数的绝对值 |
| `accept(NEWSOCKET, GENERICSOCKET)` | 在 socket 上等待连接 |
| `alarm(SECONDS)` | 在指定的秒数后发送警报信号 |
| `atan2(Y,X)` | 返回 Y/X 的反正切 |
| `bind(SOCKET, NAME)` | 为已打开的 socket 关联名称 |
| `binmode(FILEHANDLE)` | 将文件处理为二进制文件 |
| `bless(REF, PACKAGE)` | 使引用项成为包中的一个对象 |
| `caller(EXPR)` | 返回关于子程序调用的信息 |
| `cd(EXPR)` | 将目录更改为 EXPR 指定目录 |
| `chmod(LIST)` | 更改一组文件的权限 |
| `chomp(VARIABLE)` | 移除与特殊变量 `$` 当前值匹配的末尾字符 |
| `chop(VARIABLE)` | 切掉最后一个字符（用于移除字符串末尾的换行符） |
| `chown(LIST)` | 更改一组文件的所有者 |
| `chr(NUMBER)` | 返回 ASCII 代码为 NUMBER 的字符 |
| `chroot(FILENAME)` | 将根目录更改为指定的 FILENAME |
| `close(FILEHANDLE)` | 关闭指定的文件 |
| `closedir(DIRHANDLE)` | 关闭由 opendir 打开的目录 |
| `connect(SOCKET, NAME)` | 初始化连接 |
| `cos(EXPR)` | 返回 EXPR 的余弦 |
| `crypt(PLAINTEXT, SALT)` | 加密字符串 |

| 表 24-3 DM 续 |
| 函数调用 | 描述 |
| --- | --- |
| `dbmopen(ASSOC, NAME, MODE)` | 将数组与 DBM 文件关联 |
| `dbmclose(ASSOC)` | 解除关联 |
| `defined(EXPR)` | 如果 EXPR 定义则返回真 |
| `delete $ASSOC{KEY}` | 从关联数组中删除值 |
| `die(LIST)` | 打印错误并退出 |
| `dump(LABEL)` | 产生转储 |
| `each(ASSOC)` | 返回关联数组的下一个键值对 |
| `getrent` | 从 `/etc/group` 获取组信息 |
| `getgrgid(GID)` | 根据组 ID查找组文件项 |
| `getgrnam(NAME)` | 根据组名查找组文件项 |
| `getpeername(SOCKET)` | 返回 socket 另一端的地址 |
| `getlogin` | 返回当前登录信息 |
| `eof(FILEHANDLE)` | 如果到达文件末尾返回真 |
| `eval(EXPR)` | 像执行子程序一样执行 EXPR |
| `exec(LIST)` | 运行另一个程序 |
| `exists($KEY)` | 如果关联数组存在指定的键则返回真 |
| `exit(EXPR)` | 退出 Perl 程序 |
| `exp(EXPR)` | 返回 EXPR 的次方 |
| `cntl(FILEHANDLE, FUNCTION, SCALAR)` | 对文件执行各种控制操作 |
| `fileno(FILEHANDLE)` | 返回文件句描述符 |
| `flock(FILEHANDLE, OPERATION)` | 锁定文件以防其他进程访问单个文件 |
| `fork` | 创建子进程并返回子 ID |
| `format NAME = picture line list` | 定义用于写入函数的输出格式 |
| `forml(PICTURE, LIST)` | 根据 PICTURE 格式化值列表 |
| `getc(FILEHANDLE)` | 从文件读取下一个字符 |
| `getgrp(PID)` | 返回指定进程 ID 的当前进程组 |
| `getppid` | 返回父进程的进程 ID |
| `getpriority(WHICH, WHO)` | 返回进程的当前优先级 |
| `getprotobyname(NAME)` | 将协议名称转换为数字 |
| `getprotynumber(NUMBER)` | 将协议数字转换为名称 |
| `getprotoent` | 从 UNIX 的 `/etc/networks` 获取网络协议信息 |
| `getpwent` | 从密码文件 (UNIX 中的 `/etc/passwd`) 获取项 |

| 表 24-3 (续) |
| 函数调用 | 描述 |
|---|------|
| `getpwam(NAME)` | 将用户名转换为密码文件中的对应条目 |
| `getpuid(UID)` | 将数字用户 ID转换为密码文件中的对应条目 |
| `getservname(NAME, PROTO)` | 将服务（端口）名称转换为相应的端口号 |
| `getservbyport(PORT, PROTO)` | 将服务（端口）号转换为名称 |
| `getservent` | 从 UNIX 的 `/etc/services` 文件获取条目 |
| `getsockname(SOCKET)` | 返回套接字此端的地址 |
| `getsockopt(SOCKET, LEVEL, OPTNAME)` | 返回请求的套接字选项 |
| `glob(EXPR)` | 返回对应通配符表达式的文件 |
| `gmtime(EXPR)` | 将二进制时间转换为格林威治标准时间 (GMT) 的九元素列表 |
| `goto(LABEL)` | 跳转到由 LABEL 标识的语句 |
| `grep(EXPR, LIST)` | 在 LIST 中搜索表达式出现的次数 |
| `hex(EXPR)` | 返回十六进制 EXPR 对应的十进制值 |
| `index(STR, SUBSTR, POSITION)` | 返回字符串首次出现的位置（搜索从 POSITION 指定的字符位置开始） |
| `int(EXPR)` | 返回 EXPR 的整数部分 |
| `ioctl(FILEHANDLE, FUNCTION, SCALAR)` | 控制各个各个方面 |
| `join(EXPR, LIST)` | 通过连接列表元素返回单个字符串 |
| `keys(ASSOC_ARRAY)` | 返回关联数组的键数组 |
| `kill(LIST)` | 向进程列表发送信号 |
| `last(LABEL)` | 退出由 LABEL 标识的循环 |
| `lc(EXPR)` | 返回 EXPR 的小写版本 |
| `lcfirst(EXPR)` | 将 EXPR 的第一个字符改为小写后返回 EXPR |

## 第 24 章：Shell 和 Perl 脚本

| 函数调用 | 描述 |
|--- |--- |
| `length(EXPR)` | 返回字符数 |
| `link(OLDFILE, NEWFILE)` | 创建 NEWFILE 作为 OLDFILE 的链接 |
| `listen(SOCKET, QUEUESIZE)` | 在套接字上等待传入的连接 |
| `local(LIST)` | 使列表中的变量对子程序局部 |
| `localtime(EXPR)` | 将二进制时间转换为本地时间的九元素列表 |
| `log(EXPR)` | 返回 EXPR 的对数（以 e 为底） |
| `stat(FILEHANDLE)` | 返回文件的统计信息（如果文件指向符号链接，则返回符号链接的信息） |
| `m/PATTERN/g` | 执行模式匹配 |
| `map(EXPR, LIST)` | 对 LIST 中的每个项求表达式 EXPR |
| `mkdir(FILENAME, MODE)` | 创建 FILENAME指定的目录 |
| `msgctl(ID, CMD, ARG)` | 对消息队列执行消息控制操作 |
| `msget(KEY, FLAGS)` | 获取对应 KEY 的消息队列标识符 |
| `msgrcv(ID, VAR, SIZE, TYPE, FLAGS)` | 从消息队列标识符 ID 接收消息 |
| `msgsnd(ID, MSG, FLAGS)` | 向消息队列标识符 ID 发送消息 |
| `my(EXPR)` | 在子程序或大括号 {... 包围的块声明一个或多个私有变量 |
| `next(LABEL)` | 开始由 LABEL 标识的循环的下次迭代 |
| `no(Module LIST)` | 停止使用 Perl 模块 |
| `oct(EXPR)` | 返回 EXPR 中八进制数的十进制等价值 |
| `open(FILEHANDLE, EXPR)` | 打开名为 EXPR 的文件，并将该文件与 FILEHANDLE 关联 |
| `opendir(DIRHANDLE, EXPR)` | 打开名为 EXPR 的目录，并将该目录与 DIRHANDLE 关联 |
| `ord(EXPR)` | 返回 EXPR 中第一个字符的 ASCII 码 |

## 表 24-3 (续)

| 函数调用 | 描述 |
|---|---|
| `pack(TEMPLATE, LIST)` | 取值列表并返回包含结构的字符串（TEMPLATE 指定打包方式） |
| `pipe(READHANDLE, WRITEHANDLE)` | 打开用于读写的管道 |
| `pop(ARRAY)` | 移除并返回数组的最后一个元素 |
| `pos(SCALAR)` | 返回上一次模式匹配的位置（执行全局搜索 /PATTERN/g 时适用） |
| `print(FILEHANDLE, LIST)` | 向 FILEHANDLE 标识的文件打印项列表 |
| `printf(FILEHANDLE, LIST)` | 格式化输出到文件 |
| `push(ARRAY, LIST)` | 将 LIST 中的值追加到 ARRAY 的末尾 |
| `q/STRING/` | 处理 STRING，替换变量名（类似于单引号字符串） |
| `qq/STRING/` | 处理 STRING，替换变量名（类似于双引号字符串） |
| `quotemeta(EXPR)` | 为正则表达式中特殊意义的所有字符添加反斜杠前缀后返回 EXPR 的值 |
| `qw/STRING/` | 单词列表（类似于圆括号） |
| `qx/STRING/` | 执行命令（类似于反引号） |
| `rand(EXPR)` | 返回 0 到 EXPR 之间的随机值 |
| `read(READHANDLE, SCALAR, LENGTH)` | 从文件读取指定的字节数 |
| `readdir(DIRHANDLE)` | 从目录句柄读取目录条目 |
| `readlink(EXPR)` | 返回符号链接指向的文件名 |
| `recv(SOCKET, SCALAR, LEN)` | 从套接字接收消息 |
| `redo(LABEL)` | 重启由 LABEL 标识的循环 |
| `ref(EXPR)` | 如果 EXPR 是引用则返回真（对象的引用） |
| `rename(OLDNAME, NEWNAME)` | 将 OLDNAME 改名为 NEWNAME |

## 第 24 章：Shell 和 Perl 脚本

| 函数调用 | 描述 |
|--- |--- |
| `require(FNAME)` | 包含名为 FNAME 的模块 |
| `reset(EXPR)` | 清除全局变量 |
| `return(LIST)` | 从子程序返回列表 |
| `reverse(LIST)` | 反转元素的顺序 |
| `rewind(DIRHANDLE)` | 将目录句柄重置为开头 |
| `index(STR, SUBSTR)` | 返回 SUBSTR 在 STR 中的位置 |
| `index(STR, SUBSTR, POSITION)` | 返回字符串首次出现的位置（搜索从 POSITION 指定的字符位置开始） |
| `index(STR, SUBSTR, POSITION)` | 返回首次出现... |
| `rmdir(FILENAME)` | 删除 FILENAME指定的目录 |
| `s/PATTERN/g` | 执行模式匹配 |
| `scalar(EXPR)` | 在标量上下文求表达式 EXPR |
| `seek(FILEHANDLE, POSITION)` | 将文件句柄移动到位置 |
| `seek(DIRHANDLE, POSITION)` | 将目录句柄移动到位置 |
| `select(FILEHANDLE, BITS, TIMEOUT)` | 检查是否有更多文件已准备好输入 |
| `semctl(ID, CMD, ARG)` | 控制共享内存设置，如权限 |
| `semget(KEY, SIZE, FLAGS)` | 分配共享内存段 |
| `semop(KEY, OPSTRING)` | 执行信号操作 |
| `send(SOCKET, MSG, FLAGS)` | 向套接字发送消息 |
| `setgroup(PID, PGRP)` | 设置进程组 |
| `sethostent(STOPEN)` | 打开主机数据库（UNIX 中的 `/etc/hosts` 文件） |
| `setnetent(STOPEN)` | 打开网络数据库（UNIX 中的 `/etc/networks` 文件） |
| `setpwent` | 打开 UNIX 中的 `/etc/passwd` 文件 |
| `setservent(STOPEN)` | 打开 UNIX 中的 `/etc/services` 文件 |
| `setsockopt(SOCKET, LEVEL, OPTNAME, OPTVAL)` | 设置指定的套接字选项 |
| `setgrp(NAME)` | 设置 `/etc/group` 中的组信息 |
| `setpriority(WHICH, WHO, PRIORITY)` | 为进程设置优先级 |
| `setprotoent(STOPEN)` | 打开协议数据库（UNIX 中的 `/etc/protocols` 文件） |
| `shift(ARRAY)` | 移除并返回数组的第一个值 |
| `shmctl(ID, CMD, ARG)` | 控制共享内存设置，如权限 |
| `shmget(KEY, SIZE, FLAGS)` | 分配共享内存段 |
| `shmread(ID, VAR, POS, SIZE)` | 从 ID 标识的共享内存段读取 |
| `shmwrite(ID, STRING, POS, SIZE)` | 向 ID 标识的共享内存段写入 |
| `shutdown(SOCKET, HOW)` | 关闭套接字连接 |
| `sin(EXPR)` | 返回 EXPR 指定角的正弦（弧度） |
| `sleep(EXPR)` | 睡眠 EXPR 秒 |
| `socket(SOCKET, DOMAIN, TYPE, PROTOCOL)` | 为指定类型打开套接字并附加到文件句柄 SOCKET |
| `socketpair(SOCKET1, SOCKET2, DOMAIN, TYPE, PROTOCOL)` | 创建一对未命名的套接字 |
| `sort(LIST)` | 对列表进行排序并返回数组 |
| `splice(ARRAY, OFFSET, LENGTH, LIST)` | 替换 ARRAY 中的元素 |
| `split(/PATTERN/, EXPR, LIMIT)` | 将 EXPR 拆分为字符串数组 |
| `sprintf(FORMAT, LIST)` | 返回一个包含按格式格式化的 LIST 元素的字符串 |

# 第 24 章：Shell 与 Perl 脚本 759

| 函数调用 | 描述 |
| --- | --- |
| `sqrt(EXPR)` | 返回 EXPR 的平方根 |
| `srand(EXPR)` | 设置随机数生成的种子 |
| `stat(FILEHANDLE)` | 返回一个包含文件统计信息的 13 元素列表 |
| `study(STRING)` | 对 STRING 进行处理，以便后续对字符串进行多次模式匹配 |
| `substr(EXPR, OFFSET, LEN)` | 从字符串 EXPR 中返回子字符串 |
| `symlink(OLDFILE, NEWFILE)` | 创建 NEWFILE，作为指向 OLDFILE 的符号链接 |
| `syscall(LIST)` | 调用 LIST 第一个元素指定的系统函数（并将后续列表元素作为参数传递） |
| `sysopen(FILEHANDLE, FILENAME, MODE, PERMS)` | 打开名为 FILENAME 的文件并将其与 FILEHANDLE 关联 |
| `sysread(FILEHANDLE, SCALAR, LENGTH, OFFSET)` | 从文件中读取指定数量的字节 |
| `system(LIST)` | 执行 LIST 中的 shell 命令 |
| `syswrite(FILEHANDLE, SCALAR, LENGTH, OFFSET)` | 向文件写入指定数量的字节 |
| `tell(FILEHANDLE)` | 返回从文件开始到当前位置的字节数 |
| `telldir(DIRHANDLE)` | 返回重定向函数从目录句柄读取的当前位置 |
| `tie(VARIABLE, PACKENAME, LIST)` | 将变量关联到实现该变量的包 |
| `time` | 返回自 GMT 1970年1月1日 00:00:00 以来的秒数 |
| `times` | 返回当前进程的秒数 |
| `tr/SEARCHLIST/REPLACE_LIST/cds` | 将搜索列表转换为替换列表 |
| `truncate(FILEHANDLE, LENGTH)` | 将文件 FILEHANDLE 截断至指定的 LENGTH |
| `uc(EXPR)` | 返回 EXPR 的大写版本 |

# 表 24-3（续）

| 函数调用 | 描述 |
|---|---|
| `ucfirst(EXPR)` | 将 EXPR 的第一个字符更改为大写后返回 |
| `umask(EXPR)` | 设置创建文件时时使用的权限掩码（这规定了不允许对文件执行的操作） |
| `undef(EXPR)` | 取消 EXPR 的定义 |
| `unlink(LIST)` | 删除文件列表 |
| `unpack(TEMPLATE, EXPR)` | 将字符串解包为数组并返回该数组 |
| `shift(ARRAY, LIST)` | 将 LIST 插入到 ARRAY 的开头 |
| `tie(VARIABLE)` | 断开变量与包之间的绑定 |
| `use(MODULE)` | 开始使用一个 Perl 模块 |
| `time(LIST)` | 修改一组文件的访问时间和和修改时间 |
| `values(ASSOC_ARRAY)` | 返回一个包含关联数组所有值的数组 |
| `vec(EXPR, OFFSET, BITS)` | 将 EXPR 视为整数向量，并返回向量的指定元素 |
| `wait` | 等待子进程终止 |
| `waitpid(PID, FLAGS)` | 等待特定的子进程（由 PID 标识）终止 |
| `wantarray` | 返回当前子程序是否在数组上下文中被调用 |
| `warn(LIST)` | 在标准错误上产生一条警告消息（由 LIST 指定） |
| `write(FILEHANDLE)` | 向文件写入一条格式化记录 |
| `y/SEARCHLIST/REPLACE_LIST/cds` | 将搜索列表转换为替换列表 |

## 理解 Perl 包（Packages）和模块（Modules）

Perl 包是将数据和子程序组合在一起的方法。本质上，它是一种使用变量和子程序名称而不会与程序其他部分使用的任何名称冲突的方法。包的概念在 Perl 4 中就已经存在。

包提供了一种控制命名空间的方法——命名空间指的是变量和子程序名称的集合。尽管你可能没有意识到，当你编写 Perl 程序时，它会自动属于一个名为 `main` 的包。除了 `main` 之外，Perl 库还有其他包（这些包位于 Perl 5 安装目录下的 `lib` 子目录下），也可以定义自己的包。

你很快就会学会，Perl 模块是遵循特定指南的包。

### Perl 包

你可以将 Perl 包认为是组织一组相关 Perl 子程序的方便方法。另一个优点是，在包中定义的变量和子程序名称不会与程序其他地方使用的名称发生冲突。因此，一个包中名为 `$count` 的变量在该包内是唯一的，且不会与 Perl 程序其他地方的 `$count` 冲突。

一个 Perl 包位于单个文件中。`package` 语句用于文件开头，用于将该文件声明为一个包并赋予包一个名称。例如，`timelocal.pl` 文件在一个名为 `timelocal` 的包中定义了许多子程序和变量。`timelocal.pl` 文件在不同处有如下 `package` 语句：

```
package timelocal;
```
