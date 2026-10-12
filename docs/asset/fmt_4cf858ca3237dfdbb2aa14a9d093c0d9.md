
前两条记录表示`trumpeter`和`parrot`是`swans.foobirds.org`域的权威服务器。最后两条记录表示`arctic`和`trumpeter`是`swans.foobirds.org`域的权威服务器。

另外两条记录属于子域。它们被称为地址记录（address records）：

```
trumpeter.swans  IN  A      172.16.18.15

arctic.terms      IN  A      172.16.6.1
```

这两个地址都用于位于当前域子域中的名称服务器。这些地址记录被称为粘合记录（glue records），因为它们有助于将所有域名连接在一起。为了连接到名称服务器，你必须拥有它的地址。如果`arctic`的地址只能从`arctic`自己获取，就会出现问题。出于这个原因，当子域被委托时，位于子域中的名称服务器名称会被放在父域中。

### 反向域文件

反向域文件将 IP 地址映射到主机名。这与数据库将主机映射到地址的操作相反。

但这之所以被称为反向域的另一个原因是：所有的 IP 地址都是反向书写的。例如，反向域`172.16.5.2`被写为`2.5.16.172.in-addr.arpa`。这种反转是为了使其与域名的结构兼容。IP 地址是从最通用的到最具体的。对于网络地址，它经过子网并最后以主机结束。主机名则相反。它从主机开始，经过子域和域名，最后以顶级域名结束。为了像格式化主机一样格式化地址，地址的主机部分被反向写入，网络部分写在最后。网络地址变成了域名，而主机变成了域内的主机名。

在我们的示例中，网络地址`172.16.0.0`变成了域名`16.172.in-addr.arpa`。该域的区域文件显示在列表 4.12 中。

### 列表 4.12：DNS 反向区域文件

```
;      地址到主机名的映射。

;$TTL 1w

@    IN SOA wren.foobirds.org. sara.wren.foobirds.org. (
       199902702      ; Serial
       21600            ; Refresh
       1800             ; Retry
       60480            ; Expire
       900                ; Negative cache TTL
       IN NS      wren.foobirds.org.
       IN NS      falcon.foobirds.org.
       IN NS      bear.mammals.org.

n1.5  IN FTR     wren.foobirds.org.
2.5 IN PTR robin.foobirds.org.
3.5 IN PTR parrot.foobirds.org.
4.5 IN PTR hawk.foobirds.org.
5.5 IN PTR crow.foobirds.org.
17.5 IN PTR puffin.foobirds.org.
20.5 IN PTR falcon.foobirds.org.
11.2 IN PTR trumpet.ewans.foobirds.org.
1.6 IN NS arctic.terns.foobirds.org.
6 IN NS falcon.foobirds.org.
```

与其他区域文件一样，反向区域以一条 SOA 记录和几条 NS 记录开始，它们的作用与之前解释过的域数据库中的对应项相同，具有相同的字段。

PTR 记录构成了反向域的大部分，因为它们用于将地址翻译为主机名。看第一个 PTR。名称字段`1.5.`不是一个完全限定名称，因此它被解释为当前域，从而我们得到`1.5.16.172-in-addr.arpa`作为名称字段的值。`1.5.16.172-in-addr.arpa`的数据字段是`robin.foobirds.org`。

PTR 记录的数据字段是主机名。`1.5.16.172-in-addr.arpa`的数据字段是`robin.foobirds.org`。`3.5.16.172-in-addr.arpa`的数据字段是`parrot.foobirds.org`。`4.5.16.172-in-addr.arpa`的数据字段是`hawk.foobirds.org`。`5.5.16.172-in-addr.arpa`的数据字段是`crow.foobirds.org`。`17.5.16.172-in-addr.arpa`的数据字段是`puffin.foobirds.org`。`20.5.16.172-in-addr.arpa`的数据字段是`falcon.foobirds.org`。`11.2.16.172-in-addr.arpa`的数据字段是`trumpet.ewans.foobirds.org`。

PTR 记录构成了反向域的大部分，因为它们用于将地址翻译为主机名。看第一个 PTR。名称字段`1.5.`不是一个完全限定名称，因此它被解释为当前域，从而我们得到`1.5.16.172-in-addr.arpa`作为名称字段的值。

```
[root]# service named status

named not running.

[root]# service named: [ OK ]
```

如果你的 Linux 系统没有像 Red Hat 提供的这样的`named`脚本，你可以通过输入`named &`来从命令行启动`named`。然而，`named`很少从命令行启动，因为在每次系统启动时它都会自动运行，而且由于`rndc`信号意味着它不需要停止并重新加载新配置。在讨论`rndc`之前，让我们先看看如何使用信号来让`named`加载新配置并执行其他任务。

### named 信号处理

信号处理是 BIND 版本有所区别的一个领域。BIND 8 及更早版本处理多个信号。BIND 9 仅处理：`SIGHUP`和`SIGTERM`。在 BIND 9 下，`SIGHUP`重新加载 DNS 数据库，而`SIGTERM`终止进程。你可以在 BIND 8 中使用信号，但在 BIND 9 中不能使用。你可以使用`rndc`来控制 BIND，这将在下一节中介绍。尽管如此，BIND 8 接受以下信号。

`SIGHUP`会导致`named`重新加载`named.conf`文件并重新加载命名服务器数据库。使用`SIGHUP`会立即触发重新加载。在主服务器上，这意味着本地数据库文件被重新加载到内存中。在从服务器上，这会立即重新加载本地磁盘副本，并向主服务器发送 SOA 记录查询以检查是否有新配置。

`SIGINT`导致`named`将缓存转储到`named.db`。转储文件包含了本地服务器知道的所有域信息。检查此文件，你将看到服务器已学习信息的完整图景。对于任何 DNS 初学者来说，检查缓存都是一项非常有趣的练习。

使用`SIGUSR1`进行跟踪。每个随后的`SIGUSR1`信号都会增加跟踪级别。跟踪信息被写入`named.run`。如果你要查找的问题发生在启动阶段非常早，以至于`SIGUSR1`信号不起作用，也可以在`named`命令行上使用`-d`开启跟踪。`SIGUSR1`的优势在于它允许在怀疑出现问题时开启跟踪，而无需停止并重启`named`。

`SIGUSR1`的反面是`SIGUSR2`。它关闭跟踪并关闭跟踪文件。发出`SIGUSR2`后，你可以检查该文件，或者如果它变得太大则将其删除。

`kill`命令用于向运行中的进程发送信号。正如其名所示，默认情况下它发送信号。要用它发送不同的信号，请在命令行上指定信号。例如，使用`-INT`发送`SIGINT`信号。`kill`命令行上必须提供进程 ID (PID)，以确保信号发送到正确的进程。

你可以使用`ps`命令或使用`/etc/init.d/named`脚本的`status`参数来获取进程 ID。例如：

```
$ ps ax grep named

271 7 S 0:00 /usr/sbin/named

7138 p0 S 0:00 grep named
```

在某些情况下，你可以通过列出`named.pid`文件来获取进程 ID：

```
$ cat /var/run/named/named.pid
```

通过组合其中一些命令，你可以直接向`named`发送信号。例如，要重新加载命名服务器，你可以输入以下命令：

```
kill -HUP 'cat /var/run/named/named.pid'
```
