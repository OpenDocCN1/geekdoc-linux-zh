

拦截代理，或透明地，这意味着用户甚至不需要意识到代理的存在。Web 流量从端口 80 重定向到 Squid 所在的端口，Squid 对浏览器来说就像一个标准的 Web 服务器。

透明使用 Squid 是一个两部分的过程，首先需要正确配置 Squid 以接受非代理请求，其次需要将 Web 流量重定向到 Squid 端口。配置的第一部分在 Squid 模块中执行，而第二部分可以在 Linux 防火墙模块中执行。也就是说，假设你使用的是 Linux，否则你应该查阅 Squid FAQ 透明缓存/代理 [http://www.squid-cache.org/Doc/FAQ/FAQ-17.html] 条目。

## 为透明配置 Squid

为了使 Squid 充当透明代理，它必须配置为接受普通 Web 请求，而不仅仅是（或除了）代理请求。在这里，你将学习该过程的这一部分，检查控制台配置和 Webmin 配置。控制台配置已解释，Webmin 配置在下图所示。

以 root 身份，用你喜欢的文本编辑器打开 squid.conf 文件。该文件的位置取决于你的操作系统和安装方法，通常位于从源码安装时的 /usr/local/squid/etc，或 Red Hat 风格系统上的 /etc/squid。首先你会注意到 http_port 选项。这告诉你 Squid 将监听的端口。默认情况下，这是端口 3128，但如果你需要的话可以更改它。接下来你应该按图 12-19 所示配置以下选项。

![](img/d84604054810a13cacfdac212ebee2f7_271_0.png)

图 12-19：Squid 的透明配置

```
httpd_accel_host virtual
httpd_accel_port 80
httpd_accel_with_proxy on
httpd_accel_uses_host_header on
```

这些选项，如本文件杂项选项部分所述，将 Squid 配置如下。httpd_accel_host virtual 使 Squid 充当任意数量 Web 服务器的加速器，这意味着 Squid 将使用请求头信息来判断用户想要访问哪个服务器，并且 Squid 在与客户端通信时会表现得像一个 Web 服务器。
httpd_accel_port 80 配置 Squid 将请求发送到源服务器的端口 80，即使它可能在另一个端口接收请求，例如 3128。httpd_accel_with_proxy on 允许你继续将 Squid 用作传统代理以及透明代理。这并不总是必要的，但当你尝试使透明工作时，它确实使测试变得容易得多，这将在后面的故障排除部分中进一步讨论。最后，

httpd_accel_uses_host_header on 告诉 Squid 它应根据头中找到的主机名来确定从哪个服务器获取内容。透明配置必须这样设置此选项。

## Linux 防火墙配置用于透明代理

iptables 部分的透明配置同样简单。目标是劫持所有在 HTTP 端口（即端口 80，用数字表示）上的传出网络流量。iptables 以其惊人的功能和灵活性，允许你用一条命令行或一条规则来完成此操作。同样，配置对于 Webmin 界面和控制台配置都显示并讨论。

> 注意 Linux 防火墙模块在 Webmin 版本 1.00 中是新的。所有之前的版本都缺少此模块，因此要执行这些步骤，你需要使用最新的 Webmin 版本。

首次进入 Linux 防火墙模块时，将显示数据包过滤规则。为你的目的，你需要编辑网络地址转换规则。因此，从 Showing IPtable 按钮旁边的下拉列表中选择它，然后单击该按钮以显示 NAT 规则。

现在，通过单击 PREROUTING 部分页面右侧的 Add rule 按钮，在 PREROUTING 链中添加一条新规则。

填写以下字段。应采取的操作应为 Redirect，Target ports for redirect 设置为 3128。接下来你需要指定哪些客户端应重定向到 Squid 端口。如果你知道单个接口上的所有端口 80 流量都应重定向，最简单的方法是指定 Incoming interface，但你也可以指定 Source address 或 network。接下来，将 Network protocol 设置为 Equals TCP。最后，将 Destination TCP or UDP port 设置为 80。单击 Create 以将新规则添加到配置中。再次回到主页面后，单击 Apply Configuration 按钮使新规则生效。最后，将防火墙设置为在启动时激活，以便在重新启动时重定向继续生效。

```
# iptables -t nat -I PREROUTING 1 -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 3128
```

虽然 iptables 工具的详细描述超出了本节范围，但应简要说明此配置中发生了什么。首先，你将一条规则插入 NAT 路由路径的第一条 PREROUTING 链中，使用命令的 -t nat -I PREROUTING 1 部分。接下来你定义了哪些请求将被处理；在这种情况下，iptables 将处理所有来自连接到设备 eth0 的网络的数据包。这由规则的 -i eth0 部分定义。然后是选择要处理的协议；在这里你选择了 TCP，使用 -p tcp 部分。然后，最后的匹配规则指定了你希望重定向作用于的目的端口，使用 --dport 80 部分。最后，iptables 被告知对匹配先前定义条件的数据包做什么；具体来说，它将数据包 REDIRECT --to-port 3128。

## 13

## 网络配置

![](img/d84604054810a13cacfdac212ebee2f7_274_0.png)

Webmin 中的第四个类别标签是 **Networking** 相关配置。具体来说，这里是你会找到用于配置 net、xinetd、iptables、NFS 导出、NIS 客户端和服务器以及网络接口的模块。Networking 类别是在 Webmin 版本 1.0 中引入的，因此如果你出于某种原因使用的是更早的 Webmin 版本（立即升级；它是免费的！），这些模块将位于其他类别标签下。

## NFS 导出

**NFS Exports** 模块列出所有导出的目录。单击 **Add a new export** 将带你到 **Create Export** 页面，如图 13-1 所示。

![](img/d84604054810a13cacfdac212ebee2f7_275_0.png)

## 图 13-1：创建 NFS 导出

在前面的图中，你可以看到该模块允许你选择要导出的目录，并为该目录选择许多选项以及应向谁导出该目录。

## 导出详细信息

以下选项配置要导出的目录的位置、类型和权限：

### 要导出的目录

这只是你想要导出的目录的完整路径。

### 活动？

当不需要时，可以通过选择 no 来禁用导出。否则，只要 NFS 服务器正在运行，导出将始终处于活动状态并可用。

在接下来的几个字段中，可以选择访问控制，以规定哪些机器或网络上的用户将被允许挂载导出的目录。

### Everyone

指定任何人都可以挂载该目录。这类似于匿名 FTP 服务器。

> 警告 在导出目录给所有人时要极其谨慎。如果你的本地网络没有非常好的防火墙保护，外部人员将能够挂载你的导出目录。外部人员也可能对你的服务器发动拒绝服务攻击，因为 NFS 在面对蓄意攻击者时以其可靠性不佳而闻名。始终最好将 NFS 导出限制为仅需要访问的机器，并且另外实施防火墙以阻止本地网络之外的人甚至尝试连接到你的 NFS 服务器。

