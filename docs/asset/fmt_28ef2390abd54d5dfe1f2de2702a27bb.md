
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

如何在父区域和子区域中更换密钥的问题一直以来似乎需要父区域和子区域之间的协作与通信。DS 记录的创建、独立的密钥签名密钥和区域签名密钥的使用，以及多个密钥的使用有助于解决这个问题。

包含在`DNSKEY`资源记录中的密钥可以是密钥签名密钥（KSK）也可以是区域签名密钥（ZSK）。一种称为`SEP`（“安全点”）的新标志位区分了它们。标志位的第 15 位对 KSK 设置为 1，对 ZSK 设置为 0。这种约定使得当标志位被视为十进制时，KSK 的标志位为奇数，ZSK 为偶数。其值分别为 257 和 256。

可以生成并签名多个密钥，以便实现从一个密钥到另一个密钥的平滑过渡。如果子区域更改其密钥签名密钥，可以在不通知父区域的情况下进行。

## 第 17 章：DNS：域名系统

`RRSIG`记录是资源记录集（RRset）的签名。它证明数据已由私钥签名且未被篡改。`RRSIG`记录包含以下内容：

- 用于签名的算法
- RRset 的标签
- 签名的过期时间
- 签名的起始时间
- 用于验证的密钥标签
- 签名间隔
- 签名本身

这是一个`RRSIG`记录的示例：

| 字段 | 值 |
| :--- | :--- |
| 算法 | 8 (RSASHA256) |
| 标签 | |
| 过期时间 | 20231231000000 |
|起始时间 | 20230101000000 |
| 密钥标签 | 12345 |
| 间隔 | 3600 |
| 签名 | [base64 签名] |

签名区域的过程涉及几个步骤：

1. 生成 KSK 和 ZSK。
2. 在区域中发布公钥。
3. 向父区域提交 DS 记录。
4. 使用 ZSK 对 RRset 进行签名。
5. 在区域中发布 RRSIG 记录。

密钥过期时，必须进行滚动。这涉及生成新密钥、更新区域以及更新父区域中的 DS 记录。此过程必须小心进行，以避免破坏验证。

### 或 NSD 命令

```
$ ldns-keygen -a RSASHA1 -b 1024 example.com

Kexample.com.+005+23301

$ ldns-keygen -a RSASHA1 -b 2048 -k example.com

Kexample.com.+005+00682
```

为`example.com`生成一对使用 RSA 和 SHA-1 算法的 1,024 位 ZSK 密钥以及对应的 2,048 位 KSK 密钥.³⁰¹ UDP 数据包大小限制的突出问题表明，最好使用区域签名密钥（ZSK）并频繁更换它们。你可以使用更长的签名密钥（KSK）来帮助恢复某些安全性。生成密钥需要一些时间——在老旧的笔记本电脑上，短密钥需要一两分钟，较长密钥需要半小时或更久。

两个密钥生成器都会将生成的密钥的基础文件名打印到标准输出。在本示例中，`example.com`是密钥名称，`005`是 RSA/SHA-1 算法套的标识符，而`00682`是称为密钥标识符、指纹或密钥标签的哈希值.³³¹ BIND 密钥生成器生成两个文件（`.key`和`.private`），而 NSD 密钥生成器生成三个文件（`.key`, `.private`和`.ds`）：

- `Kexample.com.+00523301.key` # 公区域签名密钥
- `Kexample.com.+00523301.private` # 私有区域签名密钥
- `Kexample.com.+00523301.ds` # ZSK 的 DS 记录（仅限 NSD）

- `Kexample.com.+006682.key` # 公共签名密钥
- `Kexample.com.+006682.private` # 私有签名密钥
- `Kexample.com.+006682.ds` # KSK 的 DS 记录（仅限 NSD）

可用多种加密算法，每种算法都有可能的密钥长度。你可以运行不带参数的`dnssec-keygen`或使用`ldns-keygen -a`查看当前支持的算法列表。BIND 和 NSD 都可以使用其他软件生成的密钥。

根据软件版本，某些算法名称可能会加在前面。如果你想对签名的负答使用 NSEC3 记录而不是 NSEC 记录，你必须使用特定的 NSEC3 算法生成兼容 NSEC3 的密钥；请参考`ldns-signzone`或`dnssec-keygen`的主页面。

`.key`文件包含一个`example.com`的单个`DNSKEY`记录。例如，这里是区域签名公钥，已截断以适应页面。你可以看出来它是 ZSK，因为其标志字段为 257，而不是 KSK。

```
example.com. IN DNSKEY 256 3 5 AWeAAE:7Te60wV5a8PpnRe4XR8MGl!
```

- 30. 2,048 位显然是过剩的；许多站点使用 1,500 位更少。
- 31. 为了方便比较 BIND 和 NSD 的过程，我们调整了指纹以使 BIND 和 NSD 的集合匹配。在现实生活中，每个密钥都会有不同的指纹。

## 区域签名

这些公钥必须被`$SIGNED`或插入到区域文件中，位于末尾或 SOA 记录之后。要将密钥复制到区域文件，你可以使用`cat>>`追加它们，或在文本编辑器中粘贴。

由 NSD 密钥生成器`ldns-keygen`生成的`.ds`文件包含 DS 记录；如果 DNS-SEC 完全部署，对应 KSK 的 DS 记录将存储在父区域中。DS 记录可以从 KSK 的 DNS-KEY 资源记录生成，而签名的区域除了 KSK 的 DNSKEY 记录外，还需要它。以下是 DS 记录的样式：

```
example.com.      3600 IN DS 23301 1 5bd844108d8fea34b3bc2f2135...

example.com.      3600 IN DS 00682 1 0df8f86b716833ff2732509...
```

任何密钥对的私钥都可以离线存储，或者至少存不在公共互联网的机器上。这种预防对于动态更新的区域是不实行的，对于假设寿命很长的区域签名密钥也是如此。考虑一下签名密钥（KSK），即一个从外部无法访问的隐藏主服务器（用于 ZSK）。打印出私钥 KSK 或将其写入 USB 闪盘并锁在箱子里，直到你再次需要它。

在锁好私钥的同时，将新密钥输入密钥日志文件也是个好机会。你不需要包含密钥本身，只需要 ID、算法、日期、目的等。

默认签名有效期为：`RRSIG`（资源记录集的 ZSK 签名）为一个月，`DNSKEY`记录（ZSK 的 KSK 签名）为三个月。目前的最佳实践是长度为 1,024 位的 ZSK 使用三个月到一年，以及长度为 1,280 位的 KSK 使用一两年.^³ 由于建议的密钥保留期比默认签名有效期长，如果密钥没有，，必须在签名区域时指定更长的有效期，或者定期对区域重新签名。

## 区域签名

现在你已经有了密钥，可以使用`dnssec-signzone` (BIND) 或`ldns-signzone` (NSD) 对你的区域进行签名，这些方法会为资源集添加 RRSIG 或 NSEC 记录。这些命令读取你的原始区域文件并生成名为`zonefile.signed`的已签名副本。BIND 的语法是：

```
dnssec-signzone [-o zonename] [-N increment] [-k KSKfile] zonefile [ZSKfile]
```

其中文件名默认为`zonefile`，密钥文件由上述`dnssec-keygen`生成。

- 32. 使用类似`Kexample.com.*`的命令追加到`zonefile`而不是替换它。
- 33. 表格列出了各种机构建议的密钥长度。

## 第 17 章 DNS：系统

如果你按照区域命名你的数据并保持原始密钥文件的名称，命令简化为：
```
dnssec-signzone [-N increment] zonefile
```

`-N increment`标志会自动增加 SOA 记录中的序列号。你也可以指定`uniqtime`值将序列号更新为自1970 年 1 月 1 日以来的秒数，或者`keep`值防止`dnssec-signzone`修改原始序列号。序列号在签名文件中增加了，但在原始文件中没有。以下是使用上述密钥的示例：

```
$ sudo dnssec-signzone -o example.com -N increment -k example.com.+005+00682 example.com.+005+23301
```

签名文件按字母顺序排序，并包含了手动添加的 DNSKEY 记录以及签名期间生成的 RRSIG 和 NSEC 记录。区域的序列号已经增加。如果你用 NSEC3SHA1 算法生成密钥，将使用上述标志签名区域。`dnssec-signzone`的一些有用选项有：

- `-g` 生成父区域所需的 DS 记录
- `-l` 如果父区域未签名则生成 DL 记录
- `-s start-time` 设置签名生效
- `-e end-time` 设置签名过期
- `-t` 打印统计

签名有效日期可以是`yyymmddmmss`格式的绝对时间，也可以相对于现在的`+N`格式。默认签名有效期是从过去的一个月到未来的三十天。这是一个指定签名有效期到 2010 年底的示例：

```
$ dnssec-signzone -N increment -e 2010123123559 example.com
```

在 NSD 下，签名区域的语法是：
`dnssec-signzone [-o zone] [key ...]`

你可以列出两个密钥并让`dnssec-signzone`识别哪个是 KSK 哪个是 ZSK。例如：

```
$ sudo dnssec-signzone example.com Kexample.com.+005+23301
```

通过`dnssec-signzone`，你可以使用`-e yyyymddmmss`标志设置签名过期日期。要在签名间隙生成 NSEC3 记录而不是 NSEC 记录，请使用标志`-n -s salt`。

## 区域签名

签名区域通常比原始区域大四到十倍，所有的逻辑排序都丢失了。像`mail-relay A 63.173.189.2`这样的变成了几行：

```
mail-relay.example.com. 57600 A 63.173.189.2

57600 RRSIG A 5 3 57600 200907022234636

20090622234636 23301 example.com.

Y7s9jDWYuuXUvoteRzRGdFlk+rzuB8Liowew

01ITGfIlhbRsgkkppeFYVRUBk7kVRNGGuYwyk

dRSQIJ9QRw=

3600 NSEC mail-relay2.example.com. A RRSIG NSEC

3600 RRSIG 5 3 3600 20090222234636

20090622234636 23301 example.com.

4QXyPrBwChseFnotymGeProBMw7ur7eES5WK+40

WNs8N4hbkpJAU77RRNH0pLIHBdQmmyYw=
```

实际上，区域文件不再是人类可读的，由于 RRSIG 和 NSEC 记录的存在无法手动编辑。用户部分是必不可少的！

除了 DNSKEY 之外，每个资源记录集（同一区域相同类型的记录）都会获得来自 ZSK 的一个签名。DNSKEY 资源记录由 ZSK 和 KSK 签名，因此会有多个 RRSIG。签名的 Base-64 表示结尾的等号数量取决于长度变为 4 的倍数。

一旦你的区域完成了签名，剩下的工作就是将你的名称服务器指向区域的签名版本。如果你使用`named.conf`并将 NSD 的`file`参数改为`example.com.signed`，对应的配置文件是`named.conf`，你用它处理区域文件。

最后，重启名称服务器进程并告诉它重新加载配置文件。对于 BIND，执行`sudo rnd config`然后执行`rnd restart`。对于 NSD，执行`sudo rebuild`然后执行`sudo nscd restart`。

我们现在正在对 DNSSEC 区域签名！要进行更改，你可以编辑原始未签名区域，也可以编辑已签名区域并重新签名。编辑签名区域是一场逻辑上的噩梦，但它比重新签名整个区域快得多。确保删除与你更改的记录对应的 RRSIG 记录。你可能想对未签名区域进行相同的更改以避免版本偏差。

# 第17 章 DNS：域名命名系统

如果你将已签名的区域（zone）作为参数传递给`dnssec-signzone`或`ldns-signzone`，任何未签名的记录都将被签名，任何即将过期的记录签名将被标记为“即将过期”（Close to expiring），这定义为已有效期的四之三。重新签名通常会导致更改，因此请确保你增加了区域序列号（serial number），或者在 BIND 中，在`dnssec-signzone`命令行使用`-N increment`子句来自动增加区域序列号。

DNSSEC 配置的本地部分就此结束。剩下的就是棘手的问题：如何将安全 DNS 区域孤岛连接到 DNS 层次结构中其他已签名的部分。我们需要将 DS 记录放入已签名的父区域，或者使用域名验证（domain validation）的解决方案。接下来的章节将涵盖这些任务。

## DNSSEC 信任链

继续我们之前的 DNSSEC 设置示例，`example.com`现在已签名，其名称服务器已启用了 DNSSEC。这意味着在查询时，它们使用了 EDNS0（扩展 DNS 协议）以及数据包 DNS 头部中的 DNSSEC 选项。在回答带有该位设置的查询时，它们会在答案中包含签名数据。

接收到签名答案的客户端可以通过适当的公钥检查记录的签名来验证。但它是从该区域自身的`DNSKEY`记录中获取此密钥的，如果你仔细想，这听起来相当可疑。有什么什么能阻止冒充者同时提供虚假记录和验证这些记录的虚假公钥呢？

这个问题有几种可能的答案。你的站点必须至少实现其中一种；否则，你所有的 DNSSEC 工作将是徒劳。

标准的解决方案是在它的区域文件中为你的父区域提供一个 DS 记录。由于 DS 记录源自父区域，它由父区域的私钥认证。如果客户端信任你的父区域，那么就信任该父区域的 DS 记录准确反映了你区域的公钥。

父区域反过来由其父区域认证，以此类推回到根节点（root）。当 DNSSEC 完全部署时，你预先需要知道的唯一密钥是用于签名根区域的公钥，它可以在引导整个区域过程的根提示（root hints）中找到。

如果你足够幸运有一个已签名的父区域，只需将你的父区域管理员提供 DS 记录和用于签名的`DNSKEY`即可。BIND 的`dnssec-signzone`的`-g`标志会生成名为`dset-domain`和`keyset-domain`的文件，这些文件可以安全地交付给你的父区域，直接添加到父区域文件中。同样，NSD 的`ids-keygen`在生成密钥时会在`ds`文件中生成所需的 DS 记录并在`.key`文件中生成`DNSKEY`记录。注意：

> 34. 如何判断你的父区域是否签名？尝试使用`dig +dnssec`或`drill -D`。

## DLV：辅助验证（lookaside validation）

在你的父区域安装相应的 DS 记录之前，你必须在你自己的区域中发布`DNSKEY`记录。

如果你的父区域未签名，你必须提供其他方式让外部世界验证你 DNS 中发布的公钥确实属于你。有三种不同的方法：

- 使用一个或多个信任锚点仓库（TAR）来发布你的公钥；例如来自 SecSpider 的。要在你的服务器上使用 TAR 密钥，请从 SecSpider 获取密钥列表、从 IANA 获取（仅包含 TLD）或从 RIPE-NCC TAR 获取（包含它们自己的区域，主要是欧洲 TLD 和反向区域）。将这些放入你名称服务器配置文件的`trusted-keys`子句中。
- 使用由 ISC（互联网系统联盟会）提供的域名辅助验证服务器。该服务本质上让`isc.org`成为你的自适应 DNS 父区域。它是简单且免费的；参见`isc.org/ops/dlv`。其他其他 DLV 服务器，但你只能使用一个，且 ISC 的非常成熟且良好。
- Vantage 守护进程与你信任的朋友的副本合作，形成一个守护社交网络，可以从互联网上的不同站点独立获取密钥并比较其结果以判断它们是否真实。

我们将在下一节中更详细地描述 DLV 解决方案。但请记住，这三个选项都是旨在帮助渐进部署 DNSSEC 的临时解决方案。如果你的父区域已经签名，甚至不要考虑这些选项。只需给你的父区域提供相应的 DS 记录即可。

## DLV：辅助验证（lookaside validation）

感知 DNSSEC 的缓存服务器首先接收签名的查询响应，并匹配其`DNSKEY`记录指定的域名公钥。客户端尝试通过在父区域中查找 DS 记录来验证密钥。如果没有可用的 DS 记录，客户端会在原始域名查找 DLV 记录；或者重定向到`dlv.isc.org`或任何作为该区域代养父的 DLV 服务器。当客户端从`dlv.isc.org`获取 DLV 记录时，它可以验证信任链。为你的区域设置 DLV 服务只需生成相应的 DLV 记录并将其放在正确的位置。

DLV 记录只是伪装的 DS 记录。记录类型不同，但记录体相同。记录的名称字段也经过修改，以便将记录放入 DLV 提供者的区域中。例如，`example.com`可能变成`example.dlv.isc.org`。

在 BIND 中，`dnssec-signzone -l`（小写 L）生成 DLV 记录：

```
$ sudo dnssec-signzone -l dlv.isc.org example.com
```
