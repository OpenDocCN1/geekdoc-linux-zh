
`-b` 选项会创建一个分离签名文件。该签名文件与所签名文件同名，但带有 `.gpg` 或 `.asc` 后缀，具体取决于指定的是普通（二进制）签名还是 ASCII 装甲签名。

## 加密文件

假设你拥有某个人的公钥，并且想为他加密一些内容。该密钥已被添加到公钥环中，文件也已准备好加密，现在只需要一条命令来加密它。

以下命令即可实现：

```bash
gpg -r recipient -e filename
```

接收者参数（`-r`）需要足以让 GPG 在其公钥环中找到对应 ID 的标识符。例如，再次以谢尔曼的 `signme` 文件为例：

> 约翰，
>
> 这里有些不对劲……
> 你能过来看一下吗？
>
> 谢谢……
>
> 谢尔曼

谢尔曼可以执行以下命令来加密 `signme` 文件，以便只有约翰能够读取它：

```bash
gpg -r john -e signme
```

如你所见，已创建了一个名为 `signme.gpg` 的文件，并已准备好发送给约翰。这是一个二进制文件，因为谢尔曼没有指定需要 ASCII 装甲。如果将该命令改为

```bash
gpg -r john -ea signme
```

那么生成的文件就是 `signme.asc`；它与清单 25.5 类似。

### 清单 25.5 带 ASCII 装甲的加密文件

```text
-----BEGIN PGP MESSAGE-----

Version: GnuPG v1.0.1 (GNU/Linux)

Comment: For info see http://www.gnupg.org

hQEOA3XvegfNjZsUEAQAstJC1WqPBt1ZGsLM1bkYbgSiI2/lTjTP/B2QS58/0EmD

M0vJwYwxKX4y0nGTl/DDKzx9P3RCMUpwrdP4cejq9S04BXmbUMKkWcwQueOQTG

2oAfK3u1/VrTgC6S0YnO9hQYSRChUCX1b2nQA3zmty+aODMecDTWcICiQQrEqE

AKvDp76yKaEmaAvrpnypYkVyVEys+HuEwfp7U8hBUiP5JbjqcdSprRHH4wuam0p

91lv/izrvo15gNgi4eyXHGQrzY/sE2UHRhplHMTV0IcMvPJvikB2Z8nSgyb61eKh

WJ85M+T5wJaQIn3yUz8GMSIIoAh+USG6hi7CposclWMycB56ypt6uVaKqGppk1U

hc1wnTcu2uHqPYNWeHhV78xksrW3NxvSft+Va5lufST3LNwn_gcjvGRP6i7ZQ+0E

/NDKzicDSCZd0BTKKF3HQFGv3/wEv0d+7bfdbruRYxqUjVtUQGt0zWjP4K4DMYwqN

6MSCwt6MW5a0FP4WyvvF91d5mluA6rga7o8wwn1irY1NLsv+jsDGzy8+fR1DIP

5YHf63rJQW0a1Sygm9hGXEiJ+joAN1/xGEMxDzfNBNe3g17UD/1F/C7aihPRSEJ

2v7RUpGSP63HL1m8CGWhac90AathaipDTJ32DONNJv+VZ4/4JgkEa+1K15kShBEiB

ocwokVgfuQSzv5pzn/pFAuAISJ6c2HUvI7wu4SjYgg+1QlahQuXEPwaqMgkRxkc

wW5bXTC2cnrBE6WEw==

=0A4T

-----END PGP MESSAGE-----
```

如果谢尔曼打算通过电子邮件将加密文件发送给约翰，这种方法是更加合适的选择。

当约翰收到这个文件后，他在阅读之前需要先解密它。该文件是用他的公钥加密的，而他有对应的私钥，因此他只需对加密文件运行 `gpg`——它知道接下来该怎么做。

在输入私钥密码后，使用以下语法解密文件：

```bash
gpg -d signme.asc
```

由于文件是 ASCII 装甲格式，它首先被解码回二进制形式，然后再进行解密。如果要解密的文件已经是二进制格式，则可以省略这一步骤，但其余解密过程完全相同。

如果该文件仅供约翰查看，而谢尔曼担心文件在约翰收到之前被篡改，他可以在加密的同时对文件进行签名。这提供了普通加密所不具备的额外一层保障。如果文件被篡改，签名将不匹配，并会出现警告（如前一节所述）。

执行这些操作的命令类似于加密命令与签名及 ASCII 装甲命令的组合：

```bash
gpg -r john -bea signme
```

生成的文件看起来类似于典型的 ASCII 装甲加密文件，但当文件被解密时，为签名而采取的额外步骤就值得了。对加密文件或二进制文件进行签名是确保它们自加密以来未被篡改的好方法。许多软件包，尤其是与安全相关的软件包，都进行了签名。这一过程已经防止了至少一个通过互联网匿名 FTP 提供的安全程序遭到破坏。

## 故障排除

*我已经设置好了我的电子邮件客户端，但似乎在发送邮件时遇到了问题。邮件总是被退回，并提示发件人域名必须可解析（sender domain must resolve）。*

您可能已将电子邮件客户端配置为使用本地主机的 `sendmail`，而不是 ISP 的。由于垃圾邮件发送者对电子邮件系统的滥用，这种方式将不再有效。如果系统没有有效的 MX 记录，大多数 MTA 不会接受来自这些系统的邮件。请将您的电子邮件客户端改为指向 ISP 的外发邮件主机。

*我在家中将电子邮件设置为通过工作单位的 `sendmail` 服务器发送，而不是通过 ISP，但我一直收到错误消息 `550 relaying denied`（中继被拒绝），邮件无法发出。*

默认情况下，`sendmail` 不允许任何来自外部系统且目的地为另一个外部系统的邮件。这被称为中继（relaying），是被禁止的。您需要请求管理员开放您 ISP 的网络、您的 IP 或您的 IP 范围（如果您是动态分配 IP 的拨号连接）。或者，您需要拨号连接到工作单位，通过工作邮件服务器发送邮件。

*但我就是工作系统的管理员。我该如何实现上述操作？*

遗憾的是，过去 Caldera 选择不将 `access_db` 构建到他们的 `sendmail` 配置中。如果仍然如此，您需要在 `sendmail.mc` 文件中添加类似这样的一行 `access_db`：

```
FEATURE(`access_db', `hash /etc/mail/access.db')
```

在您重新构建 `sendmail` 配置文件后，您可以启动此功能并执行以下操作：

以 `root` 身份，`cd` 到 `/etc/mail`。创建一个名为 `access` 的文件。在此文件中放入适当的条目以允许自己访问，例如：

```
192.168.0        RELAY
```

第一列可以是完整的或部分的 IP 地址（部分表示该块中的整个 IP 范围）或域名。在某些情况下，您还可以指定电子邮件地址。可以替换 `RELAY` 的合法值包括 `OK`、`REJECT`、`DISCARD` 或某些错误代码和文本。

然后，您需要发出以下命令来创建 `access.db` 文件：

```
makemap hash access.db <access
```
