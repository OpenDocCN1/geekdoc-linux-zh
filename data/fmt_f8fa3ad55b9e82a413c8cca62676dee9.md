
## `/var/named/named.local` 文件

最后一个区域包含 localhost 的反向查找信息。这里引用的文件是 `/var/named/named.local`，如列表 18-4 所示。

列表 18-4：`/var/named/named.local` 文件包含内部网络 `127.0.0.1` 的反向查找信息

```
$TTL    86400

@               IN SOA      @ root.localhost. (

                                                1997022700 : serial

                                                28800        : refresh

                                                14400        : retry

                                                360000       : expire

                                                86400 ) : minimum

               IN NS         localhost.

               IN PTR        localhost.
```

### 区域文件

区域文件包含关于 IP 地址的资源记录 (`RR`)。典型的区域文件如列表 18-5 所示。

```
:Start of Authority Record
:Last modified May 2000
$TTL    86400

@               IN SOA      tactechology.com. root.tactechology.com.
```

# 第18 章：BIND：域名系统 (DNS)

```
2000052101 : Serial
2880521 : Refresh
14400 : Retry
604800 : Expire
86400 ) Minimum
```

; 命名服务器 (NS)
@ IN NS main.tactechology.com
@ IN NS p200.tactechology.com.

; 邮件服务器 (MX)
@ IN MX 10 main
@ IN MX 200.tactechology.com.

; 地址记录 (A)
localhost A 127.0.0.1
ns IN A 207.172.250.185
ns IN A 207.172.250.186
www IN A 207.172.250.185
ftp IN A 207.172.250.185

; 指向记录 (PTR)
PTR localhost

> A 区域文件可以包含许多类型的资源记录 (`RR`)，它们按照它们在区域文件中通常出现的顺序列出，并在下文中进行解释。

### SOA: 权威起始 (START OF AUTHORITY)

权威起始 (`SOA`) 是区域文件的第一行。`SOA` 标识了该命名服务器是该域名信息的权威源。每个区域文件仅有一个 `SOA`，它包含以下数据：

```
@ IN SOA main.tactechology.com. root.tactechology.com. (

200052101 : Serial

8h : :Refresh

2h : :Retry

1w : :Expire

1d) :Minimum TTL
```

`SOA` 行的第一个字符是一个特殊符号，意味着“查看此域名”。`@` 代表互联网。`SOA` 意味着权威起始。该域名的权威服务器是 `main.tactechology.com`，而 `root.tactechology.com` 是管理员的电子邮件地址。注意域名名末后的点。如果不包含这些点，则域名名将附加到该条目之后。

## 第三部分：互联网服务

左括号允许第一行进行扩展，使得左括号和右括号之间的任何内容都被视为一行。

括号内的信息会被传递给其他命名服务器（从主服务器从属服务器），它们使用这些信息来更新自己的记录。包含 `-200052101: Serial` 的行是文件的序列号。从属服务器将它们的数字与其存储的信息进行比较。如果数字相同，说明信息没有变化，无需下载此文件。如果序列号不同，则下载该文件以更新从属服务器中的信息。序列号可以是任何所需的数字，只要它能够递增以表示文件的修订。分号表示该行末尾的内容是注释。

![](img/8c5ce181a0f26bec693ad7f04bbfb6fe_461_0.png)

序列号字段的推荐格式是 `YYYMMDDN`，分别代表年、月、日和修订号。每当你更改此文件中的信息时，务必递增修订号。如果你忘记递增序列字段中的修订号，你的 DNS 修改将不会生效。

`Refresh` 是服务器在刷新数据之前应该等待的时间。`Retry` 是服务器在之前的尝试失败后，尝试联系主服务器之前应该等待的时间。

`Expire` 意味着从属主在指定期间无法联系主服务器，数据将过期并应被清除。

`Minimum` 规定了数据的生存时间 (`TTL`)。此参数用于缓存命名服务器，并告诉它们如何在缓存中保留数据。

`SOA` 包含的所有信息可以放在同一行中，但通常如之前所示进行编写。`SOA` 头部中项目的排列顺序是至关重要的。下文将进一步解释有关服务器的额外描述性项目。

### NS：本域中的命名服务器

显示命名服务器的名称。

### A：名称的 IP 地址

显示命名服务器的 IP 地址。

### MX 记录：邮件交换记录

`MX` 记录指定了域名的邮件服务器。在 `tactech.com` 区域文件中，列出了两个 `MX` 地址，一个后面跟着数字 `10`，另一个后面跟着数字 `20`。任何发送到 `tactechtechnology.com` 的邮件都会去 `main.tactech.com`，因为它的数字较。优先级由数字最低的地址决定，其优先级最高。因此，`main` 是主邮件服务器，`p200` 是备邮件服务器。如果 `main` 无法接收邮件，邮件将发送到 `p200`。`p200` 会尝试将邮件发送给 `main`，因为这也是它的主邮件服务器。当 `main` 再次能够接收邮件时，它将接收 `p200` 接收的所有邮件。

### PTR：地址名称映射的指针

用于指向命名服务器。

### CNAME：标准名称

显示主机的真实名称。

### TXT：文本信息

允许输入描述性信息。

### WKS：已知服务

允许输入描述性信息。

### HINFO：主机信息

通常显示硬件和软件类型。

### 反向区域文件

反向区域文件用于提供反向查找信息。在之前的示例中你搜索了域名。这被称为反向查找。

### 配置缓存服务器

你现在知道哪些文件需要配置，也知道需要放置在它们中的信息。在本节中，你将设置缓存服务器。如前所述，所有类型的服务器都使用六个文件。六个文件中三个是实际配置文件，另外三个用于提供全局参数。

在完成所有之前的步骤后，是时候设置 `named` 守护进程并检查工作了。

在命令提示符输入 `service started`，等待提示符返回，然后输入 `nslookup localhost`。如果你看到像列表 18-7 显示的屏幕，说明你成功配置了缓存服务器。

# 第 18 章：BIND：域名命名系统 (DNS)

地址: `127.0.0.1#53`

名称: `localhost`
地址: `127.0.0.1`

`[root@laptop root]#`

### 配置从服务器 (Slave Server)

接下来，你为你的域名设置一个从服务器。该步骤与你已经完成相似，并且并没有以前复杂得多。你已经有了三个文件，只需要稍微修改 `/etc/named.conf` 文件并添加另外两个文件即可完成从服务器的配置。

在你想要作为从服务器的服务器上，进入 `/etc/named.conf` 文件并添加两个区域（zones）：一个用于服务器的正向查找，另一个用于反向查找。对于正向查找，你需要添加以下内容。（在本例中，主服务器名为 `main.tactechtechnology.com`，从服务器名为 `p200.tactechtechnology.com`。请务必使用你自己的域名和 IP 地址，而不是示例内容。）

```
zone "tactechtechnology.com" (

  notify no;

  type slave;

  file "tactech.com";

  masters ( 192.168.1.1 );

)
```

对于反向查找，添加此部分：

```
zone "1.168.192.in-addr.arpa" (

  notify no;

  type slave;

  file "tac.rev";

  masters ( 192.168.1.1 );

)
```
