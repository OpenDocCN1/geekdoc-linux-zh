
我们已经通过 `named.conf` 中的这一行开始这部分了：

```
zone "0.0.127.in-addr.arpa" (
type master;
file "pz/127.0.0";
;
```

请注意该文件中 `in` 结尾处缺少 `'.'`。这表示我们现在将定义 `0.0.127.in-addr.arpa` 区域，我们是该区域的主服务器，并且它存储在名为 `pz/127.0.0` 的文件中。我们已经开始编写该文件，内容如下：

# 附录 G：名称服务器文档

```
@ IN SOA ns.linux.bogus. hostmaster.linux.bogus. (
      1 ; Serial
      8H ; Refresh
      2H ; Retry
      1W ; Expire
      1D) ns.linux.bogus.
1 PTR localhost.
```

请注意该文件中所有完整域名的结尾都有 `'.'`，这与 `named.conf` 文件形成对比。有些人喜欢在每个区域文件开头使用 `$ORIGIN` 指令，但这是多此一的。区域文件的起始位置（即它在 DNS 层次结构中的位置）是在 `named.conf` 文件的 `zone` 部分指定的，在本例中，它是 `0.0.127.in-addr.arpa`。

这个“区域文件”包含 3 目“资源记录”（RRs）：一个 `SOA` RR、一个 `NS` RR 和一个 `PTR` RR。`SOA` 是 Start Of Authority（授权起始）的缩写。“`@`” 是一个特殊符号，表示起始位置，由于该文件的“域”列显示为 `0.0.127.in-addr.arpa`，第一行的意思是：

```
0.0.127.in-addr.arpa IN SOA ...
```

`NS` 是 Name Server（名称服务器）。该行开头没有 `'@'`，由于上一行是以 `'@'` 开头的，所以它是隐式的。这为你节省了一些打字量。因此，`NS` 行也可以写成：

```
0.0.127.in-addr.arpa IN NS ns.linux.bogus
```

它告诉 DNS 哪台机器是 `0.0.127.in-addr.arpa` 域的名称服务器，即为 `ns.linux.bogus`。“`ns`” 是名称服务器的习惯命名，就像 Web 服务器通常被命名任何名称一样。

最后，`PTR` 记录显示 `0.0.127.in-addr.arpa` 子网中地址为 `1` 的主机（即 `127.0.0.1`）名为 `localhost`。

`SOA` 记录是所有区域文件的引导部分，每个区域文件中应该恰好有一个。它描述了区域、它源于何（一台名为 `ns.linux.bogus` 的机器）、谁负责其内容（`hostmaster@linux.bogus`，你应该在此处插入你的电子邮件地址）、该区域文件的版本号（`serial: 1`）以及其他与缓存和二级 DNS 服务器相关的内容。对于其余字段（`refresh`, `retry`, `expire` 和 `minimum`），使用本 HOWTO 中使用的剩余数字，你需要确保安全。

## 附录 G：名称服务器文档 499

现在重启你的 `named`（命令是 `ndc restart`）并使用 `nslookup` 检查你的操作：

```
$ nslookup

Default Server: localhost
Address: 127.0.0.1

> 127.0.0.1
Server: localhost
Address: 127.0.0.1

Name: localhost
Address: 127.0.0.1
```

这样它成功地从 `127.0.0.1` 获取了 `localhost`，很好。现在处理我们的主任务 `linux.bogus` 域，在 `named.conf` 中插入一个新的“`zone`”区域部分：

```
zone "linux.bogus" {
  notify no;
  type master;
  file "pz/linux.bogus";
};
```

再次注意 `named.conf` 中域名缺失的 `'.'`。在 `linux.bogus` 区域文件中，我们将放置一些数据：

```
; Zone file for linux.bogus;
; The full zone file
@ IN SOA ns.linux.bogus. hostmaster.linux.bogus. (
    199802151 ; serial, todays serial
    8H ; refresh
    2H ; retry
    1W ; expire
    1D ) minimum
```

## 附录 G：名称服务器文档 500

```
;NS Address of name server
MX 10 mail.linux.bogus ; Primary Exchanger
MX 20 mail.friend.bogus ; Secondary Exchanger

localhost A 127.0.0.1
ns A 192.168.192.2
mail A 192.168.196.4
```

关于 `SOA` 记录必须注意两点：`ns.linux.bogus` 必须是一个 `A` 记录。`SOA` 记录中提到的机器不能是 `CNAME` 记录。“`ns`”名称可以是任何合法的主机名。接下来，`hostmaster.linux.bogus` 应该被读作 `hostmaster@linux.bogus`，这应该是一个电子邮件地址，或者是维护 DNS 的人的邮箱。关于该域的任何邮件都将发送到这里列出的地址。名为 `'hostmaster'` 的通常预期有效。

此文件中有一个新的 RR 类型，即 `MX`，或邮件交换器。它告诉邮件系统发送给 `someone@linux.bogus` 的邮件到 `mail.linux.bogus` 或 `mail.friend.bogus`。每个名字前面的数字是优先级。数字最小（`10`）的 RR 是邮件应该发送的地方。如果失败，邮件可以发送到数字更大的二级邮件处理器，即 `mail.friend.bogus`，它的优先级为 `20`。运行 `nslookup` 重启：

```
$ nslookup
> set q-any
> linux.bogus
Server: localhost
Address: 127.0.0.1

linux.bogus
origin = ns.linux.bogus
addr = hostmaster.linux.bogus
serial = 199802151
refresh = 28800 (8 hours)
retry = 7200 (2 hours)
expire = 604800 (7 days)
minimum = 86400 (1 day)
linux.bogus nameserver = ns.linux.bogus
linux.bogus preference = 10, mail exchanger = mail.bogus.linux.bogus
```

## 附录 G：名称服务器文档 501

linux.bogus preference = 20, mail exchanger = mail.friend.bogus

linux.bogus nameserver = ns.linux.bogus

ns.linux.bogus internet address = 192.168.196.2

mail.linux.bogus internet address = 192.168.196.4

经过仔细检查，你将发现一个错误。这一行：

linux.bogus preference = 10, mail exchanger = mail.bogus.linux.bogus

是完全错误的。应该是：

linux.bogus preference = 10, mail exchanger = mail.linux.bogus

我故意犯了一个错误，以便你从中学习 :-) 在区域文件中，我们发现行：

```
MX 10 mail.linux.bogus ; Primary Exchanger
```

缺少了一个点。或者多了一个 `'linux.bogus'`。如果机器名在区域文件中不以点结尾，起始位置会被添加到末尾，导致双的 `linux.bogus.linux.bogus`。因此，

```
MX 10 mail.linux.bogus. ; Primary Exchanger
```

或者

```
MX 10 mail ; Primary Exchanger
```

都是正确的。我更倾向于后一种形式，输入更少。有些 `bind` 专家不同意，也有人同意这一点。在区域文件中，域要么写全并以 `'.'` 结尾，要么完全不包含，在这种情况下它默认为起始位置。

我必须强调的是，在 `named.conf` 文件中域名后面不应该有 `''`。你不知道有多少次多一个或少一个点导致了事情搞砸并让人困惑不已。

# 附录 G：名称服务器文档

好了，在这里表达完观点后是新的区域文件，其中包含一些额外信息：
