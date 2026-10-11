

![图 7.7](img/c7771e8540507f2b00c088c7a411b57b_313_0.png)

**图 7.7**
DirXML 创建驱动向导。

![图 7.8](img/c7771e8540507f2b00c088c7a411b57b_313_1.png)

**图 7.8**
定义 DirXML 驱动集属性。

- 5. 在 **名称（Name）** 字段中，输入您的驱动集（Driver Set）对象在 eDirectory 树中的名称。
- 6. 在 **上下文（Context）** 字段中，浏览并选择您希望在树中创建驱动集对象的容器。
- 7. 在 **服务器（Server）** 字段中，浏览并选择您希望与驱动集对象关联的服务器。
- 8. 勾选 **在此驱动集上创建新分区（Create a new partition on this driver set）**。

> **警告** 默认情况下，创建驱动向导会在 eDirectory 树中的 DirXML 驱动集对象上创建一个新分区。这样做是为了确保该驱动集对象分区的主副本（Master replica）保留在安装了 DirXML 的服务器上。

如果您取消选中此选项，DirXML 仍会正常运行。但是，如果您将驱动集对象所在分区的所有副本移动到另一台服务器，DirXML 将停止工作。

在多服务器环境中，您应该将此分区在多台服务器之间进行复制，以提高容错能力。

- 9. 点击“下一步”。将出现如图 7.9 所示的屏幕。

![图 7.9](img/c7771e8540507f2b00c088c7a411b57b_314_0.png)

**图 7.9**
选择 DirXML 驱动。

- 10. 标记 **从服务器导入预配置的驱动（.XML 文件）（Import a pre-configured driver from the server (.XML file)）**。
- 11. 从下拉列表中，选择 **DelimitedTextCSVSample.XML** 驱动。
- 12. 点击“下一步”。将出现如图 7.10 所示的屏幕。

![图 7.10](img/c7771e8540507f2b00c088c7a411b57b_314_1.png)

**图 7.10**
配置 DirXML 分隔文本驱动。

- 13. 在 **驱动名称（Driver Name）** 字段中，输入您的分隔文本驱动的名称。
- 14. 在 **输出目录（Output Directory）** 字段中，输入本地文件系统中驱动输出文件将被创建和存储的目录路径。如果该目录不存在，您必须在启动驱动之前创建它。
- 15. 在 **输入目录（Input Directory）** 字段中，输入本地文件系统中输入文件将存储的目录路径。如果该目录不存在，您必须在启动驱动之前创建它。
- 16. 在 **用户容器（User Container）** 字段中，输入您希望驱动创建的用户在树中存储的容器。如果该容器不存在，您必须在启动驱动之前创建它。

> **用户容器（User Container）** 字段要求您使用一种与本书中所学截然不同的格式来输入值。而不是 edirectory 格式或 LDAP 格式，此字段要求您使用类似文件系统目录路径的斜杠格式来输入容器。
>
> 例如，如果您想将用户放置在 **IF.CLE** 容器中，您应在此字段中输入 **/CLE/IF**。请注意，您使用的是斜杠，而不是点号或逗号。此外，请注意方向已改变。不是从树中最低的对象开始并向上追溯到树根，而是从最顶层的容器开始并向下追溯到用户将驻留的容器。

- 17. 点击 **下一步（Next）**。将显示如图 7.11 所示的屏幕。

![图 7.11](img/c7771e8540507f2b00c088c7a411b57b_315_0.png)

- 18. 通过完成以下步骤，为树中的驱动对象分配权限：
    - a. 选择 **定义安全等价物（Define Security Equivalences）**。
    - b. 点击 **添加（Add）**。
    - c. 浏览并选择一个用户对象，该对象在树中具有对该容器的 Supervisor 权限，或者具有 Browse、Create、Delete 和 Rename 权限（该容器是用户对象将被创建的地方，同时也包含驱动集对象）。您创建的驱动对象将获得分配给此用户对象的 eDirectory 权限。
    - d. 点击 **确定（OK）**。
- 19. 通过完成以下步骤，防止您的 admin 用户对象被同步：

> **由于 admin 不代表实际的员工，因此您不应该将其复制到 DirXML 系统中的其他数据库。例如，您不希望 admin 出现在 PeopleSoft 数据库或 PBX 系统中。**
>
> **此外，根据您的规则和过滤器配置方式，您可能无意中会将来自其他数据库的更改同步到 admin 用户对象，从而可能导致该对象在树中无法使用。**

    - a. 选择 **排除管理角色（Exclude Administrative Roles）**。
    - b. 点击 **添加（Add）**。
    - c. 浏览并选择您的 admin 用户对象。
    - d. 点击 **确定（OK）**。
- 20. 点击 **下一步（Next）**。将显示如图 7.12 所示的摘要屏幕。

![图 7.12](img/c7771e8540507f2b00c088c7a411b57b_316_0.png)

**图 7.12**
DirXML 创建驱动摘要屏幕。

- 21. 点击 **完成并显示概览（Finish with Overview）**。将显示 DirXML 概览屏幕，如图 7.13 所示。

### 使用 DirXML 同步用户身份

**图 7.13**
包含已停止驱动的 DirXML 概览。

![图 7.13](img/c7771e8540507f2b00c088c7a411b57b_317_0.png)

- 22. 通过选择带减号图标的红色圆圈，然后选择 **启动驱动（Start Driver）** 来启动驱动。
- 23. 等待驱动启动。
- 24. 当驱动启动后，红色圆圈将变为阴阳图标，如图 7.14 所示。

**图 7.14**
包含已启动驱动的 DirXML 概览。

![图 7.14](img/c7771e8540507f2b00c088c7a411b57b_317_1.png)

请记住，分隔文本驱动是一个评估驱动。如果您未在 90 天内激活它，驱动将关闭。要激活驱动，请选择 **DirXML 概览（DirXML Overview）** 页面右上角显示的 **需要激活（Activation Required）** 链接，如图 7.15 所示。您将进入 Novell 网站，在那里您可以注册。按照网页上显示的提示完成激活。

![图 7.15](img/c7771e8540507f2b00c088c7a411b57b_318_0.png)

**图 7.15**
激活驱动。

让我们在实验练习 7.1 中练习在您的服务器上实施使用分隔文本驱动的 DirXML。

## 实验练习 7.1：使用 DirXML 分隔文本驱动

在这个实验中，您将在服务器上配置 DirXML 分隔文本驱动。然后，您将测试您的驱动配置。完成以下步骤：

- 1. 打开终端会话，通过输入 `su -` 并提供密码 `novell` 更改为 root 用户帐户。
- 2. 在 shell 提示符下，通过输入以下命令在您的 `/tmp` 目录中创建输入和输出目录：
    - `mkdir /tmp/DirXML`
    - `mkdir /tmp/DirXML/Input`
    - `mkdir /tmp/DirXML/Output`
- 3. 运行 web 浏览器，通过导航到 `https://your_server_IP_address/nps/Manager.html` 打开 iManager。
- 4. 使用密码 `novell` 以 admin 身份进行身份验证。
- 5. 使用 eDirectory 管理角色下的“创建对象”任务，在 **IFICLE** 中创建一个名为 **DirXMLUsers** 的组织单元（Organizational Unit）。
- 6. 在 DirXML 管理角色下，选择“创建驱动”任务。
- 7. 在“创建驱动欢迎”屏幕上，选择 **在一个新的驱动集中（In a new driver set）** 选项，然后点击 **下一步（Next）**。
- 8. 在 **名称（Name）** 字段中，输入 **CLEDriverSet**。
- 9. 在 **上下文（Context）** 字段中，输入 **IFICLE**。
- 10. 在 **服务器（Server）** 字段中，输入 **CLE1.IFICLE**。
- 11. 勾选 **在此驱动集上创建新分区（Create a new partition on this driver set）**，然后点击 **下一步（Next）**。
- 12. 标记 **从服务器导入预配置的驱动（.XML 文件）（Import a pre-configured driver from the server (.XML file)）**。
- 13. 从下拉列表中，选择 **DelimitedTextCSVSample.XML** 驱动，然后点击 **下一步（Next）**。
- 14. 保留 **驱动名称（Driver Name）** 字段中的默认名称。
- 15. 在 **输出目录（Output Directory）** 字段中，输入 `/tmp/DirXML/Output`。
- 16. 在 **输入目录（Input Directory）** 字段中，输入 `/tmp/DirXML/Input`。
- 17. 在 **用户容器（User Container）** 字段中，输入 `CLE1\IFC\DirXMLUsers`。
- 18. 点击 **下一步（Next）**。
- 19. 通过完成以下步骤，为树中的驱动对象分配权限：
    - a. 选择 **定义安全等价物（Define Security Equivalences）**。
    - b. 点击 **添加（Add）**。
    - c. 浏览并选择 **admin.IFCLE**。
    - d. 点击 **确定（OK）**。
- 20. 通过完成以下步骤，防止您的 admin 用户对象被同步：
    - a. 选择 **排除管理角色（Exclude Administrative Roles）**。
    - b. 点击 **添加（Add）**。
    - c. 浏览并选择 **admin.IFCLE**。
    - d. 点击 **确定（OK）**。
    - e. 点击 **下一步（Next）**。
- 21. 点击 **完成并显示概览（Finish with Overview）**。
- 22. 注意驱动并未运行。暂不要启动它。相反，选择分隔文本驱动图标。将显示如图 7.16 所示的屏幕。

![图 7.16](img/c7771e8540507f2b00c088c7a411b57b_320_0.png)

**图 7.16**
驱动概览。

- 23. 通过完成以下步骤，检查订阅者通道上的架构映射规则：
    - a. 在订阅者通道上，选择架构映射规则。
    - b. 注意只有用户对象类被映射。选择 **属性（Properties）**。将显示如图 7.17 所示的屏幕。

