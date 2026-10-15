
[recon-ng/default] >

```bash
[recon-ng/default] > marketplace list
```

### 步骤 2：市场搜索

```bash
[recon-ng/default] > marketplace search
```

#### 模块接口

Usage: `marketplace <info|install|refresh|search>`

```bash
[recon-ng/default] > marketplace install csv

# Module installed: import/csv_file

# Module installed: reporting/csv

# Reloading modules...
```

```bash
[recon-ng/default] > modules load import/viewdns_reverse_whois
```

| Path | Version | Status | Updated |
|---|---|---|---|
| `discovery/info_disclosure/cache_snmp` | 1.1 | not installed | 2020-10-13 |
| `discovery/info_disclosure/interesting_files` | 1.1 | not installed | 2020-01-13 |
| `exploitation/injection/command_injector` | 1.0 | not installed | 2019-10-24 |
| `exploitation/injection/path_bruter` | 1.2 | not installed | 2019-10-28 |
| `import/csv_file` | 1.1 | not installed | 2019-08-09 |
| `import/list` | 1.0 | not installed | 2019-06-24 |
| `import/mapcan` | 1.0 | not installed | 2020-09-05 |
| `import/nmap` | 1.0 | not installed | 2019-08-26 |
| `recon/companies-contacts/bing_linkedin_cache` | 1.0 | not installed | 2019-08-24 |

```bash
[recon-ng/default] > modules load viewdns_reverse_whois

[recon-ng/default/viewdns_reverse_whois] > options set SOURCE google.com

SOURCE => google.com

[recon-ng/default/viewdns_reverse_whois] > run

------

GOOGLE.COM
```

## 7.6 Maltego

`Maltego` 是由 `Paterva` 创建的工具，经验分析师和 `OSINT` 探员在使用得非常好。`Maltego` 可以在范围内发现并收集有关潜在目标的信息。它可以以图表可视化收集到的信息。`Maltego` 可以从 `OSINT` 收集信息，并检查人员、团体、企业、网络框架、联盟和网站之间的真实连接。IT 安全专家、程序员、情报机构和政府协会利用 `Maltego` 来协助他们的特殊目标。

`Maltego` 是一个可以确定以下对象之间的关系和现实链接的程序：

- 人群（社交网络）
- 组织
- 网站
- 域名
- `DNS` 名称
- 网
- `IP` 地址
- 文档和文件

![img/8ce6ad080bbaee4f550e48ea7a3d6ee_163_0.png](img/8ce6ad080bbaee4f550e48ea7a3d6ee_163_0.png)

**图 60 Maltego**

来自 `Maltego` 的域名示例输出

![img/8ce6ad080bbaee4f550e48ea7a3d6ee_164_0.png](img/8ce6ad080bbaee4f550e48ea7a3d6ee_164_0.png)

## 7.7 Google Hacker

`Google` hacking 是使用网络爬虫寻找互联网上的安全漏洞，例如 `Google`。Web 上常见两种类型的漏洞：编程漏洞和配置错误。

尽管有一些专注于特定框架并试图寻找允许他们获取的漏洞的入侵者，但远多入侵者是从特定的编程缺陷或他们明确知道如何利用的普通客户端配置错误开始，这通常是用户或用户安装的程序无意配置的结果。可以挖掘出的信息范围是惊人的，几乎是无限的，包括各种“个人身份识别信息 (PII)”、秘密文档、密码、网络数据等等。所有这些都可以在没有复杂工具的情况下挖掘。只需要一个网络搜索引擎，使用基本的搜索运算符来缩小搜索结果，例如目标并孤立特定的网站或域名，搜索特定文件类型，搜索 `URL` 空间或搜索特定的敏感短语。

`GHDB` 中包含的一些搜索引擎类别包括：

- 产品敏感告告
- 包含目录路径等敏感信息的错误消息
- 带有敏感数据、密码和用户名的文件
- 敏感购物数据
- 关于 Web 服务器的详细信息

### Google Hacking Database (GHDB)

搜索 `Google` 攻击数据库或浏览 `GHDB` 类别

| Date | Title | Category |
|---|---|---|
| 2018-07-19 | `title:HTTP Server Test Page powered by CentOS` | Web Server Date |
| 2018-07-17 | `inurl:"debug/default/view|panel|config"` | Files Containing |
| 2018-07-16 | `inurl:configuration.php and text:"$password="` | Files Containing I |

**图 61 Google Hacking**

# Secbay Press

- `inurl` • `inurl` 将结果限制在网站 `URL` 包含所有指定短语、单词或字符串的网站上。例如：`inurl:admin`

- `allurl` • `allinurl` 与 `inurl` 相同，但略有不同。它将结果限制在网站 `URL` 包含所有指定短语的网站上，但 `inurl` 可以显示仅包含短语中某一个单独单词的网站。例如：`allinurl:admin login`

- `intitle` • `intitle` 将结果限制在标题中包含指定短语、单词或字符串的文档上。例如：`intitle:engineering`

- `allintitle` • `allintitle` 大多与 `intitle` 相同，仅略有不同。它将将结果限制在标题中包含所有指定短语、集合或单词的文档上。例如：`allintitle:engineering books`

`https://image.slideshare.com/presentation-150818125558-iva1-app6892/95/google-dorks-and-sql-injection-13-638.jpg?cb=1439902931`

- `filetype` 或 `ext` • 它将显示所有包含指定类型文档的网站。例如：`filetype:pdf` 或 `ext:pdf`

- `intext` • 它将显示所有在网站正文中包含指定文本或短语的结果页面或网站。例如：`intext:hacking`

- 包含敏感信息的文件（Files Containing Juicy Info）`Google` 搜索：`inurl::com/configuration.php-dist` 查找服务器上 `PHP` 数据库的配置文件

## 7.8 whois

### sudo whois google.com

```bash
whois -all -v google.com

Domain Name: GOOGLE.COM

Registrar Domain ID: 2138514_DOMAIN_COM-VRS

Registrar WHOIS Server: whos.markmonitor.com

Registrar WHOIS URL: http://www.markmonitor.com

Updated Date: 2019-09-09T13:39:04Z

Creation Date: 1997-09-15T04:14:00Z

Registrar Expiry Date: 2028-09-14T00:00:02Z

Registrar: Markmonitor Inc.

Registrar IANA ID: 209

Abuse Contact Email: email:abusecomplaints@markmonitor.com

Abuse Contact Phone: +1.2083809540

Domain Status: ClientDeleteProhibited https://icann.org/app#clientDeleteProhibited

Domain Status: ClientTransferProhibited https://icann.org/app#clientTransferProhibited
```
