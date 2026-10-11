

- 版本：[3]
- 驱动程序名称：[Canon iR8500 PS3]
- 架构：[Windows NT x86]
- 驱动程序路径：[\\10.160.50.8\print$\W32X86\3\cns3g.dll]
- 数据文件：[\\10.160.50.8\print$\W32X86\3\iR8500sg.xpd]
- 配置文件：[\\10.160.50.8\print$\W32X86\3\cns3gdu.dll]
- 帮助文件：[\\10.160.50.8\print$\W32X86\3\cns3gh.hlp]

- 依赖项：[\\10.160.50.8\print$\W32X86\3\auclpmnt.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\uues32p.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\tnl32.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\ausvdriv.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cnspdc.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\aussapi.dat]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cns3407.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cns3gg.hlp]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cns3sp1.cnt]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\MBAPI.DLL]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\WBIFPC.DLL]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpccview.exe]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpccspl.exe]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpccspl.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpcsp1.exe]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\ccspl.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cfinc32.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpcq407.dll]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpcqm407.hlp]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cpcqm407.cnt]
- 依赖项：[\\10.160.50.8\print$\W32X86\3\cns3ggr.dll]

- 监视器名称：[]
- 默认数据类型：[]

## 打印机驱动程序信息 3：

- 版本：[2]
- 驱动程序名称：[Canon iR5000-6000 PS3]
- 架构：[Windows NT x86]
- 驱动程序路径：[\\10.160.50.8\print$\W32X86\2\cns3g.dll]
- 数据文件：[\\10.160.50.8\print$\W32X86\2\iR5000og.xpd]
- 配置文件：[\\10.160.50.8\print$\W32X86\2\cns3gdu.dll]
- 帮助文件：[\\10.160.50.8\print$\W32X86\2\cns3gh.hlp]

- 依赖文件：[\\10.160.50.8\print$\W32X86\2\AUCLPMNT.DLL]
- 依赖文件：[\\10.160.50.8\print$\W32X86\2\ausdrv.dll]
- 依赖文件：[\\10.160.50.8\print$\W32X86\2\cnsmdp.dll]
- 依赖文件：[\\10.160.50.8\print$\W32X86\2\aussapi.dat]
- 依赖文件：[\\10.160.50.8\print$\W32X86\2\cns3407.dll]
- 依赖文件：[\\10.160.50.8\print$\W32X86\2\cns3gg.cnt]
- 依赖文件：[\\10.160.50.8\print$\W32X86\WBAPI.DLL]
- 依赖文件：[\\10.160.50.8\print$\W32X86\NBIPC.DLL]
- 依赖文件：[\\10.160.50.8\print$\W32X86\cns3gum.dll]

- 监视器名称：[CPCA 语言监视器2]
- 默认数据类型：[]

如果我们分别将“版本 2”和“版本 3”的文件写入不同的文本文件并进行比较，会得到如下结果：

```
root# sdiff 2-files 3-files
```

```
cns3g.dll                             cns3g.dll
iR8500sg.xpd                        iR8500sg.xpd
cns3gui.dll                         cns3gui.dll
cns3g.hlp                           cns3g.hlp
AUCPLMNT.DLL                        | aucplmNT.dll
> ucs32p.dll
> tn132.dll

aussdrv.dll                         aussdrv.dll
cnspdc.dll                          cnspdc.dll
aussapi.dat                         aussapi.dat
cns3407.dll                         cns3407.dll
CnS3G.cnt                           CnS3G.cnt
NBAPI.DLL                           NBAPI.DLL
NBIPC.DLL                           NBIPC.DLL
cns3gum.dll                         | cpcview.exe
> cpcdsp1.exe
> cpcqm.exe
> cpcspl1.dll
> cfine32.dll
> cpcr407.dll
> Cpcqm407.hlp
> cpcqm407.cnt
> cns3ggr.dll
```

不要被骗了！虽然不同版本的驱动程序中同名文件可能存在，但其内容可能不同，如下面的大小比较所示：

```
root# for i in cns3g.hlp cns3gui.dll cns3g.dll; do
    smbclient \\/10.160.50.8/print/$ -U 'Administrator/\'x\'xxxx\'' \
        -c "cd W32X86/3; dir $i; cd .. ; cd 2; dir $i"; \
done
```

| 文件名 | 属性 | 大小 | 日期 |
| :--- | :--- | :--- | :--- |
| CNS3G.HLP | A | 122981 | 2002年5月30日 星期四 02:31:00 |
| CNS3G.HLP | A | 99948 | 2002年5月30日 星期四 02:31:00 |
| CNS3G0U.DLL | A | 1805824 | 2002年5月30日 星期四 02:31:00 |
| CNS3G0U.DLL | A | 1785344 | 2002年5月30日 星期四 02:31:00 |
| CNS3G.DLL | A | 1145088 | 2002年5月30日 星期四 02:31:00 |
| CNS3G.DLL | A | 15872 | 2002年5月30日 星期四 02:31:00 |

在我们的示例中，差异甚至比这里展示的要多。结论：您必须仔细选择每个驱动程序版本的正确文件。不要仅依赖文件名，也不要互换属于不同驱动程序版本的文件。

## 20.8.6 Samba 和打印机端口

Windows NT/2000 打印服务器会为每个打印机关联一个端口。这些端口通常采用 `LPT1:`、`COM1:`、`FILE:` 等形式。Samba 也必须支持与打印机关联端口的概念。默认情况下，系统中只存在一个名为“Samba 打印机端口”的打印机端口。Samba 实际上并不需要这样的“端口”来进行打印；相反，这是 Windows 客户端的要求。当它们请求获取此信息时，它们坚持被告知有一个可用的端口；否则，它们会抛出错误消息。因此，Samba 伪造端口信息以使 Windows 客户端满意。

Samba 内部也不支持**打印机池化**的概念。打印机池化将逻辑打印机分配给多个端口，作为负载均衡或故障转移的一种形式。

如果您出于某种原因需要定义多个端口（我的用户和老板不应该知道他们在与 Samba 交互），请配置 `enumports` 命令，该命令可用于定义一个生成系统端口列表的外部程序。

## 20.8.7 避免常见的客户端驱动程序配置错误

现在打印功能可以工作了，但仍存在问题。大多数作业打印正常，有些完全无法打印。有些作业的字体有问题，显示效果不佳。有些作业打印速度快，有些则慢如蜗牛。我们无法涵盖所有情况，但我们希望鼓励您阅读第 21 章“CUPS 打印支持”中第 21.10.16 节关于“避免错误的 PostScript 驱动程序设置”的简短段落。

# 20.9 Imprints 工具集

Imprints 工具集提供了 Windows NT APW 的 UNIX 等价物。如需完整信息，请参阅 Imprints 的网站以及 Imprints 源代码发行版中包含的文档。本节仅简要介绍 Imprints 的功能。

不幸的是，Imprints 工具集不再被维护。截至 2000 年 12 月，该项目需要新的维护者。最重要的技能是 Perl 编程以及对其在 Samba 中使用的基于 MS-RPC 的打印技术感兴趣。如果您愿意自愿参与，请在 Samba 技术邮件列表中协调您的工作。该工具集仍然可用，但仅适用于一系列拥有预制备包的旧打印机型号。如果 Imprints 想要有未来，则需要为较新的打印设备提供软件包。有关 Imprints 工具集的信息可从 Imprints 主页获取。

### 20.9.1 什么是 Imprints？

Imprints 是一组支持以下目标的工具：

- 提供有关 Windows NT 和 95/98 打印机驱动程序包的中央信息库。
- 提供创建 Imprints 打印机驱动程序包所需的工具。
- 提供一个安装客户端，该客户端可从中央互联网（或内网）Imprints 服务器库获取打印机驱动程序，并在远程 Samba 和 Windows NT/4 打印服务器上安装它们。

### 20.9.2 创建打印机驱动程序包

创建打印机驱动程序包的过程超出了本文档的范围（有关更多信息，请参阅 Samba 发行版中包含的 Imprints.txt）。简而言之，Imprints 驱动程序包是一个压缩的 tar 包，包含驱动程序文件、相关的 INF 文件以及安装客户端所需的控制文件。

### 20.9.3 Imprints 服务器

Imprints 服务器实际上是一个数据库服务器，可以通过标准 HTTP 机制进行查询。数据库中的每个打印机条目都有一个关联的 URL，用于实际下载该包。每个包都通过 GnuPG 进行数字签名，这可用于验证下载的包确实是 Imprints 数据库中引用的那个。强烈建议不要禁用此安全检查。

