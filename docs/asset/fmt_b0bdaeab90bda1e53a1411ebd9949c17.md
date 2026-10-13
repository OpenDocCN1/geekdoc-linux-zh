
```
homeboys: :include/home/alphonse/homeboys.aliases
```

假设文件`/home/alphonse/homeboys.aliases`包含：

```
alphonse
joe
betty
george
```

效果与此别名相同：

```
homeboys: alphonse, joe, betty, george
```

该指令对于自动生成、频繁或由邮件管理员以外的用户管理的列表非常有用。如果你发现某个用户要求频繁更改邮件别名，你可能希望将其纳入你的控制。你必须小心；最新版本的 Sendmail 对其引用的文件权限非常挑剔。如果这些任何文件或父目录具有组或世界可写权限，这些文件可能会被忽略，这可能导致 sendmail 停止工作甚至无法启动。这类问题通常被记录在你的系统消息文件（`/var/log/messages`或`/var/log/maillog`，取决于`syslog`的配置）。

# SMTP 与协议

第 7 章

183

# 邮件发送到程序

它也可以用于将邮件内容发送到程序。例如，许多邮件列表都设置了这种功能，你可以向一个特殊地址`list-request`发送邮件来获取有关该列表的信息或订阅该列表。信件的正文通常包含一个单词，如`help`或`subscribe`，这会触发程序向发送者邮件寄送一个信息文件。假设`gonzo`邮件列表有这样一个地址，名为`gonzo-request`：

```
gonzo-request: |/usr/local/lib/auto-gonzo-reply
```

以别名的形式，管道符号（`|`）告诉`sendmail`使用程序邮件发送器，该程序通常定义为`/bin/sh`（参见本章后文“M 运算符：邮件发送器定义”）。`sendmail`将消息传递到`/usr/local/lib/auto-gonzo-reply`的标准输入，如果它正常退出，`sendmail`就认为邮件已送达。

# 邮件发送到文件

你也可以创建一个别名，让`sendmail`发送到文件。这种别名以正斜杠（`/`）开头，后面将是你想要追加的文件完整路径。一个例子是`nobody`别名，这在运行网络文件系统（NFS）的系统中很常见：

```
nobody: /dev/null
```

指定文件的别名会导致`sendmail`将其消息追加到命名的文件中。由于特殊文件`/dev/null`是UNIX的垃圾桶（bit-bucket），此别名只是直接将邮件丢弃。

# 设置 sendmail

最简单的方法是展示如何设置`sendmail` RPM软件包以及`sendmail-cf`包，后者安装了构建你自定义配置文件所需的所有文件。接下来，选择一个与你的站点需求紧密匹配的`sendmail.mc`文件，并根据需要对其进行调整。然后，你需要使用`make`工具制作一个`sendmail.cf`。接着，测试`sendmail`及其配置文件。最后，安装`sendmail.cf`和其他辅助文件。

![](img/fbfff30e42d507bc7531108a281d6cf4_220_0.png)

# 图 7.1

红帽控制面板。

![](img/fbfff30e42d507bc7531108a281d6cf4_221_0.png)

点击“运行级别编辑器”（Runlevel editor）后，你将看到如图 7.2 所示的多个运行级别。确保`sendmail`位于你要求的所有运行级别中。默认情况下，它应该存在于所有显示的运行级别中。如果不是，只需点击最侧的窗口，向下滚动到`sendmail`，选择它，然后点击“添加”（Add）并选择运行级别 3。

# 图 7.2

运行级别编辑器。

![](img/fbfff30e42d507bc7531108a281d6cf4_221_1.png)

此外，如果你的系统还没有别名文件（aliases file），你必须创建一个。如果是红帽系统（Red Hat），它将是`/etc/aliases`，但根据你的UNIX版本，某些系统可能会将其置于`/usr/lib/aliases`。别名文件的位置在`sendmail.cf`中给出，因此你可以将其放在任何你需要的地方。你可能还需要修改系统的DNS数据库，但这些信息在这里没有介绍（参见第 17 章）。未来的Sendmail版本会将所有辅助`sendmail`文件存放在`/etc/mail`目录。

# 获取源码

红帽Linux自带了`sendmail` 8.9.3。幸运的是，这是编写本书时的最新版本。如果你担心安全（你确实应该担心），你将希望通过定期检查`comp.security.announce`新闻组来跟踪任何新版本的发布。`sendmail`的最新版本始终可以在`http://www.sendmail.org`找到。当发现安全漏洞时，会发布新版本或补丁，你应该在新版本发布后尽快升级自己的系统。等待红帽发布已应用新补丁的RPM包是明智的；否则，你需要获取补丁并将其应用到源码中，就像处理其他红帽配置更改一样。这一过程绝非易事。请检查`ftp://updates.redhat.com/6.0/i386`或世界各地的各种红帽镜像站点以获取红帽RPM更新。

注意，下载文件的示例名称取决于`sendmail`的最新版本：对于红帽6.0中包含的`sendmail`，`sendmail` RPM被称为`sendmail-8.9.3-10.i386.rpm`。此外，由于文件是压缩的，在传输它们之前必须给FTP提供二进制传输命令。注意，你应该将完整的电子邮件地址作为FTP密码——例如，`mylogin@gonzo.gov`。

# 解包源码并编译 sendmail

只有当尚未以RPM发布`sendmail`新版本，且你立即需要新功能或修复时，才需要阅读本节。假设你已经从`ftp://ftp.sendmail.org`下载了源码。

现在你有了源码，需要解开它。由于这是一个压缩`tar`包，你必须首先解压缩它，然后从`tar`存档中提取单个文件。执行此操作的示例命令为：

```
root@gonzo src]# tar xzvf sendmail-8.9.3-tar.gz
```

现在准备好编译`sendmail`了。但在之前阅读以下文件，它们包含了关于你下载的特定版本的最新消息：

- `RELEASE_NOTES`
- `KNOWNBUGS`
- `READ_ME`

你可能还想检查位于`http://www.sendmail.org/faq`的Sendmail常见问题解答（FAQ）。这是关于常见错误或如何设置特定配置的有用信息来源。

# 配置服务 第二部分

还要注意，《Sendmail 安装与操作指南》（SIOG）位于`doc/`子目录中。现在运行`cd`查看目录中有哪些文件：

```
root@gonzo src]# cd sendmail-8.9.3/src
root@gonzo src]# ls
```

`Makefile` `collect.c` `parseaddr.c` `srvmtp.c`

`Makefiles` `conf.c` `mailq.o` `pathname.h` `stab.c`

`READ_ME` `conf.h` `mailq.1` `queue.c` `stats.c`

`TRACEFLAG` `convtime.c` `mailists.h` `readcf.c` `sysexits.c`

# 表 7.1 续表

| 命令字符 | 命令语法与示例 | 功能 |
| --- | --- | --- |
| D | `DX string` | 定义宏 `x`，其字符串值为 `string`。 |
| D | `DMhub.gonzo.gov D(MacroName}value` | 定义长宏 `(MacroName)` 的值为 `value`，并在稍后通过 `${MacroName}` 引用。 |
| C | `D{Relay}mailhub.gonzo.gov CX word1, word2, and等.` | 将类 `X` 定义为 `word2` 等等。 |
| F | `Clocalhost myucname FX/path/to/a/file` | 通过文件读取并定义类 `x`。 |
| H | `Fw/etc/mail/host_aliases H7mailerflag?name:template H7F?From: Sq` | 定义邮件头。`OX` 选项参数 | 设置选项 `x`。绝大多数命令行选项可以在 `sendmail.cf` 中设置。 |
| P | `OL9 # 设置日志级别为 9 Pclass=nn` | 根据邮件的类别设置邮件投递优先级。 |
| V | `Pjunk=-100 Vn` | 告诉 V8 `sendmail` 配置文件的版本级别。 |
| K | `Kname class arguments Kuuchosts hash /etc/mail/uucphsts` | 定义键文件（数据库映射）。 |
| M | `Mname, field_1=value_1... Mprog, P=/bin/sh,F=lsD,A=sh -c su` | 定义邮件传输器（mailer）。 |
