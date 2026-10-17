
当需要关闭实例以适应计划停机时，可以通过发出 `shutdown immediate` 命令关闭实例。此特定关闭选项将优雅地断开任何用户连接，并且实例重新启动后不需要崩溃恢复。

```
Connected to:
Oracle Database 10g Enterprise Edition Release 10.1.0.2.0 - Production
With the Partitioning, OLAP and Data Mining options

SQL> shutdown immediate;
Database closed.
Database dismounted.
ORACLE instance shut down.
```

正如您所见，显示的序列与数据库正常打开时呈现的顺序相反。

如果出于任何原因需要快速关闭数据库，可以发出 `shutdown abort` 命令：

```
SQL> shutdown abort
ORACLE instance shut down.
```

有时在 `shutdown immediate` 挂起时需要这样做。如果打开另一个 `sqlplus` 会话，这将终止 `shutdown immediate`。但是，启动时将需要自动实例崩溃恢复。

## 从 Enterprise Manager 数据库控制启动

除了如前所示通过 `SQL*Plus` 启动实例，或通过前一章中与 RAC 相关的 `srvctl` 命令启动实例外，您还可以使用 Enterprise Manager 数据库控制（与 EM Grid Control 相反）。Enterprise Manager 数据库控制应已通过数据库服务器安装过程自动安装；它使用 Web 服务器在您的 Oracle 系统上监听 5500 端口。

### 访问数据库控制

数据库控制通过 Web 浏览器访问。用于访问控制台的字符串是

```
http://sysname:5500/em
```

此字符串应调用 Enterprise Manager 数据库控制界面，您可以在其中通过 Web 浏览器启动和关闭实例。

### 管理 Enterprise Manager 数据库控制服务

如果无法访问 Enterprise Manager，可以通过 `emctl` 命令检查其状态，如下所示：

```
[oracle@ptc6 oracle]$ emctl status dbconsole
TZ set to US/Central
Oracle Enterprise Manager 10g Database Control Release 10.1.0.2.0
Copyright (c) 1996, 2004 Oracle Corporation. All rights reserved.
http://ptc6:5500/em/console/aboutApplication
Oracle Enterprise Manager 10g is running.
Logs are generated in directory
/opt/oracle/product/10.1.0/db_1/ptc6_orcl/sysman/log
```

### 启动 Enterprise Manager

如果 Enterprise Manager 数据库控制未运行，可以使用 `emctl` 命令启动它。Enterprise Manager 可以通过 `emctl start dbconsole` 命令启动，如下所示：

```
[oracle@ptc6 oracle]$ emctl start dbconsole
TZ set to US/Central
Oracle Enterprise Manager 10g Database Control Release 10.1.0.2.0
Copyright (c) 1996, 2004 Oracle Corporation. All rights reserved.
http://ptc6:5500/em/console/aboutApplication
Starting Oracle Enterprise Manager 10g Database Control ... started.
Logs are generated in directory
/opt/oracle/product/10.1.0/db_1/ptc6_orcl/sysman/log
```

### 停止 Enterprise Manager

如果您希望停止 Enterprise Manager，可以使用 `emctl` 命令停止它。Enterprise Manager 通过 `emctl stop dbconsole` 命令停止，如下所示：

```
[oracle@ptc6 oracle]$ emctl stop dbconsole
TZ set to US/Central
Oracle Enterprise Manager 10g Database Control Release 10.1.0.2.0
Copyright (c) 1996, 2004 Oracle Corporation. All rights reserved.
http://ptc6:5500/em/console/aboutApplication
Stopping Oracle Enterprise Manager 10g Database Control ... Stopped.
```

## Oracle Database 10g 和 CSSD

在 Oracle RAC 环境中，Oracle 实例会通过 Oracle Cluster Ready Services 自动启动。在独立系统中，CSS Daemon（`cssd`）会自动启动 Oracle 实例。`CSSD`（Cluster Services Synchronization Daemon）即使在独立系统中也会自动安装。此守护进程会在系统启动时自动启动 Oracle 实例。为了更改此行为，可以手动修改文件 `/etc/init.d/init.cssd`。

## 用户身份验证

与管理实例状态一样，另一个常见但关键的管理任务是用户账户管理。Oracle 服务器使用多种身份验证方法。这些包括数据库身份验证、操作系统身份验证、网络身份验证、远程身份验证、中层身份验证和 SSL 身份验证。

### 数据库身份验证

这是连接到 Oracle 的“标准”身份验证方法。唯一的要求是活动用户账户、关联的密码以及适当的系统权限。密码以加密格式存储在数据字典中。锁定和解锁用户账户可以进一步管理身份验证。这可以在不删除用户的情况下控制数据访问。密码也可以设置为在一定时间后过期，并且可以强制执行密码复杂度。

### 操作系统身份验证

Oracle 数据库可以设置以接受操作系统身份验证。这通过 OS 账户演示，或者当 `dba` 可以以 `"/ as sysdba"` 或 `"/ as sysoper"` 登录数据库时。在这些情况下，假定用户已通过操作系统的用户名/密码挑战，因此是可信用户。`oracle` 用户被设为数据库安装过程创建的操作系统组 `OSDBA` 和 `OSOPER` 的成员。

### 网络身份验证

Oracle 的身份验证可以基于网络授权。这意味着使用第三方网络身份验证服务（Kerberos、SESAME）。在此同一分组中，还支持基于证书的 PKI（公钥基础设施）身份验证。这是一种非常复杂且安全的方法，包含多个重要组件，包括：

- 使用 SSL 的会话管理
- 支持对证书进行签名和验证数据的 OCI 和 PL/SQL 过程
- “钱包”的使用，或定义的、可传输的安全凭证集合，包括公钥、用户证书以及一组用户的信任点
- 来自第三方证书颁发机构（如 VeriSign 或 Thawte）的 X.509v3 证书

`Oracle Internet Directory` 用于管理用户属性和用户权限。

### 远程身份验证

远程身份验证可通过 `RADIUS`（远程身份验证拨入用户服务）进行身份验证。

### 中间层身份验证

在多层环境中，例如 `OracleAS 10g`，Oracle 通过保留身份和限制权限来控制中间层应用程序的完整性。此类方案还受益于连接池，允许多个用户共享访问 Oracle。为了使用连接池，建议使用 Oracle Call Interface（`OCI`）创建轻量级会话，允许数据库密码身份验证。这通过中间层保留真实用户的身份，同时合并数据库连接。这些轻量级会话可以有密码创建，也可以无密码创建。

### SSL 身份验证

根据数据库初始化参数文件的配置，Oracle 数据库可以通过 SSL 对会话进行身份验证。此方法可以设置以绕过 Oracle Internet Directory。然而，这不允许企业级证书身份验证。此外，Oracle 10g R2 允许使用安全 HTTP 协议（`HTTPS`）。

SSL 是一种由 Netscape 开发的工业标准安全协议，用于提供安全的网络连接。SSL 连接使用 RSA 公钥密码术和对称密钥密码术发送加密数据。这提供了身份验证、加密和数据完整性。
