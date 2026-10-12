
长期使用 `nslookup` 的用户可能会惊讶地发现老朋友被收起来了。嗯，消息并不像你想的那么糟——BIND 团队只是试图减少其工具之间的重叠。

在最简单的用法中，`host` 允许你从命令行将主机名解析为 IP 地址。例如：

```
[root@tux root]# host theorb.com
thorb.com has address 209.133.83.16
```

我们也可以使用 `host` 进行反向查找。例如：

```
[root@tux root]# host 209.133.83.16
16.83.133.209.IN-ADDR.ARPA domain name pointer taz.hyperreal.org
```

这可能导致各种有趣的发现。在这种情况下，我们看到 `thorb.com` 与 `taz.hyperreal.org` 是相同的。很可能 `taz.hyperreal.org` 也在“虚拟托管”其他域。

![](img/ec2066d370d3af1a767664d36aa7ddfe_359_0.png)

如果你熟悉 `nslookup`，别担心，它仍然存在。然而，由于 BIND 团队正试图让人们远离它，当你需要查找 A 记录和 PTR 记录以外的记录，或者需要查询非你自己的服务器时，请考虑使用 `dig` 工具（下文将讨论）代替。

## dig

域名信息检索器 `dig` 是收集 DNS 服务器信息的绝佳工具。`dig` 命令的典型格式为

```
[root@tux /root]# dig @server domain query-type
```

其中 `@server` 是你想要查询的 DNS 服务器的名称，`domain` 是你感兴趣要查询的域名，而 `query-type` 是你试图获取的记录名称（A, MX, NS, SOA, HINFO, TXT, 或 ANY）。

例如，要从 DNS 服务器 `ns1.ucsd.edu` 获取域 `whitehouse.gov` 的 `mx` 记录，你需要运行：

```
[root@ford /root]# dig @ns1.ucsd.edu whitehouse.gov mx
```

`dig` 程序功能极其强大。你应该阅读随 `dig` 安装的手册页，以学习如何使用其中一些更高级的功能。

## whois

**whois** 命令用于确定域的拥有权。有关域所有者信息并非其记录的强制部分，通常也不会放置在 TXT 或 RP 记录中。因此，你需要使用 **whois** 技术来收集这些信息，该技术会报告域的实际所有者，以及所有者的传统邮件地址、电子邮件地址和技术联系电话。

```
[root@ford root]# whois collab.net
Whois Server Version 1.3

Domain names in the .com, .net, and .org domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.

   Domain Name: COLLAB.NET
   Registrar: NETWORK SOLUTIONS, INC.
   Whois Server: whois.networksolutions.com
   Referral URL: http://www.networksolutions.com
   Name Server: NS.HYPERREAL.ORG
   Name Server: NS1.COLLAB.NET
   Name Server: NS2.COLLAB.NET
   Name Server: NS3.COLLAB.NET
   Updated Date: 05-Nov-2001

>>> Last update of whois database: Thu, 26 Oct 2000 06:47:54 EDT <<<
The Registry database contains ONLY .COM, .NET, .ORG, .EDU domains and Registrars.

Found cronic referral to whois.networksolutions.com.

The Data in the VeriSign Registrar WHOIS database is provided by VeriSign for information purposes only, and to assist persons in obtaining information about or related to a domain name registration record. VeriSign does not guarantee its accuracy. Additionally, the data may not reflect updates to billing contact information. By submitting a WHOIS query, you agree to use this Data only for lawful purposes and that under no circumstances will you use this Data to: (1) allow, enable, or otherwise support the transmission of mass unsolicited, commercial advertising or solicitations via e-mail, telephone, or facsimile; or (2) enable high volume, automated, electronic processes that apply to VeriSign (or its computer systems). The compilation, repackaging, dissemination or other use of this Data is expressly prohibited without the prior written consent of VeriSign. VeriSign reserves the right to terminate your access to the VeriSign Registrar WHOIS database in its sole discretion, including without limitation, for excessive querying of the WHOIS database or for failure to otherwise abide by this policy. VeriSign reserves the right to modify these terms at any time. By submitting this query, you agree to abide by this policy.

Registrant:
Collaboration Networks Inc. (COLLAB6-DCM)
8000 Marina Blvd, Suite 600
Brisbane, CA 94005
US

Domain Name: COLLAB.NET

Administrative Contact, Technical Contact:

Hostmaster General (JBI348-ORG) hostmaster@COLLAB.NET

Collabnet  
8000 Marina Blvd, Suite 600  
Brisbane, CA 94005  
US  
650-228-2500  
Fax: 650-228-2501

Record expires on 13-May-2003.  
Record created on 13-May-1999.  
Database last updated on 17-Aug-2002 03:38:04 EDT.

Domain servers in listed order:

NS1.COLLAB.NET 64.125.134.21  
NS2.COLLAB.NET 64.125.178.141  
NS3.COLLAB.NET 63.211.145.15  
NS.HYPERREAL.ORG 209.153.83.22
```

保持自有域的 **whois** 信息最新非常重要。如果发生非常规事件，例如你的站点遭受攻击或被变成垃圾邮件中继服务器，你最有可能通过电话而不是电子邮件被联系。在这种情况下，没有当前且相关的信息可能会给你造成很大的伤害。

## 其他参考资料

显然，像 DNS 这样存在已久的协议无法在几页短文中被总结。如果你需要探索超出本模块讨论范围之外的 DNS 内容，我强烈推荐以下文献：

- *DNS and BIND, Fourth Edition*，由 Paul Albitz 和 Cricket Liu 编写（O’Reilly & Associates, 2001）出色地深入了 DNS 真正复杂的细节。如果你想要进行子域划分、进行 DNS 负载均衡，或者基本上做任何不寻常的事情，请拿起这本书。你正在阅读这样的模块是获得合理扎实理解并上手的好方法，但正是像 DNS and BIND 这样的书让你能飞得更高。
- 欲了解底层运作的更多细节，参见 Richard Stevens 编写的 *TCP/IP Illustrated, Volume 1: The Protocols*（Addison-Wesley, 1994–1996）。它包含一个专门关于 DNS 的章节，其中有逐包分析和关于其如何运作的基本解释。

有几个与 DNS 相关的 RFC，其中最著名的是 1034 和 1035。其中几个包含在 BIND 文档中，可以在 Red Hat 的 `/usr/share/doc/bind-9.2.1/rfcs/` 目录中找到。你也可以从 http://www.rfc-editor.org 在线获取它们。如果你对前沿技术感到好奇，请访问 Internet Engineering Task Force (IETF) 的 http://www.ietf.org 查看他们的最新动态。

## 模块总结

在本模块中，我们涵盖了启动各种类型 DNS 服务器所需的所有信息。我们讨论了

- Internet 上的名称解析
- `/etc/hosts` 文件
- 配置 Linux 客户端使用 DNS 的过程
- 配置 DNS 服务器作为主服务器、从服务器和缓存服务器
- 建立站点所需的记录类型
- `named.conf` 文件中大多数配置选项
- 用于配合 DNS 服务器进行故障排除的工具
- 额外的信息来源

凭借 BIND 文档中关于服务器配置方式的信息，以及本模块中呈现的完整服务器的实际配置文件，你应该能够从头到尾执行完整的安装。

就像任何软件一样，没有完美的，BIND 和这里讨论的相关文件和程序可能会出现问题。别忘了也查看专门致力于 DNS 和 BIND 的网站以及各种新闻组以获取额外信息。

你会发现很多人可以帮助你解决你的问题。记住在你自己学会之后再去帮助别人！

