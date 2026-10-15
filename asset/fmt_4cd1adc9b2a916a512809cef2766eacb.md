
WHOIS 用于确定谁注册了域名（例如 `domain.com`）。WHOIS 的问题在于，你需要查询正确的服务器才能获取所需的信息。例如，你可以查询 VerSign/Network Solutions WHOIS 服务器来获取 `.com`、`.net` 和 `.org` 域名，但对于其他域名（如 `.ca` 或 `.uk`），必须使用不同的服务器。

## Windows 中的 WHOIS

Windows 默认不包含 WHOIS 客户端。虽然有一些 Windows WHOIS 客户端，但它们并不常见。很多人并不使用实际 WHOIS 客户端，而是使用基于 Web 的 WHOIS 服务。最常用 VerSign/Network Solutions 网站，地址为 `www.netsol.com/cgi-bin/whois/whois`，如图 20 所示。

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_116_0.png)

图 6-20：Network Solutions/VerSign 在线 WHOIS 工具。

使用 WHOIS 工具非常简单：在框中输入并点击 Go 按钮。6-21 显示了来自 Web 工具的 WHOIS 结果。如你所见，显示了关于域名的所有信息。这些信息包括管理和技术联系人、区域联系（zone contact）下的域名注册商，以及与域名相关的 DNS 服务器。此外，还有域名注册日期和续期日期。

## Unix 中的 WHOIS

大多数版本的 Unix 都有 WHOIS 工具。如果你的 Unix 或 Linux 版本不包含 WHOIS，或者在安装过程中没有安装，你可以通过查找适当软件包或下载源码版本（`www.linux.it/-md/software/`）并编译来安装它。这些版本中许多具有不同的功能，但 Linux 自带最多的是一个具有完整功能集的增强版本。你可以通过在 shell 提示符下输入 `WHOIS` 来查看所有选项的列表，如图 6-22 所示。屏幕将显示所有 WHOIS 选项列表。

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_117_0.png)

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_118_0.png)

图 6-22：提示符下的 WHOIS，不带任何选项即可显示可用选项列表。

```bash
$ whois
root@ ~
File Edit Settings Help
HOST connect to server-HOST
  hide disclaimers
  do a lookup for specified ATTRIBUTES
  exact match [RRAP only]
  one level specific lookup [RRAP only]
  find all specific address
  find first level specific matches
  find first version specific matches
  turn off recursive lookup
  connect to PORT
  force to show local copy of the object event
  if not confirmed
  tell server to leave out syntactic sugar
  accept the solution from SOURCE
  [SOURCE]
  [TYPE]...
  TYPE
  only lookup for objects of TYPE
  request template for object 'all' for a list of
  query specified server [RRAP only]
  recursive aggregation objects too [RRAP only]
  only keys are returned [RRAP only]
  is making done
  display this and exit
  output version information and exit
  --verbose
  --version
[root@back]# 
```

尽管 WHOIS 有许多选项，但它使用起来非常简单。较新 Linux 版本带的增强型 WHOIS 会自动确定使用哪个 WHOIS 服务器。在 Linux 下使用 WHOIS 非常简单：`WHOIS <domain>`。结果将会显示，如图 6-23 所示。

Linux 的输出与 Web 端 WHOIS 工具显示的内容相同，因为它们查询的是同一个数据库。

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_118_1.png)

图 6-23：WHOIS 客户端的输出。

## 第 7 章：安装 Microsoft DNS 服务器

3. 在“Windows 组件向导”中，选择“网络服务”（不勾选复选框），点击“详细信息”按钮打开“网络服务”对话框。

4. 勾选“域名名称系统 (DNS)”复选框，如图 7-3 所示，然后点击“确定”。

图 7-3：选择域名名称 (DNS) 并点击“确定”。

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_124_0.png)

5. 点击“Windows 组件向导”中的“下一步”开始安装 DNS。

系统会提示你插入 Windows CD。安装将继续，完成后你将看到一个对话框。

6. 点击“完成”关闭该对话框，并点击“添加/删除程序”对话框中的“关闭”。

在完成上述步骤后，是时候重新应用已应用于你系统的任何服务包了。例如，如果你的系统中安装了 Pack 2，你应该重新安装它，以将任何服务包更新应用到 DNS 服务器。此问题在较新的操作系统（.NET Server 系列）中并不关键。如果使用的是较早版本的 Windows，这可能非常重要，因为服务包更新仅会更新在执行服务包时已安装的服务。

## 通过活动目录让 DNS 运行起来

关于活动目录 (`AD`) 和 DNS 集成的完整讨论超出了本书的范范围；然而，你应该确保理解以下几个重要概念。许多关于高级活动目录和 Windows 2000 Server 的书籍都涵盖了这个主题，此外还有微软服务器主页上相关的技术白皮书：

`www.microsoft.com/windows2000/server/`

此外，活动目录会与 DNS 自动集成，不需要手动配置。事实上，除非安装了 DNS 服务器，否则无法使用活动目录。因此，跟随我们关于 DNS 在活动目录中起什么作用的概述是值得的。

在过去（Windows NT 4.0 及更早版本），局域网上的计算机可以使用遵循 NetBIOS（网络基本输入/输出系统）协议的计算机名相互通信。可以使用 `\computer` 语法访问其他计算机。NetBIOS 无法可靠地支持多网段的网络，对于较大的网络，需要另一种解决方案。如果网络跨越多个工作段，则必须实现多个 Windows Internet 命名服务 (`WINS`) 服务器，通过共享查询 WINS 服务器来查找主机的 IP 地址，从而允许跨多个网段的通信（类似于路由器）。然而，WINS 在系统管理员中声誉极差，被认为仅在偶尔是可靠的，且不适合处理大量的客户端系统（可扩展性差）。

随着 Windows 2000 Server 的引入，Windows NT 4.0 及更早的传统域控制器模型被取消，取而代之的是活动目录。活动目录服务维护了网络上所有用户、计算机和组的数据库。Windows NT 模型中的域控制器在 Windows 2000 模型中被活动目录服务器所取代，并且完全消除了对 NetBIOS 协议的依赖，尽管该协议仍被支持。

由于 NetBIOS 在很大程度上已被淘汰，WINS 不再作为局域网计算机的命名服务。相反，取而代之的是 Windows DNS 服务。Windows 2000 以及所有后续操作系统中的 Windows DNS 服务使用动态 DNS 服务器。因此，工作站可以在 DNS 数据库中自动注册其名称和 IP 地址，就像基于 Windows NT 4.0 的系统在 WINS 中注册其 NetBIOS 名称一样。Windows 2000 和更新系统会自动配置为在 DNS 中动态注册，因此只要系统连接到网络，就可以使用名称进行访问。

除了维护计算机数据库外，DNS 服务还维护了一份可用服务列表，例如域控制器和全局资源目录。这些服务在 DNS 中使用定位 (`SRV`) 记录进行维护。（我们在第 9 章中讨论这些和其他记录类型）。请记住，这些记录是供寻找特定服务的使用的。客户端在 DNS 数据库中查找服务，并通过 SRV 记录指向适当的服务器。

## 第 7 章：安装 Microsoft DNS 服务器 111

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_130_0.png)

图 7-8：在服务器上创建第一个区域。

3. 如果你选择通过“配置 DNS 服务器向导”（Configure DNS Server Wizard）配置区域，请选择“是”，创建一个正向查找区域并点击“下一步”。
