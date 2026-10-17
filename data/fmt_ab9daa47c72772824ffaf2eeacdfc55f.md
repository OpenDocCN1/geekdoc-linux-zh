
E.ROOT-SERVERS.NET internet address = `192.203.230.10`

I.ROOT-SERVERS.NET internet address = `196.148.17`

F.ROOT-SERVERS.NET internet address = `192.5.5.241`

G.ROOT-SERVERS.NET internet address = `192.112.36.4`

这告诉我们所有的 `ROOT-SERVERS.NET` 服务器都可以用来继续询问其中任何一个。我们将继续询问。现在我们想知道谁提供下一级域名：`mit.edu`：

```
> mit.edu.

Server: c.root-servers.net

Address: 192.33.4.12
```

```
Non-authoritative answer:

mit.edu nameserver = W20NS.mit.edu

mit.edu nameserver = BITSY.mit.edu

mit.edu nameserver = STRAWB.mit.edu
```

```
Authoritative answers can be found from:

W20NS.mit.edu internet address = 128.70.160

BITSY.mit.edu internet address = 128.72.0

STRAWB.mit.edu internet address = 128.71.0
```

`w20ns` 和所有 `mit.edu` 服务器，我们选择一个并询问上一级：`ai.mit.edu`：

```
> server W20NS.mit.edu.
```

主机大小大小敏感，但我使用鼠标点击并粘贴，是从屏幕上复制的。

```
Server: W20NS.mit.edu

Address: 128.70.160
```

# 520 附录 G：服务器文档 495

```
> ai.mit.edu.

Server: W20NS.mit.edu

Address: 128.70.160
```

```
Non-authoritative answer:

ai.mit.edu nameserver = ALPHA-BITS.MIT.EDU

ai.mit.edu nameserver = GRAPE-NUTS.MIT.EDU

ai.mit.edu nameserver = TRIX.MIT.EDU

ai.mit.edu nameserver = MUESLI.MIT.EDU

ai.mit.edu nameserver = LIFE.MIT.EDU

ai.mit.edu nameserver = BEET-CHEEK.MIT.EDU

ai.mit.edu nameserver = MINI-WHEATS.MIT.EDU

ai.mit.edu nameserver = COUNT-CHOCULA.MIT.EDU

ai.mit.edu nameserver = MINTARA.LCS.MIT.EDU
```

```
Authoritative answers can be found from:

AI.MIT.EDU nameserver = ALPHA-BITS.AI.EDU

AI.MIT.EDU nameserver = GRAPE-NUTS.AI.EDU

AI.MIT.EDU nameserver = TRIX.AI.EDU

AI.MIT.EDU nameserver = MUESLI.AI.EDU

AI.MIT.EDU nameserver = LIFE.AI.EDU

AI.MIT.EDU nameserver = BEET-CHEEK.AI.EDU

AI.MIT.EDU nameserver = MINI-WHEATS.AI.EDU

AI.MIT.EDU nameserver = COUNT-CHOCULA.AI.EDU

AI.MIT.EDU nameserver = MINTARA.LCS.AI.EDU
```

```
ALPHA-BITS.AI.EDU internet address = 128.52.32.55

GRAPE-NUTS.AI.EDU internet address = 128.52.36.4

TRIX.AI.EDU internet address = 128.52.37.6

MUESLI.AI.EDU internet address = 128.52.39.7

LIFE.AI.EDU internet address = 128.52.32.22

BEET-CHEEK.AI.EDU internet address = 128.52.54.11

MINI-WHEATS.AI.EDU internet address = 128.52.38.22

COUNT-CHOCULA.AI.EDU internet address = 128.52.38.22

MINTARA.LCS.MIT.EDU internet address = 128.26.0.3
```

所以 `museli.ai.mit.edu` 是 `ai.mit.edu` 的名称服务器：

```
> server MUESLI.AI.MIT.EDU

Default Server: MUESLI.AI.MIT.EDU

Address: 128.52.39.7
```

现在我更改查询类型，我们已经找到了名称服务器，现在我们要查询关于 `prep.ai.mit.edu` 的所有信息。

- `set q-any`
- `prep.ai.mit.edu.`

# 496 附录 G：服务器文档

```
Server: MUESLI.AI.MIT.EDU

Address: 128.52.39.7
```

`prep.ai.mit.edu` CPU = dec/decstation-5000.25 OS = unix
`prep.ai.mit.edu`
inet address = `128.159.0.42`, protocol = tcp
ftp net smtp finger
`prep.ai.mit.edu` internet preference = 1, mail exchanger = gnu-life.ai.mit.edu
`prep.ai.mit.edu` internet address = `128.159.0.42`
`ai.mit.edu` nameserver = beet-chex.ai.mit.edu
`ai.mit.edu` nameserver = alpha-bits.ai.mit.edu
`ai.mit.edu` nameserver = mini-wheats.ai.mit.edu
`ai.mit.edu` nameserver = trix.ai.mit.edu
`ai.mit.edu` nameserver = muesli.ai.mit.edu
`ai.mit.edu` nameserver = count-chocula.ai.mit.edu
`ai.mit.edu` nameserver = mintara.lcs.mit.edu
`gnu-life.ai.mit.edu` internet address = `128.70.0.160`
`beet-chex.ai.mit.edu` internet address = `128.72.0`
`alpha-bits.ai.mit.edu` internet address = `128.71.0`
`mini-wheats.ai.mit.edu` internet address = `128.52.38.22`

# 附录 G：名称服务器文档 497

一个较少被谈及但同样重要的域是 `in-addr.arpa`。它和“普通”域名一样也是嵌套的。`in-addr.arpa` 允许我们在拥有地址时获取主机名。这里需要注意的一点是，在 `in-addr.arpa` 域中，IP 地址是反序书写的。如果你有一台机器的地址：`192.128.52.43`，解析过程就像 `prep.ai.mit.edu` 的示例一样：查找 `addr.arpa` 服务器，查找 `in-addr.arpa` 服务器，查找 `192.in-addr.arpa` 服务器，查找 `52.128.192.in-addr.arpa` 服务器，最后为 `43.528.192.192.in-addr.arpa` 查找所需的记录。是不是很聪明吧？（说“是”）。不过，数字的反转可能会让你感到困惑。

我刚刚撒了一个谎。DNS 的工作方式并不完全像我刚才告诉你的一样。但它已经足够接近。

## 4.2. 我们自己的域

现在来定义我们自己的域。我们将创建一个 `linux.bogus` 域并在其中定义机器。我使用了一个完全虚假的域名，用以确保我们不会打扰到“外面”的任何人。

在开始之前还有一点：主机名中并不是所有字符都是允许的。我们仅限于英语字母 `a-z`、数字 `0-9` 以及字符 `'-'`（连字符）。请仅使用这些字符。对于 DNS 来说，大小写字母是相同的，`pat.uo.no` 与 `Pat.Uio.No` 是完全相同的。
