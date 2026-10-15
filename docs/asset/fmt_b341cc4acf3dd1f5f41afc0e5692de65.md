
```c
while (1) {
    fd = accept(socket, NULL, NULL);    /* 接收调用 */
    fpin = fopen(fd, "r");               /* 将其转换为 FILE 类型 */

    fgets(fpin, request, LEN);          /* 读取客户端请求 */
    read_until_crnl(fpin);              /* 跳过参数 */
    process_rq(request, fd);            /* 响应客户端 */

    close(fpin);                        /* 断开连接 */
}
```

为了清晰起见，省略了每个系统调用和函数中的错误检查。

### 处理请求

请求处理包括识别命令以及对参数执行操作：

```c
process_rq(char *rq, int fd) {
    char cmd[11], arg[513];
    if (fork() != 0)                     /* 如果是子进程，执行工作 */
        return;                          /* 如果是父进程，则返回 */
    sscanf(rq, "%10s %512s", cmd, arg);
    if (strcmp(cmd, arg) != 0)         /* 检查命令 */
        cannot_do(fd);
    else if (not_exist(arg))           /* 参数是否存在？ */
        do_404(arg, fd);                /*否：通知用户 */
    else if (isadir(arg))               /* 是目录吗？ */
        do_ls(arg, fd);                 /* 是：列出内容 */
    else if (ends_in_cgi(arg))         /* 名字是 X.cgi ？ */
        do_exec(arg, fd);               /* 是：执行它 */
    else                              /* 否则 */
        do_cat(arg, fd);                /* 显示内容 */
}
```

## 第12章 连接与协议：编写 Web 服务器

该服务器为每个请求创建一个新的子进程来处理。子进程随后将请求拆分为命令和参数。如果命令不是 `GET`，服务器将返回针对未实现命令的 HTTP 代码。如果命令是 `GET`，服务器期望看到目录名称、以 `.cgi` 字符串结尾的可执行程序名称，或者一个普通文件的名称。如果没有指定名称的目录或文件，服务器将报告错误。

如果存在该名称的文件或目录，服务器将决定执行哪种操作：`ls`、`exec` 或 `cat`。

### 目录列出函数

`do_ls` 函数处理列出目录的请求：

```c
do_ls(char *dir, int fd) {
    FILE *fp; /* 将 socket转换为 FILE *
    fp = fdopen(fd,"w");
    header(fp,"text/plain"); /* 发送 HTTP 响应头
    fprintf(fp,"\r\n"); /* 头部结束标记 */
    fflush(fp); /* 强制写入 socket */

    dup2(fd,1); /* 将 socket 设置为 stdout *
    dup2(fd,2); /* 将 socket 设置为 stderr *
    close(fd); /* 关闭 socket *
    execl("/bin/ls","ls","-l",NULL); /* ls -l 执行工作 *
    perror(dir); /* 或者未执行 *
    exit(1); /* 子进程退出
}
```

我们没有在这个函数中使用 `open`，就像我们在上一章的目录列出器中那样做的那样。通过直接调用 `ls`，我们消除了从用户向运行的 传递参数字符串引起的问题。

### 其他函数

代码的其他部分在本章后面会给出。该程序可以工作，但是不完整且不安全的。一些需要的修复如下：

- (a) 消除僵尸进程

- (b) 缓冲区溢出保护

- (c) CGI 程序应该能看到多个环境变量

- (d) HTTP 头部应该包含更多信息

另一方面，该程序是用大约 230 行 C 代码（包括注释和空行）编写的完整 Web 服务器。

## 12.5.5 运行 Web 服务器

编译代码然后在端口上运行程序：

```bash
$ cc webserv.c sockclib.c -o webserv
./webserv 12345
```

你现在可以通过 `http://yourhostname:12345/` 访问你的 Web 服务器。在该目录中放置一个 html 文件，并使用 `http://yourhostname:12345/filename.html` 打开它。创建一个如下 shell 脚本：

```bash
#!/bin/sh
## hello.cgi - 一个活泼的 cgi 页面
printf "Content-type: text/plain\nhello\n";
```

调用 `hello.cgi`，使用 `chmod` 将其权限设置为 755，然后使用浏览器通过 `http://yourhostname:12345/hello.cgi` 调用脚本。

### 12.5.6 Webserv 源代码

这是这个简单 Web 服务器的代码：
