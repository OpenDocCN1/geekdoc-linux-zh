
如果将 `DB_CACHE_SIZE` 减小到 20MB，鉴于相同的数据库活动量，你可以预期会有 6614 次物理读。同样，如果将缓冲池缓存增加到 100MB，鉴于相同的数据库活动量，你可以预期会有 4866 次物理读。

通过这种方式，缓冲池缓存顾问功能提供了“苹果对苹果”的比较，即根据 `DB_CACHE_SIZE` `init.ora` 参数大小的增加或减少，预计会增加或减少多少物理 I/O。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_305_0.png)

查询输出显示，一旦 `DB_CACHE_SIZE` 增加到 80MB，预计物理 I/O 数量不会显著减少。从 80MB 增加到 90MB 仅会使物理 I/O 减少 2 次，并且估计超过 90MB 的增加不会进一步减少物理 I/O。

数据库缓冲池缓存的增加通常并非直接的线性关系。例如，将 `DB_CACHE_SIZE` 的值加倍并不一定会使缓冲池缓存命中率加倍。

改进缓冲池缓存性能的另一种技术是将缓冲池缓存划分为多个缓冲池。

## 使用多个缓冲池

默认情况下，所有数据库段都在默认池中竞争使用相同的数据库缓冲池缓存缓冲区。这可能导致一种情况：一些仅受少数应用程序用户关注的不经常访问的表，将更常用的数据缓冲区从内存中挤出。为了避免这种情况，Oracle 提供了将数据库缓冲池缓存划分为多达三个称为 `缓冲池` 的独立区域的能力。然后，段被显式分配给由 DBA 决定的适当缓冲池。

### 缓冲池类型

在创建任何缓冲池之前，你必须确定希望使用哪些类型的池。每个缓冲池都用于根据你预计应用程序访问这些段的频率来缓存段：

- `Keep Pool`：用于缓存你极少（如果有的话）希望其离开数据库缓冲池缓存的段。该池的大小由 `init.ora` 参数 `DB_KEEP_CACHE_SIZE` 指定，单位为字节、千字节、兆字节或吉字节。使用 Keep Pool 是可选的。其默认大小为 0 字节。
- `Recycle Pool`：用于缓存你极少（如果有的话）希望其保留在数据库缓冲池缓存中的段。`Recycle Pool` 的大小由 `init.ora` 参数 `DB_RECYCLE_CACHE_SIZE` 指定，单位为字节、千字节、兆字节或吉字节。使用 Recycle Pool 也是可选的。其默认大小为 0 字节。
- `Default Pool`：用于缓存未指定给 Keep 或 Recycle 池的段。该池的大小由 `init.ora` 参数 `DB_CACHE_SIZE` 指定，单位为字节、千字节、兆字节或吉字节。Default Pool 是必需的。其默认大小为 48 兆字节。此参数不能设置为 0。

除非在 `init.ora` 中另有指定，否则仅在实例启动时创建 Default Pool。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_306_0.png)

如果使用多个块大小，可以为每个块大小的缓冲池缓存创建 Keep、Recycle 和 Default Pool。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_306_1.png)

与从分配给 Default Pool 的内存中扣除 Keep 和 Recycle 池内存的 Oracle8i 不同，Oracle9i 独立地为三种缓冲池类型中的每一种分配内存。这使得可以在不影响分配给剩余池的内存的情况下，单独修改每个缓冲池的大小。

在配置缓冲池之前，你需要确定哪些段将被缓存在 Keep 和 Recycle 池中。

## 确定要缓存哪些段

确定要在非默认缓冲池中缓存哪些段，以及在哪些池中缓存它们，需要对应用程序、其段以及段是如何被访问的有透彻的了解。确定应将哪些段分配给每个缓冲池的一种方法是确定哪些段当前缓存在默认池中，并将这些段分类为包含在 Keep 或 Recycle 池中的候选者。四个视图 `V$BH`、`DBA_OBJECTS`、`V$CACHE` 和 `DBA_USERS` 可用于此目的。

## 使用 V$BH 和 DBA_OBJECTS 识别缓存候选者

`V$BH` 和 `DBA_OBJECTS` 视图都包含有用的信息，可以帮助你识别当前缓存在缓冲池缓存中的段。利用这些信息和对应用程序的了解，你可以确定这些对象中是否有任何一个应该缓存在 Keep 或 Recycle 池中，以提高缓冲池缓存的性能。表 5.6 和表 5.7 描述了将这些视图用于将段分配到适当缓冲池的有用列。

### 表 5.6 V$BH 视图的部分说明

| 列名 | 说明 |
| --- | --- |
| `BLOCH#` | 缓冲区高速缓存中缓存块的块号 |
| `OBJD` | 缓冲区高速缓存中缓存块所属对象的对象 ID |

### 表 5.7 DBA_OBJECTS 视图的部分说明

| 列名 | 说明 |
| --- | --- |
| `OBJECT_ID` | 分配给该对象的数字标识符 |
| `OWNER` | 该对象的所有者 |
| `OBJECT_NAME` | 该对象的名称 |
| `OBJECT_TYPE` | 对象类型（例如，表、索引、视图） |

`V$BH` 视图实际上是为调整运行 Oracle9i 实时应用程序集群（RAC）功能的 Oracle 服务器而设计的。然而，对于非 RAC 系统，它也有用，因为它显示了每个缓存段中当前有多少个缓存缓冲区位于数据库缓冲区高速缓存中。通过查询 `V$BH` 和 `DBA_OBJECTS` 视图并使用公共列 `OBJECT_ID`，你还可以查看哪些对象当前被缓存在缓冲区高速缓存中；这些对象正在使用多少缓冲区高速缓存缓冲区；以及这些对象的所有者、名称和类型：

```sql
SQL> SELECT obj.owner,
            obj.object_name,
            obj.object_type,
            COUNT(DISTINCT bh.block#) "Num. Buffers"
  FROM   dba_objects obj, v$bh bh
  WHERE  obj.object_id = bh.objd
  AND    owner != 'SYS'
  GROUP BY obj.owner,
           obj.object_name,
           obj.object_type
  ORDER BY 4;
```

| OWNER | OBJECT_NAME | OBJECT_TYPE | Num. Buffers |
| --- | --- | --- | --- |
| APPS | EMPLOYEE | TABLE | 12 |
| APPS | EMPLOYEE_PK_ID | INDEX | 10 |
| APPS | REGION | TABLE | 8 |

该查询排除了属于用户 SYS 的段，因为它们通常是数据字典段，在正常处理过程中几乎总是保留在 LRU 列表上。

使用该查询的输出，我们可以看到 EMPLOYEE 和 REGION 表以及 EMPLOYEE_PK_ID 索引当前被缓存在内存中。根据其使用模式，这些段可能是 Keep 池或 Recycle 池的良好候选者。查找类似信息的另一种方法是查询 `V$CACHE` 和 `DBA_USERS` 视图。

## 使用 V$CACHE 和 DBA_USERS 识别缓存候选项

两个额外的视图，`V$CACHE` 和 `DBA_USERS`，可以提供关于可能成为 Keep 池或 Recycle 池缓存良好候选者的段的更多信息。表 5.8 和表 5.9 描述了这些视图中有助于将段分配到适当缓冲区高速缓存池的选定列。

### 表 5.8 V$CACHE 视图的部分说明

| 列名 | 说明 |
| --- | --- |
| `BLOCK#` | 缓冲区高速缓存中缓存块的块号 |
| `NAME` | 缓冲区高速缓存中缓存段的名称 |
| `KIND` | 缓冲区高速缓存中缓存的段类型（例如，表、索引） |
| `OWNER#` | 分配给拥有其块被缓存在缓冲区高速缓存中的段的数据库用户的标识符 |

### 表 5.9 DBA_USERS 视图的部分说明

| 列名 | 说明 |
| :--- | :--- |
| `USERNAME` | 数据库用户的名称 |
| `USER_ID` | 分配给数据库用户的标识符 |

![](img/832fbc6aca8b6075843ca6f2356c0a8d_309_0.png)

在使用 `V$CACHE` 视图之前，你必须通过运行 Oracle 提供的名为 `CATPARR.SQL` 的脚本创建它。该脚本应作为用户 SYS 登录时运行。在 Unix 系统中，该脚本位于 `$ORACLE_HOME/rdbms/admin/admin`；在 Windows 2000 系统中，位于 `%ORACLE_HOME%\rdbms\admin\admin`。与 `V$BH` 类似，`V$CACHE` 动态性能视图实际上也是为调整 Oracle9i 实时应用程序集群而设计的。
