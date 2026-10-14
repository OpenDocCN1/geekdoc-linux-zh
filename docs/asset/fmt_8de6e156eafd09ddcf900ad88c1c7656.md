
`C:\MIG80 DBNAME=MYOB NEW_DBNAME=MYNEW SPOOL=MYLOG`

迁移工具将运行 ASCII `.bsq` 文件，该文件会创建一个 `migrate` 用户，并构建视图来支持迁移过程。完成后，它将在指定的位置（或默认位置）留下一个日志文件（通过 `SPOOL` 选项），并在 `ORACLE_HOME/dbs` 子目录下留下一个二进制数据文件 (`conv<SID>.dbt`)。

### 5. 为转换准备 Oracle 7 数据库
这是运行迁移工具后发生的独立且关键的阶段。要准备 Oracle 7 数据库，请删除（或重命名）Oracle 7 控制文件，因为将在此处创建 Oracle 8 控制文件。确保所有其他文件、数据文件和重做日志（`redo log files`）完好无损。

此外，通过设置 `ORACLE_HOME` 环境变量（NT 上的注册表或 UNIX 上的 shell 环境变量）指向新的 Oracle8 目录位置来准备操作系统环境。然后，重置 Oracle 二进制执行文件路径（适当 NT 注册表子树中的 Image Path，或必要时 UNIX 上的 shell `PATH`，尽管 `ORACLE_HOME` 变量在 UNIX 上应该已经处理了这个问题），如果 `ORACLE_SID` 发生变化，请重置它。

编辑你的 Oracle 8 `init.ora` 文件，包含 `compatible=8.0.0`（或更高）的参数设置。此外，删除任何过时的 Oracle 7 参数。（请参阅你的服务器手册以获取最新列表）确保你的 `control_files=()` 以及其他文件位置（如 `bdump` 和 `cdump`）的参数设置是正确的（即：不包含 Oracle 7 的路径引用）。

将转换数据文件 (`conv<SID>.dbt`) 从 Oracle 7 的 `ORACLE_HOME/dbs` 子目录复制到 Oracle 8 的 `ORACLE_HOME/dbs` 子目录。

### 6. 转换你的数据库
这是无法回头的步骤。换句话说，在你运行 `convert` 后，无论你的数据库转换成功与否，无法在不进行完全冷还原的情况下恢复到 Oracle 7。要此此，请在 `svmgr1` (UNIX) 或 `svmgr38` (NT) 中运行以下命令：

```
svrmgr1> connect internal
svrmgr1> startup mount
svrmgr1> alter database convert;
svrmgr1> alter database open resetlogs;
```
