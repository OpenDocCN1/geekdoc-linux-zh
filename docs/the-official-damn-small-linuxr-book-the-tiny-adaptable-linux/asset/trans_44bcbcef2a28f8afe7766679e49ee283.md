

回想一下FreeDOS中用于输入文件名的Tab键快捷方式。如果你正在使用Windows，并且已经熟悉unzip，那么你只需再解压两个DSL系统文件到C:\即可。

在将DOS启动文件复制到C:\驱动器之前，我们先测试一下你的设置。如果你不需要任何额外的启动选项，在启动的FreeDOS A:提示符下输入

```
A:\> bootdsl
```

如果需要额外的启动参数，应将其添加到文件linld.c1中。你可以使用DOS的type命令查看该文件的内容。DOS软盘上也提供了vi编辑器，可以根据需要编辑此文件以添加或更改启动选项。

测试完通过bootdsl批处理文件启动后，你现在就可以复制通过原生DOS模式启动DSL所需的DOS文件了。在仍然从DSL FreeDOS工具软盘启动的情况下，执行以下操作：

```
A:\> copy a:\bin\linld.com c:\
A:\> copy a:\linld.c1 c:\
A:\> copy a:\bootdsl.bat c\
```

现在，将你的DOS或Windows计算机重启到原生DOS模式。对于Windows 9x，通常意味着按住F8键。启动到原生DOS后，在DOS启动提示符下输入bootdsl即可启动DSL。

恭喜！你现在已经使用linld DOS引导加载程序完成了DSL的Frugal DOS安装。接下来，你应该选择一个备份设备（参见第4章“配置和保存DSL设置”）；要开始使用MyDSL扩展，请参见第5章“使用MyDSL扩展应用程序”。

## 使用LoadLin从原生DOS模式引导DSL

另一种流行的原生DOS模式Linux引导加载程序是loadlin.exe，版本1.6c，作者为Hans Lermen。这是一个DOS EXE程序，而不是COM程序。更多信息请访问其网站：

```
http://elsrv.ffm.fgan.de/~lermen/
```

这个DOS引导加载程序使用一个简单的DOS文本文件来存储启动选项。因此，和linld.com一样，继续你现有的Poorman安装。你已经有位于c:\KNOPPIX\KNOPPIX的KNOPPIX文件，下载的DSL.Zip文件也在c:\上。你已经能够从DSL启动软盘启动，并且知道了你的额外启动选项（如果需要的话）。

让我们从DSL FreeDOS工具软盘启动，如果你还没有解压，请解压另外两个DSL系统文件：

```
A:\> C:
C:\> unzip dsl-33~1.zip linux24
C:\> unzip dsl-33~1.zip minirt24.gz
```

在C驱动器上设置任何loadlin DOS文件之前，你应该先尝试通过loadlin引导DSL来测试：

```
A:\> loadlin @options.txt
```

如果需要额外的启动选项，应将其添加到options.txt文件中，并重新启动，直到你满意loadlin能够正常工作。接下来，将loadlin DOS文件复制到你的C:驱动器：

```
C:\> copy a:\bin\loadlin.exe c:\
C:\> copy a:\options.txt c:\
```

将DOS或Windows计算机重启到原生DOS模式。Windows 98通常需要按住F8键。启动到DOS提示符后，输入loadlin @options.txt来引导DSL。

恭喜！你现在已经完成了DSL的Frugal DOS Loadlin安装。接下来，你应该选择一个备份设备（关于备份数据的信息，请参见第4章）；要开始使用MyDSL扩展，请参见第5章。

## 重新审视POORMAN安装

为什么重新讨论这个主题？对某些人来说，真正的挑战可能是如何将KNOPPIX/KNOPPIX文件放到他们系统的硬盘上。毕竟，没有那个关键文件，你两种方法都无法使用。以下是将KNOPPIX/KNOPPIX文件获取到硬盘上的几种方法。

## 使用另一台机器

你实际上可以拆下目标计算机的硬盘，临时将其安装到另一台具有可启动CD-ROM或网络访问权限的计算机中。安装DSL。由于DSL使用KNOPPIX的硬件检测，将硬盘装回目标计算机后，开机时会检测到新的环境。你可能需要根据这台机器调整启动选项。拆卸硬盘，尤其是笔记本电脑的硬盘，可能不是一件容易或理想的任务。请继续阅读其他克服这一任务的方法。

## 通过PCMCIA实现Poorman’s DSL

许多笔记本电脑都有PCMCIA插槽。有些可能有PCMCIA硬盘。此外，还有PCMCIA CompactFlash适配器。有了这种易于移除的设备，你可以将此PCMCIA插入一台功能更强的计算机（可启动CD-ROM或网络访问），并将KNOPPIX/KNOPPIX复制到PCMCIA的内存中。

要在目标计算机上从PCMCIA启动，你需要准备第二张DSL启动软盘。PCMCIA模块软盘，即图8-1中DSL安装选项中的菜单选项11，可以创建该软盘。因此，再次使用功能更强的计算机创建此软盘，或者直接下载并使用rawrite创建它。

回到目标计算机，插入PCMCIA卡，并使用以下命令从DSL启动软盘启动：

```
boot: dsl frompcmcia
```

在启动过程中，系统会提示你插入PCMCIA模块软盘。和往常一样，你可能会发现需要额外的启动选项。关于可能需要使计算机硬件启动DSL的启动选项示例，请参见第2章。

## 通过USB驱动器实现Poorman’s DSL

这是什么？USB在第6章中已讨论过，而你的机器无法从USB启动。但是你看，使用一台功能更强的机器来创建闪存盘，如第6章所述，你可以使用DSL标准启动软盘这样引导DSL Poorman’s：

```
boot: dsl fromusb
```

## 通过Zip驱动器实现Poorman’s DSL

你们中的一些人可能仍然拥有Iomega zip驱动器。因为这也是一种可移动设备，你可以将KNOPPIX/KNOPPIX文件复制到zip驱动器上。然后，使用DSL标准启动软盘，用以下命令启动：

```
boot: dsl fromzip
```

## 从一叠软盘安装

如果你有一台非常老的PC，你可能没有PCMCIA接口，没有USB端口，当然也没有zip驱动器。那么，你肯定有一个软盘驱动器！

