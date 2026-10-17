
尽管默认设置允许用户无需额外配置即可打印，但您可能希望修改其中一些设置，以便更有效地管理您的打印资源。

您可以通过执行以下操作修改设置：

- 创建额外的打印机
- 管理 `Printer Agents`
- 使用 `Printer Driver Profiles`
- 启用 `Novell iPrint Direct`
- 管理打印作业

## 创建额外的打印机

在创建额外的打印机之前，请确保满足以下先决条件：

- 拥有目标容器中其关联 `Printer` 对象将驻留的 `Supervisor` 权限。
- 被指定为控制此打印机的 `Print Manager` 的管理员。
- 正在运行 `Driver Store`。
- 正在运行 `Print Manager`。

要创建额外的打印机，请执行以下操作：

1. 从 `Novell iManager` 选择 `iPrint > Create Printer`。

请参阅图 12-28 所示内容。

![](img/9129877170834ca9d5fdac5319bf5f12_458_0.png)

Figure 12-28

2. 填写字段。

选择 `Help` 以获取字段的说明。

3. 选择 `OK`。

4. 选择 `Next`。

请参阅图 12-29 所示内容。

![](img/9129877170834ca9d5fdac5319bf5f12_458_1.png)

Figure 12-29

5. 选择此打印机的 `drivers`。

如果此打印机的打印机驱动程序未列出，您仍然可以创建打印机。

在打印机创建后，您可以将打印机驱动程序添加到 `Driver Store`，然后通过选择 `Manage Printer > Drivers` 将驱动程序关联到打印机。

这些驱动程序将在用户将来安装打印机时自动下载到用户的工作站。

由于随产品提供的打印机驱动程序列表有限，您可以将驱动程序添加到 `Driver Store`。

如果您未选择驱动程序，用户在首次在其工作站上安装此打印机时将被提示提供包含适当驱动程序的磁盘。

6. 通过选择 `Next` 创建打印机。

## 管理 Printer Agents

使用 `Novell iManager`，您可以管理 `Printer Agents`。您可以启动和关闭 `Printer Agent`，暂停和恢复输入和输出，查看打印机信息，更改配置设置，并更改打印机驱动程序。

执行以下操作：

1. 从 `Novell iManager` 选择 `iPrint > Manage Printer`。
2. 浏览并选择您想要管理的 `printer`。

请参阅图 12-30 所示内容。

![](img/9129877170834ca9d5fdac5319bf5f12_459_0.png)

Figure 12-30

3. 使用带标签的属性页（或 Firefox 中的下拉列表）完成适当的任务。

## 使用 Printer Driver Profiles

`Printer driver profiles` 允许您为 Windows 打印机驱动程序设置驱动程序默认值。然后将打印机驱动程序配置文件关联到打印机，以便在安装打印机时使用您想要的设置进行配置。

例如，在一家律师事务所中，您可能希望默认纸张尺寸为法律尺寸。这意味着每当打印机和相应驱动程序安装在工作站上时，纸张尺寸都会设置为法律尺寸。

要使用打印机驱动程序配置文件，您需要知道如何执行以下操作：

- 创建、修改和删除打印机驱动程序配置文件
- 将打印机驱动程序配置文件与打印机关联

### 创建、修改和删除打印机驱动程序配置文件

在创建打印机驱动程序配置文件时，您直接使用特定于平台的打印机驱动程序。因此，您需要从与打印机驱动程序相同的操作系统平台创建和修改配置文件。

例如，要创建或修改 Windows 2000 打印机驱动程序配置文件，您必须从 Windows 2000 工作站访问 `Novell iManager` 并完成任务。

执行以下操作：

1. 从 `Novell iManager` 选择 `iPrint > Printer Driver Profile`。
2. 浏览并选择您想要存储驱动程序配置文件并使其可供该管理器上的打印机使用的 `Print Manager`。
3. 选择以下其中一项：
   - `Create Printer Driver Profile`—创建新的打印机驱动程序配置文件。
   - `Delete Printer Driver Profile`—删除现有的打印机驱动程序配置文件。
   - `Modify Printer Driver Profile`—更改现有打印机驱动程序配置文件的设置。
4. 选择 `OK`。

### 将打印机驱动程序配置文件与打印机关联

在创建打印机驱动程序配置文件后，您需要将其与打印机关联。执行以下操作：

1. 从 `Novell iManager` 选择 `iPrint > Manage Printer`。
2. 浏览并选择您想要修改的 `printer`。
3. 选择 `Drivers > printer_driver_operating_system`。
4. 从 `Available Drivers` 列表中选择打印机驱动程序。
5. 从所选驱动程序的 `Available Driver Profiles` 列表中选择您想要与此打印机关联的 `profile`。

如果您不希望关联配置文件，请选择 `None`。

6. 通过选择 `OK` 保存更改。

## 启用 Novell iPrint Direct

`Novell iPrint Direct` 启用的打印机的用户会直接将打印作业发送到打印机，而不是先发送到 `Print Manager`。作业会以 `LPR` 或原始 `9100` 格式发送到打印机，具体取决于打印机网关自动加载命令的设置。

![](img/9129877170834ca9d5fdac5319bf5f12_460_0.png)

尽管这大大减少了服务器通信，但审计打印作业的能力就丢失了。`Novell iPrint Direct` 仍然支持驱动程序更新，并且打印机信息是通过 SNMP 直接从打印机收集的。

执行以下操作：

1. 在 `Novell iManager` 中，选择 `iPrint > Manage Printer`。
2. 浏览并选择要启用 `Novell iPrint Direct` 打印的 `printer`。
3. 选择 `Client Support > Novell iPrint Direct`。
4. 选择 `Enable iPrint Direct Printing` 选项。

## Manage Print Jobs

以下提供了 `Novell iPrint` 的打印作业管理功能信息：

- View Print Job Information
- Delete Print Jobs
- Change the Order of Print Jobs

被指定为打印机管理员或操作员的用户可以对路由到该打印机的所有作业执行这些任务；单个作业所有者只能对其自己的打印作业执行这些任务。

### View Print Job Information

您可以通过执行以下操作查看特定打印机等待处理的单个打印作业的信息：

1. 在 `Novell iManager` 中，选择 `iPrint > Manage Printer`。
2. 浏览并选择作业发送到的 `printer`。
3. 选择 `Printer Control > Jobs`。

打印作业信息将显示出来。

### Delete Print Jobs

管理员可以在作业尚未开始打印后提交时删除任何打印作业。用户只能删除自己的打印作业。

执行以下操作：

1. 在 `Novell iManager` 中，选择 `iPrint > Manage Printer`。
2. 浏览并选择作业发送到的 `printer`。
3. 选择 `Printer Control > Jobs`。
4. 选择要删除的作业旁边的 `check box`。
5. 选择 `Delete`。

### Change the Order of Print Jobs

有时，您可能需要将作业提前打印，排在已提交到打印机但尚未开始打印的其他作业之前。管理员、管理员和操作员可以移动任何作业在列表中的位置。用户只能移动自己的作业，并且只能将其向下移动。

执行以下操作：

1. 在 `Novell iManager` 中，选择 `iPrint > Manage Printer`。
2. 浏览并选择作业发送到的 `printer`。
3. 选择 `Printer Control > Jobs`。
4. 选择要修改的作业旁边的 `check box`。
5. 通过选择 `Promote` 将打印作业向上移动。

## Install the Novell iPrint Client
