
| `chown` | 修改文件的所有者/所属组 | 465 |
| `close` | 关闭文件 | 450 |
| `closedir` | 关闭目录流 | 463 |
| `connect` | 连接到命名套接字 | 519 |
| `dup` | 复制文件描述符 | 466 |
| `dup2` | 类似于 `dup()` | 466 |
| `execcl` | 用可执行文件替换进程 | 481 |
| `execpl` | 类似于 `execcl()` | 481 |
| `execcv` | 类似于 `execcl()` | 481 |
| `execvp` | 类似于 `execcl()` | 481 |
| `exit` | 终止进程 | 478 |
| `fchmod` | 类似于 `chmod()` | 466 |
| `fchown` | 类似于 `chown()` | 465 |
| `fcntl` | 各种文件特性 | 468 |
| `fork` | 复制进程 | 475 |
| `fstat` | 类似于 `stat()` | 462 |
| `ftruncate` | 类似于 `truncate()` | 472 |
| `getgid` | 返回进程的有效组 ID | 484 |
| `getuid` | 返回进程的有效用户 ID | 484 |
| `getgid` | 返回进程的真实组 ID | 484 |
| `getostbyname` | 返回描述 Internet 主机的结构 | 525 |

| 名称 | 摘要 | 描述页码 |
|---|---|---|

| `gethostname` | 返回主机名 | 525 |
| `getgid` | 返回进程进程组 ID | 498 |
| `getpid` | 返回进程 ID 号 | 475 |
| `getppid` | 返回父进程 ID 号 | 475 |
| `getuid` | 返回进程的真实用户 ID | 484 |
| `htonl` | 将主机格式数字转换为网络格式数字 | 526 |
| `htons` | 类似于 `htonl()` | 526 |
| `inet_addr` | 返回 32 位 IP 地址 | 524 |
| `inet_ntoa` | 返回字符串格式的 IP 地址 | 525 |
|  | 控制设备 | 469 |
| `kill` | 向指定的进程或进程组发送信号 | 492 |
| `lchown` | 类似于 `chown()` | 465 |
| `link` | 创建硬链接 | 469 |
| `listen` | 设置等待的套接字连接数 | 517 |
| `lseek` | 移动到文件的特定偏移量 | 449 |
| `lstat` | 类似于 `stat()` | 462 |
| `memset` | 给数组填充特定值 | 526 |
| `mkdir` | 创建目录 | 471 |
| `mkfifo` | 创建命名管道 | 505 |
| `mknod` | 创建特殊文件 | 471 |
| `nice` | 更改进程优先级 | 483 |
| `ntohl` | 将网络格式数字转换为主机格式数字 | 526 |
| `ntohs` | 类似于 `ntohl()` | 526 |
| `open` | 打开或创建文件 | 446 |
| `opendir` | 为 `readdir()` 打开目录流 | 463 |

| 名称 | 摘要 | 描述页码 |
|---|---|---|

| `pause` | 接收信号时挂起调用进程 | 490 |
| `perror` | 显示最近一次系统调用的消息 | 435 |
| `pipe` | 创建未命名管道 | 502 |
| `read` | 将字节从文件读入缓冲区 | 447 |
| `readdir` | 从打开的流读取目录项 | 463 |
| `setgid` | 设置进程的有效组 ID | 484 |
| `setuid` | 设置进程的有效用户 ID | 484 |
| `setgid` | 设置进程的真实和有效组 ID | 484 |
| `setpgid` | 设置进程的真实和有效进程组 ID | 497 |
| `setuid` | 设置进程的真实和有效用户 ID | 484 |
| `signal` | 指定信号到达时采取的操作 | 490 |
| `socket` | 创建未命套接字 | 515 |
| `stat` | 返回文件的状态信息 | 462 |
| `sync` | 将所有文件缓冲区写入磁盘 | 472 |
| `sysctl` | 检查或修改内核参数 | 591 |
| `truncate` | 截断文件 | 472 |
| `unlink` | 删除文件 | 451 |
| `wait` | 等待子进程 | 480 |
| `write` | 从缓冲区写入文件 | 448 |

## 参考文献

- [Anderson, 1986] Anderson, Gail. UNIX 指南，Sams。
- [Anderson, 1995] Anderson, Mark and Paul Case. Shell 编程，Waite Group。
- [Bar, 2000] Bar, Morris. Linux 系统，McGraw-Hill。
- [Bar, 1995] Bar, Daniel. Shell 命令，Prentice Hall。
- [Bovet, 2002] Bovet, Marco. Linux 内核，O'Reilly。
- [Cheswick, 1994] Cheswick, William. UNIX 网络编程，Addison-Wesley。
- [Fink, 2003] Fink, Martin. Linux 商业化与开源，Prentice Hall。
- [Garfinkel, 1996] Garfinkel, Simon and Steve Spaffer. UNIX 与安全，Addison-Wesley。
- [Horspool, 1992] Horspool, R. UNIX 环境，Sams。
- [Kernighan, 1992] Kernighan, Brian and Gene Pope. UNIX 编程，Prentice Hall。
- [Maxwell, 2001] Maxwell, Scott. Linux 核心注释，The Berkeley。
- [Medneigh, 1996] Medneigh, David. Perl 示例，Que。
- [Nemeth, 2002] Nemeth, Levi, Garth Snyder, and Trent R. Hein. Linux 管理手册，APT Hall。
- [Oram, 1991] Oram, Andrew and Steve Talbot. 管理项目，O'Reilly。
- [Quercia, 1993] Quercia, Valeria and Tim O'Reilly. X Window 系统用户指南，OSF/Motif 版，O'Reilly & Associates。
- [Roberts, 1991] Roberts, Ralph, Mark Boyd, Stephen G. Kochan, and Patrick H. Wood. UNIX 桌面指南，Sams。
- [Rochkind, 1986] Rochkind, Marc J. 高级 UNIX 编程，Prentice Hall。
- [Sage, 1986] Sage, Russell G. UNIX 大技巧，Sams。
- [Salus, 1994] Salus, Peter H. UNIX 的四世纪，Addison-Wesley。
- [Sarwar, 2003] Sarwar, Syed Mansoor, and Khaled Al-Saqabi. Linux 和 UNIX 编程工具：软件开发者入门，Addison-Wesley。
- [Stevens, 1992] Stevens, W. Richard. UNIX 环境高级编程，Addison-Wesley。
- [Stevens, 1998] Stevens, W. Richard. UNIX 网络编程，第二版，Prentice Hall。
- [Waite, 1987] Waite Group and Michael Waite (Editor). UNIX 论文，Sams。

# 索引

## 符号

- `#`, 172, 182
- `!!`, 182
- `$`, 172, 185
- `$`, 214, 253
- `$!`, 214, 253
- `#$`, 214, 253
- `$$$`, 186, 214, 253
- `$*`, 186
- `$<`, 301
- `$?`, 196, 214, 233, 253, 270
- `$70`, 301
- `$@`, 214, 253
- `$_`, 214, 279
- `$0`, 186
- `$!`, 186
- `Sargv`, 301
- `$CDPATH`, 238, 279, 284
- `$cdpath`, 301
- `$COLUMNS`, 279
