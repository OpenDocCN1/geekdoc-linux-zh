
| 编译 JSP（Pre-compile JSP） |  |
| 安装应用程序的目录（Directory to Install Application） | `/installedApps/dhcp3906` |
| 分发应用程序（Distribute Application） |  |
| 使用二进制配置（Use Binary Configuration） |  |
| 部署 EJBs（Deploy EJBs） |  |
| 应用程序名称（Application Name） | `ITSOBankEAR` |
| 为资源创建 MBeans（Create MBeans for Resources） |  |

**图 8-16** Step 1：部署选项

- 7. 点击 `Next`（下一步）进入步骤 2 为消息 Bean 提供监听端口（Provide Listener Ports for Messaging Beans），确保监听端口正确。

最后，你必须`保存`你所完成的操作配置。否则，所有设置在 WebSphere 配置中都不会生效。

## 8.1.4 安装 ITSO Bank EAR 文件

本节讨论了如何使用管理控制台在应用程序中安装 ITSO Bank EAR 文件。在此任务期间，你将安装整个 J2EE 应用程序（如 `.ear`、`.war` 和 `JAR` 文件）。

安装应用程序请遵循以下步骤：

- 1. 启动 5 版本的 WebSphere 管理控制台。
- 2. 从左侧框架中，展开 `Applications`（应用程序）。点击 `Install Application`（安装应用程序）链接（图 8-14）。

- 服务器
- 应用程序
  - 企业级应用程序
  - 安装新应用程序
- 资源

**图 8-14** 安装新应用程序

- 3. 弹出准备安装应用程序（Preparing for application install）框架（图 8-15）。使用 `Browse`（浏览）按钮指定你之前存储 EAR 文件的目录（在我们的示例中：`/opt/WebSphere/AppServer/installableApps`）。选择 `Local path.`（本地路径）。

![](img/88f7c0f0eff8122fc71c8c318ea660bf_179_0.png)

**图 8-15** 准备安装应用程序

- 4. 点击 `Next`（下一步）按钮。
- 5. 从默认绑定（Default bindings）框架中，采用默认设置并点击 `Next`（下一步）。
- 6. 现在通过七个步骤。在准备应用程序（Preparing application）框架的 *Step 1*（第 1 ）中，指定安装应用程序的目录。（在我们的示例中：`/opt/WebSphere/AppServer/installedApps/dhcp39065`。`dhcp39065` 目录通常是应用程序安装时的节点名）。在 Application Name（应用程序名称）字段中输入 `ITSOBankEAR`（图 8-16）。

> **注意：** 步骤的数量取决于 EAR 文件的内容。在我们的示例中，我们有七个步骤。如果你只需要部署 Web 应用程序，步骤可能少于七步。

允许安装企业级应用程序和模块

-> Step 1：提供执行安装的选项

指定用于准备和安装应用程序的各种选项。

| 应用程序部署选项（AppDeployment Options） | Enable |
| --- | --- |
| 编译 JSP（Pre-compile JSP） |  |
| 安装应用程序的目录（Directory to Install Application） | `/installedApps/dhcp3906` |
| 分发应用程序（Distribute Application） |  |
| 使用二进制配置（Use Binary Configuration） |  |
| 部署 EJBs（Deploy EJBs） |  |
| 应用程序名称（Application Name） | `ITSOBankEAR` |
| 为资源创建 MBeans（Create MBeans for Resources） |  |

**图 8-16** Step 1：部署选项

- 7. 点击 `Next`（下一步）进入步骤 2 为消息 Bean 提供监听端口（Provide Listener Ports for Messaging Beans），确保监听端口正确。

最后，你必须`保存`你所完成的操作配置。否则，所有设置在 WebSphere 配置中都不会生效。
