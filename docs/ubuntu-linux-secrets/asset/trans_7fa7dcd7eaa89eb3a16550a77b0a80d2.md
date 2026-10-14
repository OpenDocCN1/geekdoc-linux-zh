

parameter 是 DNS 服务器的主机名。还应有一个关联的 A 记录来标识 DNS 服务器的 IP 地址。

## The HINFO Record

可以通过使用 HINFO 记录，将有关计算机的附加信息提供给 DNS 服务器。HINFO 记录的格式为

```
host [TTL] [class] HINFO hardware software
```

此记录的参数为：

- host：信息适用的计算机的主机名。
- hardware：计算机使用的硬件类型。
- software：计算机的操作系统类型和版本。

HINFO 记录是可选的，并且由于安全问题，现在已很少使用。

## The PTR Record

除了 A 记录之外，区域中的每台计算机都应有一个 PTR 记录。此记录允许 DNS 服务器从计算机的 IP 地址执行反向查询。如果没有此信息，远程服务器将无法确定您的计算机所在的域名。PTR 记录的格式为

```
IN-ADDRname [TTL] [class] PTR name
```

此记录中使用的参数为

- IN-ADDRname：IP 地址的反向 DNS 名称。如果这听起来令人困惑，那确实如此。此名称允许 DNS 服务器从计算机的 IP 地址向后工作。IP 地址为 192.168.0.1 的计算机的 IN-ADDRname 将为 1.0.168.192.IN-ADDR.ARPA。
- name：如 A 记录中所找到的计算机的主机名。

> PTR 记录对于允许对主机 IP 地址进行反向查找至关重要。如果没有它，像防火墙这样的设备就无法根据其 IP 地址确定您的主机的主机名或域。

## The MX Record

随着电子邮件的普及，DNS 系统为定义邮件服务器提供特殊支持也就不足为奇了。这是通过使用 MX 记录完成的。MX 记录指示远程邮件服务器将邮件转发到您的区域的位置。MX 记录的格式为

```
name [TTL] [class] MX preference host
```

此记录的特殊参数为

- **name:** 区域名称（如果区域名称为空，则为 SOA 区域）。此参数也可以是主机名，如果您想将特定主机网络的邮件重定向。
- **preference:** 一个整数，表示如果指定了多个邮件服务器，远程服务器应尝试连接的顺序，其中 0 为最高优先级（优先级随着数字的增加而降低）。此参数用于为区域创建主邮件服务器和辅助邮件服务器。当远程邮件服务器查询 DNS 服务器以获取负责该区域的邮件服务器时，服务器和优先级的完整列表将被发送。远程邮件服务器应尝试连接到列出的最高优先级邮件服务器，如果失败，则按优先级继续向下列表。
- **host:** 邮件服务器的主机名。还应有一个关联的 A 记录来标识邮件服务器的 IP 地址。

大多数较大的域都有多个可以接受该域邮件的邮件服务器。常见的情况是多个邮件服务器具有相同的 preference 值。当这种情况发生时，发送邮件服务器可以发送到具有相同 preference 值的列表中的任何邮件服务器。

## Sample DNS Configuration

如果您允许您的 ISP 代管您的域名和电子邮件，他们将在其 DNS 数据库中拥有记录，以将您的域标识给 Internet。SOA 记录将标识您的域名，但指向 ISP 主机作为权威主机。您域的 NS 记录将指向您 ISP 的 DNS 服务器，而您的 MX 记录将指向您 ISP 的邮件服务器。

就其余 Internet 而言，这些计算机是您网络的一部分，即使它们实际上并不存在于您的网络上。以下是 ISP 如何在其 DNS 数据库中定义区域定义的示例：

```
smallorg.org IN SOA master.isp.net. postmaster.master.isp.net. (
1999080501 ; unique serial number
8H ; refresh rate
2H ; retry period
1W ; expiration period
1D ; minimum

NS ns1.isp.net. ; defines primary name server
NS ns2.isp.net. ; defines secondary name server

MX 10 mail1.isp.net. ; defines primary mail server
MX 20 mail2.isp.net. ; defines secondary mail server

www CNAME host1.isp.net ; defines your www server address
ftp CNAME host1.isp.net ; defines your FTP server address

host1.isp.net A 10.0.0.1
1.0.0.10.IN-ADDR.ARPA PTR host1.isp.net ; pointer address
```

前六行显示了您新域的 SOA 记录。ISP 将您的域名 smallorg.org 指向 ISP 服务器 master.isp.net。

