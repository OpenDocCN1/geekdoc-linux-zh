
# 402 第 12 章 连接与协议：编写 Web 服务器

```c
/* webserv.c - 一个最小的 Web 服务器 (版本 0.2)
用法: 端口号
特性：支持 GET 命令
fork 创建新的子进程处理每个请求
存在安全漏洞，用于演示 */
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <unistd.h>
#include <string.h>

main(int ac, char *argv[]) {
    int sock, fd;
    FILE *fpin;

    if (ac != 1) {
        fprintf(stderr, "usage: portnumber\n");
        exit(1);
    }

    sock = socket(AF_INET, SOCK_STREAM, 0);

    while(1) {
        fd = accept(sock, NULL, NULL);    /* 接收调用 */
        fpin = fopen(fd, "r");               /* 将其转换为 FILE */

        fgets(fpin, request, BUFSIZ);          /* 读取客户端请求 */
        read_until_crnl(fpin);              /* 跳过参数 */
        process_rq(request, fd);            /* 响应客户端 */

        fclose(fpin);                        /* 断开连接 */
    }
}

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

header ( FILE *fp, char *content_type ) {
    fprintf(fp, "HTTP/1.0 200 OK\r\n");
    if ( content_type )
        fprintf(fp, "Content-type: %s\r\n", content_type);
}

cannot_do(int fd) {
    FILE *fp = fdopen(fd, "w");
    fprintf(fp, "HTTP/1.0 501 Notplemented\r\n");
    fprintf(fp, "Content-type: text/plain\r\n");
    fprintf(fp, "\r\n");

    fprintf(fp, "That command is not implemented\r\n");
    fclose(fp);
}

do_404(char *item, int fd) {
    FILE *fp = fdopen(fd, "w");
    fprintf(fp, "HTTP/1.0 404 Not Found\r\n");
    fprintf(fp, "Content-type: text/plain\r\n");
    fprintf(fp, "\r\n");

    fprintf(fp, "The item you requested: %s\r\nis not found\r\n",
        item);
    fclose(fp);
}

do_ls(char *dir, int fd) {
    FILE *fp; /* 将 socket转换为 FILE *
    fp = fdopen(fd,"w");
    header(fp,"text/plain"); /* 发送 HTTP 响应头 */
    fprintf(fp,"\r\n"); /* 头部结束标记 */
    fflush(fp); /* 强制写入 socket */

    dup2(fd,1); /* 将 socket 设置为 stdout *
    dup2(fd,2); /* 将 socket 设置为 stderr *
    close(fd); /* 关闭 socket *
    execl("/bin/ls","ls","-l",NULL); /* ls -l 执行工作 *
    perror(dir); /* 或者未执行 *
    exit(1); /* 子进程退出
}
}

isadir(char *fp) {
    struct stat info;
    return ( stat(fp, &info) != -1 && S_ISDIR(info.st_mode));
}
not_exist(char *fp)
```

```c
/*---------------- cgi 相关内容：用于检查扩展名的函数和
用于运行程序的函数。--------------------------------------*/
char *file_type(char *f)
/* 返回文件的扩展名 */
{
  char    *cp;
  if ( (cp = strchr(f, '.')) != NULL)
    return cp+1;
}
ends_in_cgi(char *f) {
  return ( strcmp(file_type(f), "cgi") == 0 );
}
do_exec(char *prog, int fd) {
  FILE    *fp;
  fp = fdopen(fd, "w");
  header(fp, NULL);
  fflush(fp);
  dup2(fd, 1);
  dup2(fd, 2);
  close(fd);
  execl(prog,prog,NULL);
  perror(prog);
}
```
