
# 网络配置与证书管理

在保存并退出之前，取消以下两行的注释：

```
user nobody
group nobody
```

## 转发

现在我们可以使用编辑将设置转发到我们连接的计算机上。可以通过运行以下命令来实现：

```bash
echo 1 >/proc/sys/net4/ip_forward
```

我们需要编辑`sysctl.conf`，用`nano /etc/sysctl.conf`打开它。找到并取消注释：

```
net.ipv4.ip_forward=1
```

然后重启以生效。

你即将输入的内容被称为区别性名称，或简称`DN`。

有几个字段你可以留空。

对于某些字段将有一个默认值，而空字段将保持留白。

`国家名称（两位字母代码）`[UK]

`州或省份（全称）`[可选]

`地点（城市）`[Bournemouth]

`组织名称（例如，公司）`[example]

`组织名称（部门）`[Department of Excellence]

`通用名称（例如，您的用户名或服务器名称）`[client]

`邮箱地址`[@example.com]

请输入以下“额外”属性以包含在您的证书请求中：

`挑战密码`

`可选密码`

使用来自`/etc/openvpn/easy-rsa/openvpn-2.4.0.conf`的配置。

检查与签名是否匹配。

签名通过。

主体的区别性名称如下：

`countryName=[PRINTABLE: UK]`

`stateOrProvince=[PRINTABLE: UK]`

`localityName=[PRINTABLE: Bournemouth]`

`organizationName=[PRINTABLE: example, Inc]`

`organizationalUnitName=[PRINTABLE: Department of Excellence]`

`commonName=[PRINTABLE: client]`

`optionalName=[PRINTABLE: server]`

`emailAddress=[PRINTABLE: examplehosting.com]`

证书有效期至 2025年6月5日 15:09:24 (3650 天)。

`签名证书 (y/n)`

已生成 1 个请求中的 1 个，已确认。[y/n]

写入 1 条新目到数据库。

数据库已更新。

```
root@ubuntu:/etc/openvpn/easy-rsa# 
#
```

```
# /etc/openvpn/easy-rsa/keys/server.crt,server.key,ca.crt /etc/openvpn
```

> 一旦你设置好了从客户端连接到服务器的方法，你就可以开始测试你的输出。

一旦完成，你最终可以使用以下命令通过客户端启动服务器：

```
# service openvpn start
```

使用`openvpn status`检查它是否正在运行。

## 15 为客户端创建密钥

我们现在根据客户端名称本身为客户端构建一个唯一的密钥。你可以直接在这里使用以下命令创建它：

```
./build-key [name]
```

再次提醒，不要提供密码或可选的公司信息，确保你签署了证书并提交了。

## 17 将文件移动到客户端

一旦设置好所有的密钥和文件，你需要将文件移动到想要连接到此服务器的客户端。这包括四个文件：

第一个客户端证书以及我们下文指定的名称：

```
/etc/openvpn/easy-rsa/keys/[name].crt
/etc/openvpn/easy-rsa/keys/[name].key
```

另外两个文件用于每个客户端，它们是：

```
/etc/openvpn/easy-rsa/keys/client.ovpn
/etc/openvpn/ca.crt
```

## 16 准备配置

我们供所有客户端使用的示例文件已经存在于文件系统中，但我们需要将其移动到正确的位置以对其发挥最大作用。我们还对复制期间的示例文件进行了分组，以更符合客户端的需求：

## 18 远程连接

一旦你设置好了客户端连接到服务器的方法，你就可以利用 VPN 的全部功能开始测试服务器了。无论是为了业务还是仅仅在家里，这都是一种不受限制的工作或使用互联网的简单方法。

```
# /usr/share/doc/openvpn/examples/sample-config-files/client.conf /etc/openvpn/easy-rsa/keys/client.ovpn
```

www.linuxuser.com 29

# ERPNext 教程

## 使用 ERPNext 管理你的业务资源

学习如何使用开源`ERPNext`高效地管理你的业务

![](img/572ad2c12aa08801c9a4044d6a88fdc5_29_0.png)

`Nitish Tiwari` 是一位软件开发者和开源爱好者。他在会议上演讲并为各种杂志撰写文章，并帮助公司采用开源软件来满足业务需求。

精益（Lean）是这个世纪的流行词——所有组织无论大小，都希望用更少的时间、更少的资源完成更多、更好的事情。虽然这说起来容易，但对于小企业来说，要做到精准到位是很的。为什么不能朝着你想要的方向移动呢？这并不是单一的原因，因为最大的挑战在于公司初始阶段，人们更关注增长和计划，导致了额外的人员和资源。

### 01 安装

`ERPNext` 可以以最适合你用例的安装类型进行安装。安装 `ERPNext` 的第一个且可能最简单的方法是下载 `VirtualBox` 镜像并在 `VirtualBox` 上运行。`VirtualBox` 是由 `Oracle` 支持的开源虚拟化工具。它适用于几乎所有主流平台（`Windows`、`Mac`、`Linux`）。因此，你可以在系统上安装 `VirtualBox`，然后启动 `ERPNext VirtualBox` 镜像，通过浏览器访问 `http://localhost:8080`，使用凭据（`admin` 和密码）登录。

当公司做大并意识到需要管理资源时，已经太晚了。所以为什么不提前计划并有机增长呢？

我们将探索开源 `ERPNext` 如何帮助你管理公司的资源。无论你是小企业还是大企业，这并不——都需要管理资源。`ERPNext` 提供了从 `CRM` 到人力资源以及会计管理的各种工具。我们使用 `Ubuntu 14.04 LTS` 作为 `ERPNext` 存储主机。

安装 `ERPNext` 的另一种方法是通过 `GitHub` 上的自动化脚本。只需打开命令行提示符并输入以下命令：

```bash
wget https://raw.githubusercontent.com/frappe/bench/master/install/setup_frappe.sh
sudo bash setup_frappe.sh --production
```

首页看起来简洁，选项隐藏在不同的章节下![](img/572ad2c12aa08801c9a4044d6a88fdc5_29_1)

## 设置用户和权限

在安装了 `ERPNext` 并填充了基础数据后，下一步是设置系统中的用户及其权限。`ERPNext` 使用基于角色的权限系统，你可以根据角色分配权限。添加新用户，前往`Users/Permissions`。点击用户链接，你将看到用户列表。点击左角的`New`按钮。注意名称和邮箱是必须的。输入详情后点击`Save`。页面将重定向到用户详情，你可以在那里设置角色。你还有设置密码第三方身份验证的选项。

## 系统设置

下一步是个性化设置。前往`Settings`，你将找到所有可用设置。第一个是`System Settings`（系统设置），允许你设置语言、日期和首页显示的模块。下一个是`Naming Series`（命名系列），你可以在那里设置事务的命名系列。

## 导入数据

如果你已经从之前的安装或列表中某些 `ERP` 相关数据，可以轻松导入。只需前往`Setup/Data Import`  CSV 文件并按照说明操作![](img/572ad2c12aa08801c9a4044d6a88fdc5_30_png)

# ERPNext 教程

## 显示/隐藏功能

`ERPNext` 允许你管理首页上显示的应用程序以保持界面整洁。通过勾选或取消勾选复选框隐藏所有应用程序，应用程序将从页面移除![](img/572ad2c12aa08801c9a4044d6a88fdc5_31_0.png) ![](88fdc5_31_1.png)

## 04 价格列表

所有你需要采购的产品和物品，以及你的组织销售的成品，都有与之关联的价格。现在价格不再仅仅是成本函数；还有其他因素如需求和运输成本。在动态场景下，它用于设置不同的参数。`ERPNext` 支持价格列表，你可以从`Buying/Selling/Setup/Price` 章节轻松访问它们。查看价格列表，有两个默认列表可用。

## 06 建立品牌
