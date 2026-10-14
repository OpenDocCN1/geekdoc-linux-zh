

- logging—此语句在 named.conf 及包含文件中应仅出现一次。它控制日志级别和日志文件路径。
- options—在此部分配置全局 named 服务器选项。请注意，此部分在 named.conf 及包含文件中应仅出现一次。
- server—此语句定义特定名称服务器的信息和行为。
- zone—此语句定义一个区域以及该区域的特定行为和信息。

子语句—如前所述，子语句是在主语句内使用的块。在本章中，我们将只定义本章中会用到的子语句。要获取所有子语句的完整参考，请启动您喜欢的 Web 浏览器并打开文件：file:/usr/doc/packages/bind/html/config.html，如果您安装了 BIND 8.x，该文件会本地存储在您的 Linux 分区上。

## The named.conf Syntax

请看以下示例，该示例使用了 options 语句和 directory 子语句：

// An example of using the options statement
options {
    directory "/var/named";
};
```

在此示例中，大括号 {} 用于创建 options 语句块。在此块内，directory 子语句被定义，它指示 BIND 使用 /var/named 作为其输出文件的默认目录。以下是使用 zone 语句的示例。在此语句中，从 /var/named/root.hints 文件定义的根级区域：

```
zone "." IN{
    type hint;
    file "root.hints";
};
```

前一节指出，当名称服务器启动时，它应缓存在 root.hints 文件中找到的名称服务器。此文件应位于 options 部分指定的路径中，在本示例中为 /var/named/root.hints。root.hints 文件应如下所示：

```
G.ROOT-SERVERS.NET.    5w6d16h IN A    192.112.36.4
J.ROOT-SERVERS.NET.    5w6d16h IN A    198.41.0.10
K.ROOT-SERVERS.NET.    5w6d16h IN A    193.0.14.129
L.ROOT-SERVERS.NET.    5w6d16h IN A    198.32.64.12
M.ROOT-SERVERS.NET.    5w6d16h IN A    202.12.27.33
A.ROOT-SERVERS.NET.    5w6d16h IN A    198.41.0.4
H.ROOT-SERVERS.NET.    5w6d16h IN A    128.63.2.53
B.ROOT-SERVERS.NET.    5w6d16h IN A    128.9.0.107
C.ROOT-SERVERS.NET.    5w6d16h IN A    192.33.4.12
D.ROOT-SERVERS.NET.    5w6d16h IN A    128.8.10.90
```

```
E. ROOT-SERVERS.NET. 5w6d16h IN A 192.203.230.10
I. ROOT-SERVERS.NET. 5w6d16h IN A 192.36.148.17
F. ROOT-SERVERS.NET. 5w6d16h IN A 192.5.5.241
```

您始终可以从 NIC 获取这些服务器的列表，通过连接到 Internet 并发出以下命令：

```
bash#dig @rs.internic.net . ns >root.hints.new 2>&1
```

此命令将获取根级主服务器的列表并将其放置在名为 root.hints.new 的文件中。

现在，/etc/named.conf 中的第二个区域条目如下：

```
zone "0.0.127.in-addr.arpa" IN{
    type master;
    file "127.0.0.zone";
};
```

在此示例中，0.0.127.in-addr.arpa 定义了一个新的区域，即您的本地主机。您本地主机的地址应以相反顺序放置。请注意，在定义区域时，最左边的数字未包含在内。同样，描述行为的配置文件是名为 /var/named/127.0.0.zone 的文件。此文件应如下所示：

```
1- $ORIGIN 0.0.127.in-addr.arpa.
2- @ 1D IN SOA localhost. root.localhost. (
3-           42          ; serial
4-           3H          ; refresh every 3 hours
5-           15M         ; retry every 15 minutes
6-           1W          ; expiry of cache is 1 week
7-           1D )        ; minimum time is one day
8-           1D IN NS    localhost.
9- 1               1D IN PTR localhost.
```

尽管乍一看很可怕，但此文件的格式很简单。此文件应以 $ORIGIN 开头，每个域名应以点结尾。如果未输入点，BIND 将附加 origin 地址，即 localhost。在文件中 = localhost 作为 BIND 解释它，但文件中 localhost = 127.0.0.localhost 作为 BIND 解释它。以下是此文件格式的分解：

- Line 1—$ORIGIN 语句定义 DNS 所属的层次结构。
- Line 2—@ 是一个特殊符号，表示 origin。此文件的 origin 域为 0.0.127.in-addr.arpa，因为它是从 named.conf 文件调用的。该行翻译如下：

```
0.0.127.in-addr.arpa. IN SOA localhost. root.localhost.
```

- Lines 3—序列号，也称为版本号，用于二级服务器检查区域更改时。如果您对该文件控制的区域进行任何更改，您必须增加此数字以反映区域信息的更新。
- Lines 4–7—这些行定义 BIND 对缓存地址的行为。
- Line 8—使用 NS 资源记录，该记录定义 origin 的域名，此行将名称定义为本地主机。
- Line 9—行开头的数字 1 将附加到 origin 的 IP 地址。整个新的 IP 地址将被设置为名称本地主机。

NOTE 区域文件可以包含的最重要的三个资源记录 RR 是 SOA、NS 和 PTR。第一个是起始授权资源记录 SOA。此记录定义主机或域分支的 origin。第二个资源记录是名称服务 NS。NS 告诉 DNS origin 的域名。第三个是指针资源记录 PTR，它从 origin 定义子网和主机。

## Setting Up a Caching Only Name Server

现在您已经建立了知识库，是时候使用它了。设置一个仅缓存的名称服务器是减少名称查找时间的好方法。如果您的机器位于局域网 LAN 上，如果您告诉局域网上的其他人也将其用作域名服务器，它将减轻现有名称服务器的负载。

## Setting Up the Server

您应首先设置主配置文件 /etc/named.conf。在您喜欢的编辑器中打开该文件并输入以下配置：

```
1 options {
2   directory "/var/named";
3   check-names master warn;
4   pid-file "/var/run/named.pid";
5   datasize default;
6   stacksize default;
7   coresize default;
8   files unlimited;
9   recursion yes;
10  multiple-cnames no;
11  // forwarders {    //This section would enhance the performance
12  //   xxx.xxx.xxx.xxx; //uncomment those and add your primary DNS
13  //   xxx.xxx.xxx.xxx; //and secondary DNS
14  // };
15 }
```

```
16 zone "." IN {
17 type hint;
18 file "root.hint";
19 };
20 zone "0.0.127.in-addr" IN {
21 type master;
22 file "127.0.0.zone";
23 check-names fail;
24 };
```

第 11-14 行仅对微调很重要。它们减轻了您机器的负载。如果您有另一台机器作为名称服务器运行，请在转发列表中包含其 IP。如果您没有，请添加您的主 DNS 和辅助 DNS。如果您使用调制解调器连接到 Internet，您应在转发列表中输入 ISP 的 DNS 地址。

要配置的第二个文件是 /var/named/root.hints。幸运的是，此文件随 SuSE Linux 预先准备好。但是，您应定期更新此文件。在连接到 Internet 时，发出以下命令以获取根名称服务器的新副本：

```
bash#dig @rs.internic.net . ns >root.hints.new 2>&1
```

此命令将获取最新根名称服务器的副本并将其保存到名为 root.hints.new 的文件中。获取此文件后，您可以覆盖原始 root.hints 文件，从而确保您始终拥有最新版本的根名称服务器。每周执行一次此操作是个好主意。

要配置的第三个文件是 /var/named/127.0.0.zone。此文件应仅负责本地主机机器。此文件随 SuSE Linux 预先配置，应包含以下内容：

```
$ORIGIN 0.0.127.in-addr.arpa.
@       1D IN SOA     localhost. root.localhost. (
                        42      ; serial
                        3H      ; refresh
                        15M     ; retry
                        1W      ; expiry
                        1D )    ; minimum

1       1D IN NS      localhost.    ;127.0.0 is a name server
        1D IN PTR     localhost.   ;localhost = 127.0.0.1
```

现在，您应该已完成仅缓存名称服务器的配置。通过发出以下命令重新启动 named 以便它可以使用新配置：

```
bash#/sbin/init.d/named restart
```

## Using the Caching Only Name Server

要使用新配置的服务器，您应告诉解析器使用您的本地主机作为主名称服务器。使用 YaST，打开系统管理，网络配置，

