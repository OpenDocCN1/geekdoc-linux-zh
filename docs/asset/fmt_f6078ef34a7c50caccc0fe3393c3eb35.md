
![](img/aeda3be9ee318bedd42850d461da0f28_420_1.png)

### 处理命令行参数

文件结构填充了来自命令行参数的相关信息。

### 读取主页

`home_page`函数将在后面给出，它创建一个TCP连接，向服务器发送命令，然后读取主页。这是第一个连接，它在我们建立多个连接之前独立完成。

### 初始化全局变量

初始化两个描述符集，一个用于读取，一个用于写入。`maxfd`是`select`的最大描述符（初始化为-1，因为描述符是非负的），`nleftconn`是剩余读取的文件数（当变为0时完成），`nleftconn`是仍需要TCP连接的文件，`nconn`是当前打开的连接数（不会超过第一个命令行参数）。

### 与服务器建立连接

我们的`tcp_connect`与服务器建立连接。

### 向服务器发送HTTP命令；读取响应

向主页（通常名为`/`）发送HTTP GET命令。读取响应（我们不对响应做任何操作）并关闭连接。

下一个函数图15.17所示的`start_connect`启动非阻塞连接。

### 创建套接字，设置非阻塞

我们调用`host_serv`函数（图11.5）来查找并连接主机名和服务名，返回`addrinfo`结构数组的指针。我们只使用第一个结构。创建一个TCP套接字并设置为非阻塞。

# 418 非阻塞 I/O 第15章

图15.17 发起非阻塞连接。

## 发起非阻塞连接
发起非阻塞连接并将标志位设置为`F_CONNECTING`。套接字描述符同时设置为读就绪和写就绪，`select`将等待这两个条件中的任意一个出现，以作为连接已完成的指示。如果有必要，我们还会更新`maxfd`。

### 处理连接完成

如果`connect`返回，则连接已经完成，此时`write_get_cmd`函数（下文所示）将向服务器发送一个命令。我们为`connect`设置了非阻塞标记，但绝不会将其重置为默认的阻塞模式。这里，由于我们只向套接字写入了极少量数据（下一个函数中的`GET`命令），这样做是安全的，我们假设该命令的大小远小于套接字能够缓存的容量。即使`write`在非阻塞标记下返回了短计数值，我们的写入函数也会处理这种情况。保持非阻塞状态对后续执行的读取没有影响，因为我们总是调用`select`等待套接字变为可读。

图15.18显示了`write_get_cmd`函数，它向服务器发送一个HTTP GET命令。

```
1 #include "web.h"

2 void

3 write_get_cmd(struct file fptr)

4 {

5 int n;

6 char line[MAXLINE];

7 n = sprintf(line, sizeof(line), GET_CMD, fptr->f_name);

8 Write(fptr->fd, line, n);

9 printf("wrote bytes by %s\n", fptr->f_name);

10 fptr->fd = F_fd; /* clears F_CONNECTING */

11 FD_SET(fptr->fd, &fdset); /* will read server's reply */

12 if (fptr->fd > maxfd)

13 maxfd = fptr->f_fd;

```

图15.18 向服务器发送HTTP GET命令。

## 构建命令并发送

构建命令并将其写入套接字。

## 设置标志位

设置文件的`F_READ`标志，这会清除`F_CONNECTING`标志（如果已设置）。该描述符向主循环指示该描述符用于输入。该描述符也被设置为读就绪集，并在必要时更新`maxfd`。

我们返回图15.19中的`main`函数，从我们在图15.19中上次停止的地方继续执行。这是程序的主循环：只要还有更多文件需要处理（`lefterrno`大于0），就可能地尝试启动另一个连接，然后对所有活跃的描述符进行`select`，处理非阻塞连接的完成和数据的到达？

## 我们可以发起另一个连接吗？

如果我们没有达到同时连接数量的限制，并且有额外的连接需要建立，则找到一个尚未处理的文件（通过`f_flags`为0来指示），并调用`start_connect`发起连接。活跃连接数增加（`nconn`），且剩余等待建立的连接数减少（`lefterrno`）。

## select: 等待事件发生

`select`等待可读性或可写性。正在进行非阻塞连接的描述符将在两个集中都被启用，而连接完成且正在等待服务器数据的描述符将仅在读就绪集中被启用。

## 非阻塞 I/O

```
while (nleftread > 0) {

    while (nconn < maxconn && nleftconn > 0) {

        /* 找到一个要读取的文件 */
        for (i = 0; i < nfiles; i++) {
            if (file[i].f_flags == 0)
                break;
            if (i == nfiles) {
                err_quit("%neftconn = %d but not found", nleftconn);
                start_connect(&file[i]);
                nconn++;
                nleftconn--;
            }
        }
    }

rs = rset;
ws = wset;
n = Select(maxfd + 1, &rs, &ws, NULL, NULL);
for (i = 0; i < nfiles; i++) {
    flags = file[i].f_flags;
    if (flags == 0 || flags & F_DONE)
        continue;
    fd = file[i].f_fd;
    if (fd & F_CONNECTING) {
        if (FD_ISSET(fd, &rs) | FD_ISSET(fd, &ws)) {
            n = strerror(error);
            if (getockopt(fd, SOL_SOCKET, SO_ERROR, &error, &n) < 0)
                err_ret("nonblocking connect failed for %s", file[i].f_name);
        } else if (error == 0) {
            /* 连接已建立 */
            printf("connection established for %s\n", file[i].f_name);
            FD_CLR(fd, &wset); /* 不再进行写性测试 */
            write_get_cmd(&file[i]);
        }
    } else if (n > Read(fd, buf, sizeof(buf)) == 0) {
        printf("end-of-file on %s\n", file[i].f_name);
        Close(fd);
        file[i].f_flags = F_DONE; /* 清除读取标记 */
        FD_CLR(fd, &rset);
        nleftread--;
        nconn--;
    } else {
        printf("read %d bytes from %s\n", n, file[i].f_name);
    }
}
```
