
## 表 13.15 与缓存相关的 /etc/httpd.conf 指令。

| 指令 | 用途 | 值 |
| :--- | :--- | :--- |
| **CacheDefaultExpire** | 设置项在 Apache 缓存中保留的默认时间，超过该时间后项将过期。 | 小时数 |
| **CacheGcInterval** | 指定检查缓存的频率，以确保其大小不超过指定的限制。 | 小时数，包括以十进制格式表示的小数部分小时 |
| **CacheLastModifiedFactor** | 实现一个公式，根据上次更改的时间计算项应保持缓存的频率。 | 乘以上次更改时间的十进制因子 |
| **CacheMaxExpire** | 指定项在缓存中保留的最大时间，在此期间不需要检查其来源服务器是否有更新版本。 | 小时数 |
| **CacheRoot** | 指定存储 Apache 缓存的位置。 | 缓存路径 |
| **CacheSize** | 指定允许缓存增长的最大大小，超过此大小需要清理。 | 以 K 为单位的尺寸 |
| **NoCache** | 标识不需要缓存的特定项。 | 空格分隔的列表，包含不应包含在缓存中的主机、域名和项中的术语 |

最后，我们来到了虚拟主机部分。首先是：

```
#NameVirtualHost 12.34.56.78:80
#NameVirtualHost 12.34.56.78
```

**NameVirtualHost** 指令通常用于以下格式：

```
NameVirtualHost IPaddress:port
```

此指令用于指定哪些接口和端口包含虚拟 Web 服务器。设置完成后，继续执行以下操作：

```
#<VirtualHost ip.address.of.host.some-domain.com>
# ServerAdmin webmaster@host.some-domain.com
# DocumentRoot /www/docs/host.some_domain.com
# ServerName host.some_domain.com
# ErrorLog logs/host.some-domain.com-error_log
# CustomLog logs/host.some_domain.com-access_log common
#</VirtualHost>
```

`<VirtualHost>` 语句用于更清晰地定义主机及其行为。如果需要，你甚至可以在此语句内构建一长串指令。这里看到的是典型的最低配置。这里使用的元素都不是新的。最后：

```
#<VirtualHost default:*
#</VirtualHost>
```

如果你使用虚拟主机，建议取消注释此部分。这可以确保任何发往非虚拟主机地址的 HTTP 请求都被发送到主服务器。

# 其他 Linux Web 服务器

Apache 当然不是 Linux 下唯一的 Web 服务器。现有多种解决方案。有些是开源的，有些是专有的，还有一些拥有自己的许可证，你在决定使用之前应该熟悉这些许可证。有些替代方案是免费的，有些是商业的，或者具有商业功能。如果你不确定是否想要使用 Apache，想要调查其他选项，或者你需要 Apache 无法提供的功能，请参见表 13.16，了解可用选项的列表以及获取更多信息的地方。

**表 13.16 适用于 Linux 的 Web 服务器。**

| 名称 | 主页 |
| :--- | :--- |
| AOLserver | www.aolserver.com |
| EmWeb | www.agnanat.com/emweb/solutions/ |
| GoAhead Web Server | www.goahead.com/webserver/webserver.htm |
| Hawkeye | http://hawkeye.net |
| iServer | www.servertec.com/products/iws/iws.html |
| Java Web Server | http://java.sun.com |
| RapIdControl For Web | www.rapidlogic.com/products/rc_web.html |
| RomPAGER | www.allegrosoft.com/rproduct.html |
| Roxen | www.roxen.com/products/ |
| SpyGlass MicroServer | www.spyglass.com/solutions/technologies/microserver/ |
| vqServer | www.vqsoft.com |
| Xitami | www.xitami.com |
| Zeus Web Server | www.zeustech.net/products/zeus3/ |

还有一些“小 footprint”的 Web 服务器解决方案，这意味着它们占用的 RAM 很少。这些主要对网络设备开发者感兴趣，但你可能会发现它们在某些用途上也有用。

## 即时解决方案

### 安装 Apache

要在 Red Hat Linux 下安装 Apache Web 服务器，请执行以下操作：

- 1. 在你打算用作 Web 服务器的机器上以 root 身份登录。
- 2. 将 Red Hat CD-ROM 插入 CD-ROM 驱动器。
- 3. 输入 “mount /mnt/cdrom” 将 CD-ROM 添加到文件系统中。
- 4. 输入 “cd /mnt/cdrom/RedHat/RPMS” 切换到包目录。
- 5. 输入 “rpm -ivh apache-1\*” 并按 Tab 键补全文件名，然后按 Enter 键安装包。

### 配置 Apache

要配置你的 Apache Web 服务器，请执行以下操作：

- 1. 在你打算用作 Web 服务器的机器上以 root 身份登录。
- 2. 按照下一节“配置 Apache 访问”中的说明设置服务器访问信息。
- 3. 按照本章稍后“配置 **httpd**”一节中的说明设置服务器本身。
- 4. 按照本章稍后“配置 Web 浏览器看到的内容”一节中的说明，设置用户浏览你的 Web 目录时可以看到的内容。
- 5. 输入 “/etc/rc.d/init.d/httpd restart” 以重启 Apache。

> **注意：** 在非 Red Hat 发行版中，你可能需要使用不同的重启方法。

## 配置 Apache 访问

要进行初始访问配置，请执行以下操作：

- 1. 在你打算用作 Web 服务器的机器上以 root 身份登录。
- 2. 输入 "vi /etc/httpd/conf/httpd.conf"。

> **注意：** 如果你使用的是原始 Red Hat 6.1 发布或更早版本，你可能会发现这些信息位于文件 access.conf 中。

- 3. 输入 "<Directory>" 并按 Enter。你会跳转到这一行：

```
<Directory />
```

- 4. 输入 "/" 并再次按 Enter 以重复搜索。这会将你带到下一行：

```
<Directory /home/httpd/html>
```

- 5. 如果你不打算将 Web 页面存储在 /home/httpd/html 中，输入 “i” 进入插入模式，然后编辑目录以指向你打算用作 Web 服务器基础目录的位置。

- 6. 将光标向下移动到下一行：

```
Options Indexes Includes FollowSymLinks
```

- 7. 如果你想更改这些 **Options** 且当前不在插入模式下，输入 “i”。表 13.3 概述了这些功能的作用以及你可用的替代方案。

- 8. 将光标向下移动到下一行：

```
AllowOverride None
```

- 9. 如果你想更改允许的重写且当前不在插入模式下，输入 “i”。表 13.3 概述了 **None** 功能的替代方案。然而，请考虑你是否真的希望这些配置系列在你的整个 Web 层次结构中被其他人覆盖。

- 10. 如果你正在使用此服务器设置内联网，且你的互联网 Web 服务器在另一台机器上，将光标向下移动到下一行：

```
order allow,deny
```

然后，将其更改为 **order deny,allow** 或 **order mutual-failure**。

- 11. 如果你正在使用此服务器设置内联网，且你的互联网 Web 服务器在另一台机器上，将光标向下移动到下一行：

```
allow from all
```

然后，将其更改为反映谁应该拥有访问权限。例如，对于整个 C 类网络 192.168.22.0，你可能使用：

```
allow from 192.168.22.
```

- 12. 将光标向下移动到以下行：

```
<Directory /home/httpd/cgi-bin>
```

- 13. 如果你计划将此服务器使用的 CGI 保留在另一个位置，输入 “i” 进入插入模式，然后将 /home/httpd/cgi-bin 更改为新位置。

- 14. 如果你不打算允许任何人使用 CGI，请注释掉整个此部分，这意味着将其更改为如下所示：

```
#<Directory /home/httpd/cgi-bin>
#AllowOverride None
#Options ExecCGI
#</Directory>
```

我强烈建议保留此 **AllowOverride** 语句不变。除非你有特定原因，否则不要给予人们关于 CGIs 的自由。如果你想，可以更改 **Options** 语句，但在此处仍需谨慎。表 13.3 列出了替代方案。

- 15. 将光标向下移动到以下行：

```
#<Location /server-status>
```

- 16. 如果你想允许人们在任何给定时间查看服务器状态，通过移除前面的井号来取消注释此部分，使其看起来像这样：

```
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from .your_domain.com
</Location>
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_470_0.png)

