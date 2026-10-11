
![](img/7933c44717ab0711177ea7153f959fc5_238_0.png)

不同的选项。本节将描述构建选项，并指出 Red Hat 5.2/6.0 发行版中使用的选项。

为了本目录中的示例，我们假设 TCP\_wrappers 源树已加载到 /usr/src/tcp\_wrappers。TCP\_wrappers 的编译时选项全部通过 Makefile 控制。这是你在执行 make 之前需要进行所有必要更改的地方。表 10.1 列出了 Makefile 中的选项（称为宏）、它们的含义，以及该选项是否用于编译 Red Hat 5.2/6.0 中找到的二进制文件。

## 表 10.1 TCP\_Wrappers 编译时选项

| 选项 | 描述 | Red Hat 使用情况 |
| :--- | :--- | :--- |
| REAL\_DAEMON\_DIR | 网络守护进程（如 in.telnetd 和 in.ftpd）所在的完全限定目录。 | /usr/sbin |
| TLI | 用于开启 System V.4 风格的传输层接口 (TLI) 支持。 | 否 |
| RANLIB | 建立索引以加快库链接速度。 | 默认 |
| ARFLAGS | 指定与 ar 一起使用的标志，如下所述。 | 默认 |
| AR | 创建、修改和提取存档或库。 | 默认 |
| AUX_OBJ | 指定用于链接的额外目标文件。 | 无 |
| STRINGS | 指定各种字符字符串比较和操作例程。如果 C 库不包含它们，则使用此选项。 | 否 |
| LIBS | 指定在链接时包含的目标库。 | 无 |
| SYSTYPE | 指定系统特定的编译器选项。 | 无 |
| BUGS | 指定提供已知系统 bug 解决方案的宏。 | 默认 |
| NETGROUP | 指定使用 NIS 网络组。如果你正在使用网络组，请打开此选项。 | 否 |
| VSYLOG | 如果系统支持 vsylog 函数调用，请使用此选项。默认情况下会打开，即使你的系统不使用此函数，也不会导致问题。 | 是 |
| STYLE | 如 `hosts_options(5)` man 手册页中所述，开启语言扩展。它包含宏 PROCESS_OPTIONS。默认情况下是关闭的。 | 是 |
| FACILITY | 指定用于日志记录的 syslog 设施。默认是 LOG_MAIL（在 /etc/syslog.conf 中指定为 mail）。可以通过 SEVERITY 选项动态更改；参见第 203 页的表 10.3。 | LOG_AUTH/PRIV |
| SEVERITY | syslog 级别。默认是 LOG_INFO（在 /etc/syslog.conf 中指定为 info）。可以通过 SEVERITY 选项动态更改；参见第 203 页的表 10.3。 | 默认 |
| DOT | 使主机名后添加一个 "."，以减少 DNS 搜索时间。如果你不使用 DNS，你可能希望关闭此功能，这也是默认设置。请注意，Red Hat 5.2/6.0 启用了此功能，这意味着如果你不使用 DNS，你应该将其关闭并重新编译。 | 是 |
| AUTH | 始终尝试通过 RFC931 调用查找远程用户名。默认是关闭的。开启后，当访问控制文件要求时，将执行 RFC931 调用。 | 否 |
| RFC931_TIMEOUT | 将 RFC931 查询的默认超时时间设置为 10 秒。可以通过 `rfc931` 选项动态更改；参见第 203 页的表 10.3。 | 默认 |
| UMASK | 设置 tcpd 下运行的进程的 umask。默认值为 022。 | 默认 |
| ACCESS | 启用主机访问控制。默认是开启的。 | 是 |
| TABLES | 指定访问控制文件的位置。默认情况下，它们是 /etc/hosts.allow 和 /etc/hosts.deny。 | 默认 |
| PARANOID | 此选项导致执行反向（IP 地址到主机名）查找。当反向查找提供与正向查找冲突的信息时，此选项会自动断开连接。关闭此选项仅禁用此机制的自动化性质；仍可以通过 PARANOID 选项调用 paranoid 模式；参见第 203 页的表 10.3。 | 否 |
| HOSTNAME | 选择自动化的客户端主机名查找。默认情况下是开启的。关闭此选项仅允许通过访问控制文件控制主机名查找。 | 否 |
| KILL_OPT | 如果开启，拒绝任何在 IP 头中启用了源路由的连接请求。默认是关闭的。 | 是 |

对表 10.1 的几点说明是必要的。在“Red Hat 使用情况”列中，“否”表示未使用或关闭了指定的选项（在 *Makefile* 中用 # 字符注释掉）。“是”表示使用了该选项或将其开启（取消注释）。“默认”表示 *Makefile* 中为该选项提供了多个选择，并且使用了最初取消注释的那个。请确保阅读 *README* 文件和 man 手册页，包括 *hosts_access*、*hosts_options*、*tcpd*、*tcpdchk* 和 *tcpdmatch*。这些文件最初都位于 */usr/src/tcp_wrappers* 顶级构建目录中。

## 顺便说一下...

如果你想知道 Red Hat 的人为他们的发行版使用了哪些编译时选项，事实是，他们在一个以 .spec 为后缀的命名适当的文件中维护此信息。此文件是源 *RPM* 的一部分，因此当你安装它时，它默认会位于目录 */usr/src/redhat/SPECS* 中。对于 *TCP_wrappers*，该文件名为 *tcp_wrappers-7.6.spec*。要确定编译时选项，请在此文件中搜索 *Patch* 关键字，它将指定补丁文件的名称；在这种情况下是 *tcpw7.2-config.patch*，它位于目录 */usr/src/redhat/SOURCES* 中（使用 *locate* 或 *find* 确定位置）。该文件是简单的 *diff* 输出，可以使用 patch 应用于 *TCP_wrappers Makefile* 或通过阅读来确定使用了哪些选项。请注意，该文件会在被删除的行前报告 –，在添加的行前报告 +。虽然 *TCP_wrappers* 并非如此，但你经常会在 .spec 文件中发现由 make 调用指定的额外编译时选项。此文件也可以用于构建其程序。有关更多详细信息，请参阅第 28 页 *RPM Resources* 中引用的 *Maximum RPM*。

## 为 TCP\_Wrappers 运行 make linux

一旦你确定了想要使用哪些选项，请通过相应修改 *TCP_wrappers Makefile* 来实现它们。即使你打算使用表 10.1 中描述的默认值，你也必须编辑 Makefile 并取消注释适当的单个 REAL\_DAEMON\_DIR 实例，或进行适当的修改条目。此外，在运行 make 之前，你还需要进行以下更改。

编辑 /usr/src/tcp\_wrappers（或你放置源树的任何位置）中的 Makefile，并更改条目

```
CFLAGS = -O -DFACILITY=${FACILITY} $(ACCESS) $(PARANOID) $(NETGROUP) \
```

为

```
CFLAGS = -DFACILITY=${FACILITY} $(ACCESS) $(PARANOID) $(NETGROUP) \
```

也就是说，删除 -o。继续编辑 Makefile 并更改条目

```
linux:
@make REAL_DAEMON_DIR=${REAL_DAEMON_DIR} STYLE=${STYLE} \\
        LIBS = RANLIB=ranlib ARFLAGS=rv AUX_OBJ=setenv.o \\
        NETGROUP= TLI= EXTRA_CFLAGS="-DBROKEN_SO_LINGER" all
```

为

```
linux:
@make REAL_DAEMON_DIR=${REAL_DAEMON_DIR} STYLE=${STYLE} \\
        LIBS = RANLIB=ranlib ARFLAGS=rv AUX_OBJ= \\
        NETGROUP= TLI= \\
        EXTRA_CFLAGS="-DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED" all
```

此处显示的更改删除了 setenv.o 并添加了 -DSYS_ERRLIST_DEFINED。现在你准备好运行 make linux 了。示例 10-3 显示了一些输出。编译完成！

## 示例 10-3 make linux 输出示例

```
# make linux
make[1]: Entering directory '/usr/src/tcp_wrappers'
cc -DFACILITY=Log_MAIL -DHOSTS_ACCESS -DPARANOID -DGNETPEERNAME_BUG \
 -DDBROKEN_FGETS -DLIBC_CALLS_STKOK -DDAEARNUMASK=022 -DREAL_DAEMON_DIR='/usr/
sbin' -DSEVERITY=Log_INFO -DRCF931_TIMEOUT=10 -DHOSTS_DENY='/etc/hosts.deny' \
 -DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED \
 -Dvsyslog=mvsySlog -DALWAS_HOSTNAME -c tcpd.c
cc -DFACILITY=Log_MAIL -DHOSTS_ACCESS -DPARANOID -DGNETPEERNAME_BUG \
 -DDBROKEN_FGETS -DLIBC_CALLS_STKOK -DDAEARNUMASK=022 -DREAL_DAEMON_DIR='/usr/
sbin' -DSEVERITY=Log_INFO -DRCF931_TIMEOUT=10 -DHOSTS_DENY='/etc/hosts.deny' \
 -DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED \
 -Dvsyslog=mvsySlog -DALWAS_HOSTNAME -c hosts_access.c
...
<lots of output snipped>
...
cc -DFACILITY=Log_MAIL -DHOSTS_ACCESS -DPARANOID -DGNETPEERNAME_BUG \
 -DDBROKEN_FGETS -DLIBC_CALLS_STKOK -DDAEARNUMASK=022 -DREAL_DAEMON_DIR='/usr/
sbin' -DSEVERITY=Log_INFO -DRCF931_TIMEOUT=10 -DHOSTS_DENY='/etc/hosts.deny' \
 -DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED \
 -Dvsyslog=mvsySlog -DALWAS_HOSTNAME -c tcpdchck.c
```
