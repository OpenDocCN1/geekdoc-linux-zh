
```
IN MX preference_value mail_server_hostname.
```

例如：

```
IN MX 0 mail.ad-engine.com.
```

优先级数字只有在你拥有多个邮件服务器时才有用。例如：

```
IN MX 10 fast-mail-server.ad-engine.com.
```

```
IN MX 20 slow-mail-server.ad-engine.com.
```

这里，优先级数字越低表示优先级越高。现在你已经学习了 DNS 资源记录的基础知识，可以准备创建主、辅和仅缓存的 DNS 服务器了。

## 使用 bindconf 配置 DNS 服务器

通常不建议在服务器上安装 X Window 系统，因为管理服务器并不需要这样的图形用户界面，而且 X 会使系统更容易受到黑客攻击，因为许多 X 程序不断被发现存在漏洞。然而，如果你必须在 DNS 服务器上使用 X Window 系统，你也可以利用 Bind 配置工具（bindconf）来配置 DNS 服务器（BIND）。如果你没有在服务器上安装 X，这也是我的建议，那么你可以跳到下一节。

![](img/9eb7e89292d2f85707b4d49102c865b7_475_0.png)

> 如果你决定使用 bindconf，你绝不能手动修改 /etc/named.conf 文件，因为 bindconf 每次使用时都会重新创建该文件。也就是说，如果你手动修改此文件，你的更改将在下次使用 bindconf 时丢失！

当你从 xterm 窗口运行 bindconf 时，会出现类似图 15-1 的窗口。

默认情况下，bindconf 会创建一个名为 localhost 的主区域，并具有适当的反向 DNS 配置。这在主菜单窗口中显示。此配置仅用于回环地址。

![](img/9eb7e89292d2f85707b4d49102c865b7_476_0.png)

图 15-1 bindconf 主屏幕。

## 为域名创建正向主 DNS 区域

假设你想为名为 evoknow.com 的新域名创建一个正向主区域。请执行以下操作：

- 1. 在主 bindconf 窗口中单击 Add 按钮，你将看到如图 15-2 所示的屏幕。选择 Forward Master Zone 选项并在名称输入区域输入适当的域名，然后单击 OK 继续。

![](img/9eb7e89292d2f85707b4d49102c865b7_476_1.png)

图 15-2 选择区域类型。

- 2. 你将看到如图 15-3 所示的屏幕。你可以将联系地址更改为比 root@localhost 更合适的地址。

![](img/9eb7e89292d2f85707b4d49102c865b7_477_0.png)

图 15-3 名称到 IP 翻译窗口。

如果你想设置区域生命周期信息，请单击 Time Settings 按钮，这将打开如图 15-4 所示的屏幕。将刷新率、重试率、过期率、最小时间等设置为所需的任何设置。在大多数情况下，默认值是可以的。

![](img/9eb7e89292d2f85707b4d49102c865b7_477_1.png)

图 15-4 区域生命周期信息窗口。

- 3. 现在你必须为此域名添加一个名称服务器（NS）记录。在添加 NS 记录之前，请确保你已为名称服务器主机定义了 A（地址）记录。单击图 15-3 所示窗口中 Records 下的 Add 按钮会打开如图 15-5 所示的屏幕。选择 Host 作为资源记录类型并为此 A 记录输入主机名和 IP 地址。

![](img/9eb7e89292d2f85707b4d49102c865b7_478_0.png)

图 15-5 添加 A（地址）记录。

以相同的方式为此域名添加任意数量的主机。在此示例中，我添加了 ns1.evoknow.com 和 mail.evoknow.com。

- 4. 从图 15-3 所示的窗口中，选择域名（evoknow.com）并单击 Edit 按钮以打开如图 15-6 所示的域设置窗口。在 Name Servers 部分下，单击 Add 按钮并输入名称服务器主机的名称，在此示例中为 ns1.evoknow.com。同样，如果你为邮件服务器设置了主机，可以在 Mail Exchangers 部分下添加它，如本示例所示。邮件交换机优先级是一个任意数字。如果设置了多个邮件服务器，编号最低的邮件服务器将被视为最高优先级的邮件服务器。单击 OK 返回主菜单。

![](img/9eb7e89292d2f85707b4d49102c865b7_478_1.png)

图 15-6 为新域名添加名称服务器和邮件服务器。

- 5. 在为新域配置添加了至少一个名称服务器后，你可以在主菜单屏幕中选择 File ⇨ Apply，然后将为所选域名（本例中为 evoknow.com）创建新的 /etc/named.conf，其中包含适当的 master 配置。此外，还将在 /var/named 目录中创建一个名为 evoknow.com.zone 的新区域文件，其中包含区域的主配置数据。

## 为域名创建反向主区域配置

假设你想为名为 evoknow.com 的新域名创建一个反向主区域。请执行以下操作：

- 1. 确保你已按照上一节所述创建了正向主区域。
- 2. 在主 bindconf 窗口中单击 Add 按钮，你将看到类似图 15-7 所示的屏幕。选择 Reverse Master Zone 选项并在 IP 地址输入区域输入网络的 IP 地址的前三个八位组。单击 OK 继续。

![](img/9eb7e89292d2f85707b4d49102c865b7_479_0.png)

图 15-7 添加反向区域。

- 3. 在 IP 到名称翻译屏幕（如图 15-8 所示）中，你应该添加名称服务器以及你希望提供反向 DNS 的任何其他主机。
- 4. 在添加所有主机后，你应该单击 OK 并返回主菜单，其中应显示你的正向和反向

![](img/9eb7e89292d2f85707b4d49102c865b7_480_0.png)

图 15-8 在反向 DNS 配置中添加名称服务器和其他主机。

区域配置名称。选择 File ⇔ Apply 以应用你的配置，创建必要的反向区域文件，更新 /etc/named.conf。

## 手动配置 DNS 服务器

如果不使用基于 X Window 系统的 bindconf 工具，你必须通过使用 vi 等文本编辑器手动编辑和创建配置文件来手动配置 DNS 服务器。

## 配置主（主用）DNS 服务器

本节中的说明假设我在 ns.evoknow.com 主机上运行一个 DNS 服务器（named），并且我刚刚在 Internic 注册了一个名为 classifiedworks.com 的域名。现在我想在 ns.evoknow.com 上设置 DNS 以为新域名提供主名称服务。方法如下。

- 1. 首先，我需要在 /etc/named.conf 文件中创建以下区域语句：

```
zone "classifiedworks.com" {
    type master;
    file "classifiedworks.db";
};
```

此语句指定我的名称服务器是 classifiedworks.com 域的主名称服务器。

- 2. 现在我需要在名称服务器的工作目录（由 options { directory path }; 语句指定）中创建一个名为 classifiedworks.db 的区域文件。列表 15-2 是 classifiedworks.com 域的此类区域文件的示例。

### 列表 15-2 一个示例区域文件

```
@   IN  SOA  ns.evoknow.com. kabir.evoknow.com. (
        1999020100  ; Serial
        7200        ; Refresh - 2 hours
        3600        ; Retry  - 1 hour
        43200       ; Expire - 12 hours
        3600 )      ; Minimum - 1 hour

IN NS ns.evoknow.com.
IN MX 10 mail.evoknow.com.

www IN CNAME www.evoknow.com.
ftp IN A 206.171.50.55
```

在这里，我设置了 SOA 和 NS 记录，说明 ns.evoknow.com 是 classifiedworks.com 域的名称服务器。

- 3. 因为我想在此域的邮件在 mail.evoknow.com 主机上接收，所以我设置了一个 MX 记录来实现这一点。

- 4. 我设置了一个名为 `www.classifiedworks.com` 的别名，指向 `www.evoknow.com`。
- 5. 最后，我为 `ftp.classifiedworks.com` 设置了一个 A 记录，使其指向 206.171.50.55。

使用各种资源记录，你可以根据需要配置区域文件。区域文件配置并存储在 DNS 服务器的工作目录中后，该域的主名称服务器配置即完成。

## 配置从（辅助）DNS 服务器

配置从或辅助 DNS 服务器非常简单。你唯一需要手动更新的文件是 `/etc/named.conf` 文件。例如，假设我想使用名为 ns2.evoknow.com 的 DNS 服务器作为 classifiedworks.com 域的辅助名称服务器。我需要做的第一件事是在 ns2.evoknow.com named 服务器的 `/etc/named.conf` 文件中创建如下的区域语句：

```
zone "classifiedworks.com" {
    type slave;
    file "classifiedworks.db";
};
```

因为这是一个从或辅助服务器，所以我不需要手动创建 classifiedworks.db 文件。我可以使用名为 named-xfer 的程序从 classifiedworks.com 域的主名称服务器获取该文件，该程序随 named 发行版提供。因为我知道 classifiedworks.com 域的主名称服务器名为 ns.evoknow.com，所以我可以按如下方式运行 named-xfer 命令：

```
named-xfer -z classifiedworks.com -f classifiedworks.db \
-s 0 ns.evoknow.com
```

这里 -z 选项指定区域名称，-f 选项指定区域文件名，-s 选项指定信息当前所在的名称服务器。
