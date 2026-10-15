

使用运行 Samba 的 Linux 计算机可以成为在 DOS、Windows 或 OS/2 计算机网络上共享打印机的绝佳方式。如第 14 章“准备共享打印机”所述，您可以“原始”共享打印机，使用您所使用的特定型号的 Windows 驱动程序，或使用 Ghostscript 使打印机对 Windows 看起来像一台 PostScript 打印机。当然，如果打印机内置了 PostScript，这两种选项在实践中会产生非常相似的结果。

打印机共享要求您已安装并运行 Samba。基本 Samba 配置在第 11 章“Samba：与 DOS、Windows 和 OS/2 共享文件”中有所介绍，特别是在标题为“设置 Samba 选项”的部分。本章帮助您配置 Linux/Samba 打印服务器。

## 设置 Samba 打印机选项

与 Samba 文件共享一样，您可以使用 GUI 实用程序配置 Samba 打印机共享，也可以通过直接编辑 /etc/smb.conf 文件进行配置。不幸的是，随 Red Hat Linux 6.0 提供的 linuxconf 版本对 /etc/smb.conf 中打印机共享信息的格式要求相当严格，并且 linuxconf 的 Samba 打印机配置部分不能与许多配置一起使用。因此，您可能需要使用 Samba Web 管理工具（SWAT；参见第 262 页的侧边栏）作为 Samba 的 GUI 配置工具。图 16.1 显示了 SWAT 显示 Samba 打印机共享配置。

![](img/5d4d3092919d1d16884788127447cc6d_411_0.png)

由于 GUI 打印机配置选项与文本模式 /etc/smb.conf 文件中的选项非常相似，我主要关注后者。如果您使用 GUI 配置工具，只需在该工具中定位适当命名的选项即可根据本章提供的信息进行调整。

## 共享部分或全部打印机

关于打印机共享的最重要决定之一是您是否要共享部分或全部打印机。Samba 可以从 /etc/printcap 文件中提取信息来共享所有打印机，就像 lpd 对 UNIX 风格的打印机共享所做的那样。或者，您可以为要共享的每台打印机创建单独的共享定义。

要为所有打印机创建默认共享，请创建一个名为 [printers] 的共享。Samba 读取 /etc/printcap 文件并在找到的每台打印机的第一个名称下创建一个共享，使用 [printers] 共享设置的选项。

> NOTE
> 
> 使用 linuxconf 或 SWAT 等 GUI 工具创建共享时，应省略共享名称中的方括号（{ }）。

> NOTE
> 
> 如果您使用 SWAT 管理包含 [printers] 共享的 Samba 配置，SWAT 会显示从该共享包含的所有打印机的名称。SWAT 用星号 (*) 标记这些自动加载的打印机。您无法从配置中删除它们，但可以编辑它们。编辑时，SWAT 会为修改后的配置创建一个单独的共享，并且该修改后的配置会覆盖该打印机 [printers] 共享的配置。

例如，以下是默认打印机共享的示例配置：

```
[printers]
    path = /var/spool/samba
    print ok = Yes
```

各种选项的含义将在后面描述。或者，假设服务器在 /etc/printcap 中定义了三台打印机，但您只想共享其中两台。您可以创建如下条目：

```
[canon]
path = /var/spool/samba
print ok = Yes
```

```
[lexmark]
path = /var/spool/samba
print ok = Yes
```

总体而言，这两个条目会导致共享 canon 和 lexmark 打印机。您也可以使用个性化列表为不同打印机设置不同的选项。例如，您可以使用 hosts allow 选项（p. 268）指定哪些主机可以共享特定打印机。

## 设置打印机名称

如果您选择使用 [printers] 共享定义，Samba 会使用打印机的第一个 /etc/printcap 名称作为该打印机的 Samba 共享名称。否则，Samba 通常使用您放在方括号中的名称来搜索匹配的 /etc/printcap 条目并作为共享名称。如果您希望 Samba 导出在与 Linux 队列名称不同的名称下可用，您可以使用 printer 选项来实现，如下所示：

```
[lexmark]
path = /var/spool/samba
printer = lp0
print ok = Yes
```

此共享定义使 Linux lp0 打印机在名称 lexmark 下可用。

## 使打印机可浏览

如果您希望打印机出现在 Windows 网络邻居中，如图 16.2 所示，您必须确保共享是可浏览的（p. 270），就像文件共享一样。有两种方法可以完成此任务：

- 在 /etc/smb.conf 文件的 [global] 部分放置 load printers = yes 选项。实际上，yes 是此参数的默认值，因此如果您希望所有打印机都出现，则不必指定它。
- 在各个共享条目中放置 browsable = yes 选项。与 load printers 一样，默认值是 yes，因此在大多数情况下您不应需要调整此参数。

