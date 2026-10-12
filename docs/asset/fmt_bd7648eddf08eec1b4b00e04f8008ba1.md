
| 参数 | 说明 |
| :--- | :--- |
| `-kx` | 提取密钥 |
| `-kv` | 查看密钥 |
| `-kc` | 查看密钥的指纹 |
| `-ke` | 编辑密钥 |
| `-kr` | 移除密钥 |
| `-ks` | 对密钥进行签名 |
| `-krs` | 从密钥中移除签名 |
| `-kd` | 吊销密钥 |
| `-b` | 将数字签名从签名消息中分离 |
| `-W` | 加密后擦除（删除）明文文件 |
| `-m` | 使用 UNIX `more` 命令查看解密后的明文 |

以下命令提取公钥副本，以便每个人都能获得一份：

```
$ pgp -kxa userid ~/.pgp/pubring.pgp
```

当你拥有某人的 PGP 密钥后，将其添加到你的密钥环中。之后，你可以加密并发送消息给他们。在这种情况下，发送者应该是你。

```
$ pgp -e file recipient_userid
```

如果你想对消息进行签名，请用你的私钥像这样进行签名：

```
$ pgp -s file -u sender_userid
```

你可以像这样结合这两种方法：

```
$ pgp -es textfile recipient_userid -u sender_userid
```

要解密加密文件或验证数字签名，请使用此命令：

```
$ pgp encrypted_file -o plaintextfile
```

![](img/8ad518fddafc7f5e73715a2604b61d50_306_0.png)

> 提取密钥时，不要将你的私钥（`~/.pgp/secring.pgp`）提取到文件中。某人可能会获得其副本并解密你的文件或电子邮件。

## 运行扫描以检查漏洞

当你的系统相对安全时，对其运行扫描以检查安全性。使用如图 9-1 所示的 `SATAN` 等工具来检查问题，因为如果你不这样做，别人肯定会做。

其他值得使用的好工具包括像 `iptraf` 这样的数据包嗅探器，用于查看通过你的系统检查的信息类型。`iptraf` 程序查看通过网络发送的数据包，并提供诸如电子邮件内容、包含登录名和密码的 `telnet` 会话，或挂载网络文件系统等信息。

其他不错的工具还包括 `TAMU Tiger` 和 `ISS` 的 `S3`。你可以免费针对本地主机运行许多安全程序演示。在下面的示例中，我将展示在测试用的 `Slackware Linux` 主机上运行互联网安全扫描器后的结果是什么样的。

![](img/8ad518fddafc7f5e73715a2604b61d50_306_1.png)

图 9-1：查看 `SATAN`

要启动 `ISS`，你可以运行文本模式或 `X` 模式。要在文本模式下运行，请使用：

```
# /opt/security/iss/iss
```

要在 `X` 模式下运行，请使用：

```
# /opt/security/iss/xiss &
```

图 9-2 展示了主 `xiss` 屏幕的样子。

要配置 `ISS`，点击“配置扫描器”按钮，并勾选你想测试的漏洞利用。图 9-3 是“配置扫描器”屏幕的样子。如果你正在处理生产或实时系统，用户正在执行实际工作，你可能不希望运行拒绝服务攻击。

![](img/8ad518fddafc7f5e73715a2604b61d50_307_0.png)

![](img/8ad518fddafc7f5e73715a2604b61d50_308_0.png)

图 9-3：查看 `XSS` 扫描器配置界面

当配置好扫描器后，请配置分析器。为此，请单击“配置分析器”按钮。这将决定报告的生成结构。图 9-4 展示了分析器配置界面的样子。

![](img/8ad518fddafc7f5e73715a2604b61d50_308_1.png)

图 9-4：查看 `XSS` 分析器配置界面

现在，要运行扫描器，请按下“开始扫描”按钮。扫描器运行完成后，单击“开始分析”，并选择你想要的报告类型（请参考此处提供的示例报告）。列表 9-3 展示了一份扫描报告，其中列出了每个主机的漏洞数量及其类型。

### 列表 9-3：每个主机的漏洞数量

```text
Internet Security Scanner (C)1992-1997
ISS SAFEsuite Version 4.3.8
By Internet Security Systems, Inc.
Analysis Report

Summary Report of Vulnerabilities
Summary Information
Hosts Scanned: 1
Hosts with Active Services: 1
Hosts with No Services: 0
Start Time: Tue Jul 7 15:40:21 1998
End Time: Tue Jul 7 15:44:12 1998
Total Time: 3 minutes 51 seconds
Scan Completed Normally

Total Number of Vulnerability Risks: 10
Average Number of Vulnerability Risks per Active Hosts: 10.00
```

报告的第一部分是漏洞总数以及每个主机的平均数量。由于我们只扫描了一个主机，因此总数应等于平均值。

```text
Maximum License Number Reached: 0
Out of Range: 0
Open Ports via Socks Service [High Risk]: 0
Open Defaults found through Telnet [High Risk]: 0
Open Defaults found through Rexec [High Risk]: 0
Open Defaults found through FTP [High Risk]: 0
Open Defaults found through POP3 [High Risk]: 0
Accounts accessible through Rsh [High Risk]: 0
X Check [High Risk]: 1
```

它发现的第一个漏洞位于 `X` 窗口系统。大多数漏洞通常只有一种通用的利用方式，因此如果发现风险，描述之后通常会有相应的一条记录。
