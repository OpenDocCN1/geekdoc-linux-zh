
`OEMREP_192.168.2.135` =

  (`DESCRIPTION` =

    (`ADDRESS_LIST` =

      (`ADDRESS` = (`PROTOCOL` = `TCP`) (`HOST` = `192.168.2.135`) (`PORT` = `1521`))

    )

  (`CONNECT_DATA` =

    (`SID` = `oemrep`)

    (`SERVER` = `DEDICATED`)

  )

```

你给服务器起的名称出现在第一行，条目的其余部分包含服务器的 IP 地址或主机名、连接端口以及 SID。

当我们尝试寻找数据库服务器时，使用了 `nmap`。然后我们使用 `TLSLSNR` 验证在 TCP `1521` 端口上运行的服务确实。我们可以通过检查密码来枚举 SID，但由于 `OSScanner` 可以一次性完成这些工作，让我们使用它。接下来，我们检查了对数据库 `LOWFRUIT` 的扫描结果。在本练习中，我们想要渗透数据库 `OEMREP`。图 3.15 显示了 `OSScanner` 工具对 `OEMREP` 的报告。

## 第 3 章 数据库测试简介

### 图 3.15 OEMREP 的 Oscanner 报告

![](img/2714962ecb7769011405633c8d4d1fc9_214_0.png)

我们看到 `SYS` 账户已启用并正在使用密码 `SYS`。该账户将允许我们访问数据库中的所有表。为了连接到数据库，我们将启动 Enterprise Manager Console 并添加数据库 `OEMREP`。图 3.16 显示了已添加 `OEMREP` 数据库的 Enterprise Manager Console。

### 图 3.16 Enterprise Manager Console 和 OEMEP 数据库

![](img/2714962ecb7769011405633c8d4d1fc9_215_0.png)

我们暂时不会连接到数据库，相反，我们想要启动 SQL*Plus Worksheet（选择 Tools | Database Applications | SQL*Plus Worksheet），然后连接到数据库（在新窗口中，选择 File | Change Database Connection）并使用 `SYS` 的账户和密码。一旦建立连接，我们将导出用户名和密码哈希值。Oracle 将密码以哈希形式存储在 `SYS.USER$` 表中。使用简单查询 `select name,password from sys.user$ where type=1;` 我们得到了图 3.17 所示的结果。现在我们拥有了破解密码所需的哈希值和用户名。

### 图 3.17 用户名和密码查询结果

![](img/2714962ecb7769011405633c8d4d1fc9_216_0.png)

为了破解密码，我们将使用一个名为 `orm`（[www-johnjohn.org/tools/orab/index.html]）的工具。该工具运行在 Windows 上，并带有一个用于字典攻击的默认字典。它还可以对密码哈希进行暴力破解攻击。图 3.18 显示了通过字典攻击和暴力破解破解的一些 `OEMREP` 密码。你可以看到暴力破解花费相当的时间。幸运的是，暴力破解尝试的是所有的字符组合，而不是尝试所有的字母组合再添加特殊字符。

### 图 3.18 使用 OraBF 破解的密码

命令提示符

```
orah v0.7.4.(C)2005 orm@toolcrypt.org

Trying default passwords:

password found:STITCH

C:\orah-v0.7.4.oraBF.exe F628EFBFBD930169:BOOMER 4\orah v0.7.4.(C)2005 orm@toolcrypt.org

Trying default passwords:

password found:BOOMER 4

C:\orah-v0.7.4.oraBF.exe C50B6DD81A80397:MPF 4\orah v0.7.4.(C)2005 orm@toolcrypt.org

Trying default passwords...

password found:MPF 4

C:\orah-v0.7.4.oraBF.exe 9EHPF236BFD4098:HIIGUE 4\orah v0.7.4.(C)2005 orm@toolcrypt.org

Trying default passwords...done

Starting brute force session using charset:

8515C4A75F9B6B5E3340066E804YZ

press 'q' to quit. any other key to see status

current password:BOGN_M

1622079961 passwords found. elapsed time 00:43:53, t/s:631133

password found:HIIGUE:STOTAM

1759F4539 passwords found. elapsed time 00:46:30, t/s:630482

C:\orah-v0.7.4\>
```

由于我们在数据库上拥有 `SYS` 账户，我们现在“拥有”了数据库。然而，通过捕密码文件并破解密码，我们可以利用获得的信息将渗透测试扩展到服务器数据库链接之外，或者可能通过服务器信任。就像 SQL Server 的示例一样，这仅仅是开始。文中再次强调，本章描述的工具（Oracle 客户端除外）都是开源工具。在这里表示它们时带有一条警告：在进行评估之前，请先在实验室环境中测试这些工具。我们对这些工具的信心并不代表它们保证没有木马或其他任何恶意软件。

要将你的数据库渗透测试提升到下一个，有必要学习 SQL。学习 SQL 有很多资源，无论是通过互联网、课堂培训，还是按照自己的节奏自学。无论你选择哪种方法，请确保你也学习了每个软件厂商语言的细微差别。一旦学会了 SQL，你就可以探索高级渗透技术，这些技术允许你利用数据库在服务器上执行命令、使用服务器执行网络命令、创建你自己的存储过程、提升数据库内的权限并窃取数据。

## 更多信息

本章中的某些工具基于命令行，并且需要特定的开关。作为复习，这里是本章涵盖的工具以及开关摘要（如果适用）。

### 发现数据库

发现 SQL Server 默认 TCP 端口：

```
nmap -sS 1433 x.x
```

发现 SQL Server 默认 UDP 端口：

```
nmap -sU 1433 x.x
```

发现 Oracle Server 默认 TCP 端口：

```
nmap -sS 1521 x.x
```

发现 Oracle Server 默认 UDP 端口：

```
nmap -sU 1521 x.x
```
