
## 开源工具

尽管看起来可能有些矛盾，但 Windows 操作系统也有一些非常优秀的开源工具可用。我们在侦察阶段使用的某些开源工具将在接下来的节中进行讨论。

> 地下室笔记：Windows 开源工具的兴起

多年来，用于渗透测试的 `PERL` 和 `Java` 工具已适用于 Windows 和 Unix 环境。遗憾的是，脚本编写者倾向于使用 shell 转义（shell escapes）来执行复杂任务，这往往将我们用于侦察的工具限制在 Unix 环境。相反的是，随着 `C` 语言和 `.NET` 环境的出现，工具的流行似乎再次增长。这可能归于编码人员追求易用性和灵活性（例如易于图形化界面），但也仅仅是工具之间“共鸣”的一个简单案例。`[jar-dnsbrute](www.sensepost.com/research/)` 位于 `BILE` 软件套件中的 `jar-dnsbrute` 脚本是一个 DNS 暴力破解工具，用于不允许 DNS 区域传输的情况。`jar-dnsbrute` 将使用指定的域名并配合主机名列表来执行正向 DNS 查询。该脚本是多线程的，一次可以设置多达 10 个线程。（见图 1.36）。

`Paradoxical as it may seem, there are some very good open source tools available for the Windows operating system. Some of the open source tools that we use in the reconnaissance phase are discussed in the section that follows.`

> Notes from the Underground: The Emergence of Open Source Tools for Windows

`PERL` and `Java` tools for penetration testing have been available for both the Windows and Unix environments for years. Sadly however, the tendency of script writers to use shell escapes to perform tricky tasks has often limited the tools we use for reconnaissance to the Unix environment. Ironically, the emergence of `C` and the `.NET` environment the popularity of tools appears to be growing again. This probably has to do with the ease and flexibility that coders (think easy graphical interfaces), but also only be a simple case of ‘resonance’ between tool.

The following answer is not:
The following answer is not authoritative:
The following answer is not verified as authentic by the server:
```
syngress.com 940 IN A 155.212.56.73
syngress.com 168867 IN NS ns1.convert.net
syngress.com 168867 IN NS ns2.convert.net
additional information:
ns1.convert.net 106680 IN A 216.41.101.15
ns2.convert.net 106680 IN A 216.41.101.17
```

## dig (Domain Information Groper)

`dig` is a tool used to query DNS name servers, can be used to query DNS lookups, and displays returned data. With `dig`, works similarly to `nslookup` but is more flexible. With `dig`, a user can perform `A`, `TXT`, `MX`, and `NS` queries. (See Figure 1.37.)

## Figure 1.37 MX Lookup via Dig

```
```
