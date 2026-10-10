
## 配置证书模板

准备就绪。此练习假设您已按照之前的练习说明，在名为 `CA` 的 `lucernepublishing.com` 域中的 Windows Server 2008 Active Directory 成员服务器上安装了 Active Directory 证书服务角色。
- 以 `lucernepublishing.com` 域的默认管理员身份登录到 `CA`。
- 单击“开始”，然后选择 `Server Manager`。在左侧窗格中，展开 `Roles` 节点、`Active Directory Certificate Services` 节点和 `Certificate Templates` 节点。
- 要创建一个新的证书模板以允许用户自动注册，请右键单击 `User` 模板并单击 `Duplicate Template`。将显示“重复模板”屏幕，提示您输入此模板应支持的最小操作系统版本。
- 选择 `Windows Server 2008, Enterprise Edition` 并单击 `OK`。将显示“新模板属性”窗口。
- 在 `General` 选项卡上，在 `Template Display Name` 文本框中键入 `LUCERNEPUBLISHING-User-Cert`。验证 `Publish certificate in Active Directory` 选项旁有勾选标记，如图 13-6 所示。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_317_0.png)
- 单击 `Security` 选项卡。单击 `Domain Users`，然后在 `Read`、`Enroll` 和 `Autoenroll` 旁勾选复选框。
- 单击 `Subject Name` 选项卡。移除 `Include e-mail name in subject name` 选项旁的勾选标记。在 `Include this information in the alternate subject name` 部分，移除 `E-mail name` 旁的勾选标记。
- 单击 `Superseded Templates` 选项卡。单击 `Add`。将显示“添加已弃用模板”屏幕。
- 选择内置的 `User` 证书模板，然后连续单击 `OK` 两次以继续。
- 右键单击 `Computer` 模板并单击 `Duplicate Template`。将显示“重复模板”屏幕，提示您输入此模板应支持的最小操作系统版本。
- 选择 `Windows Server 2008, Enterprise Edition` 并单击 `OK`。将显示“新模板属性”窗口。
- 在 `General` 选项卡上，在 `Template Display Name` 文本框中键入 `LUCERNEPUBLISHING-Computer-Cert`。验证 `Publish certificate in Active Directory` 选项旁有勾选标记。
- 单击 `Security` 选项卡。单击 `Domain Computers`，然后在 `Read, Enroll, and Autoenroll` 旁勾选复选框。
- 单击 `Superseded Templates` 选项卡。单击 `Add`。将显示“添加已弃用模板”屏幕。
- 选择内置的 `Computer` 证书模板，然后连续单击 `OK` 两次以继续。
- 右键单击 `Web server` 模板并单击 `Duplicate Template`。将显示“重复模板”屏幕，提示您输入此模板应支持的最小操作系统版本。
- 选择 `Windows Server 2008, Enterprise Edition` 并单击 `OK`。将显示“新模板属性”窗口。
- 在 `General` 选项卡上，在 `Template Display Name` 文本框中键入 `LUCERNEPUBLISHING-WebServer-Cert`。验证 `Publish certificate in Active Directory` 选项旁有勾选标记。
- 单击 `Security` 选项卡。单击 `Add`。将显示“选择用户、计算机或组”屏幕。
- 单击 `Object Types`，在 `Computers` 旁勾选复选框，然后单击 `OK`。键入 `CA` 并单击 `OK`。在允许列中，在 `Enroll` 和 `Autoenroll` 旁勾选复选框。
- 单击 `Superseded Templates` 选项卡。单击 `Add`。将显示“添加已弃用模板”屏幕。
- 选择内置的 `Web Server` 证书模板，然后连续单击 `OK` 两次以继续。
- 钻取到 `Roles→Active Directory Certificate Services→lucernepublishing-CA-CA→Certificate Templates`。注意这与之前步骤中的证书模板控制台不同，尽管显示名称相似。右键单击 `Certificate Templates` 文件夹并单击 `New→Certificate Template to Issue`。将显示“启用证书模板”屏幕，如图 13-7 所示。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_318_0.png)

图 13-7

启用证书模板
- 单击 `LUCERNEPUBLISHING-User-Cert` 并单击 `OK`。
- 重复前两步，配置 `CA` 以颁发 `LUCERNEPUBLISHING-Computer-Cert` 和 `LUCERNEPUBLISHING-WebServer-Cert` 证书模板。

暂停。您可以保持登录到 `CA` 成员服务器以进行后续练习或注销。

在上一个练习中，你在 Windows Server 2008 网络中启用了多个证书模板的自动注册。在下一部分，你将配置和管理从 Windows Server 2008 CA 获取 PKI 证书的用户和计算机注册流程。

## 管理证书注册

使用 `Windows Server 2008` `CA`，你可以根据组织需求通过多种方式管理证书注册。本节介绍了可用于注册各种实体（如用户和工作站）以获取 PKI 证书的机制，以及需要专用证书的场景，例如网络设备和智能卡注册代理所使用的证书。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_319_0.png)

在 Windows Server 2008 Active Directory 环境中，你可以使用以下功能的任意组合来自动化 PKI 证书的分发：
- `证书模板`可用于通过控制与每个模板相关的安全设置来自动化 PKI 证书的分发。证书模板管理单元中的“安全”选项卡允许管理员在证书模板上配置以下任何权限：
  - `完全控制` ACL 允许用户对特定模板执行任何操作；这应仅保留给 CA 管理员。
  - `读取` ACL 允许用户或计算机读取证书模板。
  - `写入` ACL 允许用户或计算机修改证书模板；这也应保留给 CA 管理员。
  - `注册` ACL 允许用户或计算机基于此模板手动请求证书。
  - `自动注册` ACL 允许用户或计算机基于此模板自动获得证书。为了使自动注册权限生效，必须为相关用户、计算机或组配置注册权限。此外，你需要使用组策略为 Active Directory 域配置自动注册策略。
- `组策略`可用于建立 Active Directory 域的自动注册设置。与其他 GPO 设置一样，这是通过“组策略管理” MMC 管理单元进行管理的。控制 PKI 自动注册的相关设置可以在“用户配置”→`Windows 设置`→`安全设置`→`公钥策略`或“计算机配置”→`Windows 设置`→`安全设置`→`公钥策略`节点中找到。`证书服务客户端——自动注册`节点包含以下设置：
  - 自动注册证书。
  - 不自动注册证书。
  - 如果选择自动注册证书的选项，你还可以选择以下一个或多个设置：
    - 续订过期的证书，更新待处理的证书，并移除已吊销的证书。
    - 更新使用证书模板的证书。
    - 到期通知，在证书剩余生命周期仅占特定百分比时发出通知。
- `证书请求向导`允许用户使用“证书” MMC 管理单元手动创建证书请求文件；该向导创建可用于由 CA MMC 基于请求生成证书的请求文件。
- `CA Web 注册`允许用户通过 Web 界面手动请求证书，默认位于运行 CA Web 注册角色服务的 CA 上的 `https://<CA 名称>/certsrv`。

## 管理证书注册
