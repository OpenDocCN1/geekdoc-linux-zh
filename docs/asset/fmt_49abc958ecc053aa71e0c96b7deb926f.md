
```
migrate_hosts.pl /etc/hosts
dn: cn=mira.aceindustry.com,ou=devices,dc=aceindustry,dc=com
objectclass: iHost
objectclass: device
objectclass: top
ipHostNumber: 10.1.70.5
cn: mira
cn: www.aceindustry.com
cn: mira.aceindustry.com
```

```bash
$ migrate_password.pl /etc/passwd
dn: cn=Joe Bloggs,ou=people,dc=aceindustry,dc=com
cn: Joe Bloggs
objectclass: top
objectclass: person
objectclass: organizationalPerson
objectclass: inetOrgPerson
objectclass: posixAccount
objectclass: account
mail: jbloggs@aceindustry.com
givename: Joe
suid: jbloggs
userPassword: (crypt)daCXgaxahRNkg
loginShell:/bin/sh
uidNumber: 20
gidNumber: 20
homeDirectory:/home/jbloggs
```

通过执行此过程，我们为以后在 Elasticsearch 中应用 LDAP 奠定了基础。以下是该过程最初的样子。请注意从配置信息中获取的默认值。

```bash
[root@pavilion migration#] ./migrate_all_online.sh
输入您想要导入的 X.500 命名上下文：[dc=bellmeade]
输入您的 LDAP 服务器名称 [ldap]: pavilion
输入管理器 DN: [cn=manager,dc=bellmeade]:
输入用于绑定的凭据：
```

在此时，我们输入了根 DN 的密码，然后执行了导入。

正在导入到 `dc=bellmead`...

正在迁移别名...

正在迁移组...

正在迁移主机...

正在迁移网络...

正在迁移用户...

正在迁移协议...

正在迁移 RPC...

正在迁移服务...

正在迁移组...

正在迁移组（按用户）...

正在迁移组（按主机）...

正在导入到 LDAP...

添加新条目 `ou=People,dc=example,...`

运行多次并没有坏处。如果条目已存在，它不会被替换。创建的 LDAP 条目描述了 Linux 系统的用户和服务。

## LDAP 搜索客户端

今天有许多客户端使用 LDAP 服务。两种常见的 Web 浏览器都具有 LDAP 能力。如果你使用之前描述的导入程序，可能立即与这些客户端配合。

## Internet Explorer LDAP 客户端

Microsoft Internet Explorer (IE) 5.5 随 Windows 2000 发布。IE 6.0 随 Windows XP 发布。每个都可以接受 LDAP URL。URL 指定了 LDAP 协议和 LDAP 服务器的 DNS 路径。我们在 URL 后附加 LDAP 路径标记并按回车。IE 会为你对特殊字符和空格进行任何编码。见图 15–3。属性被分组到选项卡面板。注意我们可以将条目添加到 Windows 地址框。如果我们登录到 Windows 2000 或 Windows XP 域，此地址框将包含在 Active Directory 中。在 Evolutions 则不然。IE 不在 Linux 上运行，但我们大多数客户端运行在 Windows 2000 专业版或 Windows XP 专业版上。授权员工或任何对目录服务器具有授权访问的人可以通过互联网访问这些信息，只要防火墙规则允许访问目录服务器。通 Web 客户端可能是接下来讨论的 Netscape 名称和地址录。

## Netscape 地址录

Netscape Communicator 在其地址录中提供了一个更实用的 Internet LDAP 客户端。在这里，我们不需要折腾 URL。我们通过对话框在应用程序中配置一个或多个目录服务，如果服务器使用非标准端口，它会询问 DNS 名称和端口。它像电子邮件或新闻服务器一样保持配置，除非我们将其删除。

## Lou Mauget 属性

| 摘要 | 姓名 | 家庭 | 业务 | 个人 | 其他 | NetMeeting | 数字 ID |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 公司: | Resolutions | | 职位: | IT 经理 | | | |
| 街道地址: | 1501 Soapstone Dr | | 部门: | | | | |
| | | | | 办公室: | | | |
| 城市: | Durham | | | 电话: | 919-898-2762 | | |
| 州/省: | NC | | | 传真: | | | |
| 邮政编码: | 17794 | | | 呼机: | | | |
| 国家/地区: | | | | IP 电话: | | | |
| | | | | 查看地图 | | | |
| Web 页面: | http:// | | | Go | | | |

图 15-3 IE 显示的 `ldap:://pavilion.bellmeade cn=Lou.Mauget,dc=bellmeade`。

条目字段提供了实时搜索功能。在这里，如果网络连接良好，我们开始看到 LDAP 的惊人速度。图 15-1 显示我们输入了姓名的三个字符。结果迅速出现。LDAP 服务器是我们的 Elsolutions Open LDAP 目录。某些名称出现了两次。这是因为它们出现在 Elsolutions 的两个不同路径中。一个是用于测试的。另一个用于使用。这里没有出现的另一个问题是搜索会在名称的任何地方查找输入字符串，而不仅仅前缀。我们觉得这并不直观。我们将在在本章后面的部分为自己的 facebook 应用程序编写前缀。它将搜索前缀，而不是内部子字符串。

尽管如此，此应用程序展示了 LDAP 的实用性。任何在访问特定订单的任何操作系统上拥有 Netscape Communicator 的都可以。图 15-3 IE 显示的 `ldap:://pavilion.bellmeade cn=Lou.Mauget,dc=bellmeade`。

条目字段提供了实时搜索功能。在这里，如果网络连接良好，我们开始看到 LDAP 的惊人速度。图 15-1 显示我们输入了姓名的三个字符。结果迅速出现。LDAP 服务器是我们的 Elsolutions Open LDAP 目录。某些名称出现了两次。这是因为它们出现在 Elsolutions 的两个不同路径中。Onesolutions is for.. The The is is is...

15-

![](img/992.png)

第 15 章 • 目录集成

## Elsolutions 的目录策略

## Elsolutions 的电话簿

## Elsolutions 的目录策略

## Elsolutions 的目录策略

## Elsolutions 的目录策略

## Elsolutions 的目录策略

## 482

## 第 15 章 目录集成

当源代码被传输时，许多脚本应用是可以二进制可传输的，因为它们执行的是源代码。

我们有几种脚本语言可以选择。包括 TCL、Perl 和 Python。每种语言都能在 Linux 或 Windows 2000/XP 上的 POSIX Cygwin 上运行给定的应用程序副本。

我们的 Elsolutions 应用将使用本地 GUI。回想一下，可用的 LDAP GUI 工具包可以在 Win32 和 X 上运行。

我们需要一个 LDAP 绑定。Perl 至少有两个 LDAP 模块可用。这种语言拥有大量的可用扩展程序，其数量可能仅次于 Java 的扩展程序数量。

让我们决定使用 Perl。GUI 将用 Perl/Tk 实现。LDAP 绑定将源自 Perl-LDAP，即在 `http://perl-ldap.sourceforge.net/` 提供的 `Net::LDAP` 模块。该模块不需要运行时库。如果在构建时启用了可选支持，它 100% 的代码都能使用带有 MD5 加密的 LDAP 和 URI 记法。这对于未来的 Elsolutions LDAP 应用将很有用。

我们的电话应用程序是如何设计的？回想第 8 章“用户界面”，GUI 应用是事件驱动的。至少 GUI 必须的接口是事件驱动的。这意味着窗口将包含一些 UI 控件（小部件），这些控件绑定到事件处理器上。当用户与小部件交互时，就会调用处理器来执行应用程序逻辑的某部分。我们将应用程序分为三层：

- 视图（View）：与用户交互的表示层。
- 控制器（Controller）：绑定到小部件的事件处理器。
- 模型（Model）：供控制器处理器使用的应用程序逻辑。

让我们从用例的角度考虑该应用程序。我们邀请用户在输入框中输入姓氏的前缀字符。列表框将动态显示行，每行由一个用户名、电子邮件和电话号码组成，对应于具有当前前缀的姓氏。当用户输入字符时，结果将迅速实时显示。

我们确实需要一个输入部件和一个列表框部件。我们可以通过编写构建 GUI 的代码来开始程序。我们可以先用空的应用程序逻辑来测试程序。视图逻辑将位于一个 `build_ldap` 运行时中。主程序将建立 Perl 模块环境，定义 LDAP 连接的一些常量属性，获取与 LDAP 目录的连接，并调用 `Tkloop` 事件管理器。当我们向部件添加绑定时，事件循环管理器将调用我们的控制器代码。以下是我们的主程序。处理将不会越过 `MainLoop` 调用继续。它将在控制器和模型层的用户输入的影响下控制我们的整个应用程序。

```perl
#!/usr/bin/perl -w
use strict;
use Tk;
use Net::LDAP qw(:all);

# 修改这些全局 LDAP 常量以适应
my $ldap_ip = "pavilion.bellmeade";
my $default_base = "dc=bellmeade";
my $default_attrs = ['cn','telephoneNumber', 'mail'];

# 目录连接
my $ldap = Net::LDAP->new($ldap_ip) or die "$@";
my $msg = $ldap->bind( version => 3 );

# 构建 GUI，进入循环
buildGui;
mainLoop;
```

我们选择添加一个按钮来清除输入和列表框，另一个按钮来扩展程序。几个标签部件将标识输入框和列表框的用途。用于 Tk pack 管理器的三个 Tk frame 使我们能够对部件进行分组。这是带有控制路由器的绑定的 `buildGui` 子程序。我们在初始测试中省略了它们。

```perl
# 用部件填充主窗口
sub buildGui {
    my $mw = MainWindow->new;
    $mw->title("Elsolutions Directory");

    # 将主窗口划分为帧
    my $searchFrame = $mw->Frame()
      ->pack(side => 'left');
    my $buttonFrame = $searchFrame->Frame()
      ->pack(side => 'bottom');
    my $resultFrame = $mw->Frame()
      ->pack(side => 'left');
    $searchFrame->Label(-text => "Enter Last Name: ")->pack();

    # 搜索参数
    my $lastNameEntry = $searchFrame->Entry(
      -text => "m",
      -takefocus => 1)->pack();

    # 搜索输入字段每次按键绑定到 do_search
    my $lastNameListbox;
    $lastNameEntry->bind("<Key>",
      sub { do_search($lastNameEntry, $lastNameListbox) });

    # 搜索结果
    $resultFrame->Label(-text => "Name, E-Mail, Phone")->pack();
    $lastNameListbox = $resultFrame->Scrolled('Listbox',
      -scrollbars => 'both',
      -selectmode => 'single',
      -width => 60,
      -height => 5)->pack();
    $lastNameListbox->bind("Double-Button-1", \&display_details);

    # 清除按钮
    $buttonFrame->Button(-text => "Clear",
      -command => [\&do_clear, $lastNameEntry, $lastNameListbox]
    )->pack(side => 'left');

    # 退出按钮
    $buttonFrame->Button(-text => "Exit",
      -command => [\&do_exit])->pack(side => 'left');

    # 赋予焦点
    $lastNameEntry->focus();
}
```

到为止我们还没有显示 LDAP 代码。输入字段绑定到 `do_search`。退出按钮绑定到 `do_exit`。清除按钮绑定到 `do_clear`。

```perl
# 退出句柄
sub do_exit {
    exit;
}
```

（注：此处原文存在大量重复，我已根据逻辑进行了整合）。

## 485 Elsolutions 策略

引用作为参数传递。首先，回调函数清除结果。接下来，它获取输入字段内容。只有当内容具有有限长度时才会调用 LDAP 搜索。这种检查防止在按下 Shift 键时调用搜索。搜索请求匹配以内容开头的姓氏的所有条目。

```perl
sub do_search {
    my ($lastNameEntry, $listbox) = @_;

    $listbox->delete(0, 'all');

    my $lname = $lastNameEntry->get();

    if (length($lname) < 1) { return; }

    # 调用 LDAP 
    print "Search arg: $lname*";

    my $result = LDAPsearch($ldap, "sn=$lname*");

    display_results($result, $listbox);
}
```

`LDAPsearch` 子程序是什么？它是应用层的核心。我们在主程序中建立了 LDAP 连接。如果失败，应用程序将崩溃。连接返回 `ldap` 引用是我们唯一的全局标量。搜索子程序接收 `ldap` 引用和搜索字符串作为强制参数。两个可选参数默认为 LDAP 树搜索基以及需要的 `cn`、`mail` 和 `telephoneNumber` 属性。回想这些被设置为主程序的全局属性。这四个参数简单地传递给 `Net::LDAP` 模块的 `search` 方法。结果无论好坏都会返回给调用者。

```perl
sub LDAPsearch {
    my ($ldap, $searchString, $attrs, $base) = @_;

    # 默认可选参数
    if (!$base) { $base = $default_base; }
    if (!$attrs) { $attrs = $default_attrs; }

    my $result = $ldap->search(
        base   => "$base",
        scope  => "sub",
        filter => "$searchString",
        attrs  => $attrs
    );

    return $result;
}
```

结果是如何出现在结果列表框小部件中的？`do_search` 子程序调用 `display_results` 子程序将搜索结果渲染到列表框中。如果发生错误或未找到结果，`display_results` 将安全地渲染为空内容。

```perl
#-
# Render results into passed listbox
#-
sub display_results {
    my ($results, $listbox) = @_;

    # Enumerate sorted array of DNs
    my $entries = $results->sorted;

    my $entr;
}
```
