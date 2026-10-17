
可以对监听器进行配置，使得许多管理操作在更改之前需要用户提供密码。默认情况下，没有设置监听器密码，因此在安装 Oracle 后这是一个要采取的重要步骤。要设置监听器密码，请运行监听器控制工具（Listener Control Utility），连接到相关的监听器并输入以下内容，将 `password` 替换为你自己合适的强密码。这样做会在 `$ORACLE_HOME\network\admin` 目录下的 `listener.ora` 文件中添加条目。

```
LSNRCTL> CHANGE_PASSWORD
Old password: <enter>
New password: password
Reenter new password: password
LSNRCTL> SAVE_CONFIG
```

使用 Oracle Net Manager 设置监听器密码。你可以在监听器通用参数（General Parameters）的身份验证选项卡中进行操作。

## 管理限制

除了用密码锁定监听器外，你还可以限制在提供正确密码时可以远程执行的操作。这有助于实现分层安全，应该予以注意。编辑 `$ORACLE_HOME\network\admin` 目录下的 `listener.ora` 文件并添加以下条目：

```
ADMIN_RESTRICTIONS_listener=on
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_737_0.png)

将 `listener` 替换为保护监听的名称。

## 移除 PL/SQL 外部过程功能

虽然 PL/SQL 外部过程提供的额外功能相当方便，但它确实存在安全漏洞，攻击者可能发现它比你更有用。因此，建议在大多数情况下将其移除。要做到这一点，请编辑 `$ORACLE_HOME\network\admin` 目录下的 `listener.ora` 和 `tnames.ora` 文件。

在 `listener.ora` 文件中，找到类似于下面的部分：

```
SID_LIST_LISTENER =
(SID_LIST =
(SID_DESC =
(SID_NAME = PLSExtProc
(ORACLE_HOME = C:\ora9ias
(PROGRAM = extproc))
)
(SID_DESC =
(GLOBAL_DBNAME =db.HEPHAESTUS.ngsoftware.com)
(ORACLE_HOME = C:\ora9ias
(SID_NAME = iasdb)
)
)
```

移除 `PLSExtProc` 的条目：

```
SID_LIST_LISTENER =
(SID_LIST =
(SID_DESC =
(GLOBAL_DBNAME = iasdb.HEPHAESTUS.ngsoftware.com)
(ORACLE_HOME = C:\ora9ias
(SID_NAME = iasdb)
)
)
```

请注意，根据你安装 Oracle 的方式和位置，`PLSExtProc` 条目可能是 `iache_extproc` 或简单的 `extproc`。打开 `tnsnames.ora` 文件并找到类似于下面代码的部分并将其删除。

```
EXTPROC_CONNECTION_DATA =
(
  CONNECT_DATA =
    (ADDRESS = (PROTOCOL = TCP)(HOST = my_host)(PORT = 1521))
    (SERVICE = extproc)
  )
)
```

（注：此处示例代码不完整，实际操作请参考对应的 `tnsnames.ora` 结构）
