
# geeko, people, suse.de

```
dn: uid=geeko,ou=people, dc=suse,dc=de
objectClass: top
objectClass: posixAccount
objectClass: shadowAccount
objectClass: inetOrgPerson
cn: Geeko Chameleon
gidNumber: 100
givenName: Geeko
homeDirectory: /home/geeko
loginShell: /bin/bash
shadowInactive: -1
shadowMax: 99999
shadowMin: 0
shadowWarning: 7
sn: Chameleon
uid: geeko
uidNumber: 1010
shadowLastChange: 12623
```

`ldapsearch`以LDIF格式显示结果。这意味着你可以通过将数据重定向到文件，然后在另一台机器上使用`ldapadd`将数据传输到另一个LDAP服务器。

## 如何删除和修改LDAP服务器条目

在SLES 6中修改LDAP目录数据最简单的方法是修改LDIF文件并使用`ldapmodify`工具应用更改。

在以下示例中，用户`geeko`的`uidNumber`被更改为`1011`：

```
# geeko, people, suse.de
dn: uid=geeko,ou=people, dc=suse,dc=de
objectClass: top
objectClass: posixAccount
objectClass: shadowAccount
objectClass: inetOrgPerson
cn: Chameleon
gidNumber: 100
genName: Geeko
homeDirectory: /home/geeko
loginShell: /bin/bash
shadowInactive: -1
shadowMax: 99999
shadowMin: 0
shadowWarning: 7
sn: Chameleon
uid: geeko
uidNumber: 1011
shadowLastChange: 12623
```

要应用更改，请使用以下命令：

```
ldapmodify -x "cn=Manager,dc=example,dc=com" -W -f geeko.ldif
```

使用`ldapmodify`命令与使用`ldapadd`类似。`ldapmodify`将目录中的数据与LDIF文件中的数据对比，并将更改应用于目录条目。

要从LDAP目录中删除条目，请使用以下命令：

```
ldapdelete -D cn=Administrator,dc=example,dc=com -x -W "cn=geeko,dc=example,dc=com"
```

在此示例中，区分名称为`cn=geeko,dc=example,dc=com`的条目被删除。

## 如何使用图形化LDAP应用程序

可以使用图形化应用程序访问LDAP服务器。SLES 9自带了图形化LDAP浏览器GQ。在使用GQ之前，您需要安装`gql`包，因为它不是默认软件选择的一部分。

安装后，您可以通过KDE菜单中选择`System > GQ LDAP Client`来访问GQ。

启动GQ后，如图3–4所示。

![](img/501a26f547021936f65b9bd40bb47394_144_0.png)

图3-4

GQ读取文件`/etc/openldap/ldap.conf`以获取有关默认LDAP服务器的信息。

您可以对LDAP目录执行以下操作：

- 搜索目录
- 浏览目录
- 探索架构定义

## 搜索目录

这是您启动GQ后打开的默认页面。页面顶部有以下文本字段：

- 搜索过滤器（Search filter）：在此字段中，您为查询输入搜索过滤器。其语法与`ldapsearch`使用的语法相同。
- LDAP服务器：从下拉列表中选择一个LDAP服务器。

## 第3节配置网络服务

- 如果您想添加额外的服务器，需要选择`File > Preferences`打开偏好框。在Servers页面上，通过选择`New`指定一个新的LDAP服务器。
- **搜索基（Search base）**：在此字段中，您为查询指定搜索基。搜索基的语法与`ldapsearch`使用的语法相同。

输入所有必要数据后，选择`Find`开始查询。

查询结果显示在输入字段下方的列表中。双击条目可显示详细信息。

## 浏览目录

GQ的浏览页面如图3-5所示。

![](img/501a26f547021936f65b9bd40bb47394_145_0.png)

图3-5

页面左侧是一个树形菜单，可以使用它来浏览目录。通过选择条目前的箭头符号，可以展开树形结构。

您可以通过选择树形菜单中的条目，在页面右侧显示其详情。

## 探索架构定义

GQ的架构页面如图3-6所示。在该页面上您可以浏览LDAP服务器可用的架构定义。

![](img/501a26f547021936f65b9bd40bb47394_146_0.png)

图3-6

## 练习3-2使用LDAP服务器

在此练习中，您通过以下步骤使用LDAP服务器：

- 部分I：安装GQ
- 部分II：搜索
- 部分III：浏览
- 部分IV：使用LDIF文件添加用户

### 部分I：安装GQ

执行以下操作：

1. 从KDE菜单选择`System > YaST`。
2. 输入根密码并选择`OK`。
3. 从`YaST Control Center`选择`Install and Remove`。
4. 从过滤器菜单选择`Search`。
5. 在`Search`字段输入`gq`；然后选择`Search`。
6. 在右侧选择`package`。
7. 选择`Accept`安装应用程序。
8. 插入SLES 9 DVD。
9. 安装完成后，关闭`YaST Control Center`并移除DVD。

### 部分II：搜索

执行以下操作：

- 从KDE菜单选择`System > LDAP Client`。
- 确保了选择`Search`选项卡。
- 在左侧搜索字段输入`uid=geeko`。
- 在右侧搜索字段输入`dc=digitalairlines,dc=com`。
- 选择`Find`。
- 出现了一个结果行。
- 双击结果行。
- 显示了用户`geeko`的LDAP条目。
- 向下滚动验证您可以看到`geeko`的`userPassword`条目。
- 选择`Close`。
- 从菜单栏选择`File > Preferences`。
- 从配置框选择`Servers`选项卡。
- 选择条目`localhost`；然后选择`Edit`。
- 从服务器框选择`Details`。
- 在`Bind DN`字段输入：`cn=Administrator,dc=digitalairlines,dc=com`。
- 选择`OK`关闭服务器框。
- 选择`OK`关闭配置框。
- 确保搜索字段仍包含输入的查询。
- 选择`Find`。
- 提示密码时输入`novell`，然后选择`OK`。
- 双击结果行。
- 确保可以看到`geeko`的`userPassword`条目。
- 注意密码未授予匿名用户，而是授予管理员。
- 完成后，选择`Close`。

### 部分III：浏览

执行以下操作：

- 从`GQ`应用程序选择`Browse`。
- 在左侧展开`localhost`。
- 展开`dc=digitalairlines,dc=com`。
- 展开`people`。
- 显示系统所有用户。目前包含`geeko`。
- 选择`geeko`。
- 右侧显示`geeko`的用户信息。
- 关闭`GQ`窗口。

### 部分IV：使用LDIF文件添加用户

执行以下操作：

- 使用文本编辑器在`/tmp`目录下创建一个名为`tux.ldif`的文件，内容如下：

```
dn: uid=tux,ou=people,dc=digitalairlines,dc=com
objectClass: top
objectClass: posixAccount
objectClass: shadowAccount
objectClass: inetOrgPerson
cn: Penguin
gidNumber: 100
uid: Tux
homeDirectory: /home/tux
loginShell: /bin/bash
shadowInactive: -1
shadowLastChange: 12609
shadowMax: 99999
shadowMin: 0
shadowWarning: 7
sn: Penguin
uid: tux
userPassword: {crypt}GpyJ3/OQgLXZE
uidNumber: 1010
```

您也可以从您的3038 Course DVD中的`exercises/section_3`目录将LDIF文件`tux.ldif`复制到`/tmp`目录。

2. 保存文件并关闭文本编辑器。

3. 从终端窗口（以`root`身份），输入以下添加用户`tux`（全部一行）：

```
ldapadd -XD "cn=Administrator,dc=digitalairlines,dc=com" -W -f /tmp/tux.ldif
```

4. 提示密码时输入`novell`。

如果以`Administrator`身份验证失败，请尝试终端窗口并打开一个新的终端窗口。重复步骤3和4。

执行`ldapadd`命令不需要`root`权限；但后续命令需要`root`权限。

5. 输入以下为用户`tux`创建家目录：

```
cp -a /etc/skel/ /home/tux
```

6. 输入以下命令调整文件系统权限：

```
chown -R tux:users /home/tux/
```

7. 输入`exit`退出`root`登录。

8. 输入以下切换到用户`tux`：

```
su - tux
```

9. 输入密码`Novell`登录`tux`用户账户。

10. 按`Ctrl+D`退出`tux`登录。

11. 关闭终端窗口。

# 配置Apache Web服务器

## 目标3配置Apache Web服务器

Apache Web服务器是领先的Web服务器软件。Apache作为开源软件开发，并随SLES 9起。

要设置内部Apache Web服务器，您需要了解：

- Web服务器的基本功能
- 如何安装和设置基础Apache Web服务器
- Apache配置文件的结构和基本元素
- 基础Apache配置
- 如何配置虚拟主机
- 如何限制Web服务器的访问
- 如何配置OpenSSL进行连接加密

## Web服务器的基本功能

Web服务器交付Web浏览器请求的数据。数据可以是不同的格式，例如HTML文件、图像文件、Flash动画或声音文件。

Web浏览器和Web服务器使用HTTP（超文本传输协议）进行通信。图3-7显示了浏览器、服务器和HTTP之间的关系。

![](img/501a26f547021936f65b9bd40bb47394_150_0.png)

图3-7

# 如何安装和设置基础Apache Web服务器

要设置基础的Apache Web服务器，你需要执行以下操作：

- 安装所需的软件包包
- 启动并测试Web服务器
- 找到Web服务器的文档根目录(`DocumentRoot`)

# 安装所需的软件包包

要运行基础的Apache Web服务器，你需要使用`YaST`安装以下软件包：

- `apache2`。基础Web服务器软件。
- `apache2-prefork`。一个额外的Apache软件包，会影响Web服务器的多进程处理行为。
- `apache2-example-pages`。示例HTML页面。

SLES 9拥有两个版本的Apache：Apache 1系列和Apache 2系列。本节涵盖Apache 2，因为该版本将继续被开发。

当你安装上述列出的软件包包时，`YaST`会提示你也安装Apache所需的一个或多个额外软件包。通过选择“确定”来确认额外软件包的安装，以解决Apache软件包的所有依赖关系。

## 启动并测试Web服务器

安装完所需的软件后，你需要启动Web服务器。请以`root`用户身份输入以下命令执行此操作：

```
apache2 start
```

与所有服务一样，输入以下内容停止Web服务器：

```
apache2 stop
```

如果你希望Web服务器在启动机时启动，你需要输入以下内容：

```
inserv apache2
```

要测试Web服务器是否安装正确，打开Web浏览器并输入以下地址：

```
http://localhost
```

浏览器将显示图3–8所示的页面。

如果你的SLES 9连接到了网络，你（以及网络上的其他主机）可以通过输入以下内容远程访问Web服务器：

```
http://your_system_IP_address
```

如果你的网络提供了DNS服务器，你可以使用主机名代替IP地址。

## 配置Apache Web服务器

Apache安装测试页面 - 胜利者

文档详情浏览额外设置第一页

![](img/501a26f547021936f65b9bd40bb47394_152_0.png)

如果你能看到这个，说明该系统的Apache Web服务器软件安装成功。你现在可以向此目录添加内容并替换此页面。

# 看到的不是预期的网站？

此页面的出现是因为网站管理员更改了此Web服务器的配置。如有疑问，请联系负责维护此服务器的人员。编写Web服务器站点管理手册的Apache软件基金与维护该站点无关，也无法帮助解决问题。

Apache文档已包含在此发行版中。

你可以自由在运行Apache的服务器上使用下面的图片。感谢使用Apache！

图3-8

# 找到Web服务器的文档根目录(DocumentRoot)

Apache提供的数据默认目录是

`/srv/www/htdocs`。

该目录也被称为Web服务器的文档根目录(`DocumentRoot`)。安装完成后，它包含了上面所示的Apache示例页面。

你可以替换`DocumentRoot`目录中的数据以显示你自己的Web服务器内容。由于Web服务器以用户`id wwwwww`运行，你必须确保该用户具有访问`DocumentRoot`目录文件的权限。

如果你在`DocumentRoot`中创建了子目录，你可以通过以下Web服务器地址访问这些子目录：

```
http://your_server/name_of_subdirectory
```

如果地址中没有请求特定文件，Apache会查找名为`index.html`的文件。你可以在Apache配置文件中更改此默认文件的名称。

# Apache配置文件的结构和基本元素

要使用配置文件配置Apache Web服务器，你需要执行以下操作：

- 找到Apache配置文件
- 理解配置文件的基本规则

# 找到Apache配置文件

Apache Web服务器的配置分布在`/etc/apache2`目录下的多个配置文件中。

以下是重要的Apache配置文件：

- `httpd.conf`。主配置文件。所有其他配置都包含在这里。
- `default-server.conf`。基础服务器设置。然而，其中的选项会被其他配置文件覆盖。
- `vhost.d/`。包含虚拟主机设置的目录。在本节中你将了解到更多关于虚拟机的知识。
- `uid.conf`。配置文件。
- `listen.conf`。配置文件。
- `server-tuning.conf`。配置文件。
- `error.conf`。配置文件。
- `ssl-global.conf`。配置文件。

# 理解配置文件的基本规则

Apache Web服务器的配置分布在`/etc/apache2`目录下的多个配置文件中。

以下是重要的配置列表：

- `httpd.conf`。主配置文件。所有其他配置都包含在这里。
- `default-server.conf`。基础服务器设置。然而，其中的选项会被其他配置文件覆盖。
- `vhost.d/`。包含虚拟主机设置的目录。在本节中你将了解到更多关于虚拟机的知识。
- `uid.conf`。配置文件。
- `listen.conf`。配置文件。
- `server-tuning.conf`。配置文件。
- `error.conf`。配置文件。
- `ssl-global.conf`。配置文件。

## 配置Apache Web服务器

每当你编辑配置文件时，都需要停止并重启Apache服务器。你可以输入：

```
apache2 restart
```

如果你不确定修改是否正确，可以通过输入以下命令验证语法：

```
apache2 configtest
```

如果语法正确，命令将显示：

`Syntax OK`

## 基础Apache配置

大多数情况下，默认设置是合适的，不需要更改。

# 138第3部分配置网络服务

> Apache指令概述可见http://httpd.apache.org/docs-2.0/mod/directives.html。

## 如何配置虚拟主机

要使用Apache的虚拟主机功能，你需要了解以下内容：

- 虚拟主机概念
- 如何配置虚拟主机

# 虚拟主机概念

在默认设置下，可以使用浏览器通过以下地址访问Apache服务器：

- `http://localhost`（从运行Web服务器的计算机上）
