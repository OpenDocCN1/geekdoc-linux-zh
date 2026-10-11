

![](img/c7771e8540507f2b00c088c7a411b57b_282_0.png)

```
base-name=CLE
admin-fdn=admin.cn.our.if.o=CLE
preferred-server=192.168.1.36
positive-time-to-live=600
run-threads=5
schemas=f2307
enable-persistent-cache=YES
user-hash-size=211
group-hash-size=211
persistent-cache-entries-aging-interval=36000
persistent-cache-refresh-period=28800
persistent-cache-refresh-flag=all
create-home=no
type-of-authentication=2
certificate-file=gyesder
ldap-ssl-port=636
ldap-port=389
support-alias-names=no
support-outside-base-context=no
```

/*etc/nam.conf* $9L, 46%$

本文件中的参数解释见表 6.3。

### namcd 配置参数

| 参数 | 说明 |
| :--- | :--- |
| base-name | 此参数标识 LUM 安装所在的 eDirectory 树中的基础容器。 |
| admin-fdn | 此参数指定 eDirectory 树管理员用户的名称。 |
| preferred-server | 此参数列出 namcd 守护进程要使用的 eDirectory LDAP 服务器的 IP 地址。 |
| positive-time-to-live | 此参数指定对象信息在 namcd 守护进程的缓存中保留的时间（以秒为单位）。此值范围为 **1** 到 **2147483647** 秒。默认值为 **600**。如果您的树是静态的，您可以增加此值，因为从缓存读取比从树中读取快得多。但是，如果您的树经常发生变化，您可能希望保持当前值甚至降低它。这样做是为了确保缓存中的数据与当前树数据匹配。 |
| num-threads | 此参数标识守护进程并发使用的 CPU 线程数。默认值为 **5**。此参数可设置为 **1** 到 **25** 个线程之间的值。 |
| Schema | 此参数标识守护进程配置要使用的树的 eDirectory 模式版本。 |
| enable-persistent-cache | 此参数启用或禁用 ncsd 守护进程的缓存。 |
| user-hash-size | ncsd 守护程序使用哈希算法加密其缓存中的数据。此参数指定哈希大小。Novell 建议您使用等于或大于树中用户数量 0.25 倍的质数值。默认值为 **211**。 |
| group-hash-size | 此参数与前面的参数相同，但适用于组。推荐值相同：树中组数量的 0.25 倍。默认值为 **211**。 |
| persistent-cache-entries-aging-interval | 此参数指定时间间隔（以秒为单位），之后 ncsd 守护进程缓存中的信息将从持久缓存中移除。此值范围为 **1** 到 **2147483647** 秒。默认值为 **7200**。 |
| persistent-cache-refresh-period | 此参数指定 ncsd 守护程序从 eDirectory 刷新缓存中信息的频率（以秒为单位）。此值范围为 **1** 到 **2147483647** 秒。默认值为 **28800**。 |
| persistent-cache-refresh-flag | 此参数指定在刷新期间，是否将所有用户和组信息包含在缓存中，还是仅包含当前正在使用的信息。默认值为 **all**。另一个可能的值为 **accessed**。 |
| create-home | 指定是否为创建用户的主目录。此值可以是 **yes** 或 **no**。默认值为 **no**。 |
| type-of-authentication | 此参数指定是否使用 SSL（2）或不使用（1）。默认值为 1。 |
| Certificate-file-type | 此参数指定若配置了 SSL，则使用的证书文件的格式。值可以是 **der** 或 **base64**。默认值为 **der**。 |
| ldap-ssl-port | 此参数列出 eDirectory 服务器上 LDAP 正在使用的安全 IP 端口。默认值为 636。 |
| ldap-port | 此参数列出 eDirectory 服务器上 LDAP 正在使用的不安全端口。默认值为 **389**。 |
| support-alias-name | 此参数标识是否允许指向树中常规用户和组的 eDirectory 别名对象。默认值为 **no**。 |
| support-outside-base-context | 此参数指定是否允许以前配置的基础范围之外的对象使用 LUM。默认值为 **no**。 |

如图 6.17 所示，NNLS 安装脚本会自动配置您的系统，通常不需要额外的配置——假设您输入了正确的信息。

现在让我们看看如何在您的系统上启用 LUM 功能。

## 设置 LUM

LUM 是一个高度灵活的产品，允许您以多种不同方式配置系统。对于 CLE 认证，您只需知道如何执行基本配置，而我们将在此重点关注这一点。

要在系统上执行 LUM 的基本配置，请执行以下步骤：

> **注意** 这是一组通用步骤。我们将在接下来的实验室练习中详细介绍步骤。

1. 在 Web 浏览器中，导航到 `https://your_server_IP_address/nps/iManager.html`。
2. 以 **admin** 用户身份登录到 iManager。
3. 创建用于 LUM 访问的组。您可以创建一个组或多个组。为此，请完成以下步骤：
   - a. 在 iManager 中，向下滚动到 **eDirectory Administration** 角色并选择 **Create Object**。
   - b. 在 **Available Object Classes** 字段中，选择 **Group** 然后单击 **OK**。
   - c. 在 **Group Name** 字段中，输入您的组名。
   - d. 在 **Context** 字段中，输入您希望该组驻留的位置，然后单击 **OK**。
   - e. 当提示组已创建时，单击 **OK**。
   - f. 当提示将组转换为 LUM 组时，单击 **Cancel**。您将在稍后转换该组。
4. 通过执行以下步骤，将您希望使用 eDirectory 认证到 Linux 系统的用户填充到新组中：
   - a. 在 iManager 中，选择 **Modify Object**。
   - b. 在 **Object Name** 字段中，输入您的组名。
   - c. 在下拉列表中，选择 **Members**。
   - d. 在 **Members** 字段中，浏览并选择您希望包含在组中的每个用户对象。
   - e. 单击 **OK**。
5. 通过执行以下步骤将组转换为 LUM 组：
   - 1. 在左侧框架中，向下滚动到 **Linux User Management** 角色并选择 **Convert eDirectory Group to LUM Group**。
   - 2. 在 **Select Group** 字段中，浏览并选择您的组然后单击 **OK**。
   - 3. 当提示选择要添加该组的工作站时，选择 **Linux Workstations**。
   - 4. 在 **Linux Workstations** 字段中，浏览并选择您的 UNIX Workstation 对象然后单击 **OK**。
   - 5. 当提示 LUM 组已创建时，单击 **OK**。
6. 通过执行以下步骤将组中的每个用户转换为 LUM 用户：
   - 1. 在 **Linux User Management** 角色下，选择 **Convert eDirectory User to LUM User**。
   - 2. 在 **Select User** 字段中，浏览并选择组中的第一个用户然后单击 **OK**。
   - 3. 当提示指定用户的主组时，浏览并选择您的组。
   - 4. *取消选中*将用户转换为 Samba 用户对象的选项；然后单击 **OK**。
   - 5. 选择 **Repeat Task**。
   - 6. 对组中的每个用户重复这些步骤。

通过执行以下步骤测试配置：

1. 如果您在图形环境中运行，请按 **Ctrl+Alt+F2** 切换到 shell 提示符。如果您正在使用没有 X Window 系统的基于文本的 shell 提示符，请按 **Alt+F2**。
2. 在登录提示符处，输入已转换组中用户对象的用户名。不要包含对象的位置（context）。例如，如果您想要认证为 DCoughanour.SLC.CLE，您只需输入 **DCoughanour**。
3. 在密码提示符处提供该用户的密码。您应该看到一条消息，表明正在 */home* 中为用户创建新的主目录。

这就完成了！在实验室练习 6.2 中，您可以在服务器上配置 LUM。

