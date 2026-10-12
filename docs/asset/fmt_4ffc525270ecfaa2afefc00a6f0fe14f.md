
## 实验室练习 11.1：配置虚拟办公室

在本练习中，您将配置服务器上的虚拟办公室。然后，您配置一个虚拟团队并邀请用户加入。

> **警告**
>
> 由于虚拟办公室依赖于其他所有 NNLS 组件，您必须在尝试此实验室练习之前完成本书至此为止的所有练习。如果您尚未完成前面的练习，请先回去完成它们，然后再开始此练习。

完成以下步骤：

- 1. 通过执行以下步骤配置虚拟办公室 SMTP 服务器参数：
    - a. 打开浏览器窗口并导航到 `https://your_server_IP_address/nps/iManager.html`。
    - b. 使用密码 `novell` 以 `admin` 身份验证到 iManager。
    - c. 在左侧框架中，向下滚动到 `虚拟办公室` 角色。
    - d. 选择 `环境管理` 任务。
    - e. 验证 `启用团队创建` 是否设置为 `开`。
    - f. 在 `SMTP 地址` 行上，点击 `编辑`。
    - g. 在 `SMTP 地址` 字段中，输入服务器的 IP 地址。这将配置虚拟办公室通过您的 NetMail 服务器发送通知消息。
    - h. 在 `用户名` 字段中，输入 `admin`。这将配置通知发送到您的 admin 用户的电子邮件帐户。
    - i. 在 `密码` 字段中，输入 `novell`。
    - j. 点击 `确定`。
    - k. 点击 `保存`。
    - l. 点击 `确定`。

- 2. 通过完成以下步骤配置您的公司信息字段：
    - a. 在 iManager 中，选择 `服务管理` 任务。
    - b. 验证 `主页公司信息` 是否已启用。

### 3. 通过完成以下步骤，为 Novell 支持网站添加全局书签：
- a. 在 iManager 中，选择 `服务管理`。
- b. 选择 `书签` 选项卡。
- c. 在 `当前书签` 下，点击 `添加`。
- d. 在 `名称` 字段中，输入 `Novell 支持`。
- e. 在 `URL` 字段中，输入 `http://support.novell.com`。
- f. 点击确定。
- g. 再次点击确定。
- h. 点击 `退出` 图标。

> **提示** 如果您未退出 iManager，系统将自动以管理员用户身份将您认证到 Virtual Office。

### 4. 以 Jim Jackson 身份访问 Virtual Office 并通过完成以下内容创建一个虚拟团队：
- a. 打开第二个浏览器窗口，并导航至 `https://your_server_IP_address/vo`。
- b. 使用密码 `novell` 以 `JJackson` 的身份认证到 Virtual Office。
- c. 在 `虚拟团队任务` 下，选择 `创建虚拟团队`。
- d. 在 `名称` 字段中，输入 `Perpetual Motion Core Team`。
- e. 在 `描述` 字段中，输入 `Virtual collaboration team for the Perpetual Motion core team`。
- f. 点击 `创建`。
- g. 当提示团队已创建且 JJackson 为团队所有者时，点击确定。
- h. 在 `我的虚拟团队` 下，选择 `Perpetual Motion Core Team`。将显示 `Perpetual Motion Core Team` 主页。

> **警告** 如果您的浏览器中未安装兼容的 Java 虚拟机插件，系统将提示您下载它。如果是这种情况，请按照提示下载 Sun Java 虚拟机。如果您使用的是 Mozilla，请务必下载该插件的 Mozilla 版本。

### 5. 通过完成以下步骤，邀请 `Christopher Grayson` 和 `Diana Nelson` 加入虚拟团队：
- a. 在 `团队成员身份` 下，选择 `邀请用户`。
- b. 点击 `添加`。
- c. 点击 `搜索`。
- d. 按住 `Ctrl` 键并选择 `CGrayson` 和 `DNelson` 用户。
- e. 点击 `添加`。
- f. 点击 `发送`。
- g. 选择 `显示团队成员`。请注意，Christopher Grayson 和 Diana Nelson 并未出现在列表中。他们需要先接受邀请。

### 6. 通过完成以下步骤接受参与团队的邀请：
- a. 在 `Virtual Office` 中，选择 `登出`。
- b. 使用密码 `novell` 以 `CGrayson` 身份登录。
- c. 在左侧窗格中，选择 `管理虚拟团队`。
- d. 在 `虚拟团队` 收件箱中，选择 `Perpetual Motion Core Team [Invitation]`。
- e. 点击 `加入`。
- f. 在 `我的虚拟团队` 下，选择 `Perpetual Motion Core Team`。

### 7. 通过完成以下内容配置 `CGrayson` 的通知偏好设置：
- a. 在 `团队成员身份` 下，选择 `设置通知偏好`。
- b. 在 `通知偏好` 下，选择所有事件。
- c. 点击 `保存`。
- d. 当提示偏好设置已保存时，点击 `确定`。
- e. 点击 `登出`。

### 8. 作为 JJackson，通过完成以下步骤为虚拟团队提供项目信息：
- a. 使用密码 `novell` 重新登录为 JJackson。
- b. 选择 `Perpetual Motion Core Team`。
- c. 在 `文件` 下，选择 `上传`。
- d. 在 `上传文件` 字段中，浏览并选择一个文件。
- e. 点击 `上传`。
- f. 当提示文件已上传时，点击 `关闭`。文件将出现在 `文件` 区域。
- g. 选择 `显示团队日历`。
- h. 在 `事件` 下，选择 `新建`。
- i. 在 `主题` 字段中，输入 `核心团队会议`。
- j. 将日期设置为明天的日期。
- k. 将时间设置为上午 8:00。
- l. 勾选 `包含时间`。
- m. 在 `地点` 字段中，输入 `会议室 B`。
- n. 在 `消息` 字段中，输入 `有人带点百吉饼！`。
- o. 点击 `保存`。
- p. 当提示事件已创建时，点击 `关闭`。
- q. 选择 `Perpetual Motion Core Team`。
- r. 在 `讨论` 字段中，选择 `新消息`。
- s. 在 `主题` 字段中，输入 `市场营销问题`。
- t. 在 `消息` 字段中，输入 `我们打算如何营销我们的新永久运动引擎？`。
- u. 点击 `发布`。
- v. 点击 `登出`。

### 9. 登录为 CGrayson 并通过完成以下步骤查看 JJackson 提供的信息：
