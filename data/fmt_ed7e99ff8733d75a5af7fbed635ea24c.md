
# 784 第五部分：红帽 Linux Linux 编程

表 24-3：（续）

| 函数调用 | 描述 |
|---|---|
| `exists($ASSOC(KEY))` | 如果关联数组中的键存在则返回真 |
| `exit(EXPR)` | 退出 Perl 程序 |
| `eval(EXPR)` | 以其方式执行 EXPR |
| `exp(EXPR)` | 幂 |
| `fcntl(FILEHANDLE, FUNCTION, SCALAR)` | 控制句柄 |
| `fileno(FILEHANDLE)` | 返回文件描述符 |
| `fork()` | 创建子进程 |
| `format(PICTURE, LIST)` | 格式化输出 |
| `getc(FILEHANDLE)` | 从句柄读取下一个字符 |
| `getgroup()` | 获取组信息 |
| `getgid(GID)` | 返回数值组 ID |
| `grnam(NAME)` | 通过名称查找组 |
| `gethostbyaddr(ADDR, ADDRTYPE)` | 将地址转换为主机 |
| `gethostbyname(NAME)` | 将主机转换为地址 |
| `getsent()` | 获取记录 |
| `login()` | 登录 |
| `getpwuid(UID)` | 返回数值用户 ID |
| `getservbyname(NAME, PROTO)` | 将服务名称转换为数字 |
| `getservbyport(PORT, PROTO)` | 将端口号转换为名称 |
| `getservent()` | 获取记录 |
| `getsockname(SOCKET)` | 返回地址 |
| `getsockopt(SOCKET, LEVEL, OPTNAME)` | 获取请求的套接字选项 |
| `glob(EXPR)` | 返回对应通配符的文件 |
| `gmtime(EXPR)` | 将二进制时间转换为 GMT |
| `goto(LABEL)` | 跳转到语句 |
| `grep(EXPR, LIST)` | 在列表中搜索出现项 |
| `hex(EXPR)` | 返回十六进制的十值 |
| `index(STR, SUBSTR, POSITION)` | 返回首次出现的位置 |
| `int(EXPR)` | 返回整数部分 |
| `join(EXPR, LIST)` | 连接列表返回字符串 |
| `keys(ASSOC_ARRAY)` | 返回数组键 |
| `kill(LIST)` | 向进程发送信号 |
| `last(LABEL)` | 退出循环 |
| `lc(EXPR)` | 返回小写版本 |
| `lfirst(EXPR)` | 返回首字符为小写的 EXPR |
| `length(EXPR)` | 返回长度 |
| `link(OLDFILE, NEWFILE)` | 创建链接 |
| `listen(SOCKET, QUEUE)` | 等待接入连接 |
| `local(LIST)` | 使变量局部 |
| `localtime(EXPR)` | 将二进制时间转换为本地时间 |
| `pwent()` | 获取记录 |
| `pnam(NAME)` | 将名称转换为记录 |

# 第 24 章：Shell 和 Perl 脚本 785

| 函数调用 | 描述 |
|---|---|
| `lock SHAREDVAR` | 锁定一个共享变量 |
| `log(EXPR)` | 返回 EXPR 的对数（以 e 为底） |
| `stat(FILEHANDLE)` | 返回文件的统计信息（如果指向符号链接，则返回关于符号链接的信息） |
| `m/PATTERN/gimosx` | 执行模式匹配 |
| `map(EXPR, LIST)` | 对 LIST 中的每个项评估表达式 EXPR |
| `mkdir(FILENAME, MODE)` | 创建由 FILENAME 指定目录 |
| `msgctl(ID, CMD, ARG)` | 对消息队列执行消息控制操作 |
| `msgget(ID, FLAGS)` | 获取对应于 KEY 的消息队列标识符 |
| `msgrcv(ID, VAR, SIZE, TYPE, FLAGS)` | 从消息队列标识符 ID 接收消息 |
| `msgsnd(ID, MSG, FLAGS)` | 向消息队列标识符 ID 发送消息 |
| `my(EXPR)` | 声明存在于子程序或大括号包围块 `((..))` 中的一个或多个私有变量 |
| `next(LABEL)` | 开始由 LABEL 标识的循环的下次迭代 |
| `no(Module LIST)` | 停止使用 Perl 模块 |
| `oct(EXPR)` | 返回 EXPR 中八进制数的十进制 |
| `open(FILEHANDLE, EXPR)` | 打开文件名在 EXPR 中的文件，并将该文件与 FILEHANDLE 关联 |
| `opendir(DIRHANDLE, EXPR)` | 打开目录在 EXPR 中的目录，并将该目录与 DIRHANDLE 关联 |
| `ord(EXPR)` | 返回 EXPR 中第一个字符的数值 ASCII 代码 |
| `our EXPR` | 将 EXPR 中列出的变量声明为封装块内的有效变量（类似于 `my`，但不创建任何局部变量） |
| `pack(TEMPLATE, LIST)` | 取一个值列表并返回一个包含打包的二进制结构的字符串（TEMPLATE 指定了打包方式） |
| `package PACKAGE` | 声明当前文件为指定包的一部分 |
| `pipe(READHANDLE, WRITEHANDLE)` | 打开一个用于读写的管道 |
| `pop(ARRAY)` | 并返回数组的最后一个元素 |
| `pos(SCALAR)` | 返回上次模式匹配发生的位置（当使用 `/PATTERN/g` 进行全局搜索时适用） |
| `print(FILEHANDLE)` | 向由 FILEHANDLE 标识的文件打印项列表 |
| `printf(FILEHANDLE)` | 向文件打印格式化输出 |

| 函数调用 | 描述 |
|---|---|
| `prototype FUNCTION` | 以字符串形式返回函数的原型（原型显示了函数的声明，包括其参数） |
| `push(ARRAY, LIST)` | 将 LIST 中的值追加到 ARRA Y 的末尾 |
| `q/STRING/` | 给 STRING 加引号，但不将变量名替换为实际值（类似于单引号字符串） |
| `qq/STRING/` | 给 STRING 加引号，但会将变量名替换为实际值（类似于双引号字符串） |
| `quotemeta(EXPR)` | 返回 EXPR 的值，并对正则表达式中具有特殊含义的所有字符添加反斜杠前缀 |
| `qw/STRING/` | 给单词列表加引号（类似于模式中使用的括号） |
| `qx/STRING/` | 给命令加引号（类似于反引号） |
| `rand(EXPR)` | 返回 0 到 EXPR 之间的随机值 |
| `read(FILEHANDLE, SCALAR, LENGTH)` | 从文件读取指定数量的字节 |
| `readdir(DIRHANDLE)` | 从目录句柄读取目录条目 |
| `readlink(EXPR)` | 返回符号链接指向的文件 |
| `readpipe(EXPR)` | 返回执行系统命令 EXPR 后的输出 |
| `recv(SOCKET, SCALAR, LEN, FLAGS)` | 从套接字接收消息 |
| `redo(LABEL)` | 重启由 LABEL 标识的循环 |
| `ref(EXPR)` | 如果 EXPR 是引用则返回真（引用指向一个对象） |
| `rename(OLDNAME, NEWNAME)` | 将文件名从 OLDNAME 改为 NEWNAME |
| `require(FNAME)` | 包含 FNAME 指定的文件，并执行该文件中的 Perl 代码 |
| `reset(EXPR)` | 清除全局变量 |
| `return(LIST)` | 使用指定的值从子程序中返回 |
| `reverse(LIST)` | 反转 LIST 中元素的顺序 |
| `rewinddir(DIRHANDLE)` | 将当前位置设置为由 DIRHANDLE 标识的目录的开头 |
| `rindex(STR, SUBSTR)` | 返回字符串中子字符串的最后位置 |
| `index(STR, SUBSTR, POSITION)` | 返回字符串中子字符串最后出现的位置 |
| `rmdir(FILENAME)` | 删除由 FILENAME 指定的目录 |

# 第五部分：红帽 Linux Linux 编程

表 24-3：（续）

| 函数调用 | 描述 |
| --- | --- |
| `s/PATTERN/REPLACEMENT/ egims` | 用 REPLACEMENT 替换 PATTERN（正则表达式） |
| `scalar(EXPR)` | 在标量上下文中评估表达式 EXPR |
| `seek(FILEHANDLE, POSITION, WHENCE)` | 移动到文件中的新位置 |
| `seekdir(DIRHANDLE, POS)` | 移动到目录中的新位置 |
