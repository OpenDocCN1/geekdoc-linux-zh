
再次注意哪里有尾点，哪里没有。在 `named.conf` 文件中省略尾点与在各个区域文件中正确指定尾点同样重要。配置文件中可以指定多种类型的区域，但由于我们希望成为指定域的权威名称服务器，因此我们希望成为 `master`。另一种可能是 `slave`，这种情况下我们充当备份权威名称服务器，但从另一个更权威的服务器获取主数据。最后，该块指定区域文件的名称，后面是可选的、有权更新此区域的主机列表（如果有的话）。

> 允许其他主机更新您的区域配置文件是危险的。最佳实践要求由一个人负责维护配置文件，并在更改时重启 `named`。

`named.conf` 文件中的最后一个条目是 `include` 语句，它使 `named` 将指定文件的内容包含进来，就像它是 `named.conf` 文件本身的一部分一样。为什么要这样做？为了让系统管理员能够将敏感数据隐藏在一个权限阻止未授权访问的单独文件中。在我们的示例中，`named` 加载了一个包含 `named` 管理工具 `rndc`（本学时稍后介绍）的密钥的文件。

### 4. 由于任何给定的域名都需要至少两个在线名称服务器，因此能够拥有 `slave` 区域定义块是一个福音。如果没有它，您将不得不手动将所有区域文件分发到多个系统，并且/或者每次所需更改都要编辑两个或多个文件。

在辅助或备份 DNS 服务器上，`named.conf` 文件中的示例 `slave` 条目如下所示：

```
zone "intuitive.com" IN {

  type slave;

  file "intuitive.com.zone";

  masters { 161.58.20.91; };

};
```

此区域块告诉 `named` 联系主机 `161.58.20.91` 获取区域配置信息，并将其存储在名为 `intuitive.com.zone` 的文件中。

`named.conf` 文件和存储在 `/var/named` 中的各个区域文件相结合，使系统管理员能够为少则两三个、多则数千个域名创建功能完备的域名服务器。

#### 使用 rndc

`named` 守护进程只在启动时读取其配置文件，这意味着每次修改区域文件或 `named.conf` 文件时，您都应该重启服务器。然而，与其每次更改后都启动和停止，不如使用远程名称守护进程控制（`rndc`）程序。

##### 任务 18.3：了解 rndc

`rndc` 可以完成多种有用的管理任务，但让我们先考虑几个最基本的——如果您好奇或需要更多功能，可以阅读 `rndc` 手册页获取更多信息。

1. 最常见的操作是强制重新加载配置文件。这可以通过 `reload` 命令完成：

```
# rndc reload

#
```

如果您有很多区域文件并希望在重新加载时节省时间，请明确指定 `reconfig`，`named` 将只扫描 `named.conf` 文件以及它找到的任何新区域文件。同样，除非遇到错误，否则没有输出：

```
# rndc reconfig

#
```

2. 您可能会发现其他常用的 `rndc` 选项列在表 18.2 中。

**表 18.2：有用的 rndc 命令**

| 命令 | 含义 |
|---|---|
| `reconfig` | 重新加载 `named.conf` 文件以及找到的任何新区域文件。 |
| `reload` | 重新加载所有区域文件。 |
| `reload zone` | 仅重新加载给定的区域。 |
| `stop` | 停止服务器，保存对更新区域主文件的任何更改。 |
| `halt` | 立即停止服务器。不保存任何更改，但在服务器重启时将从日志文件回放，因此不会丢失。 |

`rndc` 仅用于 BIND 9 版本，并且包含了旧版 BIND 中 `named` 守护进程控制程序 `ndc` 所提供的大部分命令。

3. `rndc` 命令有自己的配置文件 `/etc/rndc.conf`。默认配置可能就足够了，尤其是因为 `named.conf` 中的 `controls` 语句使您能够声明允许谁使用 `rndc` 向 `named` 发送命令。

```
# cat /etc/rndc.conf

options {

    default-server localhost;

    default-key "key";

};

server localhost {

    key "rndc key";

};

key "rndc key" {

    algorithm hmac-md5;

    secret "kOsYAWlyZNCpVLYoJkdnKVkqgYJsbNctR0GyYXklQehDcurizoHtQbFhQnp";

};
```

4. 在完成 `rndc` 操作之前，运行 `named-checkzone` 工具来验证每个区域文件的语法会很有帮助。要使用此工具，请指定区域名称和区域文件：

```
# /usr/sbin/named-checkzone intuitive.com /var/named/intuitive.com.zone
```

你还可以将其放入循环中，如下所示：

```
cd /var/named

for name in *

do

  domain=`echo $name | sed 's/\.zone//'`

  echo "Domain $domain:"

  /etc/named-checkzone $domain /var/named/$name

done
```

虽然只是一个简单的工具，但 `rndc` 命令对于有效管理 `named` 和本地名称服务器至关重要。

#### 测试 DNS 配置

现在你的配置和区域文件都已就绪，是时候进行测试并确保一切正常了。

在过去，有一个名为 `nslookup` 的出色工具，为与名称服务器交互提供了一种简单的方式。最近几年，`nslookup` 已被淘汰，取而代之的是两个新工具：`dig` 和 `host`。

##### 任务 18.4：使用 dig 和 host 进行测试

在这两个工具中，你无疑会发现 `dig`（域名信息检索器）最为有用，但让我们同时看看这两者，了解它们能提供哪些功能。

- 1. 在基本形式下，`dig` 只需要一个域名即可获取信息：

```
# dig intuitive.com

; <<>> DiG 9.1.3 <<>> intuitive.com

;; global options: printcmd

;; Got answer:

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51083

;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 1

;; QUESTION SECTION:

;intuitive.com.             IN      A

;; ANSWER SECTION:

intuitive.com.      28067   IN      A       161.58.20.91

;; AUTHORITY SECTION:

intuitive.com.      79973   IN      NS      ns11a.verio-web.com.

intuitive.com.      79973   IN      NS      ns11b.verio-web.com.

;; ADDITIONAL SECTION:

ns11b.verio-web.com. 149498 IN      A       161.58.148.98

;; Query time: 5 msec

;; SERVER: 192.168.1.250#53(192.168.1.250)

;; WHEN: Fri Apr 12 01:23:58 2002

;; MSG SIZE  rcvd: 113
```
