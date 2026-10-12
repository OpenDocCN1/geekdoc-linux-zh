
# 列表 175 - 更优雅的正则表达式解决方案

这个解决方案非常聪明，但引入了一些新技巧。首先，注意 `grep -o` 选项，它将返回正则表达式找到的字符串。如果我们仔细构造表达式，这个命令将处理大部分数据。提取看起来很复杂，但非常直接。我们要搜索的字符串 `[^/]*megacorp\.com` 被封装在单引号中，正如我们提到的，它将允许扩展并将字符视为字面量。表达式中的第一个块 `[^/]*` 是取反 (`^`)，它搜索包括斜杠内的任意字符。点用反斜杠转义 (`\.`) 以强化我们寻找的是字面上的点。当 `grep` 找到以 `megacorp\.com` 结尾的字符串时，它将从行中提取并返回它。

为了使用逗号分隔的列表，这个块 `[,]*` 会排除斜杠和引号。这有很多新内容看起来让人无所措，但这是一个很好的正则表达式，它可以找到斜杠之后以 `megacorp\.com` 结尾的任何字符串，之后可以使用此正则表达式从文件中提取任意字符串。我们可以用这个正则表达式做更多，但这是一个很好的开始，也是正则表达式价值的例子。

现在我们有了从 `megacorp.com` 页面链接良好的域名列表。接下来我们将使用 `host` 来发现文件中每个域对应的 IP 地址。我们可以使用一个 `bash` 循环来实现：

```bash
kali@kali:~ for url in $(cat list.txt); do host $url;
```

```
admin.megacorp.com has address 38.100.93.83
beta.megacorp.com has address 38.100.93.88
intranet.megacorp.com has address 38.100.93.54
mail12.megacorp.com has address 38.100.93.73
```

## 列表 176 - 使用 host 命令查找 IP 地址

`host` 命令给我们的输出很多，但并非都是相关的。我们将通过将输出管道到 `grep "has address"` 来提取 IP 地址并进行排序：

```bash
kali@~$ for url in $(cat list.txt); do host $url; done | grep "has address" | cut -d " " -f2 | sort -u
```

```
38.100.93.66
38.100.93.67
38.100.93.73
38.100.93.76
38.100.93.77
38.100.93.79
38.100.93.84
38.100.93.87
38.100.93.88
```

## 列表 177 - 仅提取 IP 地址

太棒了！我们从网页提取了 `"megacorp.com"` 子域并获得了对应的 IP 地址。正如我们所看到的，有多种方法可以使用 `Bash` 和相关工具以及正则表达式来处理数据，这强化了这样一个事实：在这些主题上花费任何时间都将为未来处理数据或加速进程节省大量时间。

# 5.7.2 实用 Bash 使用 - 示例 2

在这个例子中，假设我们正处于渗透测试中间，并且对 Windows 机器具有未授权访问权限。随着继续收集信息，我们意识到它可能受到我们读过的带有 a、f、d 字母的漏洞的攻击，我们无法记得该漏洞的全名。为了尝试提升权限，我们需要搜索那个特定的漏洞。

为了做到这一点，我们需要搜索我们的标准并检查它们，直到找到正确的一个。我们可以手动通过网站 `https://www.exploit-db.com` 搜索 `"afd"`，下载匹配的漏洞将花费太长时间，但如果我们花时间编写一个 `Bash` 脚本，以后就可以轻松地使用它来自动下载漏洞。

利用我们对脚本的了解，让我们尝试自动化此任务。

我们将从 Kali Linux 上的 `SearchScript` 开始。`SearchExploit` 是 `Exploit-DB` 的一个命令行搜索工具，允许我们去到何处都创建一个漏洞数据库的离线副本。我们将 `"afd windows"` 作为搜索字符串，使用 `-w` 返回 `https://www.exploit-db.com` 的 URL 而不是本地路径，并使用 `-t` 搜索漏洞标题：

| exploit Title | URL |
| :--- | :--- |
| Microsoft Windows (x86) - 'afd.sys' Privil | https://www.exploit-db.com/exploits/40564 |

使用 Kali Linux 2 进行渗透测试

| Microsoft Windows | 'afdJoinleaf' Privilege | https://www.exploit-db.com/exploits/21844 |
| Microsoft Windows | 'afd.sys' Local Kernel | https://www.exploit-db.com/exploits/18755 |
| Microsoft Windows 7 (x64) | 'afd.sys' Dang | https://www.exploit-db.com/exploits/39525 |
| Microsoft Windows 7 (x86) | 'afd.sys' Dang | https://www.exploit-db.com/exploits/39446 |
| Microsoft Windows XP Kernel | Pooled-Based OS | https://www.exploit-db.com/exploits/42089 |
| Microsoft Windows XP | 'afd.sys' Local Ker | https://www.exploit-db.com/exploits/17133 |
| Microsoft Windows XP 2003 | 'afd.sys' Priv | https://www.exploit-db.com/exploits/6757 |
| Microsoft Windows XP 2003 | 'afd.sys' Priv | https://www.exploit-db.com/exploits/18176 |

## 列表 178 - 使用 searchploit 搜索漏洞

这是一个很好的开始，但我们需要精简结果。目前，我们只对漏洞的 URL 感兴趣，所以让我们 `grep` 搜索 `"http"` 并截取我们需要的内容。我们可以使用 `|` 作为字段分隔符并提取第二个字段：

```bash
kalikali~$ searchploit af windows -w -t | grep http | cut -f 2 -d "|"
```

```
https://www.exploit-db.com/exploits/49564
https://www.exploit-db.com/exploits/21844
https://www.exploit-db.com/exploits/18755
https://www.exploit-db.com/exploits/39525
https://www.exploit-db.com/exploits/39446
https://www.exploit-db.com/exploits/42089
https://www.exploit-db.com/exploits/17133
https://www.exploit-db.com/exploits/18176
https://www.exploit-db.com/exploits/6757
```

## 列表 179 - 从 searchploit 的输出中提取 URL

看起来好了一点。现在我们已经有了每个漏洞的 URL，可以使用 `Bash` 循环来下载文件并将其保存到本地。然而，在此之前，我们注意到每个页面都有一个下载“原始”（raw）漏洞代码的链接，这我们要需要的：

![](img/f99f528ca9845f4c256ce54e882b1345_125_0.png)

# Microsoft Windows (x86) - 'afd.sys' 本地权限提升 (MS11-046)

| EDB-ID | CVE | Author | Type | Platform | Published |
|---|---|---|---|---|--|
| 42364 | 2013-1249 | TOMISL PASKALEV | LOCAL | WINDOWS_ANY | 2014-05-18 |
| | | EXPLOIT | View Raw | VULNERABLE APP: |

```c
/*
************************************************

# Title: Windows x86 (all版本) AFD 权限提升 (MS11-046)

# Date: 2016-01-18

# Author: Tomislav Paskalev

# Vulnerable Software:

# Windows XP x86

# Windows XP SP2 x64
```
