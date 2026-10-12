
双击 `EMPNO` 字段打开字段属性对话框。勾选该框以启用“外部数据源”（External data source）。在“数据源选项”（Data Sources Options）旁边选择“浏览”（Browse）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_330_0.png)

图 5-75 Domino Designer：浏览 `DB2 EMPNO`

对于“数据连接资源”（Data Connection Resource）选择 `DB2`；对于“表”（Table）选择 `ADMINATOR.EMPLOYEE`；对于“列”（Columns）选择 `EMPNO`；然后点击 `OK`。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_331_0.png)

图 5-76 Domino Designer：选择 `EMPNO` 字段

在属性对话框的最底部，选择“键字段”（Key Field）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_332_0.png)

图 5-77 Domino Designer：`FIRSTNAME` 属性

关闭属性对话框，双击 `FIRSTNAME` 字段以打开该字段的属性对话框。启用“外部数据源”（External data source）；在“数据源选项”（Data Source Options）旁边选择`浏览`（Browse）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_333_0.png)

图 5-78 Domino Designer：浏览 `DB2 FIRSTNAME`

对于“数据连接资源”选择 `DB2`；对于“表”选择 `ADMINISTRATOR.EMPLOYEE`；对于“列”选择 `FIRSTNAME`；然后点击 `OK`。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_334_0.png)

回到属性对话框，启用“本地存储数据”（Store data locally）。这允许你在视图中查看数据。

关闭属性对话框，双击 `LASTNAME` 字段以打开该字段的属性对话框。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_335_0.png)

在“数据源选项”（Data Source Options）旁边启用“外部数据源”（External data source），并选择“浏览”（Browse）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_336_0.png)

图 5-81 Domino Designer - `LASTNAME` 数据选择

对于“数据连接资源”选择 `DB2`；对于“表”选择 `ADMINATOR.EMPLOYEE`；对于“列”选择 `LASTNAME`；然后点击 `OK`。回到属性对话框，启用“本地存储数据”（Store data locally）。这允许你在视图中查看数据。

对于 `EmployeeForm` 中的所有剩余字段，重复上述步骤：启用“外部数据源”（External data source），在“数据源选项”（Data Source Options）旁边选择“浏览”（Browse）。在属性对话框中，启用“本地存储数据”（Store data locally）。这允许你在视图中查看数据。

## Lotus Designer Rnext

显示内容：常用任务的快捷链接

- 创建一个新数据库
- 打开一个已有的数据库

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_325_0.png)

图 5-68 Domino Designer：创建新数据库

在 `Domino Designer` 中，选择“创建新数据库”。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_325_1.png)

图 5-69 Domino Designer：新数据库

对于服务器，输入你刚刚完成 `Domino for Linux` 安装以及 `DB2 for Linux` 安装的 `Domino 6` 服务器的名称。如果这是一个生产环境应用，`Domino` 和 `DB2` 服务器可能不会安装在同一台机器上。

为你的应用程序选择一个名称。我们选择了 `DB2EMP`。此应用的 `Domino 6` 模板具有相同的名称。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_326_0.png)

图 5-70 Domino Designer：数据连接

在 `Designer` 的左侧面板中，在“最近数据库”（Recent Databases）下选择“共享资源”（Shared Resources） -> “数据连接”（Data Connections） -> “新建数据连接资源”（New Data Connection Resources）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_326_1.png)

图 5-71 Domino Designer：`DB2` 数据连接

在数据连接对话框中，输入 `DB2` 的名称。在“类”（Class）和“类型”（Type）分别输入 `RDBMS` 和 `DB2`。在“用户名”（User Name）输入 `Administrator` 或适用于你 `DB2` 安装的账户，并在“密码”（Password）字段中提供密码。“数据库”（Database）输入 `SAMPLE`，然后点击“浏览元数据”（Browse Metadata）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_327_0.png)

图 5-72 Domino Designer：浏览 `Administrator.Employee`

在“浏览外部元数据”（Browse External Metadata）对话框中，选择“表”（Table）为 `ADMINISTRATOR.EMPLOYEE`，然后点击 `OK` 关闭对话框。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_328_0.png)

图 5-73 Domino Designer：`Employee` 表单

接下来，选择导航面板中的“表单”（Forms）图标，然后选择 `EmployeeForm`。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_329_0.png)

图 5-74 Domino Designer：`EMPNO` 字段属性

双击 `EMPNO` 字段打开字段属性对话框。勾选该框以启用“外部数据源”（External data source）。在“数据源选项”（Data Sources Options）旁边选择“浏览”（Browse）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_330_0.png)

图 5-75 Domino Designer：浏览 `DB2 EMPNO`

对于“数据连接资源”（Data Connection Resource）选择 `DB2`；对于“表”（Table）选择 `ADMINATOR.EMPLOYEE`；对于“列”（Columns）选择 `EMPNO`；然后点击 `OK`。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_331_0.png)

图 5-76 Domino Designer：选择 `EMPNO` 字段

在属性对话框的最底部，选择“键字段”（Key Field）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_332_0.png)

图 5-77 Domino Designer：`FIRSTNAME` 属性

关闭属性对话框，双击 `FIRSTNAME` 字段以打开该字段的属性对话框。启用“外部数据源”（External data source）；在“数据源选项”（Data Source Options）旁边选择`浏览`（Browse）。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_333_0.png)

图 5-78 Domino Designer：浏览 `DB2 FIRSTNAME`

对于“数据连接资源”选择 `DB2`；对于“表”选择 `ADMINISTRATOR.EMPLOYEE`；对于“列”选择 `FIRSTNAME`；然后点击 `OK`。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_334_0.png)

回到属性对话框，启用“本地存储数据”（Store data locally）。这允许你在视图中查看数据。

关闭属性对话框，双击 `LASTNAME` 字段以打开该字段的属性对话框。

![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_335_0.png)

在“数据源选项”（Data Source Options）旁边启用“外部数据源”（External data source），并选择“浏览”（Browse）。
