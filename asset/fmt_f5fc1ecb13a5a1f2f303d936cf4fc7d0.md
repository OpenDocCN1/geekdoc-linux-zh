
```
ion 206% trace
execve("/usr/bin/telnet", ["telnet", "foo", "136"], [/* 64 vars */]) = 0
uname("sys=Linux", node="ion", ...]) = 0
0x8066308
brk(0)
map2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x40013000
open("/etc/ld.so.preload", O_RDONLY) = -1 ENOENT (No such file or /directory)
open("/usr/lib/i686/mmx/libcns.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/usr/lib/i686/mmx", 0xbffe59c) = -1 ENOENT (No such file or directory)
open("/usr/lib/i686/libncurses.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/usr/lib/i686", 0xbffe59c) = -1 ENOENT (No such file or directory)
open("/usr/lib/libncurses.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/usr/lib/mmx", 0xbffe59c) = -1 ENOENT (No such file or directory)
open("/usr/lib/libncurses.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/usr/lib/mmx", st_mode=S_IFDIR(0755, st_size=32768, ...)) = 0
open("/home/wilding/sqlib/i686/mmx/libcurses.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/home/wilding/sqlib/i686/mmx", 0xbffe59c) = -1 ENOENT (No such file or directory)
open("/home/wilding/sqlib/libncurses.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/home/wilding/sqlib/i686", 0xbffe59c) = -1 ENOENT (No such file or directory)
open("/home/wilding/sqlib/lib/mmx/libncurses.so.5", O_RDONLY) = -1 ENOENT (No such file or directory)
stat64("/home/wilding/sqlib/lib/mmx", 0xbffe59c) = -1 ENOENT (No such file or directory)
... (此处省略重复的 trace 内容，保持逻辑一致)
```

`strace` 输出显示了 20 次查找 `libncurses.so.5` 库的失败尝试。事实上，该跟踪的 52 行中有 40 行与查找 curses 库的失败尝试。`LD_LIBRARY_PATH` 包含了许多（从开始）不包含 `libncurses.so.5` 的路径。更好的 `LD_LIBRARY_PATH` 应该在路径列表开头包含 `lib`（最终找到 `libncurses.so.5` 的地方）：

```
ion 689% echo $LD_LIBRARY_PATH
/lib:/usr/lib:/home/winding/sqlib/lib:/usr/java/lib
```

跟踪显示这个 `LD_LIBRARY_PATH` 效率得多。

### 2.5.2 PATH 变量

糟糕的 `PATH` 环境变量会导致启动成本。Shell 会搜索 `PATH` 中列目录以查找可执行文件。`PATH` 中的目录越多，Shell 查找的时间就越长。

### 2.5.3 跟踪 inetd（超级服务器）

Linux 系统通过 TCP 连接到网络。常见的示例包括 `telnet` 和 Web 通信。大多数情况下，一切运行符合预期，但如果由远程连接驱动软件遇到问题怎么办？例如，如果远程用户无法连接到系统？

这是一个使用 trace 检查传入 `telnet` 连接的示例。该示例需要权限。

第一步是找到并跟踪 `inetd` 守护进程（使用 root 权限）：

```
ion 200# ps -fea | grep inetd | grep -v grep
root 986 1 0 Jan27 ? 00:00:00 /usr/sbin/inetd
ion 201# trace -o inetd.trace -f p 986
```

在远程系统上，使用 `telnet` 客户端登录 `tel` 服务器：

```
sunfish % telnet ion
```

登录 `tel` 服务器后，按下 Ctrl-C 跳出跟踪并检查跟踪输出：

> 注意：带有 `...` 的行代表为了简化而省略的跟踪输出。

```
ion 203# less inetd.trace
986 select(13, [ 4 5 6 7 8 9 10 11 12 ], NULL, NULL, NULL) = 1(in
-[5])
986 accept(0, NULL) = 3
986 getpeername(3, {sin_family=AF_INET, sin_port=htons(63117),
-sin_addr=inet_addr("92.26.48.230")}, [16]) = 0
986 fork() = 27202
986 close(3 unfinished ...>)
27202 socket(PF_UNIX, SOCK_STREAM, 0 unfinished ...>)
986 <.. close resumed() ) = 0
27202 <.. socket resumed() ) = 13
```

系统调用等待新连接的到来。新连接在 `inetd` 的描述符 5 上到来。`accept` 系统调用创建一个

# 实际调试示例

直接连接到远程 `telnet` 客户端的新 socket 描述符。在接受新连接后，`inetd` 立即收集有关连接源的信息，包括远程端口和 IP 地址。随后 `inetd` 派生（`fork`）并关闭 socket 描述符。跟踪继续如下：

```
27202 connect(13, {sin_family=AF_UNIX, path="/var/run/.nscd_socket"}, 110) = 0

27202 dup2(3, 0) = 0
27202 close(3) = 0
27202 dup2(0, 1) = 1
27202 dup2(0, 2) = 2
27202 close(1022) = -1 EBADF (无效文件描述符)
27202 close(1021) = -1 EBADF (无效文件描述符)
27202 close(4) = 0
27202 close(3) = -1 EBADF (无效文件描述符)
27202 rt_sigaction(SIGPIPE, SIG_DFL, 8) = 0
27202 execve("/usr/sbin/tcpd", "in.telnetd", /* 16 vars */) = 0
```

跟踪输出显示了与名称服务守护进程连接（参见 `nscd` 的 man 手页）。接下来，通过复制 socket 描述符创建 `stdin` (0)、`stdout` (1) 和 `stderr` (2) 的文件描述符。随后关闭所有的 socket 描述符（从 1022 到 3），以确保 `inetd` 的任何文件描述符都不会被最终的 shell 继承。最后，派生的 `inetd` 将自己转换为访问控制程序。
