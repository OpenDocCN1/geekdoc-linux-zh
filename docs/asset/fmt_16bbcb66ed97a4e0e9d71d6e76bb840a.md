
# Kali Linux 2013 工具列表

## socat

**描述** `socat` 是用于两个独立数据通道之间双向数据传输的继电器。这些数据通道中的可以是文件、管道、设备（串口等）、伪终端、套接字（UNIX, IP4, IP6 - raw, UDP, TCP）、代理连接（文件描述符等）、GNU 命令行编辑器（readline）、程序，或这些者的组合。这些模式包括生成“监听”套接字、命名管道和伪终端。`socat` 可用于例如 TCP 端口转发（单次或守护进程）、作为外部 socks 代理工具、攻击弱的防火墙、作为 UNIX 套接字的 shell 接口、IP 继继、将 TCP 型程序重定向到串口、逻辑上连接不同计算机上的串口，或为运行带有网络连接的客户端或服务器脚本建立一个相对安全的环境（su 和 chroot）。

更多信息见：http://www.dest-unreach.org/socat/doc/README

**用法** `socat [[options]] <address>`

**用法** `socat -V`

**用法** `socat -h[h[h]] | -?[?]`

**选项** http://www.dest-unreach.org/socat/doc/socat.html#OPTIONS

**示例** `socat -TCP4:www.domain.org:80`

**示例** `socat TCP4-LISTEN:www TCP4:www.domain.org:www`

**示例** `socat -,raw,echo=0,escape=0x0f /dev/ttyS0,raw,echo=0,crnl`

**示例** http://www.dest-unreach.org/socat/doc/socat.html#EXAMPLES

## sslh

**描述** `sslh` 允许在同一个端口上接受 HTTPS 和 SSH 连接。它使得可以在 443 端口上连接到 SSH 服务器（例如从公司防火墙内部，防火墙几乎从不拦截 443 端口），同时在该端口上提供 HTTPS 服务。其原理是让 `sslh` 监听外部 443 端口，接受传入连接，判断连接类型，然后转发到适当的服务器。

**用法** `sslh [-t num] [-p listening address] [-l target address for SSL ] [-s target address for SSH] [-u username] [-P pidfile] [-v] [-V]`

**选项** http://manpages.ubuntu.com/manpages/lucid/man8/sslh.8.html

**示例**
```
# 在 /etc/default/sslh 中配置
RUN=yes
DAEMON_OPTS="-u sslh -p 0.0.0.0:443 -s 127.0.0.1:443 -P /var/run/sslh.pid"
# 启动
/etc/init.d/sslh start
```

## stunnel

**描述** `stunnel` 是一个为隧道提供 SSL/TLS 代理的程序。其原理是将未加密的连接封装在 SSL/TLS 隧道中。它可以用于为原生不支持 SSL 的应用程序提供加密，或为远程服务器提供客户端侧代理。

**用法** `stunnel [options] [config file]`

**选项**
`-f` 前台运行
`-d` 后台运行
`-c` 配置文件
`-v` 显示调试输出

**示例**
```
# 客户端配置
[my-server]
client = yes
connect = example.com:443
```

## netcat

**描述** `netcat` 是一种用于从 TCP 和 UDP 连接读取和写入数据的通用网络工具。它通常被称为网络“瑞士军刀”。

**用法** `nc [options] [host] [port]`

**选项**
`-l` 监听模式
`-p` 端口号
`-u` 使用 UDP
`-v` 详细输出
`-w` 超时

**示例** `nc -lv -p 8080`

## Weevely

**描述** `Weevely` 是一个模拟 SSH 连接的隐蔽 PHP Web shell。它是 Web 应用后渗透阶段的重要工具，可以用作隐蔽后门，或作为管理合法 Web 账户（即使是免费托管账户）的 Web shell。只需在目标 Web 服务器上生成并上传 PHP 代码，然后在本地运行 `Weevely` 客户端来传输 shell 命令即可。更多信息：https://github.com/epinnna/Weevely/wiki/Tutorial

**用法** `/.weevely generate <password> [output path]`

**用法** `/.weevely <url> <password>`

**用法** `/.weevely <url> <password> "<command>"`

**选项** `/.weevely :help`

**示例** `/.weevely.py generate p4ssword` （服务端安装）

**示例** `/.weevely.py http://target.org/w.php p4ssword "uname"`

**示例** `/.weevely.py http://target.org/w.php p4ssword ":system.info client_ip"`

## [53] 逆向工程：调试器

- `edb-debugger`
- `ollydbg`

### edb-debugger

**描述** `EDB` (Evan's Debugger) 是一个基于 Qt4 的二进制模式调试器，目标是具有与 `OllyDbg` 相当的可用性。它采用插件架构，因此可以轻松添加新功能。

**用法** n/a；GUI 工具

**示例** `.edb --symbols /lib/libc.so.6 > symbols/libc.so.6.map` （安装插件）
