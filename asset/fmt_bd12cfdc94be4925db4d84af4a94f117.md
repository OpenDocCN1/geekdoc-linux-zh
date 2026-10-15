
# 128.32.0.0 255.255.255.0

198.76.82.128 255.255.255.128

正如你所见，这个目录中有大量有用的解释性信息。

![](img/5ced0c78d748bd190e9027e5549a3622_353_0.png)

![](img/5ced0c78d748bd190e9027e5549a3622_354_0.png)

> 值得指出的是，正如注释中所说，至少到版本 8 为止，Solaris 不支持无类域间路由。这意味着，如果你拥有一个 C 类 IP 范围的非连续子集，Solaris 在联网时只能将其视为一个完整的 C 类地址。根据你的网络拓扑，这可能会成为一个显著的限制。

与 `/etc/hosts` 对应的是 `/etc/inet/hosts`：

```
# cat /etc/hosts

#

# Internet host table

#

127.0.0.1       localhost

198.76.82.131   laptop

198.76.82.132   mac

198.76.82.150   win2k

198.76.82.155   solaris loghost solaris.dsldesigns.net
# cat /etc/hosts

#

# Internet host table

#

127.0.0.1       localhost

198.76.82.131   laptop

198.76.82.132   mac

198.76.82.150   win2k

198.76.82.155   solaris loghost solaris.dsldesigns.net
```

事实证明，`/etc/hosts` 是 `/etc/inet/hosts` 的符号链接，所以它们总是保持同步是有很合理的原因的！不过还有第三个需要检查的 hosts 文件——新的 ipnodes：

```
# cat ipnodes

#

# Internet host table

#

::1             localhost

127.0.0.1       localhost

198.76.82.131   laptop

198.76.82.132   mac

198.76.82.150   win2k

198.76.82.155   solaris loghost solaris.dsldesigns.net
```

同样，系统也会尽量让它们保持同步（不过请注意，`ipnodes` 中第一个未注释掉的行是新的：`::1`）。

### 3. IP 地址存储位置

如果你一直在跟踪进度，我们已经弄清楚了几乎所有信息片段该放在哪里，只剩下我们的 IP 地址。它存储在哪里？事实证明，它被放进了 `/etc/hosts` 文件。所以让我们回过头来更好地理解这些文件之间的关系：完全限定主机名在哪个文件中指定（正式名称是 nodename 文件），以及 `hosts` 文件中出现的匹配值：

```
# cat /etc/nodename

solaris.dsldesigns.net

# grep solaris /etc/nodename /etc/inet/hosts

198.76.82.155 solaris loghost solaris.dsldesigns.net
```

因此，要更改这个特定系统的 IP 地址，我们只需更改 `hosts` 文件中的地址，并确保其中任何主机名的改动也与 `nodename` 文件中指定的名称完全一致。

我们可以通过调用 `ifconfig` 程序来检查 IP 地址（稍后在本小时中我们将谈到它）：

```
# /sbin/ifconfig pcn0

pcn0: flags=1000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2

inet 198.76.82.155 netmask ffffff80 broadcast 198.76.82.255

ether 0:50:56:54:45:9d
```

要特别注意第二行中的 `inet` 值，以确认该主机的 IP 地址。

### 4. 切换到 DHCP

要从固定 IP 方案切换到 DHCP 连接方案，我们需要深入探究 `dhcagent` 的世界，它是 Solaris 默认的 DHCP 客户端软件。令人高兴的是，Solaris 附带了一堆与 DHCP 相关的命令：

```
# man -k dhcp | grep 1

dhcpagent dhcpagent (1m) · Dynamic Host Configuration Protocol (DHCP) client daemon

dhcpconfig dhcpconfig (1m) · DHCP service configuration utility

dhcpinfo dhcpinfo (1) · display values of parameters received

→through DHCP

dhcpmgr dhcpmgr (1m) · graphical interface for managing DHCP service

dhtadm dhtadm (1m) · DHCP configuration table management utility

in.dhcpd in.dhcpd (1m) · Dynamic Host Configuration Protocol server

pntadm pntadm (1m) · DHCP network table management utility
```

具体的配置文件以需要 DHCP 连接的接口命名——在本例中为 `/etc/dhcp/pcn0`。但等等，有个好消息！删除几个固定 IP 文件的内容，再创建一堆空的与 DHCP 相关的文件，系统就会在下次开机时自动创建配置文件以及所需的任何其他 DHCP 文件。非常有帮助。下面就是在下次启动时从固定 IP 切换到 DHCP 配置所需的确切操作：

```
# alias zero='cat /dev/null > *'

# zero /etc/hostname.pcn0

# zero /etc/dhcp/pcn0

# zero /etc/notrouter
```

```
# zero /etc/defaultrouter

# zero /etc/default/dhcp

# zero /etc/resolv.conf
```

就是这样了。已存在并被清零的文件，其内容已被擦除；原本不存在的文件现在也存在了（特别是 `/etc/dhcp.pc0`）。

唯一剩下的步骤是把 `/etc/inet/hosts` 文件中的几乎全部内容删除，只保留一行 `localhost`，别无其他。它应该像这样：

```
# cat /etc/inet/hosts

127.0.0.1 localhost
```

与该主机相关的其他行会在启动时由 DHCP 客户端分配 IP 时自动填入。

> 如果你想了解如何将 Solaris 系统设置为 DHCP 服务器，最好的做法是从 Internet Software Consortium 网站（www.isc.org）下载与 Solaris 兼容的 `dhcpd`，并按照他们清晰、连贯的说明进行操作。

### 5. Mac OS X 网络配置

在结束 Unix 系统网络连接配置这个话题之前，让我们把注意力转向 Mac OS X。在基于命令行的网络配置方面，Mac 算是相当另类的一种生物。

坦白说，如果你够理性，最好的方式就是直接使用 Mac OS X 的“系统偏好设置”网络面板，如图 17.1 所示。

**图 17.1** “系统偏好设置”中的网络面板。

![](img/5ced0c78d748bd190e9027e5549a3622_356_0.png)

但如果我们总是循规蹈矩，用这种简单又聪明的办法解决问题，生活该多无趣啊。

相反，让我们深入探索一下 Mac OS X，看看这个控制面板中的信息到底保存在哪里：如果能够找到那个具体的存档文件，我们就可以手工修改它，对吧？可以说是，也可以说不是。

### 6. 配置文件位置

存储这些配置值的文件属于 Mac OS X 的系统配置区域，位于 `/var/db` 下：

```
# head -20 /var/db/SystemConfiguration/preferences.xml

<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE plist SYSTEM

"file://localhost/System/Library/DTDs/PropertyList.dtd">

<plist version="1.0">

<dict>

<key>CurrentSet</key>

<string>Sets/0</string>

<key>NetworkServices</key>

<dict>

<dict>

<key>0</key>

<dict>

<key>AppleTalk</key>

<dict>

<key>ConfigMethod</key>
