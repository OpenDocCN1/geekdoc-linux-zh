
位于`http://www.lids.org/lids-faq/lids-faq.html`的`LIDS FAQ`包含了各种应用程序的`ACL`示例，包括登录、`MySQL`、`BIND`、`OpenSSH`和`Apache`。然而，在某个阶段，你无疑需要创建自己的`ACL`，而确定应用程序所需的访问文件和能力将是你的首要任务。再次，`trace`工具被证明有用，它允许你监控应用程序执行的所有系统调用，因此是它尝试访问的所有文件。常识也可以提供帮助：如果应用程序需要绑定到特权端口（如许多网络守护进程那样），它将需要`CAP_BIND_NET_SERVICE`；它是否需要访问读取配置文件或将其写入`/var/run/`？在你部署了`ACL`之后，可以监控`/var/log/messages`以检查违规行为——如有必要——对`ACL`进行调。

## DNS 服务器的示例 LIDS ACL

我们通过查看一个适用于作为 DNS 服务器的机器的`ACL`示例来结束对`LIDS`的讨论。此`ACL`将分为两部分。第一部分是一组通用的规则，实现了基础的访问控制，适用于各种 Linux 系统，例如 DNS 服务器、桌面工作站或具有数百个域名的通用型服务器。第二部分是一组针对`BIND`的特定规则，仔细限制了`named`二进制文件访问的文件和能力。正如之前建议，我们的规则集将以包含一系列`lidsconf`命令的 shell 脚本形式存在。

## 访问控制 377

第一（也是最简单）的一步是将系统二进制文件和库设置为只读（`READONLY`），因为它们很少（合规地）更改。在执行可能更改此类文件的软件更新时，你可以使用`LFS`绕过`ACL`限制。我们将保护的目录是：`/bin`, `/sbin`, `/usr`和`/opt`。

```
/sbin/lidsconf -A -o /bin -j READONLY
/sbin/lidsconf -A -o /sbin -j READONLY
/sbin/lidsconf -A -o /usr -j READONLY
/sbin/lidsconf -A -o /opt -j READONLY
```

注意这些规则没有定义主体，导致它们被应用于系统上的所有进程。请记住，尽管`ACL`是继承的（将`/opt`标记为只读会导致`/opt/man`、`/opt/man1`等变为只读），但这并不跨越文件系统。如果`/usr`是另一个分区，这些规则就不会影响`/etc`，例如，将`/etc`标记为只读会导致

```
/sbin/lidsconf -A -o /networks -j READONLY
/sbin/lidsconf -A -o /ntp.conf -j READONLY
/sbin/lidsconf -A -o /resolv.conf -j READONLY
/sbin/lidsconf -A -o /rc.d -j READONLY
/sbin/lidsconf -A -o /services -j READONLY
/sbin/lidsconf -A -o /shells -j READONLY
/sbin/lidsconf -A -o /ssh -j READONLY
/sbin/lidsconf -A -o /sudoers -j READONLY
/sbin/lidsconf -A -o /sudoers.conf -j READONLY
```

取决于你安装的包，你可能会发现`/etc`中其他值得只读保护的文件。然而，此列表涵盖了最关键的

对`/var/log`设置适当的访问是复杂的。对于大多数文件，我们可以将它们设置为追加（`APPEND`），但`/var/log/wtmp`和`/var/log/lastlog`必须对登录用户可写，并且`halt`二进制

```
/sbin/lidsconf -A -o /var/log -j APPEND
/sbin/lidsconf -A -s /bin/login -o /var/log/wtmp -j WRITE
/sbin/lidsconf -A -s /bin/login -o /var/log/lastlog -j WRITE
/sbin/lidsconf -A -s /bin/init -o /var/log/wtmp -j WRITE
/sbin/lidsconf -A -s /sbin/init -o /var/log/lastlog -j WRITE
/sbin/lidsconf -A -s /sbin/halt -o /var/log/wtmp -j WRITE
/sbin/lidsconf -A -s /sbin/halt -o /var/log/lastlog -j WRITE
```

有了这些访问控制，获得`root`权限的入侵者可以编辑日志文件以隐藏其踪迹。缺点是，`logrotate`工具（定期轮转系统日志工具）将无法运行。虽然可以设置`ACL`允许`logrotate`对`/var/log`执行所需的写入权限，但这可能被入侵者滥用，他们可以多次执行`logrotate`直到包含其踪迹的日志被轮转并最终删除。因此，我们不建议这样做；相反，我们应该禁用`logrotate`，并手动维护日志文件。在大多数系统中，调用`logrotate`的`cron`脚本位于`/etc/cron.daily/logrotate`。删除此文件，或者注释掉其内容。

现在我们将注意力转向专门用于控制`named`二进制文件如何与系统交互的规则，因为我们可以准确预测`named`将访问哪些文件和能力，我们应该能够定义一个

# 访问控制 379

一组严密的规则。我们首先拒绝命名命名主体对整个文件系统的访问：

```
/sbin/lidsconf -A -s /usr/sbin/named -o -j DENY
```

当然，`BIND`将需要能够读取其配置文件`/etc/named.conf`以及存储在`/var/named`中的区域文件：

```
/sbin/lidsconf -A -s /usr/sbin/named -o /etc/named.conf -j READ
/sbin/lidsconf -A -s /usr/sbin/named -o /var/named -j READ
```

```
/sbin/lidsconf -A -s /usr/sbin/named -o /var/run/named -j WRITE
```

这处理了`named`所需的明显文件；但那些不那么明显的文件呢，比如库。如果你读过上一章，你已经知道解决方案是极其实用的`trace`命令，它可以显示进程的系统调用（以及所有对外部文件的访问）。注意，我们使用`-f`选项启动`named`以防止其在后台运行：

```
# strace named -f
```

在允许`trace`运行几小时后，停止进程，并对输出进行`grep`字符串`open`。生成的输出不仅显示了`named`访问的文件，还显示了访问这些文件的模式（例如，读、写等）。此列表可以简化为以下一组`LIDS`规则：
