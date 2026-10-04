

# 使用 xinetd 超级服务器 605

列表中以 telnet 开头的前两行显示 TELNET 服务的端口号为 23。此数字告诉 xinetd，任何到达端口 23 的连接请求都是为了 TELNET 服务提供的。随后，配置文件 `/etc/xinetd.d/telnet` 则会告诉 xinetd 如何处理这些请求。

`/etc/xinetd.d/telnet` 中用大括号括的属性具有以下含义：

-   * *flags 属性提供了关于如何运行 xinetd 启动的服务器的具体指令。REUSE 标志意味着如果 xinetd 重启，该服务将保持运行。*注意：*REUSE 标志现在被认为所有服务器都已隐式设置。* 

-   * *socket_type 属性设置为 stream，这告诉 xinetd TELNET 服务使用面向连接的 TCP 套接字与客户端通信。对于使用无连接 UDP 包的服务，此属性被设置为 dgram。* 

-   * *wait 属性设置为 no，这告诉 xinetd 为每个请求启动一个新服务器。如果将此属性设置为 yes，xinetd 将等待服务器退出后才启动下一个。* 

-   * *user 属性提供了 xinetd 用来运行服务器的用户 ID。在这种情况下，服务器以 root 身份运行 TELNET 服务。** 

-   * *log_on_failure 属性告诉在无法启动服务器时记录什么内容。在这种情况下，该属性被设置为 HOST，这意味着如果 xinetd 无法启动 TELNET 服务，它将记录请求服务的远程主机名称。* 

-   * *server 属性指定了为此服务运行的程序。在这种情况下，xinetd 运行 `/usr/sbin/in.telnetd` 程序来提供 TELNET 服务。* 

-   * *disable 属性在设置为 yes 时会关闭该服务。默认情况下，disable 属性设置为 yes 且 TELNET 是关闭的。* 

浏览 Fedora Core 系统上 `/etc/xinetd.d` 目录下的文件，以了解 xinetd 设置为启动的各种类型的服务。其中许多服务（如 finger）提供了入侵者可能用于侵入你系统的信息。如果这些服务尚未禁用，你可能希望通过在包含所有属性的大括号内放置以下行来关闭这些服务：

```
disable = yes
```

另一方面，如果你无法通过 telnet 连接到你的 Fedora Core 系统，请检查 `/etc/xinetd.d` 目录中的相应文件：

| 第八卷 |
| :--- |
| 第 1 章 |
| 管理服务器 |

## 606 运行独立服务器

并确保 disable 属性设置为 no，或者该行被注释掉（通过在行开头放置 # 将其从代码行变为非运行的注释）。

当你对 xinetd 配置文件进行更改时，必须通过输入以下命令来重启 xinetd 服务器：

```
/etc/init.d/xinetd restart
```

如果你想少打一些字符，可以使用以下功能完全相同的命令：

```
service xinetd restart
```

你还可以使用 `chconfig` 命令来禁用和启用由 xinetd 启动的服务。例如，要启用 TELNET 服务，请以 root 身份登录并输入以下命令：

```
chconfig telnet on
```

要再次关闭 TELNET，请输入 `chconfig telnet off`。

## 运行独立服务器

通过 xinetd 启动服务器是一种聪明的方法，但如果一个服务必须频繁启动，这种方法就不够高效。如果 Web 服务器由 xinetd 控制，那么会出现一种情况：每当用户点击 Web 页面上的链接、Web 服务收到请求时，starter 就会被启动一次。对于高需求的服务，以独立方式启动服务器是最好的，即作为守护进程运行——一个持续运行且永不的进程。这意味着服务器监听指定的端口，每当请求到达时，服务器都会通过创建自己的副本来处理它。通过这种方式，只要机器运行，服务器就会一直运行——理论上是永远的。对于 Web 服务器，一种更高效的策略是运行多个服务器副本，并让每个副本处理部分传入请求。

你可以轻松地配置你的 Fedora Core 系统自动启动各种独立服务器。我将在本节中演示。

## 手动启动和停止服务器

要启动未运行的服务，请使用 `service` 命令。例如，如果 Web 服务器 (httpd) 没有运行，你可以通过运行带有以下命令的特殊 shell 脚本来启动它：

```
/etc/init.d/httpd start
```

![](img/d9230b719dc0efd80851f363d8c6f571_632_0.png)

## 运行独立服务器 607

该命令运行 `/etc/init.d/httpd` 脚本并将 `start` 作为参数。如果 http 服务器已经在运行且你想停止它，请带 `stop` 作为参数运行相同的命令，如下：

```
/etc/init.d/httpd stop
```

要停止并启动一个服务器代理，只需使用 `restart` 作为参数：

```
/etc/init.d/httpd restart
```

Fedora Core 包含了另一个名为 `service` 的脚本，它执行相同的工作，但更容易记忆。基本上，你可以去掉 `/etc/init.d` 并将其替换为 `service` 后加一个空格。因此，要启动 httpd，你输入：

```
service httpd start
```

所有可以启动和停止的服务有哪些？答案在 `/etc/init.d` 目录的文件中。要查看它，请输入以下命令：

```
ls /etc/init.d
```

对此命令响应列出的所有文件都是安装在你的 Fedora Core 系统上的服务——你可以根据需要启动和停止它们。例如，这里是 Fedora Core 系统上的典型服务列表：

| acpid | functions | lsa | portmap | single | winbind |
| :--- | :--- | :--- | :--- | :--- | :--- |
| aep1000 | message | postgresql | smart | xfs | |
| anacron | micro_ctl | random | smb | xinded | |
| apmd | httpd | named | rawdevices | smmpd | ypbind |
| atd | netfs | readahead | ypfrowd | | |
| autofs | iptables | netlog | smtrapad | readearly | squid |
| bcm5020 | irda | rbalance | rpcssd | ssh | ypferd |
| cpused | network | - | rpcidmapd | syslog | yum |
| crond | | | | | |
| udev | | | | | |
| cups | | | | | |
| dove | | | | | |
| first | | | | | | |

## 608 运行独立服务器

使用 chconfig

named 在运行级别 0-6 的状态。named 服务的配置位于 `/etc/sysconfig/named`。要更改配置，请使用 `chconfig` 命令。

![](img/d9230b719dc0efd80851f363d8c6f571_632_0.png)

