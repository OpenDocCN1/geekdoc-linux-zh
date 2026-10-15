

b. 接下来，决定是否要将联系人列表存储在本地或远程服务器上。默认情况下，联系人列表存储在本地。如果您想设置远程联系人列表（对于分区环境强烈推荐，因为它在多个 DB2 管理服务器之间共享一个公共联系人列表），请将 DAS 配置参数 contact_host 设置为要存储联系人列表的远程 DAS 的 TCP/IP 主机名。例如，要将我们的联系人列表存储在主机 udblnx05 上，我们输入了：

```bash
db2 update admin cfg using contact_host udblnx05
```

c. 现在向管理联系人列表添加联系人：

- i. 打开控制中心并单击联系人图标。该图标位于任务栏中大致在工具菜单下方，看起来像这样：
- ii. 从系统名称下拉菜单中选择您的系统名称。
- iii. 单击添加联系人按钮。输入管理联系人的姓名和电子邮件地址。如果您希望通知发送到联系人的寻呼机，请勾选地址为寻呼机。
- iv. 单击测试按钮以验证电子邮件通知功能是否正常工作。按确定保存设置并返回联系人窗口。
- v. 如果您想创建联系人组，请单击添加组按钮，并在名称字段中输入组的名称。接下来，从可用联系人列表中选择名称并按箭头键将这些联系人添加到组中。

您也可以使用任务中心添加联系人。

d. 最后，使用以下命令打开调度程序：

```bash
db2 update admin cfg using sched_enable on
```

然后重新启动 DB2 管理服务器以使更改生效。

## 安装 DB2 文档

DB2 版本 8 在单独的 CD 上提供 HTML 和 PDF 文档。这些 CD 与您的客户端和服务器 CD 一起提供。

- **HTML 文档 CD。** 该 CD 包含 DB2 在线文档，包括帮助屏幕和信息中心。它与其它 DB2 产品分开安装，自 CD-ROM 安装，这意味着您可以在安装 DB2 后立即安装 DB2 HTML 文档，或在以后安装。您还可以将文档和信息中心安装在未安装 DB2 的机器上，例如您公司的内部 Web 服务器。这将节省单个机器上的空间。
- **PDF 文档 CD。** 与 HTML 文档不同，您无需“安装”PDF 文档。该 CD 提供可直接从 CD 读取或复制到您机器上的 PDF 文件。

## 使用 DB2 Setup 向导安装 HTML 文档

1. 插入标记为 *DB2 HTML Documentation* 的 CD-ROM。
2. 以具有 root 权限的用户身份登录系统。
3. 通过输入以下命令进入文档 CD 挂载的目录：

   ```bash
   cd /cdrom
   ```

   其中 `/cdrom` 代表 CD-ROM 的挂载点。
4. 输入 `./db2setup`。这将启动 DB2 Setup 向导。
5. 启动板打开后，单击 **Install Products** 将 DB2 文档安装到您的机器上。您还可以使用此启动板查看安装先决条件、查看发行说明，或进行 **Quick Tour** 以查看 DB2 UDB 版本 8 的功能。
6. 选择您想要安装的产品。选择 **DB2 HTML Documentation** 并单击 **Next**。
7. 欢迎使用 DB2 Setup Wizard。单击 **Next**。
8. 选择要安装的 HTML 文档组件（图 2-15）。默认情况下，db2setup 仅安装核心文档。选择您想要安装的任何额外文档，然后单击 **Next**。

### 选择要安装的 HTML 文档组件

选择您想要安装的 HTML 文档组件。

- **DB2 HTML Documentation**
  - Administration information
  - Application Development information
  - Business Intelligence information
  - Core DB2 information
  - DB2 Connect information
  - Getting started information
  - Optional component information
  - Tutorial information

**Description**

Describes how to access mainframe and midrange databases through DB2 Connect.

**Installation directory**

Directory `/opt/IBM/db2/V8.1`  
Space required: 25 MB  
Space available: 2920 MB

- Select default
- Select all
- Back
- Next
- Finish
- Cancel
- Help

1. Introduction
2. Features
3. Languages
4. Summary

![](img/d95c931f4f3da4a6bd0ee55148fefad7_87_0.png)

图 2-15 选择要安装的 HTML 文档组件

9. Languages（图 2-16）。默认情况下，DB2 Setup 仅安装英文文档。您可以通过在左侧菜单中选择它们并单击箭头（>）键来安装其他语言。

