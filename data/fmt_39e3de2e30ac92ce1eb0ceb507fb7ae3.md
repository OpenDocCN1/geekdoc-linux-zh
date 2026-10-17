
| 部门 (Department) | 此选项类似于镜像选项。但是，在目标树中指定的基础容器内，只有对象的父容器会被创建，而不是镜像整个源树层级。例如，如果你配置了 `IF.CLE` 作为基础容器，并从源树同步之前列出的相同服务对象，结果将是一个名为 `KRitter.IS.IF.CLE` 的服务对象和一个名为 `JCarr.IS.IF.CLE` 的服务对象。 |

与其他 `DirXML` 驱动程序一样，`eDirectory` 驱动程序要求安装 `DirXML` 的服务器必须拥有待同步数据所在分区的读写（Read/Write）或主（Master）副本。`DirXML` 引擎既需要能够写入数据，也需要能够读取数据；因此，只读（Read Only）或从属引用（Subordinate Reference）副本无法工作。

让我们讨论一下如何配置 `eDirectory` 驱动程序。

## 配置 eDirectory 驱动程序

与受限文本驱动程序一样，`eDirectory` 驱动程序会随 NDS 的 `DirXML` 组件自动安装。要在 `DirXML` 系统中配置此驱动程序，你需要完成以下步骤：

> **警告**
>
> 请等到接下来的实验练习再实施此驱动程序。以下步骤是通用步骤。

- 1. 运行 Web 浏览器，通过访问 `https://your_server_IP_address/nps/iManager.html` 打开 `iManager`。
- 2. 以你的管理员用户身份进行身份验证。
- 3. 在 **DirXML Management** 角色下，选择 **Create Driver** 任务。
- 4. 在 **Create Driver Welcome** 屏幕上，选择 **In a new driver set** 选项，然后单击 **Next**。
- 5. 在 **Name** 字段中，输入你的驱动程序集（Driver Set）对象在 `eDirectory` 树中的名称。
- 6. 在 **Context** 字段中，浏览并选择你希望创建驱动程序集对象的树中的容器。
- 7. 在 **Server** 字段中，浏览并选择你要与 **Driver Set** 对象关联的服务器。
- 8. 选中 **Create a new partition on this driver set**。
- 9. 单击 **Next**。显示之前图 7.9 中所示的屏幕。
- 10. 标记 **Import a pre-configured driver from the server (XML file)**。
- 11. 从下拉列表中选择 `eDIR-Driver.xml` 驱动程序。
- 12. 单击 **Next**。显示图 7.22 中所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_329_0.png)

- 13. 在 **Driver Name** 字段中，输入此驱动程序的名称。
- 14. 在 **Remote Tree Address** 和 **Port** 字段中，输入远程树中运行 `DirXML` 的服务器 IP 地址。端口号应设置为 **8196**。
- 15. 在 **Configure Data Flow** 下拉列表中，选择本地服务器将扮演的角色。你有以下选项：
  - **Bidirectional**（双向）——选择此选项将配置驱动程序向远程树发送同步事件并接受传入的同步事件。
  - **Authoritative**（权威）——选择此选项将配置驱动程序向远程树发送同步事件，但不接受传入的同步事件。
  - **Subordinate**（从属）——选择此选项将配置驱动程序接受传入的同步事件，但不发送它们。
- 16. 在 **Configuration Option** 下拉列表中，选择你希望使用的放置选项。你可以从以下选项中选择：
  - Mirrored（镜像）
  - Flat（扁平化）
  - Department（部门）

这些选项的功能在本章前面已经介绍过。你的选择取决于你希望你的 `DirXML` 系统如何工作。配置这些放置选项的文件位于 `/usr/lib/dirxml/rules/nds2nds`。

![](img/c7771e8540507f2b00c088c7a411b57b_329_1.png)

- 17. 如果你选择了 Mirrored（镜像）选项，请在 **Remote Base Container** 字段中输入用于同步的期望基础容器。
- 18. 在 **Base Container** 字段中，输入本地树中用于同步的基础容器。如果你选择了 **Mirrored**（镜像），这是与步骤 17 中的远程基础容器进行镜像的本地基础容器。如果你选择了 **Flat**（扁平化），这是放置用户的容器。如果你选择了 **Department**（部门），这是部门容器的父容器。
- 19. 如果你选择了 **Flat**（扁平化）选项，请在 **Group Container** 字段中输入本地树中放置同步组的容器。
- 20. 选择 **Next**。显示图 7.23 中所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_330_0.png)

### 图 7.23

为 `eDirectory` 驱动程序配置安全等价性和排除项。

- 21. 通过完成以下步骤，在树中为驱动程序对象分配权限：
  - a. 选择 **Define Security Equivalences**。
  - b. 单击 **Add**。
  - c. 浏览并选择一个对树拥有管理员权限的用户对象。
  - d. 单击 **OK**。
- 22. 通过完成以下步骤，防止你的管理员用户对象被同步：
  - a. 选择 **Exclude Administrative Roles**。
  - b. 单击 **Add**。
  - c. 浏览并选择你的管理员用户对象。
  - d. 单击 **OK**。
- 23. 单击 **Next**。显示图 7.24 中所示的摘要屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_331_0.png)

- 24. 单击 **Finish with Overview**。显示 `DirXML` 概览屏幕，如图 7.25 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_331_1.png)

- 25. 重复所有这些步骤，以配置另一棵树中的服务器上的 `eDirectory` 驱动程序。
- 26. 当两个驱动程序的配置完成后，通过选择带有减号图标的红色圆圈，然后选择 **Start Driver** 来启动它们。
- 27. 等待驱动程序启动。
- 28. 当驱动程序启动后，红色圆圈会变为阴阳图标。

请记住，`eDirectory` 驱动程序是评估驱动程序。如果你不在 90 天内激活它，驱动程序将关闭。要激活驱动程序，请选择 **DirXML Overview** 页面右上角显示的 **Activation Required** 链接。

此时，你应该编辑每个服务器上每个通道的过滤器和规则，以按照你期望的方式配置数据流。请记住，`DirXML` 是事件驱动的。仅仅安装和配置驱动程序*不会*自动同步两棵树。正如你将在本章后面看到的那样，你可以最初使用 `iManager` 中的 **Migrate from eDirectory** 和 **Migrate to eDirectory** 选项来同步这两棵树。

让我们在实验练习 7.3 中练习实施 `DirXML eDirectory` 驱动程序并配置这些参数。

## 实验练习 7.3：使用 DirXML eDirectory 驱动程序

在本实验练习中，您将配置两台服务器上的 `DirXML eDirectory` 驱动程序。然后，您将测试驱动程序配置。

> 要完成此练习，您需要一台第二台计算机，该计算机能够通过网络介质与您在这本书中一直使用的服务器进行通信。这可能会给您带来挑战，您可能会想跳过此练习。但在这样做之前，请注意，您可能需要了解如何配置此驱动程序才能通过 CLE 考试。

`VMware` 在这个实验中特别有用。如果有足够的系统内存，您可以在同一台物理 PC 硬件上同时运行两个虚拟 Linux 会话。更多信息请访问 `http://www.vmware.com`。

完成以下步骤：

- 1. 获取一台满足 `NNLS` 指定要求的第二台 PC 系统。

> 确保备份您想保留的这台 PC 上的任何数据！

- 2. 在这台第二台系统上安装 `SLES 8`。将该服务器命名为 `CLE2`。
- 3. 配置服务器使用 `CLE1` 作为其主 DNS 服务器。
- 4. 配置 `CLE2` 上的 NTP 守护进程，使其与 `CLE1` 同步时间。
- 5. 下载并安装 `CLE2` 上的 `OpenSLP` 包。
- 6. 配置 `slp.conf` 文件，使 `CLE2` 成为一个目录代理 (DA)，并提供与 `CLE1` 相同的作用域。请参阅第 5 章了解具体说明。
