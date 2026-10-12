
- 当提示时，浏览并选择 `/var/opt/novell/iManager/nps/packages/VirtualOffice.npm` 模块。
- 点击 `Install`。
- 重复此过程并安装 `/var/opt/novell/iManager/nps/packages/VirtualOfficeAdmin.npm` 模块。
- 模块安装完成后，关闭 iManager。
- 打开一个终端会话。
- 使用 `su -` 命令切换到你的 root 用户账户。
- 在 shell 提示符下，输入 `/etc/init.d/novell-tomcat4 stop`，然后输入 `/etc/init.d/novell-tomcat4 start`。

如果你完成了这些步骤，现在你应该能够使用 iManager 管理你的虚拟办公部署。要配置虚拟办公，你需要配置以下设置：
- iManager 中的虚拟办公服务管理设置
- iManager 中的虚拟办公环境管理设置

让我们首先看看如何配置虚拟办公服务管理设置。

### 配置服务管理设置

服务管理设置是虚拟办公最重要的配置参数。这些设置负责将各种 NNLS 组件，如 iPrint、iFolder、NetMail 和 NetStorage，与虚拟办公集成。我们将讨论如何配置以下虚拟办公参数：
- Company Info
- NetStorage
- iPrint
- eGuide
- Bookmarks
- eMail
- Public Webpage
- Change Password

让我们首先讨论如何配置虚拟办公主页的公司信息区域。

### 配置公司信息

在虚拟办公主页中，页面右侧显示了一个公司信息区域。如图 11.7 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_498_0.png)

**图 11.7**

信息框。

图 11.7 中显示的文本是该字段中的默认文本。你可能希望编辑此文本以反映关于你组织的信息。要做到这一点，请完成以下步骤：
- 打开网络浏览器并导航到 `https://your_server_IP_address/nps/Manager.html`。
- 作为你的 `admin` 用户进行身份验证。
- 向下滚动到 `Virtual Office` 角色并选择 `Services Administration` 任务。将显示图 11.8 中的屏幕。
- 在 `Language` 下拉列表中，选择你的语言。
- 在 `Company Info` 字段中，输入你想要用来描述你组织的文本。你可以以纯文本形式输入信息，或者，如果你有 HTML 经验，你可以使用 HTML 标签来标记文本。
- 点击 `OK`。

![](img/c7771e8540507f2b00c088c7a411b57b_499_0.png)

**图 11.8**

公司信息配置选项卡。

你还可以将虚拟办公与安装在你的 NNLS 服务器上的 NetStorage 服务集成。让我们接下来看看如何做。

### 将虚拟办公与 NetStorage 集成

正如我们在第 7 章“使用 DirXML 同步用户身份”中讨论的那样，虚拟办公在很大程度上依赖于 NetStorage。使用你的 NNLS 服务器上的此服务，虚拟办公可以为虚拟团队提供团队文件共享，如图 11.9 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_499_1.png)

**图 11.9**

团队文件共享。

虚拟办公还通过虚拟办公界面为每个用户提供访问其或她的 NetStorage 主页的权限。这是通过虚拟办公屏幕顶部的一个图标来实现的（见图 11.10）。

![](img/c7771e8540507f2b00c088c7a411b57b_499_2.png)

**图 11.10**

虚拟办公中的 NetStorage 图标。

当你点击此图标时，虚拟办公打开当前登录用户的 NetStorage 主页。这如图 11.11 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_500_0.png)

**图 11.11**

从虚拟办公打开的 NetStorage 主页。

要配置你的虚拟办公部署以使用 NetStorage 服务，你需要执行以下操作：
- 在 iManager 中，选择 `Services Administration` 任务。
- 选择 `NetStorage` 选项卡。将显示图 11.12 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_500_1.png)

**图 11.12**

NetStorage 配置选项卡。
- 默认情况下，`Enable` 复选框应被选中。如果没有，通过点击 `Enable` 开启 NetStorage 集成。
- 默认情况下，`Launch to this Server’s NetStorage Home Page` 选项应被选中。这将配置虚拟办公连接到安装了虚拟办公的同一服务器上的 NetStorage 服务。如果你想连接到不同服务器上的 NetStorage 服务，请选中 `Launch to a Remote Server's NetStorage Home Page` 按钮并输入 NetStorage 服务器的 IP 地址或 DNS 名称。
- 点击 `OK`。

配置好你的 NetStorage 设置后，接下来你需要将你的虚拟办公部署与 iPrint 集成。

### 将虚拟办公与 iPrint 集成

与 NetStorage 类似，虚拟办公为用户提供访问你 NNLS 服务器上 iPrint 服务的便捷方式。这是通过从用户的虚拟办公页面内部提供一个 iPrint 图标来实现的。此图标如图 11.13 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_501_0.png)

**图 11.13**

虚拟办公中的 iPrint 图标。

为了提供此访问权限，你必须使用 iPrint 服务器的地址配置你的虚拟办公服务。要做到这一点，你需要完成以下步骤：
- 在 iManager 中，选择 `Services Administration` 任务。
- 选择 `iPrint` 选项卡。将显示图 11.14 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_501_1.png)

**图 11.14**

iPrint 配置选项卡。
- 默认情况下，`Enable` 复选框应被选中。如果没有，通过点击 `Enable` 开启 iPrint 集成。
- 默认情况下，`Launch to this Server’s iPrint Home Page` 选项应被选中。这将配置虚拟办公连接到安装了虚拟办公的同一服务器上的 iPrint 服务。如果你想连接到不同服务器上的 iPrint 服务，请选中 `Launch to a Remote Server’s iPrint Home Page` 按钮并输入 iPrint 服务器的 IP 地址或 DNS 名称。
- 点击 `OK`。

将你的 NetStorage 和 iPrint 服务集成到虚拟办公后，你的下一个任务是集成你的 NNLS 服务器的 eGuide 服务。

### 将 eGuide 与虚拟办公集成

与 NetStorage 和 iPrint 类似，虚拟办公还为最终用户提供简化访问你服务器上 eGuide 服务的方式。在虚拟办公主页中，每个用户都有一个 eGuide 图标，如图 11.15 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_502_0.png)

**图 11.15**

虚拟办公中的 eGuide 图标。

当最终用户点击此图标时，虚拟办公启动它已配置使用的 eGuide 服务器上的 eGuide 主页，如图 11.16 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_502_1.png)

**图 11.16**

从虚拟办公内部启动 eGuide。

虚拟办公室（Virtual Office）还可以配置为在最终用户的虚拟办公室主页上提供快速搜索功能。此功能如图 11.17 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_503_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_503_1.png)

要将 eGuide 集成到您的虚拟办公室部署中，您需要完成以下步骤：
- 1. 在 iManager 中，选择 `Services Administration` 任务。
- 2. 选择 `eGuide` 选项卡。此时将显示图 11.18 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_503_2.png)
