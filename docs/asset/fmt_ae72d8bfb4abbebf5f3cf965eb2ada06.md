
Oracle 文档指出，它仅支持迁移到没有补丁的基础版本。例如，`8.1.6.0` 是可以的，但 `8.1.6.2` 不支持。为什么？Oracle 在一个版本发布之前不知道会发布多少个补丁，它也不会回溯并对每一个可能的补丁发布版本进行直接迁移。

这让普通的 DBA 处于困境，因为从理论上说，在所有数据库迁移之前，你必须忍受该版本中的 bug。只有在所有数据库迁移完成后，你才可以在 Oracle 的批准下对你的基础版本进行补丁。

无疑，这将导致许多 DBA 考虑他们的数据库是否达到了所需的级别，然后仍然执行迁移。从理论上讲，我不认为这会有问题，除非 Oracle 说你正在以一种“不支持”的方式运行。然而，我不建议你以不支持的方式迁移数据库。我所能说的就是无论你做什么，在尝试对生产系统进行迁移之前，请务必进行彻底测试。请像往常一样，确保你有有效的备份。

# 使用 ODMA 的迁移步骤

以下示例使用 ODMA 迁移（使用 Oracle 术语称为升级）Oracle `8.1.6.1` 数据库到 Oracle `9.0.1`。实际上，从 `8i` 到 `9i` 的迁移过程更像是升级（基本上是运行脚本），而不是从 Oracle `7.3` 到 `9i`。一旦进入工具，你会看到路径差异的地方。

迁移过程可以分为三个步骤：准备数据库、使用 ODMA 迁移数据库以及执行迁移后检查。

## 准备数据库

在迁移数据库之前，你需要执行某些步骤，如下所示：

### 1. 修改以下 `init.ora` 参数

`DB_DOMAIN = mike.com`

（你的域名会不同）。

`nJOB_QUEUE_PROCESS = 0`

`AQ_TM_PROCESSES = 0`

`REMOTE_LOGIN_PASSWORDFILE = NONE`

修改这些参数是为了停止高级队列、复制并防止需要密码文件。确保你的 `DB_DOMAIN` 也设置正确。迁移完成后，你可以重置参数并重新创建密码文件。

### 2. 增大 SYSTEM 表空间的大小

以便在升级期间两个数据字典可以同时存在。我通常需要增大 SYSTEM 表空间，但请确保至少有 `100M` 的空闲。

```sql
SQL> select file_name, bytes from dba_data_files
where tablespace_name = 'SYSTEM';
```

| FILE_NAME | BYTES |
| :--- | :--- |
| `/u02/oradata/demo/system01.dbf` | 246,022,144 |

```sql
SQL> select sum(bytes) from dba_free_space
where tablespace_name = 'SYSTEM'

SUM(BYTES)
...
720,896

SQL> alter database datafile 
'/u02/oradata/demo/system01.dbf'
resize 400M;
```

数据库已更改。

### 3. 准备 SYSTEM 表空间内部的回滚段

你你不希望它在迁移过程中溢出，也不希望它缩小。给它设置 `505` 个区（extents）的最大限制，关闭 `OPTIMAL`，并将 `PCTINCREASE` 设置为 `50%`。

```sql
SQL> alter rollback segment system
storage (maxextents 505 optimal null next 1M);
```

回滚段已更改。

```sql
SQL> alter tablespace system default storage (pctincrease 50);
```

表空间已更改。

### 4. 确保 SYS 和 SYSTEM 的默认表空间和临时表空间都是 SYSTEM

大多数 DBA 会更改表空间以避免 SYSTEM 表空间碎片，另一些人会将 SYSTEM 的默认表空间移动到 TOOLS。在迁移期间，你需要将它们都移回 SYSTEM。此外，如果你移动了 `SYS.AUDS` 侧的 SYSTEM 表空间，你必须将其移回来。

```sql
SQL> alter user sys default tablespace system
temporary tablespace system;
```

用户已更改。

```sql
SQL> alter user default tablespace system
temporary tablespace system;
```

用户已更改。

### 5. 确保 SYSTEM 表空间中没有名为 MIGRATE 的用户

你不希望它在迁移过程中溢出。ODMA 在迁移过程中会创建并删除该用户。迁移完成后你需要它。

```sql
SQL> select username, created from dba_users
where username = 'MIGRATE';
```

无结果。

### 6. 检查你是否有名为 OUTLN 的用户

该用户从 Oracle `8i` 开始自动创建，所以如果你已经在运行 `8i`，它是可以的。迁移完成后你需要它。

```sql
SQL> select username, created from dba_users
where username = 'OUTLN';
```

| USER | CREATED |
| :--- | :--- |
| OUTLN | 17-APR-00 |

### 7. 确保你没有需要恢复的数据文件

某些经验不足的人可能通过进入新版本更容易恢复数据库。

```sql
SQL> select * from v$recover_file;
```

无结果。

### 8. 正常关闭数据库并退出

技术上 `SHUTDOWN` 可以，但我认为正常关机更安全。

```sql
SQL> shutdown;

Database closed.

Database dismounted.

ORACLE 实例已关闭。

SQL> exit

Disconnected
```

### 9. 对你的数据库进行冷备份

如果迁移过程中出现问题，你需要此备份来恢复。请勿跳过此步骤。

大多数这些准备工作都是为迁移 Oracle `7` 数据库设计的，这比迁移 Oracle `8i` 数据库复杂。然而，你在这里做的任何操作都不会损害你的 Oracle `8i` 数据库，因此你现在可以进行迁移了。

## 使用 ODMA 迁移

系列步骤包含了实际迁移：

### 1. 设置环境以反映新的软件和 `ORACLE_HOME`

如果你要运行 `OUI`，还要设置 `DISPLAY`。ODMA 是一个 Java GUI，所以你运行 `OUI` 时需要相同的设置。

### 2. 在新的 `$ORACLE_HOME/bin` 中启动 ODMA

```bash
$ cd ORACLE_HOME/bin
$ odma
```

### 3. 几秒后应出现欢迎界面，如图 15.1 所示。点击 Next。

### 4. 下一个屏幕列出了尝试迁移或升级之前需要考虑的某些要求，如图 15.2 所示。点击 Next。

### 5. 下一个屏幕要求选择一个实例

这是通过生成 `oratab` 文件生成的，因此请确保你想迁移的数据库列在其中并带有当前的（迁移前）版本。在这里你需要选择 `demo` 数据库，如图 15.3 所示。

## 迁移

第 15 章

![](img/0735bb12e1d45128c662b4b409eb1bf1_426_0.png)

一次只能对一个数据库实例进行迁移或升级。存在以下实例。选择您想要迁移或升级的数据库实例。

存在以下实例。选择您想要迁移或升级的数据库实例。

数据库实例：

```
db001/oracle/product/8.1.0

db001/root/oracle/product/8.0.1

demo/1/app/oracle/product/5.0.1
```

Oracle 数据库实例：

```
demo/1/app/oracle/product/5.0.1
```
