
`/usr/lib/amanda` 下的文件都是客户端侧的 `amanda` 程序，所以那部分很容易处理。剩余的文件是原始源码包的一部分。`Amanda` 不会安装这些文件，但它们包含了用户应该看到的信息。

由于 `RPM` 无法按照列出的方式打包这些文件，让我们先跳过 `%files` 列表，检查服务器子包的列表：

`+ %files server`

`usr/sbin/amadmin`

`usr/sbin/amcheck`

`usr/sbin/amcleanup`

`usr/sbin/amdump`

`usr/sbin/amflush`

`usr/sbin/amlabel`

`usr/sbin/amrestore`

`usr/sbin/amtape`

`usr/lib/amanda/taper`

`usr/lib/amanda/dumper`

`usr/lib/amanda/driver`

`usr/lib/amanda/planner`

`usr/lib/amanda/reporter`

`usr/lib/amanda/getconf`

`usr/lib/amanda/chg-generic`

`usr/man/man8/amanda.8`

`usr/man/man8/amadin.8`

`usr/man/man8/amcheck.8`

`usr/man/man8/amcleanup.8`

`usr/man/man8/amdump.8`

`usr/man/man8/amflush.8`

`usr/man/man8/amlabel.8`

`usr/man/man8/amrestore.8`

`usr/man/man8/amtape.8`

`README`

`COPY`

`docs/INSTALL`

`docs/KERBEROS`

`docs/SUNOS4.BUG`

`docs/SYSTEM.NOTES`

`docs/TAPE.CHANGERS`

`docs/WHATS.NEW`

`docs/MULTITAPE`

`example`

## 20.4 软件包构建

`/usr/sbin` 下的文件是 `amanda` 管理员为了执行备份和恢复而运行的程序。`/usr/lib/amanda` 下的文件是在备份期间执行实际工作的服务器侧程序。随之后的是许多 `man` 页面：每个由 `amanda` 管理员运行的程序对应一个，还有一个关于 `amanda` 概述的页面。

最后还有许多未安装的文件，但它们对于客户端子包的使用非常有用。虽然这些文件与客户端子包的一部分有所重叠，但额外的文件讨论了只有 `amanda` 管理员感兴趣的功能。这里还包含一个 `example` 子目录，它包含几个用于 `amanda` 服务器的示例配置文件。

与客户端的 `%files` 列表一样，最后的文件无法按照我们列出的方式被 `RPM` 打包。我们需要使用一些 `RPM` 技巧来将它们打包。

### 应用指令

由于我们希望客户端子包包含那些通常不安装的文件，而且由于这些文件是文档，让我们对它们使用 `%doc` 指令。这将起到两点作用：

- 1. 当安装客户端子包时，它将引导 `RPM` 将它们放置在 `/usr/doc` 中一个包特定的目录中。
- 2. 它会将这些文件标记为文档，使用户可以通过简单的 `rpm -qd` 命令轻松地跟踪文档。

在查看 `%files` 列表的过程中，显然 `/usr/lib/amanda` 目录将只包含来自两个 `amanda` 子包的文件。如果删除了子包，该目录将仍然存在，这不会产生任何问题，但并不想象中那么整洁。但如果我们将该目录添加到该目录，`RPM` 将自动打包目录中的每一个文件。由于这些文件既是客户端也是服务器子包的一部分，我们需要使用 `%dir` 指令来指示 `RPM` 只打包目录。

在这些更改之后，客户端 `%files` 列表看起来是这样的：

```
%files client
%dir /usr/lib/amanda/
%usr/lib/amanda/amamad
%usr/lib/amanda/sendsize
%usr/lib/amanda/calcsize
%usr/lib/amanda/sendbackup-dump
%usr/lib/amanda/selfcheck
%usr/lib/amanda/sendbackup-gnutar
%usr/lib/amanda/runtar
%doc README
%doc COPYRIGHT
%doc docs/INSTALL

## %doc docs/SYSTEM.NOTES
%doc docs/WHATS.NEW
```

我们对对服务器 `%files` 列表应用了相同的指令：

```
+ %files server
usr/sbin/amadmin
usr/sbin/amcheck
usr/sbin/amcleanup
usr/sbin/amdump
usr/sbin/amflush
usr/sbin/amlabel
usr/sbin/amrestore
usr/sbin/amtape
%dir /usr/lib/amanda/
/usr/lib/amanda/taper
/usr/lib/amanda/dumper
/usr/lib/amanda/driver
/usr/lib/amanda/planner
/usr/lib/amanda/reporter
/usr/lib/amanda/getconf
/usr/lib/amanda/chg-generic
/usr/man/man8/amada.8
/usr/man/man8/amadmin.8
/usr/man/man8/amcheck.8
/usr/man/man8/amcleanup.8
/usr/man/man8/amdump.8
/usr/man/man8/amflush.8
/usr/man/man8/amlabel.8
/usr/man/man8/amrestore.8
/usr/man/man8/amtape.8
%doc README
%doc COPYRIGHT
%doc docs/INSTALL
%doc docs/KERBEROS
%doc docs/SUNOS4.BUG
%doc docs/SYSTEM.NOTES
%doc docs/TAPE.CHANGERS
%doc docs/WHATS.NEW
%doc docs/MULTITAPE
%doc example
```

你会注意到我们忽略了对 `man` 页面使用 `%doc` 指令。原因是 `RPM` 会自动将任何指向 `/usr/man` 的文件标记为文档。现在我们的 `spec` 文件有了完整的标记、定义了子包、拥有可以工作的构建脚本，以及每个子包的 `%files` 列表。我们为什么不尝试构建呢？

### 20.4 软件包构建

```
# rpm -ba amanda-2.3.0.spec

* Package: amanda

* Package: amanda-client

* Package: amanda-server
```

```
echo %build

Executing: %build

+ cd /usr/src/redhat/BUILD

+ cd amanda-2.3.0

+ make

Making all in common-src

...
echo %install

Executing: %install

+ cd /usr/src/redhat/BUILD

+ cd amanda-2.3.0

+ make install

Making install in common-src

...
```

```
echo %doc

Executing: %doc

Binary Packaging: amanda-client-2.3.0-6

Finding dependencies...

Requires (3): libc.so.5 libdb.so.2

usr/doc/amanda-client-2.3.0-6

usr/doc/amanda-client-2.3.0-6/COPYRIGHT

usr/doc/amanda-client-2.3.0-6/INSTALL
```
