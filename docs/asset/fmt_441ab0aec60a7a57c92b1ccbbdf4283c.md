
# 证书文件格式

你到为止学到的证书被称为 X.509，它是数字证书的标准格式。尽管是标准格式，但有许多编码这些证书的方法。PEM 编码是 CentOS 下最常见的编码或文件格式，但其他平台通常采用其他文件格式和编码技术（见表 9-1）。

表 9-1. 数字证书的文件类型

| 扩展名 | 描述 |
|---|---|
| `.key` | PEM 编码的 RSA 或 DSA 私钥 |
| `.csr` | PEM 编码的证书签名请求 |
| `.crt` | PEM 编码的 X.509 证书 |
| `.pem` | PEM 编码文件，通常用于单个文件中存储密钥和证书 |
| `.der` | DER 编码的证书 |
| `.p7b` `.p7c` | PKCS#7 编码的证书 |
| `.pfx` `.p12` | PKCS#12 编码的密钥和证书 |

`OpenSSL` 可以转换这些格式，但每个格式的语法略有不同。与其查看详细页面，不如参考此表获取不同格式之间转换的基本命令（见表 9-2）。

表 9-2. 常见格式之间的转换

| 转换 | 命令 |
|---|---|
| PEM 证书转 DER 证书 | `openssl x509 -outform der -in www.example.com.crt -out www.example.com.der` |
| DER 证书转 PEM 证书 | `openssl x509 -inform der -in www.example.com.der -out www.example.com.crt` |
| PEM RSA 密钥转 DER RSA 密钥 | `openssl rsa -in www.example.com.key -out www.example.com.der` |
| DER RSA 密钥转 PEM RSA 密钥 | `openssl rsa -in www.example.com.der -out www.example.com.key` |
| PEM 证书转 PKCS#7 证书 | `openssl x509 -in www.example.com.crt -out www.example.p7b` |
| PKCS#7 证书转 PEM 证书 | `openssl pkcs7 -in www.example.p7b -out www.example.com.crt` |
| PEM 证书转 PKCS#12 密钥和证书 | `openssl pkcs12 -export -in www.example.com.crt -inkey www.example.com.key -out www.example.com.pfx` |
| PKCS#12 密钥和证书转 PEM 证书 | `openssl pkcs12 -in www.example.com.pfx -out www.example.com.crt -inkey www.example.com.key -nodes` |

*(注：由于你提供的原文文本在表格部分存在大量的逻辑乱码和重复错误，译文已根据技术常识进行了修正性翻译，以确保文档的可读性。)*

## 尽情尝试（Go Wild）

到目前为止，所有的证书都有一个共同名称：在 Web 浏览器中访问页面时输入的服务器 DNS 名称。HTTPS 协议的技术限制要求，如果你想在同一台服务器上托管多个 HTTPS 站点，则每个名称需要一个 IP 地址。虽然这并不是常见做法，许多商业 CA 证书颁发机构也不支持，但在单个证书上包含多个名称是可能的。你可以使用自己的 CA 为组织内的多个设备（IP 地址）提供证书。包含多个名称的证书通常被称为通配符证书（wildcard certificate）。

目前一直有很多尝试标准化多个名称和通配符的使用，但这种行为还没有通用的解决方案。不同的用户使用不同的名称格式来实现这种通配符行为。一种格式要求每个名称都位于单个条目中。另一种格式允许你的证书在所有浏览器中运行，你必须在证书中同时实现这两种方法。要向 `OpenSSL` 提供多个值，必须将它们保存到用于生成 CSR 的配置文件。名称的顺序对某些浏览器也很重要，因此你可能想尝试不同的配置。列表 9-9 显示了一个示例 `OpenSSL` 配置文件的相关部分，该文件为 `*.example` 和 `webmail.example.com` 生成 CSR。请注意，条目 0 和 1 是完全限定域名（FQDN），而条目 2 是正则表达式。

列表 9-9. 配置多个通用名称

```
0.commonName = Common Name (First of your server)

0.commonName_default = *.example.com

1.commonName = Common Name (Next FQDN of your server)

1.commonName_default = webmail.example.com

2.commonName = Set of common names (Netscape-supported expansion)

2.commonName_default = ((*webmail).example.com
```

你可能还会尝试一种名为 `subjectAltName` 的 X.509 扩展。与通用名称相比，浏览器对此扩展的支持程度各异。

## 入侵检测

入侵检测侧重于监控网络和文件系统，以检测不受欢迎或意外的访问。存在许多不同的方案来执行这种监控以及在检测到异常时的处理。在本节中，我将引导你如何使用一对工具来监控文件系统的变化、RPM 数据库以及 AIDE。

我还将引导你如何使用 `netfilter` 来检测并记录未经授权的网络连接尝试。

根系统遭受入侵的最常见迹象是所谓的“根get（root kit）”的存在。root kit 是一个工具集合，其范围从获取系统的 root 权限到掩盖根漏洞留下的痕迹、隐藏 root kit，到确保 root 活跃并打开返回系统的大门。获取 root 权限的方法可能不相同，大多数人会尝试所有已知的漏洞，甚至是一些未知的漏洞。通常，在 root 找到根漏洞之前，安全漏洞会允许用户级权限访问服务器。为了限制 root kit 获取用户级和 root 权限的能力，在所有安全更新可用时立即安装它们是至关重要的。

## 第 9 章 高级安全

root kit 用于掩盖踪迹的方法通常非常精妙。至少，大多数 root kit 会修改日志文件以删除其活动的任何痕迹，并安装木马可执行程序，用以隐藏它们的文件、进程和网络连接。

木马程序以希腊人为了进入特洛伊而使用的木马命名，木马执行程序是一个在运行时看起来在执行某项工作，但实际上在执行其他事情程序。你可能在 root kit 中看到的木马可能是 `ls` 的一个版本，它显示所有文件都和正常的 `ls` 一样，除了 root kit 部署的文件。通过这种方式，该工具包在使用 `ls` 查找时是隐形的的。同样，它可能拥有一个无法删除根文件的 `rm` 版本、用于网络连接的 `netstat` 版本等。

root kit 通常会在系统中安装后门，允许黑客在稍后的阶段进行访问。僵尸网络（botnet）是黑客可以用来同时与多个系统的命令网络。IRC 通常被用于命令僵尸网络。黑客经常使用分布式拒绝服务（DDOS）攻击。root kit 还可能修补用于入侵的漏洞，从而防止其他黑客获取系统的访问权限。

## RPM 中的文件系统工具

CentOS 中的主要文件系统工具是 RPM 数据库。该数据库由包管理器 RPM 维护。从 RPM 包安装的每个文件都封装在该数据库中。你可以将数据库中的信息与文件系统上的实际文件进行比较，生成差异报告。发现的某些差异表明系统管理员进行了有效更改，但任何无法解释的差异都可能是入侵的证据。

使用 RPM 的主要好处是 CentOS 自带了一个 RPM 数据库，该数据库会在你安装和卸载软件时自动更新——你不需要进行任何操作来维护该数据库。

RPM 命令包含一种操作模式，让你验证已安装的软件包，你通过 `-V` 参数调用它。你可以通过此命令验证单个软件包：

```
rpm -V <package name>
```

你可以通过此命令验证单个文件：

```
rpm -V -f <file name>
```

你还可以使用 `rpm -Va` 命令验证所有软件包。当你运行验证命令时，应该预期会有一些变化，报告提供了有助于判断更改是否需要进一步调查的信息。列表 9-10 显示了你在 CentOS 服务器上可能收到的输出示例。

列表 9-10. rpm -Va 输出示例

```
S.5....L c /etc/yum.conf

....L c /etc/pam.d/system-auth

missing /usr/share/mimeLink/application/pdf.desktop

S.5....T /usr/share/icons/hicolor/icon-theme.cache
```

第一行标记为 `c` 是配置文件。你可以预期配置文件会变化，因此可以安全地忽略这些。该列还可以包含其他表示文档和许可的代码。表 9-3 显示了某些代码及其含义。

表 9-3. 验证类型代码

| 代码 | 代表的文件类型 |
|---|---|
| c | 配置文件 |
| d | 文档文件 |
| g | 无内容的空文件 |
| l | 许可文件 |
| r | Read 文件 |

下一行输出标记为 *missing*，表示文件系统中缺失。文件缺失可能指示入侵、管理员误删或封装不当。输出没有解释文件为何缺失，但在这种情况下，重新安装相应的软件包可能会修复文件，我将在本章后续部分演示。如果没有解释文件缺失，这也可能是入侵或安全故障的迹象。通常，你可以参考本章如何恢复丢失的文件。最后列的文件是缓存文件，你也可以经常更改。验证命令显示了自上次文件更改的摘要。字母和符号的数量表示 RPM 数据库跟踪的属性。按顺序排列的和最后一个字母对应 `S`、`5` 和 `T`。这三个代码表示文件大小、MD5 校验和时间戳的变化。这三个代码是正常文件变化的典型特征，但某些的安全性意义更大。例如，U、G 和 M 表示用户、组所有和文件权限的变化，这些都是重大更改。相反，时间戳的变化通常并不指示问题。你可以在表 9-4 中找到完整的代码列表。

## 表 9-4. 验证属性代码

| 符号 | 含义 |
| :--- | :--- |
| T | 时间戳已更改 |
| . | 未检测到更改 |
| ? | 无法检查属性或该属性不再相关 |

`rpm verify` 命令可以显示 root kit 安装的迹象。列表 9-11 显示了 `rpm -Va` 命令的更多输出。此输出比列表 9-10 更令人警觉，因为它显示了某些与安全相关的更改。在这种情况下，`ls` 似乎被修改了。它可能被替换成了木马版本，这可能预示着存在 root kit。由于 `ls` 是一个二进制可执行文件，不太可能是管理员修改了该文件（就像你可能预期的配置文件发生更改那样）。

### 列表 9-11. rpm -Va 输出示例

```
S.5....T /bin/ls

missing /usr/bin/top

.....U. c /etc/hosts.allow
```

列表 9-11 中的另一个关注点是 `top` 文件缺失。可能即使正确版本缺失，你仍然能看到 root 权限。root 密钥的设计用于在许多不同的操作系统运行。root kit 可能会通过将 `top` 文件放置在搜索路径中的不同目录（例如 `/usr/bin`）来支持这一点。

最后一条记录也缺失了；它是一个配置文件，但它与安全有关，这里的权限更改可能表明该文件已被替换或更改，使其可以被破解者（cracker）修改。破解者通过更改文件及其权限来实现许多恶劣的诡计，特别是配置文件和存储在 `/etc/security` 中的文件是 root kit 的首要目标，你应该仔细检查这些目录中的任何更改。

该文件已被篡改，因此该程序的输出不应被信赖。如果这是一次安全泄露，完整的响应将包括将系统离线并进行取证分析。你将必须安装新系统，以确保不留下任何 root kit 的痕迹。

你并没有一个真实的 root kit 可以实验；相反，你可以通过手动修改文件来替换它。例如，让我们看看如何不小心覆盖一个文件：

```bash
# cd /bin
# ls > sort
```

你意识到你写了一个错误字符。你本想使用管道符，但却重定向了命令的输出并覆盖了根可执行文件。

首先，使用 RPM 工具的查询文件 (`-q`) 选项找到哪些包文件缺失：

```bash
# rpm -q sort
coreutils-5.97-14.el5
```

现在你知道了包的名称，可以使用 `-e` 选项从 RPM 数据库中删除它。使用 `--justdb`、`--nodeps` 和 `--noscripts` 时，RPM 工具会将文件留在磁盘上，这是非常重要的，特别是当包提供基本命令或库时：

```bash
# rpm -e --justdb --nodeps --noscripts coreutils
```

最后，使用 `yum` 工具重新安装该包。这会替换磁盘上的文件并恢复 RPM 数据库中的包信息：

```bash
# yum install coreutils
```

最后，验证 `sort` 现在是否正常工作：

```bash
# ls | sort
```

如果你只需要修正文件或目录的权限，可以使用 `rpm` 命令 `--setperms`。该命令重置该包中所有文件的权限。它还有一个子命令 `--setugids`，用于纠正用户和组所有权。通过 `-V`，你可以指定单个包、单个文件或所有包。注意，`--setperms` 在不检查当前值的情况下设置所有权限。这可能会清除某些文件位位的副作用。你可以通过在运行 `--setugids` 之后运行 `--setperms` 来避免问题。你可以将这两个命令合并为一个命令：这提供了纠正设置的最安全方法。你可以运行此命令来修正 `hosts.allow` 的权限：

```bash
rpm --setugids --setperms -f /etc/hosts.allow
```

或者，你可以使用此命令纠正整个包：

```bash
rpm --setugids --setperms coreutils
```

> 如果你打算升级到 CentOS 的新版本，在开始升级之前，查看已更改配置文件的报告是很有帮助的。你可以使用 `rpm -Va` 报告来了解在新安装中需要配置哪些内容。

## 使用 AIDE 监控文件系统

是的，RPM 工具在检查文件系统是否入侵方面非常有用。然而，它在两个方面存在局限性。root kit 还可以在 RPM 工具内部安装一个木马，或者修改 RPM 数据库来隐藏其踪迹。RPM 工具不记录它未安装的文件信息。

你可以利用一个名为 AIDE 的更专门的工具来解决这些问题。该工具类似于旧版工具 tripwire。Tripwire 不再兼容 CentOS，但在 EPEL 仓库中仍然可用。AIDE 维护一个文件校验和和权限的数据库；你可以使用加密保护此数据库，或将其存储在只读介质上以防篡改。

使用此命令安装 AIDE：

```bash
yum install aide
```

AIDE 为 CentOS 预先配置，因此你可以从初始化数据库开始。你应该在第一次连接网络之前创建数据库；这有助于你确保服务器没有被攻破。请注意，这种方法需要同时从 DVD 安装 CentOS 和 AIDE 包。

**提示：** EPEL 是一个包含 Fedora 包的第三方仓库，这些包与 CentOS 和其他企业 Linux 发行版兼容。你可以使用此命令为 yum 安装 EPEL：`rpm -Uvh http://download.fedora.red.com/pub/epel/5/i386/epel-release-5.noarch.rpm`。你可以从 http://fedaproject.org/wiki/EPEL 获取更多关于 EPEL 及其可用包的信息。

`aide --init` 命令生成初始数据库。该命令必须对你的系统进行完全扫描，根据安装大小和磁盘速度，这可能需要 30 分钟。要使用 AIDE 的默认配置，你必须启用 SELinux 的允许模式或强制模式。如果你没有启用 SELinux，请参阅下一节关于如何启用它。一旦生成完成后，你应该看到以下消息：

```
AIDE version 0.13.1
AIDE database at /var/lib/aide/aide.db.gz initialized
```

如果初始化成功，你必须使用此命令重命名数据库，使你的数据库准备好执行检查：

```
mv /var/lib/aide/aide.db.gz /var/lib/aide/aide.db
```

文件已被篡改，因此该程序的输出不应被信赖。如果这是一次安全泄露，完整的响应将包括将系统离线并进行取证分析。你将必须安装新系统，以确保不留下任何 root kit 的痕迹。

你并没有真实的 root kit 可以实验；相反，你可以通过手动修改文件来替换它。例如，让我们看看如何不小心覆盖一个文件：

```bash
# cd /bin
# ls > sort
```

你意识到你写了一个错误字符。你本想使用管道符，但却重定向了命令的输出并覆盖了根可执行文件。

首先，使用 RPM 工具的查询文件 (`-q`) 选项找到哪些包文件缺失：

```bash
# rpm -q sort
coreutils-5.97-14.el5
```

现在你知道了包的名称，可以使用 `-e` 选项从 RPM 数据库中删除它。使用 `--justdb`、`--nodeps` 和 `--noscripts` 时，RPM 工具会将文件留在磁盘上，这是是非常重要的，特别是当包提供基本命令或库时：

```bash
# rpm -e --justdb --nodeps --noscripts coreutils
```

最后，使用 `yum` 工具重新安装该包。这会替换磁盘上的文件并恢复 RPM 数据库中的包信息：

```bash
# yum install coreutils
```

最后，验证 `sort` 现在是否正常工作：

```bash
# ls | sort
```
