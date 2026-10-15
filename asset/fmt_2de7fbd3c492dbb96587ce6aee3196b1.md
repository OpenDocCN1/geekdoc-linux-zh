
# iSeries for Linux 与 Kerberos 配置指南

## 1. 环境要求

`iSeries for Linux` 需要 `Kerberos` 版本 5。你可以使用 `Heimdal` 或 `MIT` 的 `Kerberos` 实现。几乎每个 Linux 发行版都包含了至少一种实现性的安装包。

## 2. PAM 认证配置

Linux 还支持使用可插拔认证模块 (`PAM`) `pam_krb` 将 `Kerberos` 作为初始登录方法。在这种情况下，`Kerberos` 用于 Linux 本地密码文件的 Linux 用户认证。对于我们的示例，我们不需要将 Linux 认证更改为 `Kerberos`，但它可以作为你环境中的另一种备用 `Kerberos` 登录方法。如果你计划使用 `pam_krb5`，请参考你发行版中关于设置的文档。

## 3. 必需组件

在 Linux 系统上安装 `Kerberos5` 及其实用工具后，你必须至少拥有以下 `Kerberos` 命令：

- `kinit`
- `klist`
- `kpasswd`

你必须拥有 `Kerberos5` 配置文件，即 `/etc/krb5.conf`。

## 4. 配置文件自定义

`krb5.conf` 包含了基础 `kerberos5` 配置，并要求根据你的环境进行自定义。需要以下关于你的 `Active Directory` 的信息：

- `Kerberos` 术语中的 Windows 登录域：默认 realm (default realm)
- Windows 服务器（域控制器）的 DNS 名称，提供以下功能：密钥分配中心 (`KDC`) 和密码服务器

如果你不确定此配置，可以在 `i5/OS` 现有的 `Kerberos` 配置中进行验证。在 IBM `i5/OS` 上，`Kerberos` 服务被称为网络认证服务 (`NAS`)，设置位于与 Linux 类似的文件中：

```
/IBM/UserData/OS400/NetworkAuthentication/krb5.conf
```

由于 `Kerberos` 和 `EIM` 必须在 IBM `i5/OS` 上已经配置，该文件必须类似于示例 2-4。双问号和括号是括号的替换，将 `??` 替换为 `<` 和 `??`，而双问号和箭头替换大括号，将 `??` 替换为 `<` 和 `>>`。

### 示例 2-4：IBM i/OS Kerberos 配置

```
<libdefaults>
default_keytab = /QIBM/UserData/DS400/NetworkAuthentication/keytab/krb5.keytab
default_realm = \ITSODOMAIN.TEST
<realms>
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test:88
kpasswd_server = master.itsodomain.test:464
}
<domain_realm>
.itso.rbm = ITSODOMAIN.TEST
<capaths>
```

示例 2-4 显示了表 2-2 中使用的设置。

| 表 2-2 IBM i/OS Kerberos 配置设置 | | |
|---|---|---|
| 说明 | 参数 | 值 |
| Kerberos Realm/我们的 Active Directory 名称 | `default_realm` | `ITSODOMAIN.TEST` |
| KDC/我们的 Active Directory 服务器 | `kdc` | `master.itsodomain.test` |
| 密码服务器/与我们的 KDC 服务器相同 | `kpasswd_server` | `master.itsodomain.test` |

## 5. Linux 配置同步

在你的 Linux 系统的配置文件 `/etc/krb5.conf` 中插入你的设置，类似于示例 2-5。按照惯例，`Realm` 始终用大写字母，而 DNS 名称用小写字母。

### 示例 2-5：/etc/krb5.conf 示例

```
[libdefaults]
default_realm = ITSODOMAIN.TEST
clockskew = 300

[realms]
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test
admin_server = master.itsodomain.test
kpasswd_server = master.itsodomain.test
}

[logging]
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/admin.log
default = FILE:/var/log/krb5libig.log

[appdefaults]
pam = {
ticket_lifetime = 1d
renew_lifetime = 1d
forwardable = true
proxable = false
retain_after_close = false
minimum_uid = 0
}
```

## 6. 域名映射

如果你的 IBM `i/OS` 使用与 Windows 域不同的域名，那么 `Kerberos` 需要知道这一点。在我们的示例中，IBM `i/OS` 在网络中的主机名为：`iseries.ito.ibm.com`，但我们的 `Kerberos Realm` 是 `ITSODOMAIN.TEST`。因此，如果服务器具有 DNS 扩展名 `.ito.ibm.com`，请在 `kerb5.conf` 文件中添加另一个部分以配置 `Kerberos` 使用 `ITSODOMAIN.TEST` 设置：

```
[domain_realm]
.itso.rbm = ITSODOMAIN.TEST
```

## 7. 注意事项

修改 `kerb5.conf` 后，检查以下注意事项：

- `Kerberos` 期望参与的系统具有一致的时间。如果系统之间的时间差超过 300 秒，建议保持低时间差。
- 如果你的 IBM `i/OS` 使用与 Windows 域不同的域名，那么 `Kerberos` 需要知道这一点。在我们的示例中，IBM `i/OS` 在网络中的主机名为 `iseries.ito.ibm.com`，但我们的 `Kerberos Realm` 是 `ITSODOMAIN.TEST`。因此，如果服务器具有 DNS 扩展名 `.ito.ibm.com`，请在 `kerb5.conf` 文件中添加另一个部分配置 `Kerberos` 使用 `ITSODOMAIN.TEST` 设置：

```
[domain_realm]
.itso.rbm = ITSODOMAIN.TEST
```

如果你计划使用 `pam_krb5`，请参考你发行版关于设置的文档。在你的 Linux 系统上安装 `Kerberos5` 及其实用工具后，你必须拥有以下 `Kerberos` 命令：

- `kinit`
- `klist`
- `kpasswd`

你必须拥有 `Kerberos5` 配置文件，即 `/etc/krb5.conf`。

`krb5.conf` 包含了基础 `kerberos5` 配置，并要求根据你的环境进行自定义。需要以下关于你的 `Active Directory` 的信息：

- `Kerberos` 术语中的 Windows 登录域：默认 realm (default realm)
- Windows 服务器（域控制器）的 DNS 名称，提供以下功能：密钥分配中心 (`KDC`) 和密码服务器

如果你不确定此配置，可以在 `i5/OS` 现有的 `Kerberos` 配置中进行验证。在 IBM `i5/OS` 上，`Kerberos` 服务被称为网络认证服务 (`NAS`)，设置位于与 Linux 类似的文件中：

```
/IBM/UserData/OS400/NetworkAuthentication/krb5.conf
```

由于 `Kerberos` 和 `EIM` 必须在 IBM `i5/OS` 上已经配置，该文件必须类似于示例 2-4。双问号和括号是括号的替换，将 `??` 替换为 `<` 和 `??`，而双问号和箭头替换大括号，将 `??` 替换为 `<` 和 `>>`。

### 示例 2-4：IBM i/OS Kerberos 配置

```
<libdefaults>
default_keytab = /QIBM/UserData/DS400/NetworkAuthentication/keytab/krb5.keytab
default_realm = \ITSODOMAIN.TEST
<realms>
ITSODOMAIN.TEST = {
kdc = master.itsodomain.test:88
kpasswd_server = master.itsodomain.test:464
}
<domain_realm>
.itso.rbm = ITSODOMAIN.TEST
<capaths>
```

示例 2-4 显示了表 2-2 中使用的设置。

| 表 2-2 IBM i/OS Kerberos 配置设置 | | |
|---|---|---|
| 说明 | 参数 | 值 |
| Kerberos Realm/我们的 Active Directory 名称 | `default_realm` | `ITSODOMAIN.TEST` |
| KDC/我们的 Active Directory 服务器 | `kdc` | `master.itsodomain.test` |
