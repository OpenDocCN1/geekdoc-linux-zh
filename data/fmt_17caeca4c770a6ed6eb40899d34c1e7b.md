
```
cache                 db.cache

;

; type        domain                  source host/file
;

primary              0.0.127.in-addr.arpa          db.0.0.127.in-addr.arpa

;

; domain maps
;

primary              sniglets.com                  db.sniglets
primary              3.168.192.in-addr.arpa        db.3.168.192.in-addr.arpa
:end of named.boot
```

`directory`指令告诉`named`在`/var/named`目录中查找数据文件。`cache`指令定义了缓存文件，在此实例中为`/var/named/db.cache`。`primary`指令告诉`named`它是以下域的授权服务器。在这种情况下，`named`是回环地址的授权服务器，也是域`sniglets.com`（数据文件为`/var/named/db.sniglets`）和 B 类网络`192.168.3`（数据文件为`db.3.168.192.in-addr.arpa`）的授权服务器。这就是配置 BIND 4 并运行所需的所有必要信息。

现在，如果我们将 BIND 4 的`/etc/named.boot`文件与 BIND 8 的`/etc/named.conf`文件进行比较，首先我们意识到格式截然不同。然而，一旦你花点时间分析`named.conf`文件，你就会意识到信息是相同的，只是指令不同。

```
; BIND 8 named.conf

;

options {

        directory "/var/named";

};
```

```conf
zone "." in {
    type hint;
    file "db.cache";
};

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "db.0.0.127.in-addr.arpa";
};

zone "sniglets.com"    in {
    type master;
    file "db.sniglets";
};

zone "3.168.192.in-addr.arpa" in {
    type master;
    file "db.3.168.192.in-addr.arpa";
};
// end for named.boot
```

`options`指令提供了一个单一入口，用于向`named`指定程序选项。在我们的示例中，指定的唯一选项是数据库目录`/var/named`。`zone`指令与`type master`结合使用，取代了 BIND 4 `named.boot`中的`primary`指令。虽然在这种情况下从 BIND 4 迁移到 BIND 8 相当直接和明显，但对于复杂的 BIND 4 DNS 安装，手工移植`named.boot`文件是非常困难的。有程序可以自动将 BIND 4 转换为 BIND 8，因此在进行重大 DNS 升级之前，一定要做好功课。

## DNS 从服务器

一旦你掌握了 DNS 主服务器的概念，创建 DNS 从服务器就几乎是轻而易举的事了。DNS 从服务器是主服务器的副本，用于在多台机器之间分配 DNS 负载，同时允许管理员只需在日常维护中管理主服务器。

### DNS 从服务器文件

要创建 DNS 从服务器，你只需要配置`/etc/named.boot`（或`named.conf`）文件，并拥有一份本地化的`db.cache`和`0.0.127.in-addr.arpa`文件副本。对于 BIND 4 的`named.boot`文件，从服务器与主服务器之间的唯一区别在于域映射被定义为`secondary`。

```named.boot
;
;
; BIND 4 named.boot
;
directory      /var/named

cache          .                     db.cache

;
; type          domain                source file
;
primary        0.0.127.in-addr.arpa  db.0.0.127.in-addr.arpa
;
; domain maps
;
secondary      sniglets.com          db.sniglets
secondary      3.168.192.in-addr.arpa  db.3.168.192.in-addr.arpa
; end for named.boot
```

将域映射定义为`secondary`会指示`named`为这些域执行区域传输。你会注意到`0.0.127.in-addr.arpa`文件仍被定义为主区域。由于`0.0.127.in-addr.arpa`文件从不改变，在每次重新加载其他文件时都重新加载它意义不大。因此，你需要确保安装一份`0.0.127.in-addr.arpa`文件的副本。

对于 BIND 8，`named.conf`文件中唯一的更改是将类型从`master`改为`slave`。除此之外，`named.conf`文件与主服务器上的`named.conf`文件完全相同。

```conf
// BIND 8 named.conf

//

options {
        directory "/var/named";
};

zone "." in {
        type hint;
        file "db.cache";
};

zone "0.0.127.in-addr.arpa" in {
        type master;
        file "db.0.0.127.in-addr.arpa";
};

zone "sniglets.com"      in {
        type slave;
        file "db.sniglets.com";
};

zone "3.168.192.in-addr.arpa" in {
        type slave;
        file "db.3.168.192.in-addr.arpa";
};
// end for named.boot
```

文件就位后，你可以像在主服务器上启动`named`一样的方式启动`named`进程。

### 更新从服务器的 DNS 信息

DNS 从服务器通过从 DNS 主服务器或对等 DNS 从服务器执行区域传输来获取其区域信息。域数据库会在给定数据库的`Refresh`指令定义的时间到期后重新加载。请注意你的`Refresh`值，因为较长的刷新间隔会导致新的 DNS 信息传播到主 DNS 服务器之外时产生延迟。

有些时候你可能不想等待 DNS 信息通过正常的区域传输机制传播。刷新 DNS 从服务器最简单的方法是删除复制的区域文件，然后重新启动`named`进程。`named`程序在启动时会自动为任何在定义的文件中不存在的区域文件发起区域传输。

![](img/415c89a1ede71e11e5040a0038b6916c_234_0.png)

`named`目录。如果文件存在，`named`会查看文件时间，计算刷新间隔，然后决定是否重新加载文件。删除适当的数据库文件将保证下载到文件的全新副本。

如果你选择使用此方法来重启你的 DNS 从服务器，你可能想要将`db.cache`和`db.0.0.127.in-addr.arpa`文件重命名为唯一名称。例如，你可以将缓存文件更改为`named.cache`，将`0.0.127.in-addr.arpa`文件更改为`named.loopback`。要使此更改生效，你只需修改你的`named.boot`或`named.conf`文件。现在，你要重启 DNS 从服务器所需要做的就是杀掉`named`进程，删除数据库文件，然后重启`named`，如图 6.6 所示。

## WINDOWS 2000 SERVER DNS
