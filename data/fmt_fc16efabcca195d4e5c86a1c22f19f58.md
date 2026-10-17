
# 386 第 9 章 网络与因特网

`dig` 工具显示了大量信息。

- `Authority Section`（权威部分）指定了主域名服务器，`Additional Section`（附加部分）指定了对应 `Authority` 部分名称的 IP 地址。
- `SERVER` 行（位于末）指定了本地系统使用的 DNS 服务器的名称和 IP 地址：这是 `dig` 获取信息的地方。
- 第二列指定了以秒为单位的 `TTL`（页 149）。
- 第三列的 `IN` 是查询类别，表示互联网类查询。
- 第四列的 `SOA`、`MX`、`NS` 或 `A` 指定了行包含的信息类型（DNS 查询类型）：
    - `NS`（名称服务器）记录指定了 `upstate.edu` 使用的名称服务器。只有在查询域时 `NS` 记录才有意义。
    - `MX`（邮件交换器）记录指定了你正在查询的域的邮件服务器。`the.` 域有多个邮件服务器。较低的偏好值是邮件优先级。`the.` 域有多个邮件服务器。
    - 给定域的 `SOA`（区域授权）。
    - 控制域的 `TTL`。
    - 控制另一个服务器何时刷新（`refresh`）。
    - 控制另一个服务器何时超时。
    - `A`（记录）指定了最后一列中的 IP 地址。

```
>>> Last update of whois database: Tue, 26 Feb 2002 05:22:08 EST <<<

注册局数据库仅包含 .COM, .NET, .ORG, .EDU 域名和

注册商。

域名注册人:

Sobell Associates Inc (SOBELL-DOM)

PO Box 1089

Menlo Park, CA 94026

US

域名: SOBELL.COM

管理联系人，账单联系人:

Sobell, Mark (MS5989) sobell@MEER.NET

Sobell Associates Inc

PO Box 1089

Menlo Park, CA 94026

[无电话]

技术联系人:

meer.net hostmaster (MN85-ORG) hostmaster@MEER.NET

meer.net

po box 390804

Mountain View, CA 94039

US

+1.888.844.6337

传真 - +1.888.844.6337

记录最后更新于 2000-04-09。

记录于 2004-04-08 过。

记录创建于 1995-04-07。

数据库最后更新于 2002-02-26 01:57:00 EST。

域名服务器排序如下:

NS.MEER.NET 140.174.164.2

NS2.MEER.NET 216.206.136.2
```
