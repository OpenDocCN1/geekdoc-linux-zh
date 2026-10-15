

MRTG 的部分是用 Perl 编写的，因此系统上也必须安装 Perl。建议使用 5.05 或更高版本。MRTG 正常运行还需要几个图形库，但它们的安装超出了本章的范围。请参考 doc/unix-guide.txt 文档（稍后会提到的 MRTG 源代码目录中）以了解确切要求。

## MRTG 安装

MRTG 应从 http://people.ee.ethz.ch/~oetiker/webtools/mrtg/pub/ 下载并放置在适当的目录中。在此示例中，使用 /usr/src。出版时 MRTG 的当前版本为 2.9.12，此处使用该版本。

下载 MRTG 包后，按以下步骤操作。

- 1. 以 root 身份登录并进入下载包的目录：
  `[root@lefty /root]# cd /usr/src`

- 2. 解压发行版：
  `[root@lefty src]# gunzip mrtg-2.9.12.tar.gz`

- 4. 解包 tarball：
  `tar xvf mrtg-2.9.12.tar`

- 5. 这将创建 MRTG 源代码树。进入源代码树：
  `[root@lefty src]# cd mrtg-2.9.12`

- 6. 执行 configure 脚本：
  `[root@lefty mrtg-2.9.12]# ./configure`

- 7. 执行 make 命令：
  `[root@lefty mrtg-2.9.12]# make`

- 8. 最后，执行 make install：
  `[root@lefty mrtg-2.9.12]# make install`

这将创建安装目录结构 /usr/local/mrtg-2/，并将所有二进制文件和适当的文件移动到该目录中。进入目录结构：
`[root@lefty mrtg-2.9.12]# cd /usr/local/mrtg-2/`

MRTG 需要一个可被 Web 服务器访问的目录。Linux 上 Apache Web 服务器的 HTML 文档常见目录位置为 /home/httpd/html/，因此 MRTG 文件可以放置在子目录中：
`[root@lefty mrtg-2]# mkdir /home/httpd/html/mrtg`

请确保根据 Web 服务器的配置使用适当的目录。还应为 MRTG 创建一个配置目录：
`[root@lefty mrtg-2]# mkdir cfg`

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_304_0.png)

图 15.3 MRTG Web 目录。

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_304_1.png)

图 15.4 MRTG 接口统计。

现在系统必须配置为定期运行 mrtg。使用 crontab 的 -e 选项使 mrtg 每五分钟运行一次：

```
[root@lefty mrtg-2]# crontab -e
```

并添加以下条目：

```
0,5,10,15,20,25,30,35,40,45,50,55 * * * * /usr/local/mrtg-2/bin/mrtg
/usr/local/mrtg-2/cfg/mrtg.cfg
```

可以使用以下命令将额外的路由器和节点添加到 mrtg.cfg 中：

```
[root@lefty mrtg-2]# bin/cfgmaker --global 'WorkDir: /home/http/html/mrtg' readaccess@192.168.1.254 >>/usr/local/mrtg-2/cfg/mrtg.cfg
```

如前所述，数据仍处于某种原始格式。MRTG 包含一个名为 indexmaker 的工具，可创建指向所有被监控节点的索引页面。要为此示例创建索引，使用以下命令：

```
[root@lefty mrtg-2]# bin/indexmaker /usr/local/mrtg-2/cfg/mrtg.cfg
> /home/http/html/mrtg/index.html
```

## index.html 文件的权限和所有权问题

index.html 文件的权限和所有权可能需要手动设置，以便 Web 服务器进程的所有者可以读取该文件。

这将创建 index.html，其中包含指向所有节点 via 图形摘要的 URL——如图 15.5 所示。

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_305_0.png)

图 15.5 带有索引页面的 MRTG。

使用 cfgmaker 添加新节点后，请确保再次运行 indexmaker。MRTG 配置好要监控的节点并有足够时间收集统计信息后，索引页面将类似于图 15.6。

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_306_0.png)

## IPTraf

IPTraf 是一种网络监控工具，侧重于实时监控网络流量。与 tcpdump 等嗅探器不同，IPTraf 报告的是 Linux 网络驱动程序所看到的流量的统计信息。与嗅探器一样，IPTraf 需要将接口置于混杂模式；因此，程序应以 root 用户身份运行。

IPTraf 的安装非常简单直接，包括解压、解包和运行设置脚本，因此此处不予介绍。

IPTraf 安装到 /usr/local/bin/ 目录，因此如果 /usr/local/bin/ 不在你的路径中，则需要执行完整文件名 /usr/local/bin/iptraf 来启动程序。

