
```
#### Documents on gist.github.com
site:gist.github.com "mxrads.com"

#### Documents on Pastebin
site:pastebin.com "mxrads.com"

#### Documents on JustPaste.it
site:justpaste.it "mxrads.com"

#### Documents on PasteFS
site:pastefs.com "mxrads.com"

#### Documents on CodePen
site:codepen.io "mxrads.com"
```

一次搜索产生了图 4-4 所示的结果。

![](img/961e81aef23040d0fbe348f58c055860_72_0.png)

图 4-4：MXR Ads 日志文件的一个片段

这似乎是一个日志文件提取物，挂在公共 Gist 上，供任何人查看。这不是很可爱吗？遗憾的是，没有立即获得关键信息，但我们确实得到了这些独特的 URL：

- format-true-v1.qa.eww1.mxrads.com

- dash-v3-beta.gretschpolitico.com

- www.surveysandsstats.com/9df6c8db758b35fa0f1d73...

我们在浏览器中测试这些。第一个链接超时，第二个链接重定向到 Google 认证页面（见图 4-5）。

![](img/961e81aef23040d0fbe348f58c055860_72_1.png)

图 4-5：在日志文件片段中发现的 Gretsch Politico 登录链接

Gretsch Politico 显然订阅了 Google Workspace（前称 G Suite）应用来管理其企业电子邮件，很可能还管理其用户目录和内部文档。我们会在稍后开始搜刮数据时记住这一点。

第三个 URL，指向图 4-6，很有希望。

![](img/961e81aef23040d0fbe348f58c055860_73_0.png)

图 4-6：在日志文件片段中发现的指向 MXR 广告调查的链接

这必定是 MXR Ads 用于收集看似无害的人们信息的那种调查之一。尝试通过他们其中一种险恶的表单来入侵 MXR Ads 或 Gretsch Politico 颇具诱惑力，但我们仍处于侦察工作的中间阶段，所以让我们先记下这一点以便稍后尝试。

### 拉取 Web 域名

被动侦察迄今为止并未为我们带来太多入口点。我认为是时候我们认真开始挖掘与 MXR Ads 和 Gretsch Politico 相关的所有域名和子域名了。我确信我们能找到比遗忘的 Gist 粘贴中那三个可怜的网站多得多的东西。希望我们能登陆到一个荒废的网站上，那里有一个狡猾的漏洞在迎接我们进入。

我们将首先通过检查证书日志中的子域名来开始搜索。

#### 来自证书

Censys (`https://censys.io/`) 是一款常规扫描证书日志以摄取所有新签发 TLS 证书的工具，并且是任何渗透测试人员域名发现工具列表中的头号工具。在由证书颁发机构签发后，证书会被推送到一个名为证书日志的中央存储库中。该存储库保存所有证书的二叉树，其中每个节点都是其子节点的哈希值，从而保证整个链的完整性。这大致遵循比特币区块链所采用的相同原理。理论上，所有签发的 TLS 证书都应公开发布，以检测域名欺骗、拼写错误抢注、同形异义字攻击以及其他欺骗和重定向用户的恶作剧方式。

我们可以搜索这些证书日志，以挖掘出符合某些条件的任何新注册，例如“mxr ads”。这幅美丽画布的丑陋一面是，所有域名和子域名名称都可在网上公开访问。因此，隐藏在 obscure 域名后面的安全性极低的秘密应用很容易暴露。Censys 和 `crt.sh` 之类的工具会探索这些证书日志，并至少将子域名枚举的速度提高一个数量级——残酷地提醒我们，即使是最甜的葡萄也可能隐藏最苦的种子。在图 4-7 中，我们使用 Censys 搜索 `gretschpolitico.com` 的子域名。

![](img/961e81aef23040d0fbe348f58c055860_74_0.png)

图 4-7：使用 Censys 查找子域名

透明度就这样了。似乎 GP 并没有费心注册子域名证书，而是选择了通配符证书：一种匹配任何子域名的通用证书。一个证书统治它们全部。无论这是出色的安全举措还是纯粹的懒惰，事实是，我们没有比顶级域名更进一步。我们在 Censys 中尝试其他顶级域名——`gretschpolitico.io`、`mxrads.tech`、`mxrads.com`、`gretschpolitico.news` 等等——但同样一无所获。我们的域名列表增长了令人震惊的胖胖的大零……但不要绝望！我们还有其他集体袖子里的技巧。

> **注意** 当然，通配符证书带来了另一个安全问题：它们是公然的单点故障。如果我们在漫游公司网络时偶然发现私钥，我们就可以拦截使用同一父域名的所有应用程序的通信流。

#### 通过收割互联网

如果证书不是收集子域名的途径，那么也许互联网可以伸出援手。`Sublist3r` 是一个很棒且易于使用的工具，可从各种来源收割子域名：搜索引擎、PassiveDNS，甚至 VirusTotal。首先，我们从官方仓库获取该工具并安装依赖项：

```
root@Point1:~# git clone https://github.com/aboul3la/Sublist3r
root@Point1:sub/# python -m pip install -r requirements.txt
```

然后我们继续搜索子域名，如清单 4-1 所示。

```
root@Point1:~# python sublist3r.py -d gretschpolitico.com
[-] Enumerating subdomains now for gretschpolitico.com
[-] Searching now in Baidu..
[-] Searching now in Yahoo..
[-] Searching now in Netcraft..
[-] Searching now in DNSdumpster..
--snip--
[-] Searching now in ThreatCrowd..
[-] Searching now in PassiveDNS..

[-] Total Unique Subdomains Found: 12
dashboard.gretschpolitico.com
```

##### 清单 4-1：使用 sublist3r 枚举域名

我们找到了 12 个子域名，这令人鼓舞。我敢打赌 `mxrads.com` 会有更好的运气。毕竟他们是一家媒体公司。然而，反复使用相同的工具和方法可能会变得无聊。对于 `mxrads.com` 域名，让我们使用不同的工具执行经典的暴力攻击，使用众所周知的子域名关键字，如 `staging.mxrads.com`、`help.mxrads.com`、`dev.mxrads.com` 等。有几款工具可供我们选择来完成这项工作。

`Amass` (`https://github.com/OWASP/Amass/`) from the Open Web Application Security Project (OWASP) is written in Golang and cleverly uses goroutines to parallelize the load of DNS queries. Whereas most other Python tools rely on the system’s DNS resolver to retrieve domains by calling functions like `socket.gethostname`, Amass crafts DNS queries from scratch and sends them to various DNS servers, thus avoiding the bottleneck caused by using the same local resolver. However, Amass is bloated with so many other colorful features, like visualizations and 3D graphs, that it may feel like wielding a 10-pound hammer to scratch an itch on your back. Tempting, but there are lighter alternatives.

我强烈推荐的是一款宣传较少但非常强大的工具 `Fernmelder` (`https://github.com/stealth/fernmelder/`)。它用 C 编写，代码不过几百行，可能是我最近尝试过的最有效率的 DNS 暴力破解工具。`Fernmelder` 接受两个输入：候选 DNS 名称列表和要使用的 DNS 解析器的 IP 地址。这就是我们将使用的方法。
