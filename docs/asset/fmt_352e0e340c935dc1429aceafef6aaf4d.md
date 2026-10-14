
```c
    if (argc < 2 || strcmp(argv[1], "--help") == 0)

        usageErr("%s username [sleep-time]\n", argv[0]);

    /* 初始化 utmp 和 wtmp 文件的日志记录 */

    memset(&ut, 0, sizeof(struct utmpx));

    ut.ut_type = USER_PROCESS; /*这是一个用户登录 */

    strncpy(ut.user, argv[1], sizeof(ut.user));

    if (time((time_t *) &ut.ut_tv_sec) == -1)

        exitErr("time"); /* 标记当前时间 */

    ut.ut_pid = getpid();

    /* 在与 'stdin' 关联的终端上设置 ut_line 和 ut_id。

       此代码假设终端名为 "/dev/[pt][sy]*"。

       "/dev/dev" 是 5 个字符；"[pt][sy]"文件名名前缀

       是 3 个字符（总共 8 个字符）。 */

    devName = ttyname(STDIN_FILENO);

    if (devName == NULL)

        exitErr("ttyname");

    if (strlen(devName) < 8) /* 永远不会发生 */

        fatal("devname is too short: %s", devName);

    strncpy(ut.ut_line, devName, 5, sizeof(ut.ut_line));

    strncpy(ut.ut_id, devName, 8, sizeof(ut.ut_id));

    printf("在 utmp 和 wtmp 中创建日志条\n");

    printf("using pid %d, line %s, id %.*s\n",

           (long)ut.ut_pid, ut.ut_line, ut.ut_id);

    setutxent(); /* 回到 utmp 文件的开头 */

    if (pututxline(&ut) == NULL) /* 将日志记录写入 utmp */

        exitErr("pututxline");

    updwtmpx(PATH_WTMP, &ut); /* 将日志记录追加到 wtmp */

    /* 休睡一会儿，我们可以检查 utmp 和 wtmp 文件 */

    sleep((argc > 2) ? atoi(argv[2]) : 15, GN_NONBLOCK, "sleep-time");

    /* 现在执行“注销”；使用之前初始化的 'ut' 的值，

       下方修改的部分除外 */

    ut.ut_type = DEAD_PROCESS; /* 注销记录所需的 */

    time((time_t *) &ut.ut_tv_sec); /* 标记注销时间 */

    memset(&ut.ut_user, 0, sizeof(ut.ut_user)); /* 注销记录具有空用户名 */

    printf("在 utmp 和 wtmp 中创建注销条目\n");

    setutextx();

    if (pututxline(&ut) == NULL)

        errxit("pututxline");

    updwmpx(_PATH_WTMP, &ut);

    /* 回到 utmp 文件的开头 */

    /* 覆盖之前的 utmp 记录 */

    /* 将注销记录追加到 wtmp */

    endutextx();

    exit(EXIT_SUCCESS);

}
```

`loginacct/utmpx_login.c`

只需执行一次，然后根据需要将它们链接到不同的可执行文件中。虽然这种技术节省了编译时间，但它仍然存在一个缺点，即我们在链接阶段必须为所有对象文件命名。此外，我们的目录可能会因为大量的对象文件而变得杂乱无章。

为了解决这些问题，我们可以将一组对象文件分组为一个单一单元，即对象库（object library）。对象库有两种类型：静态库和共享库。共享库是更现代的对象库类型，正如我们在第 41.3 节中描述的那样，它们比静态库具有若干优势。

## 旁论：在编译程序时包含调试器信息

在上面的`cc`命令中，我们使用了`-g`选项在编译后的程序中包含调试信息。通常情况下，始终创建允许调试的程序和库是个好主意。（在更早些时候，省略调试信息是为了让生成的可执行文件占用更少的磁盘和内存，但现在磁盘和内存已经很便宜了。）

此外，在某些架构（如 x86-32）上，不应指定`-omit-frame-pointer`选项，因为这会导致无法进行调试。（在某些架构上，如 x86-64，此选项默认开启，因为它不会阻止调试。）出于同样的原因，不应使用`strip(1)`去除可执行文件和库中的调试信息。

## 41.2 静态库

在开始讨论静态库之前，我们先简要描述静态库，以明确静态库的差异和优势。

静态库也被称为归档（archives），是 UNIX 系统上提供的第一种库。它们提供了以下好处：

- 我们可以将一组常用的对象文件放入一个单一库文件中，然后可以使用它来构建多个可执行文件，而无需在构建每个应用程序时重新编译源文件。
- 链接命令变得更简单。与其在链接命令行上列出一长系列对象文件，我们只需指定静态库的名称。链接器知道如何搜索静态库并提取可执行文件所需的对象。

### 创建和维护静态库

实际上，静态库仅仅是一个包含所有添加到它的对象文件副本的文件。归档还记录了每个组件对象文件的各种属性，包括文件权限、数值用户 ID 和组 ID 以及最后修改时间。按照习惯，静态库的名称格式为 `libname.a`。

静态库是使用`ar(1)`命令创建和维护的，其通用形式如下所示：

```
$ ar options archive-file...
```

`options` 参数由一系列字母组成，其中一个是操作码，其他是影响操作执行方式的修饰符。一些常用的操作码如下：

- 将对象插入归档，替换该文件名的任何之前的同名对象文件。这是创建和更新归档的标准方法。因此，我们可能通过以下命令构建归档：

```
$ cc -g -c mod1.c mod2.c mod3.c

$ ar r libero.a mod1.o mod2.o mod3.o

$ rm mod1.o mod2.o mod3.o
```

如上所示，在构建库之后，如果需要可以删除原始对象文件，因为它们不再需要了。

- (`t`，目录内容)：显示归档的目录内容。默认情况下，它会列出归档中对象文件的名称。通过添加`v`（详细）修饰符，我们可以额外看到归档中记录的每个对象的文件的其他属性，在本例中：

```
$ ar tv libero.a

iw-r---\1000/1009 101016 Nov 15 12:26 mod1.o

iw-r---\1000/1009 406668 Nov 15 12:21 2009 mod2.o

iw-r---\1000/1009 46672 Nov 15 12:21 2009 mod3.o
```

我们为每个对象看到的额外属性从左到右依次是：它添加到归档时的权限、它的用户 ID 和组 ID、大小以及修改的日期和时间。

- (`d`，删除)：从归档中删除命名的模块，在本例中：

```
$ ar d libero.a mod3.o
```

### 使用静态库

我们可以通过两种方式将程序链接到静态库。第一种是在链接命令中指定静态库名称，例如：

```
$ cc -g -c prog.o libero.a

$ cc -g -o prog.o libero.a
```

或者，我们可以将库放在链接器搜索的标准目录之一（即 `/usr/lib`）中，并使用`-l`选项指定库名（去掉`lib`前缀和`.a`后缀的库文件名）：

```
$ cc -g -o prog.o -ldemo
```

如果库位于链接器通常不搜索的目录，我们应该使用`-L`选项指定额外的目录：

```
$ cc -g -o prog.o -Lldir -ldemo
```

尽管静态库可能包含许多对象模块，但链接器只包含程序所需的那些。链接程序后，我们可以按照通常的方式运行它：

```
./prog

x1

-x2
```
