
# 16 安全 Web 开发 437

- 开发风险因素：概览 438
- 派生 Shell 438
- 使用 system() 执行 Shell 命令 439
- C 和 C++ 中的 popen() 443

## Linux 最大化安全

- Perl 中的 open() 445
- eval (Perl 和 shell) 447
- Perl 中的 exec() 447
- 缓冲区溢出 (Buffer Overruns) 448
- 关于通用用户输入 451
- 路径、目录与文件 451
- chdir() 453
- 文件 453
- 其他有趣的安全编程与测试工具 453
- 其他在线资源 455
- 总结 456

# 17 拒绝服务攻击 457

- 什么是拒绝服务攻击？ 459
- 拒绝服务攻击带来的风险 460
- 本章结构 461
- 网络硬件 DoS 攻击 461
- 针对 Linux 网络的攻击 465
- sesquipedalian.c 466
- inetd 和 NMAP 467
- l2pd 伪造打印请求 468
- mimefood.pl 469
- portmap（以及其他 RPC） 469
- UNIX Socket 垃圾回收 DoS 470
- time 和 daytime DoS 470
- teardrop.c 471
- ident 打开套字洪水 473
- Lynx/charger 浏览器攻击 474
- nestea.c 474
- pong.c 和 ICMP 洪水 475
- 死亡之信 (The Ping of Death) 476
- octopus.c 477
- 针对 Linux 的攻击 478
- Netscape Communicator 内容类型 (1) 478
- Netscape Communicator 内容类型 (2) 479
- passwd 资源耗尽 480
- xdm 481
- wtmp lock 481
