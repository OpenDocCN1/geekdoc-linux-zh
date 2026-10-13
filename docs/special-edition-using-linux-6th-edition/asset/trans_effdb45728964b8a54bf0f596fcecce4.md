
配置你的服务器拥有多个 IP 地址有几种不同的方法。如果你有多块网卡（例如两块以太网卡），每块网卡都有自己的 IP 地址。你也可以利用 Linux 的一项称为 IP 别名的功能，将多个 IP 地址分配给同一块网卡。在本节的其余部分，我们假定你已经设置并测试了计划用于 Web 站点的 IP 地址。

若要配置 Web 服务器监听多个地址，并对每个地址做出不同的响应，可以使用 `<VirtualHost>` 指令。你可以在某个服务器配置文件中使用 `<VirtualHost>` 指令来声明一个区段（很像 `<Directory>` 区段）。在 `<VirtualHost>` 指令本身中，你需要指定一个要匹配的地址。在虚拟主机区段内部，你可以指定当客户端使用该地址访问服务器时应采用的设置。对于使用其他地址访问服务器的客户端，则使用主服务器设置（任何 `<VirtualHost>` 区段之外的设置）。

对于一个具有地址 192.168.1.1 和 192.168.1.2 的机器，一个简单的虚拟主机设置如清单 33.4 所示。

**清单 33.4 IP 型虚拟主机的一个简单示例**

```apache
...
BindAddress *
Port 80
DocumentRoot /usr/local/apache/htdocs
ServerName site1.example.com

<VirtualHost 192.168.1.2>
DocumentRoot /usr/local/apache/htdocs2
ServerName site2.example.com
...
</VirtualHost>
```

在这个示例中，服务器绑定到地址 0.0.0.0:80（因为使用了 `BindAddress *` 和 `Port 80` 指令）。这意味着它接收机器上所有 IP 地址的 80 端口 TCP 请求。当服务器收到请求时，它会确定该请求是在哪个地址上接收的。如果地址是 192.168.1.1，服务器则从 /usr/local/apache/htdocs 下的文档树中取出文档进行响应。否则（当请求是在地址 192.168.1.2 上收到时），服务器则从 /usr/local/apache/htdocs2 中取出文档进行响应。在此示例中，客户端分别通过 http://site1.example.com/ 和 http://site2.example.com/ 访问这两个不同的 Web 站点。

在 `<VirtualHost>` 区段内部，你可以放置各种指令，以控制与你正在定义的特定站点相关的服务器各方面设置。这包括用于以下目的的指令：

-   定义文档命名空间。
-   控制文档和脚本处理。
-   定义目录索引选项。
-   设置日志文件选项。
-   执行访问和授权控制。

例如，若要为 htdocs2 定义逐目录选项，你可以添加一个 `<Directory>` 区段，嵌套在清单 33.4 示例中所示的 `<VirtualHost>` 区段内部。

对于你定义的每个虚拟主机，你至少需要定义一个新的 DocumentRoot。你还需要使用适当的日志指令，设置特定于该站点的传输日志和错误日志。对于你定义的每个 Web 站点（即在每个虚拟主机区段内部），你可以自行决定还要进行哪些其他定制。

你在 `<VirtualHost>` 指令本身中指定虚拟主机的 IP 地址。该地址可以包含端口号，端口号与 IP 地址之间用冒号分隔。服务器必须监听你指定的地址。在某些复杂的情况下，你可能需要结合使用 `BindAddress`、`Port` 和 `Listen` 指令，告诉服务器监听特定的地址和端口组合。`BindAddress` 和 `Port` 的用法已在本章前面讨论过。`Listen` 指令允许对 Web 服务器使用的地址进行更精确的控制。清单 33.5 中的示例使用 `Listen` 指令指定了三个要监听的独立地址，并随后将其映射到虚拟主机。

**清单 33.5 使用复杂寻址的 IP 型虚拟主机示例**

```apache
Listen 192.168.1.1:80
Listen 192.168.1.1:8080
Listen 192.168.1.2:80

<VirtualHost 192.168.1.1:80>
...
</VirtualHost>
<VirtualHost 192.168.1.1:8080>
...
</VirtualHost>
<VirtualHost 192.168.1.2:80>
...
</VirtualHost>
```

默认情况下，客户端对机器上任何未被虚拟主机指令匹配的地址进行访问时，都会使用任何虚拟主机语句之外的指令来处理。为了使各个站点的定义更加一致，你可以在 `<VirtualHost>` 指令中使用 `_default_` 关键字来代替 IP 地址，并将替代 Web 站点访问的设置放在该虚拟主机区段内。这在复杂的虚拟主机配置中可能很重要。例如，当只使用两个 IP 地址时，清单 33.6 实现了与清单 33.4 相同的效果。

**清单 33.6 在虚拟主机中使用 \_default\_**

```apache
...
BindAddress *
Port 80

<VirtualHost 192.168.1.2>
DocumentRoot /home/httpd/site2
ServerName site2.com
...
</VirtualHost>

<VirtualHost _default_:*>
DocumentRoot /home/httpd/html
ServerName site1.com
...
</VirtualHost>
```

## 使用多个 DNS 名称运行单个服务器

如果你的机器上可以配置多个 IP 地址，那么 IP 型虚拟主机是不错的选择。但是，如果你托管许多站点，可能无法获得所需的所有地址。此外，你的机器可能已经为单个 IP 地址分配了多个名称。在这些情况下，你需要使用基于名称的虚拟主机。

基于名称的虚拟主机原理与基于 IP 的虚拟主机基本相同。不过，在这种情况下，服务器还会使用客户端请求中的主机名来确定请求应使用哪个虚拟主机。基于名称的虚拟主机可以用于单个 IP 地址，也可以用于多个 IP 地址。

要进行这种设置，请使用 `NameVirtualHost` 指令指明哪些地址用于基于名称的虚拟主机。然后，在针对该地址的 `<VirtualHost>` 区段内部，使用 `ServerName` 和 `ServerAlias` 指令指定要匹配的一个名称（或一组名称）。当服务器尝试将传入请求与虚拟主机区段匹配时，它会检查客户端发送的主机名，并将其与这些名称进行比对。清单 33.7 显示了一个基于名称的虚拟主机示例。此示例显示服务器在地址 192.168.1.1 上支持两个站点名称。

**清单 33.7 基于名称的虚拟主机示例**

```apache
Listen 192.168.1.1:80
NameVirtualHost 192.168.1.1:80

<VirtualHost 192.168.1.1:80>
DocumentRoot /home/httpd/html
ServerName www.example.com
ServerAlias www www.example.com
</VirtualHost>

<VirtualHost 192.168.1.1:80>
DocumentRoot /usr/local/apache/htdocs2
ServerName www2.example.com
</VirtualHost>
```

请注意第一个虚拟主机定义中 `ServerAlias` 指令的使用。如果客户端请求包含名称 www.example.com 或仅包含 www，则使用第一个主机定义。`ServerAlias` 的用途在于，结合基于名称的托管，允许本地网络上的客户端使用简短别名，而不是完全限定的域名。

## 在同一台机器上运行多个 Web 服务器

在一台机器上运行多个 Web 站点的另一种方法是加载该 Web 服务器的多个实例。你不需要使用 `<VirtualHost>` 指令，而是为每个服务器配置一组自己的配置文件，并确保这些服务器互不干扰。

### 为每个服务器创建一组配置文件

在这种设置中，每个服务器都需要自己的启动文件和配置文件。对于 Red Hat、OpenLinux 及类似发行版，启动文件是初始化脚本 `/etc/rc.d/init.d/httpd`（对于 Debian 则为 `/etc/init.d/httpd`）。可以编辑此文件，在系统启动时运行该脚本时，为服务器添加第二个及后续的调用行。为此，请复制该文件 case 语句中 `start` 和 `stop` 部分内的命令，并对其进行编辑，以反映你想要启动的其他服务器。有关初始化脚本的更多信息，请参见第 13 章“系统初始化”。

调整配置文件的指令已在本章前面讨论过。基本上，你需要使用 `ServerRoot`、`ResourceConfig`、`AccessConfig`、`TypeConfig` 和 `MimeMagicFile` 指令，为每个服务器配置一组自己的配置文件。请注意，你可能希望共享 MIME 类型文件。如果你创建了一个新的配置目录，可以考虑使用文件系统链接，以便在两个目录之间共享 `mime.types` 和 `magic` 文件。

每个服务器实例特有的其他设置需要放在该服务器相应的配置文件中。

### 将每个服务器绑定到自己的地址或端口

为了使服务器运行时不互相干扰，它们需要使用不同的地址，或者至少使用不同的端口。在每个服务器的 `httpd.conf` 中使用 `BindAddress`、`Port` 和 `Listen` 指令，以建立该服务器使用的 IP 地址和 TCP 端口。

### 其他每实例配置变量

对于服务器的后续实例，你必须更改一些其他配置变量，以便不同的服务器进程互不干扰。这些变量包括 `ScoreBoardFile`、`LockFile` 和 `PidFile` 指令设置的值，以及日志文件位置（由 `TransferLog`、`ErrorLog`、`CustomLog` 等设置）。

## 动态共享对象（DSO）

Apache 的许多功能是通过 *模块* 提供的。模块是一段代码，它可以成为系统的一部分，也可以不成为系统的一部分，它提供特定的功能。例如，`mod_perl` 提供了一种快速加载 Perl 脚本的方式，而 `mod_mime_magic` 则允许 Apache 根据文件内容来确定文件类型。

