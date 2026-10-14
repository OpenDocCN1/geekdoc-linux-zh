
case。需要一个额外的字段，称为 Priority，它只是一个数字，用来决定该邮件服务器相对于可能配置的其他服务器的优先级，其中数字越小优先级越高，零为最低。传统上，主邮件服务器的优先级使用 10，其他服务器的优先级则以十为步长递增。所以备份邮件服务器的优先级可以为 20。对这种事实上的标准没有强制执行，因此你也可以使用 0 和 43 来表示主邮件服务器和备份邮件服务器，但遵循传统可能对可能跟随你脚步的任何管理员来说更礼貌。点击 Create 添加邮件服务器记录。

## 应用更改并测试结果

现在我们已经有了在现实世界中充分利用我们的名称服务器所需的最低配置，因此让我们重新加载 BIND 配置并确保它正在工作。首先，通过点击页面右上角的 Module Index 链接返回到 BIND 模块主页。然后点击页面底部的 Apply Changes 按钮，通知 BIND 重新加载其配置文件。

为了测试我们的工作，我们可以使用 host 程序。首先，我们将测试以确保我们的域名可以从我们的名称服务器解析：

```
[joe@delilah joe]$ host swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com has address 192.168.1.1
```

host 命令在本书的故障排除部分有进一步讨论，但我会指出我使用的参数。显然，命令的第一个参数是 swelltech.com，即我想查找的域名。而第二个参数是 192.168.1.1，即我想查询信息的名称服务器。这使我们能够在隔离中轻松设置名称服务器，而无需依赖它进行现实世界的名称服务，以便彻底测试并确认其正常工作。由于上述结果正是我们期望看到的，我们可以继续测试 MX 和 NS 记录，以确保它们也符合我们的预期：

```
[joe@delilah joe]$ host -t mx swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com mail is handled by 10 mail.swelltech.com.
```

这次，我们添加了一个额外的参数 "-t mx"，以指定我们想要检索的记录类型。通过此方法，我们可以检索任何我们想要测试的记录类型。我们目前配置的唯一其他记录类型是 NS 记录，用于指示该域的权威名称服务器，因此我们也将检查它：

```
[joe@delilah joe]$ host -t ns swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com name server ns1.swelltech.com.
```

到目前为止，一切顺利！为了完整性，让我们再进行最后一次查找，看看名称别名与普通地址记录有何不同：

```
[joe@delilah joe]$ host mail.swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

mail.swelltech.com is an alias for swelltech.com.
swelltech.com has address 192.168.1.1
```

假设你的结果一切顺利，你就可以将你的名称服务器投入服务。本章的其余部分专门介绍故障排除方法，以及 host 和 dig 实用程序的更高级用法，[content]
case。需要一个额外的字段，称为 Priority，它只是一个数字，用来决定该邮件服务器相对于可能配置的其他服务器的优先级，其中数字越小优先级越高，零为最低。传统上，主邮件服务器的优先级使用 10，其他服务器的优先级则以十为步长递增。所以备份邮件服务器的优先级可以为 20。对这种事实上的标准没有强制执行，因此你也可以使用 0 和 43 来表示主邮件服务器和备份邮件服务器，但遵循传统可能对可能跟随你脚步的任何管理员来说更礼貌。点击 Create 添加邮件服务器记录。

## 应用更改并测试结果

现在我们已经有了在现实世界中充分利用我们的名称服务器所需的最低配置，因此让我们重新加载 BIND 配置并确保它正在工作。首先，通过点击页面右上角的 Module Index 链接返回到 BIND 模块主页。然后点击页面底部的 Apply Changes 按钮，通知 BIND 重新加载其配置文件。

为了测试我们的工作，我们可以使用 host 程序。首先，我们将测试以确保我们的域名可以从我们的名称服务器解析：

```
[joe@delilah joe]$ host swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com has address 192.168.1.1
```

host 命令在本书的故障排除部分有进一步讨论，但我会指出我使用的参数。显然，命令的第一个参数是 swelltech.com，即我想查找的域名。而第二个参数是 192.168.1.1，即我想查询信息的名称服务器。这使我们能够在隔离中轻松设置名称服务器，而无需依赖它进行现实世界的名称服务，以便彻底测试并确认其正常工作。由于上述结果正是我们期望看到的，我们可以继续测试 MX 和 NS 记录，以确保它们也符合我们的预期：

```
[joe@delilah joe]$ host -t mx swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com mail is handled by 10 mail.swelltech.com.
```

这次，我们添加了一个额外的参数 "-t mx"，以指定我们想要检索的记录类型。通过此方法，我们可以检索任何我们想要测试的记录类型。我们目前配置的唯一其他记录类型是 NS 记录，用于指示该域的权威名称服务器，因此我们也将检查它：

```
[joe@delilah joe]$ host -t ns swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com name server ns1.swelltech.com.
```

到目前为止，一切顺利！为了完整性，让我们再进行最后一次查找，看看名称别名与普通地址记录有何不同：

```
[joe@delilah joe]$ host mail.swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

mail.swelltech.com is an alias for swelltech.com.
swelltech.com has address 192.168.1.1
```

假设你的结果一切顺利，你就可以将你的名称服务器投入服务。本章的其余部分专门介绍故障排除方法，以及 host 和 dig 实用程序的更高级用法，工作 through the examples 可能会为 DNS 在各种应用和环境中的工作原理提供一些见解。

## 故障排除 BIND

有许多工具可用于帮助测试和排除 BIND 配置问题的故障。大多数系统上最简单的工具是 host 命令，它只是执行地址查找或反向地址查找。可以使用 dig 获取更完整的信息。在极旧的系统上，nslookup 可能是这种类型测试唯一可用的选项，但它在许多方面相当令人困惑且不一致，不推荐使用。

### 使用 Host

host 实用程序为查找名称或地址提供了一个非常易于使用的命令行界面。在其最简单的使用形式中，给定主机名作为参数时，它将返回 IP 地址或地址。如果有可用，邮件主机地址或地址也将被返回。如果命令行参数是 IP 地址，将执行反向查找并返回主机名。host 还有一些额外的选项，可能有助于追踪 DNS 问题或测试配置的正确性。你可以查询系统默认名称服务器，也可以将服务器地址附加到命令行的末尾来查询你需要测试的任何名称服务器。

host 的最简单用法是查找地址或名称：

```
[joe@delilah joe]$ host swelltech.com
swelltech.com has address 216.40.244.74
[joe@delilah joe]$ host 216.40.244.74
74.244.40.216.in-addr.arpa domain name pointer swelltech.com.
```

上面，我请求了域名 swelltech.com 的地址，然后是地址 216.40.244.74 的名称。我也可以通过使用 -t ns 命令行选项来请求对域具有权威性的名称服务器。

```
[joe@delilah joe]$ host -t ns google.com
google.com name server ns2.google.com.
google.com name server ns3.google.com.
google.com name server ns4.google.com.
google.com name server ns1.google.com.
```

最后，可以通过使用 -t mx 选项检索 MX 记录：

```
[joe@delilah joe]$ host -t mx yahoo.com
yahoo.com mail is handled by 1 mx2.mail.yahoo.com.
yahoo.com mail is handled by 5 mx4.mail.yahoo.com.
yahoo.com mail is handled by 1 mx1.mail.yahoo.com.
```

在上面的 MX 记录示例中，yahoo.com 定义了三个邮件服务器。MX 记录有一个额外的字段来指示服务器相对于其他服务器的优先级，在这种情况下 mx1.mail.yahoo.com 和 mx2.mail.yahoo.com 的优先级为 1，因此它们将被优先于优先级为 5 的 mx4.mail.yahoo.com，后者只有在其他两个服务器不可用时才会被使用。

**NOTE** 这里没有讨论 host 实用程序的所有选项。要了解所有命令行选项的详细说明，请查阅 host 手册页，无论是通过 Webmin 手册页界面还是从命令行。

-v 选项启用详细输出，其格式与 BIND 自身的主文件格式兼容，因此可以直接导入到 BIND 配置中而无需额外解析或修改。-t 选项允许你指定要对名称服务器执行的查询类型。有许多查询类型，但常用的类型可能包括 cname，它列出主机如果可用的规范名称条目，以及 ns 类型，它列出主机的权威名称服务器。

host 的更详细选项之一是 -a 选项，它将列出主机的所有可用字段，包括所有 A 记录、CNAME 记录、NS 记录等。使用 host 对自己的名称服务器使用此选项是确保它提供你期望的所有信息的良好方法。

### 使用 dig

dig，或 domain information groper，提供查询任何域服务器以获取其服务的域信息的 ability。它在交互模式和批处理查询模式下运行。使用 dig 就像使用 host 一样，在其最简单的模式下你只需输入命令和要查找的名称。然而，dig 默认更详细并提供更广泛的信息阵列，尽管形式上不太易读。

就像 host 一样，可以查询默认系统解析器，也可以查询命令行指定的名称服务器。例如，我可以查询我的本地名称服务器关于 nostarch.com 域的信息。

```
[joe@delilah joe]$ dig @192.168.1.1 nostarch.com

; <<>> DiG 9.2.1 <<>> @192.168.1.1 nostarch.com
;; global options:  printcmd
;; Got answer:
;; ->HEADER<<- opcode: QUERY, status: NOERROR, id: 21448
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

;; QUESTION SECTION:
;nostarch.com.            IN      A

;; ANSWER SECTION:
nostarch.com.            8585    IN      A       66.80.60.21

;; AUTHORITY SECTION:
nostarch.com.            8585    IN      NS      ns1.megapath.net.
nostarch.com.            8585    IN      NS      ns2.megapath.net.

;; ADDITIONAL SECTION:
ns1.megapath.net.        123591  IN      A       66.80.130.23
ns2.megapath.net.        123591  IN      A       66.80.131.5

;; Query time: 281 msec
;; SERVER: 192.168.1.1#53(192.168.1.1)
;; WHEN: Sat Oct 26 19:42:45 2002
;; MSG SIZE  rcvd: 126
```

上面，我们有大量信息，尽管并非全部对我们都有用。首先是 dig 的版本和我们指定的命令行选项。接下来是一些状态信息，包括指示名称无错误检索的 NOERROR 标识符。如果域不存在或无法查询，则会出现 NXDOMAIN 错误或其他错误。接下来是查询的标志。在这种情况下，我们有一个查询和一个答案，它们包含在下面的 QUESTION 和 ANSWER 部分中。接下来的两项告知我们在其后跟随的 AUTHORITY 和 ADDITIONAL 部分的数量。在此
