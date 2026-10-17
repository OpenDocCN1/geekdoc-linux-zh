
# 第3章 • 保护网络资源

权限选项卡允许你控制继承。通过继承，如果你授予文件夹访问，假设新创建的文件和文件夹继承相同的访问控制列表。`“替换子容器和对象的权限项”`可以实现类似的操作。审计选项卡允许你对文件进行审计。第5章将涵盖文件审计，因此我们在这里不讨论它。所有者选项卡对于文件或目录（无论是直接还是通过 `Everyone` 组组成）非常有用，重新获取文件或目录控制权的简单方法是进入管理员拥有权限的上级并接管所有权。可以通过导航到所有者选项卡来实现。你登录的管理员用户应该已经输入在字段中。勾选`“替换子容器和对象的所有者”`并点击确定。作为新所有者，你将始终拥有访问。你可以根据需要编辑权限。

有效权限选项卡允许你指定特定的组或账户，并生成用户将拥有的访问列表。这考虑了继承、组组成以及可能存在的显式权限。要查看用户的有效权限，点击`“选择”`。在下一个屏幕上，你可以输入账户名称，如果不确定账户名称，可以点击`“高级”`。这将带你进入第三个窗口，你可以在其中搜索账户名称。你可以点击`“对象类型”`按钮将搜索限制为仅用户、组或内置实体，例如。`“位置”`按钮允许你选择在哪个系统上进行。选择搜索条件后，你会看到`“立即查找”`按钮。在没有定义搜索条件的情况下，你将看到本地机器所有账户、组和内置实体列表。点击其中并点击确定会将名称放入`“选择用户或组”`窗口中。然后你可以点击确定显示有效权限窗口。图 3.6 显示了有效权限窗口。这是了解所有各种层级过滤结果的有效方法和

访问控制。当程序或用户操作生成了你并不希望出现的`“拒绝访问”`错误时，这也是你首先要检查的地方之一。

## Windows 有效权限

![](img/0eb7273a8d9e486628f6e18d37ab22c6_165_0.png)

有时，你可能正在寻找某个安全问题，并希望查看所有的目录，而不是特定的目录或文件夹。内置的安全接口在在这方面做得并不好。不过，一些额外的工具可以做到这一点。

[`AccessEnum`](https://www.microsoft.com/technet/sysinternals/AccessEnum.jsp) 是一个 GUI 工具，你可以用它来快速识别偏离常规的权限。`AccessEnum` 可运行在 Windows NT、2000、XP 和 2003 上。它会扫描你指定的文件夹以及所有子文件夹和文件，通过这种方式，你可以快速看到哪些地方的权限被更改或以某种方式修改了。`AccessEnum` 还可以扫描注册表的一部分，寻找类似的权限偏差。这是一个巨大的优势，因为提供的用于处理注册表权限的接口非常繁琐。遗憾的是，`AccessEnum` 将访问类型简化为仅读取（Read）、写入（Write）和拒绝（Deny），所以它可能不是审计员的好朋友，但它可以帮助你发现看起来异常的地方。

另一个实用的工具是 [`AccessChk`](www.microsoft.com/technet/sys-internals/Security/AccessChk.msx)。这是一个运行在 Windows 2000、XP 和 2003 上的命令行程序。`AccessChk` 也会各种权限合并为读取、写入和拒绝权限，但该程序对于安全管理员来说是一个非常强大的工具。以下命令将列出 C 盘根目录下所有文件和文件夹的访问情况：

![](img/0eb7273a8d9e486628f6e18d37ab22c6_166_0.png)

```
I:\Internet\Firefox>accesschk eric c:\
```

`AccessChk v2.0 - Check account access of files, registry keys or services`

`Copyright (C) 2006 Mark Russinovich`

`Sysinternals - www.sysinternals.com`

```
RW c:\i386\nRW c:\My Documents\nRW c:\MSDOS.SYS\nRW c:\WINDOWS\nRW c:\IO.SYS\nRW c:\Program Files\nRW c:\Windows Update Setup Files\nRW c:\boot.ini\nRW c:\CONFIG.SYS\nRW c:\AUTOEXEC.BAT\nRW c:\ntldr\nRW c:\detect.com\nRW c:\BOOTSECT.DOS\nRW c:\Documents and Settings\nRW c:\System Volume Information\nRW c:\Recycled\
```

如果你加上 `-s` ，它将递归列出所有目录，而 `-v` 关会导致它列出所有存在的权限，而不仅仅是 R、W 和 Deny。你可以轻松地将此工具与创意编程相结合，创建一个可以生成非常有用安全报告的批处理文件，如下：

![](img/0eb7273a8d9e486628f6e18d37ab22c6_166_1.png)

```
I:\Internet\Firefox>accesschk someuser I:\testfile.txt -v
```

`AccessChk v2.0 - Check account access of files, registry keys or services`

`Copyright (C) 2006 Mark Russinovich`

![](img/0eb7273a8d9e486628f6e18d37ab22c6_166_2.png)

```
R I:\TestFile.txt
  FILE_EXECUTE
FILE_LIST_DIRECTORY
FILE_READ_ATTRIBUTES
FILE_READ_DATA
FILE_READ_EA
FILE_TRAVERSE
  SYNCHRONIZE
READ_CONTROL
```

`AccessChk` 还会扫描注册表，你可以指定一个服务而不是用户名进行报告。本章未涵盖的几个其他开关增加了 `AccessChk` 的功能和灵活性。不带任何参数运行 `AccessChk` 将导致程序输出其用法文本。

### 附加步骤

当然，你可以通过收紧用户、组以及文件级权限来采取额外的步骤来加固 Windows 系统。正如你所期的，微软在保护 Windows 系统方面拥有内部优势。你可以在 Microsoft 网站上阅读非常详尽的加固指南。以下是可用更有价值的安全文档列表：

- Windows Server 2003 安全指南：

  www.microsoft.com/technet/security/prodtech/windowsserver2003/w2003hg/sgch00.msx

- Windows XP 安全指南：www.microsoft.com/technet/security/prodtech/windowsxp/secxwinxp/default.msx

- Microsoft Windows 2000 安全加固指南：

  .microsoft.com/technet/security/prodtech/windows2000/win2khg/default.msx

- Microsoft Windows NT 4.0 和 Windows 98 威胁缓解指南：www.microsoft.com/technet/security/guidance/networksecurity/threatmi.msx

![](img/0eb7273a8d9e486628f6e18d37ab22c6_167_0.png)

虽然这些指南会详细介绍如何加固操作系统，但它们概述如下：

1. 禁用不必要的服务。
2. 补丁操作系统。
3. 收紧用户和组。
4. 配置最小化访问。
5. 配置登录参数。

这些步骤，其中涵盖了许多：
