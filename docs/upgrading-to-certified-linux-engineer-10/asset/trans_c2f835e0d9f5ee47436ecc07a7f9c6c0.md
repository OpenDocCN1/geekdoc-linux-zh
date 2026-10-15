

选择是否要为用户配置或组配置创建一个模块。你还必须输入模块的通用名称（cn）。

# 图 11-20

![](img/8279afe915b153902294b0e58311b75a_224_0.png)

显示了用户或组模块的模板。你可以在 YaST 模式文件（/etc/openldap/schema/yast.schema）中找到列出的属性。

要编辑属性的值，请从列表中选择一行，然后选择编辑。

# 图 11-21

![](img/8279afe915b153902294b0e58311b75a_224_1.png)

在属性 **susedefaulttemplate** 的行中，指定了新用户或组的模板。如果要编辑此模板，请选择 **配置模板。**

# 图 11-22

![](img/8279afe915b153902294b0e58311b75a_225_0.png)

在上部框架中，你可以看到属性及其值的列表。使用 **编辑** 编辑模板属性值。

在下部框架中，你可以为属性指定默认值。按如下方式使用下面的三个按钮：

+   - **添加。** 添加一个新的默认值。
+   - **编辑。** 编辑所选的默认值。
+   - **删除。** 删除所选的默认值。

## 练习 11-1 使用 YaST 设置 OpenLDAP

在本练习中，你使用 YaST 设置 OpenLDAP 服务器和客户端。基本 DN 为“dc=digitalairlines,dc=com”，LDAP 管理员的通用名称为“cn=Administrator,dc=digitalairlines,dc=com”，密码为“novel”。本练习中不使用 TLS/SSL。

执行以下操作：

- 第一部分 - 安装 OpenLDAP
- 第二部分 - 设置 OpenLDAP 服务器
- 第三部分 - 设置 OpenLDAP 客户端

- 1. 从主菜单启动 YaST。
- 2. 输入 root 密码（novel）并选择确定。
- 3. 从 YaST 控制中心，选择 软件 > 软件管理。
- 4. 从筛选器下拉菜单中选择 搜索。
- 5. 在搜索字段中输入 ldap；然后选择 搜索。
- 6. 在右侧，选择以下软件包：
  - nss_ldap
  - openldap2
  - openldap2-client
  - pam_ldap
- 7. 选择 接受；然后插入请求的 SUSE Linux Enterprise Server 10 DVD。
- 8. 安装完成后，取出 DVD 并关闭 YaST 控制中心。

## 第二部分 - 设置 OpenLDAP 服务器

- 1. 启动 YaST。
- 2. 启动 YaST 模块 网络服务 > LDAP 服务器。
- 3. 选择 是 以启动 LDAP 服务器。
- 4. 选择 配置。
- 5. 在 LDAP 服务器配置对话框中选择 添加数据库 以添加数据库。
- 6. 在添加数据库对话框中输入以下信息：

# 表 11-1

| 文本框 | 值 |
|---|---|
| Base DN | dc=digitalairlines,dc=com |
| LDAP Password | novell |
| Validate Password | novell |

- 7. 选择 确定。
- 8. 在左侧框架中选择 全局设置 > TLS 设置。确保选项 TLS Active 设置为 否。
- 9. 选择 完成。

## 第三部分 - 设置 OpenLDAP 客户端

- 1. 启动 YaST 模块 网络服务 > LDAP 客户端。
- 2. 选择 使用 LDAP 以激活 LDAP 用于用户身份验证。
- 3. 确保 LDAP 服务器地址 的内容为 127.0.0.1。
- 4. 确保 LDAP 基本 DN 的内容为 dc=digitalairlines,dc=com
- 5. 确保选项 LDAP TLS/SSL 已停用。
- 6. 选择 **高级配置**。
- 7. 选择 **管理设置** 选项卡。
- 8. 在文本框 管理 DN 中输入 **cn=Administrator**。
- 9. 激活选项 **附加基本 DN**。
- 10. 激活选项 **创建默认配置对象**。
- 11. 激活选项 **本机上的主目录**。
- 12. 选择 **接受**。
- 13. 选择 **完成**。
- 14. 当要求输入管理员密码时输入 **novell**。

*（练习结束）*

- **transport.** 指定传输安全强度因子。
- **tls.** 指定 TLS 安全强度因子。
- **sasl.** 指定 SASL 安全强度因子。
- **update_*.** 指定目录更新所需的安全强度因子。
- **simple_bind.** 指定简单用户名/密码身份验证所需的安全强度因子。

有关更详细的描述，请阅读 slapd.conf 手册页（man 5 slapd.conf）中关于 sasl-secprops 的部分。

**access to.** 授予一组条目和/或属性对一个或多个请求者的访问权限。

语法：**access to objects [by requesters level control]**

**objects** 和 **requesters** 由其 DN 指定。

作为 **requesters**，你也可以使用星号表示 **everybody**。**self** 表示属性的所有者对象。你也可以通过 **dn=DN** 指定 DN 或通过 **group=DN** 指定组。

**level** 可以是：

- **read**（读取访问）
- **write**（写入访问）
- **auth**（需要身份验证）
- **none**（无访问）

示例 1：

```
access to attr=userpassword
by self write
by anonymous auth
by * none

access to *
by * read
```
