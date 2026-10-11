
## 实验练习 7.3：使用 DirXML eDirectory 驱动程序

在本实验练习中，您将配置两台服务器上的 DirXML eDirectory 驱动程序。然后，您将测试驱动程序配置。

> 要完成此练习，您需要一台第二台计算机，该计算机能够通过网络介质与您在这本书中一直使用的服务器进行通信。这可能会给您带来挑战，您可能会想跳过此练习。但在这样做之前，请注意，您可能需要了解如何配置此驱动程序才能通过 CLE 考试。

VMware 在这个实验中特别有用。如果有足够的系统内存，您可以在同一台物理 PC 硬件上同时运行两个虚拟 Linux 会话。更多信息请访问 http://www.vmware.com。

完成以下步骤：

- 1. 获取一台满足 NNLS 指定要求的第二台 PC 系统。

> 确保备份您想保留的这台 PC 上的任何数据！

- 2. 在这台第二台系统上安装 SLES 8。将该服务器命名为 CLE2。

- 3. 配置服务器使用 CLE1 作为其主 DNS 服务器。

- 4. 配置 CLE2 上的 NTP 守护进程，使其与 CLE1 同步时间。

- 5. 下载并安装 CLE2 上的 OpenSLP 包。

- 6. 配置 slp.conf 文件，使 CLE2 成为一个目录代理 (DA)，并提供与 CLE1 相同的作用域。请参阅第 5 章了解具体说明。

- 7. 向 CLE2 添加多播路由并启动 slpd 守护进程。如果您需要了解具体操作说明，请参阅第 5 章。

- 8. 使用您在第 5 章实验练习中下载的 ISO 镜像和 NICI 文件，在这台第二台系统上安装 NNLS。使用以下参数：
    - **安装类型** — 快速安装
    - **树名称** — CLE2-TREE
    - **管理员名称** — cn=admin.ou=CLE.O=ANNAPOLIS
    - **管理员密码** — novell
    - **NetMail 服务器的域名** — CLE1.com

- 9. 通过完成以下步骤在您的 CLE-Tree 中添加容器以容纳同步对象：
    - a. 运行网络浏览器，导航至 `https://_your_CLE1_server_IP_address/nps/iManager.html` 以打开 iManager。
    - b. 使用密码 **novell** 以 **admin** 身份进行身份验证。
    - c. 使用 **eDirectory 管理** 角色下的 **创建对象** 任务，在 IF.CLE 中创建一个名为 **RemoteUsers** 的组织单元。
    - d. 使用 **eDirectory 管理** 角色下的 **创建对象** 任务，在 IF.CLE 中创建一个名为 **RemoteGroups** 的组织单元。

- 10. 通过完成以下步骤为您的 CLE2-Tree 准备 DirXML 同步：
    - a. 运行网络浏览器，导航至 `https://_your_CLE2_server_IP_address/nps/iManager.html` 以打开 iManager。
    - b. 使用密码 **novell** 以 **admin** 身份进行身份验证。
    - c. 使用 **eDirectory 管理** 角色下的 **创建对象** 任务，在 CLE.ANNAPOLIS 中创建一个名为 **RemoteUsers** 的组织单元。
    - d. 使用 **eDirectory 管理** 角色下的 **创建对象** 任务，在 CLE.ANNAPOLIS 中创建一个名为 **RemoteGroups** 的组织单元。
    - e. 向您的 CLE2-Tree 添加以下用户：

| 用户 | 属性 | 值 |
| :--- | :--- | :--- |
| J.Astin | First Name | John |
| | Last Name | Astin |
| | Context | CLE.ANNAPOLIS |
| | Password | Novell |
| | Title | Director of Operations |
| | Location | Annapolis, MD Office |
| | Department | Operations |
| | Telephone | 555-555-5551 |
| | Fax | 555-555-5552 |
| | Email Address | jastin@cle2.com |
| JShannon | First Name | Jerry |
| | Last Name | Shannion |
| | Context | CLE.ANNAPOLIS |
| | Password | Novell |
| | Title | Facilities Manager |
| | Location | Annapolis, MD Office |
| | Department | Operations |
| | Telephone | 555-555-5553 |
| | Fax | 555-555-5552 |
| | Email Address | jshannon@cle2.com |
| KLarsen | First Name | Kimberly |
| | Last Name | Larsen |
| | Context | CLE.ANNAPOLIS |
| | Password | Novell |
| | Title | Facilities Manager |
| | Location | Annapolis, MD Office |
| | Department | Operations |
| | Telephone | 555-555-5550 |
| | Fax | 555-555-5552 |
| | Email Address | klarisen@cle2.com |
| DAverett | First Name | Darren |
| | Last Name | Averett |
| | Context | CLE.ANNAPOLIS |
| | Password | Novell |
| | Title | Administrative Assistant |
| | Location | Annapolis, MD Office |
| | Department | Operations |
| | Telephone | 555-555-5554 |
| | Fax | 555-555-5552 |
| | Email Address | daverett@cle2.com |

- 11. 通过完成以下步骤验证两台服务器上的时间是否已同步：
    - a. 在两台服务器上打开终端会话。
    - b. 在两个 shell 提示符下，输入 `ntpq -p`。
    - c. CLE1 应报告与您在早期练习中配置的公共 NTP 时间源的偏移量小于 1 秒。请记住，偏移量以毫秒显示。
    - d. CLE2 应报告与 CLE1 的偏移量小于 1 秒。

> **注意**
> 作为替代方案，您可以配置 CLE2 从与 CLE1 相同的公共时间提供程序获取时间。只要两台服务器上的时间相同，具体采用哪种方式并不重要。

    - e. 如果同步已丢失，请参照第 5 章中列出的步骤，使用 NTP 重新建立时间同步。

- 12. 通过完成以下步骤配置 CLE1 上的 eDirectory 驱动程序：
    - a. 运行网络浏览器，导航至 `https://your_CLE1_server_IP_address/nps/iManager.html` 以打开 iManager。
    - b. 使用密码 **novell** 以 **admin** 身份进行身份验证。
    - c. 在 **DirXML 管理** 角色下，选择 **创建驱动程序** 任务。
    - d. 在 **创建驱动程序欢迎** 屏幕上，选择 **在新驱动程序集中**，然后单击 **下一步**。
    - e. 在 **名称** 字段中，输入 **CLEDriverSet2**。
    - f. 在 **上下文** 字段中，输入 **IFCLE**。
    - g. 在 **服务器** 字段中，输入 **CLE1.IFCLE**，然后单击 **下一步**。
    - h. 在 **从服务器导入预配置驱动程序（.XML 文件）** 下拉列表中，选择 **eDir-Driver.xml**，然后单击 **下一步**。
    - i. 在 **驱动程序名称** 字段中，输入 **eDir-Driver**。
    - j. 在 **远程树地址** 和 **端口** 字段中，输入您的 CLE2 服务器的 IP 地址。确保在 **端口** 字段中输入 **8196**。
    - k. 在 **配置数据流** 下拉列表中，选择 **双向**。
    - l. 在 **配置选项** 下拉列表中，选择 **扁平**。
    - m. 在用户 **基础容器** 字段中，输入 **RemoteUsers.IFCLE**。
    - n. 在 **组容器** 字段中，输入 **RemoteGroups.IFCLE**。

**警告** 在步骤 **m** 和 **n** 中，不要使用 **浏览** 按钮。这会导致问题！

    - o. 单击 **下一步**。
    - p. 选择 **定义安全等效性**。
    - q. 单击 **添加**。
    - r. 浏览并选择 **admin.IFCLE**，然后单击 **确定**。
    - s. 选择 **排除管理角色**。
    - t. 单击 **添加**。
    - u. 浏览并选择 **admin.IFCLE**，然后单击 **确定**。
    - v. 单击 **下一步**。
    - w. 在 **摘要** 屏幕上，单击 **完成并显示概览**。

- 13. 通过完成以下步骤配置 **CLE1-Tree** 中的过滤器：
    - a. 在 **iManager** 中，通过选择 **eDirectory** 图标来查看 **驱动程序概览** 屏幕。

**警告** 不要选择红色减号，它用于启动和停止驱动程序。

    - b. 在 **订阅者** 通道上，选择 **订阅者过滤器** 图标。显示的属性是允许通过过滤器的属性。
    - c. 请注意，**访问控制列表 (ACL)** 属性允许通过过滤器。应该移除它。大多数 ACL 包含特定于树的信息，这可能会导致同步问题。在 **过滤器** 中选择 **所有类**。
    - d. 在右列中，取消选择 **ACL** 属性，然后单击 **确定**。
    - e. 单击 **确定**。
    - f. 在 **发布者** 通道上，选择 **发布者过滤器** 图标。
    - g. 请注意，**ACL** 属性也在发布者通道上允许通过。重复前面的步骤以移除此属性。
