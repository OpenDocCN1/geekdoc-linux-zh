
| 4 | 1 | 104,857,600 |

SQL>

如你所见，现在有了一个包含两个成员的新在线重做日志组，每个成员大小为 100M。

Oracle 管理的文件似乎简化了管理，但这是有代价的。除非你的逻辑卷是条带（striped）且最好是镜像（mirrored），否则 Oracle 管理的文件分散磁盘 I/O 会更加困难。即使如此，将所有文件放在一个位置也是危险的，因为一个执行错误的 `rm` 命令就会摧毁一切。

# Unix 和 Linux 上的 Oracle DBA

我担心的另一个问题是“弱化” DBA 的角色并推广粗放的管理实践。虽然在之前的 Oracle 版本中具有深厚背景的 DBA 不太可能陷入这一类别，但新的 DBA 可能会掉进陷阱。如果他们从不学习分离文件，而是依赖 Oracle 来指定所有默认参数，他们将永远无法实践稳健的数据库设计原则。这在小型测试系统中可能足够，但在较大的系统中，性能将受到极大影响。我的建议是在合理的情况下使用 Oracle 管理的文件，但永远不要忘记文件管理的基础知识。

## 使用动态内存参数和多个数据块大小

Oracle 9i 最令人兴奋的特性之一是在无需重启数据库的情况下调整 SGA。显而易见，这对于有高可用性要求的系统具有巨大影响。定义数据库缓冲区缓存尺寸的过程也发生了变化。本节涵盖了这些变化。

你是否曾经拥有过一个活跃用户的生产数据库，结果发现需要增加像共享池这样的参数来满足意外之外的需求？关闭所有日志、将参数增加到比你认为正确的更高的数值，重启数据库，然后让用户回来，这非常麻烦……（此处由于原文大量重复，已按逻辑去重处理翻译）。

### 9i 服务器新特性

第 19 章

使用多个块大小会改变缓冲区缓存的尺寸计算方式。在 9i 之前，缓冲区缓存的公式如下：

```
buffer cache size = DB_BLOCK_SIZE * DB_BLOCK_BUFFERS
```

在 9i 中，此公式发生了变化。你不再通过 `DB_BLOCK_BUFFERS` 来衡量缓冲区缓存。相反，你使用 `DB_CACHE_SIZE` 参数为默认块大小指定缓冲区缓存的大小。此外，你还需要为任何非默认块大小添加每个池（pool）。新的等式如下：

```
buffer cache size = DB_CACHE_SIZE + DB/[2k...32k]/CACHE_SIZE
```

通过这种方式，你通过为特定块大小保留的每个池之和来衡量缓冲区缓存。

### 回滚表空间 (Undo Tablespaces)

Oracle 9i 还尝试减少涉及回滚段（rollback segments）的维护工作。如果你需要，仍然可以使用传统的表空间，在其中你创建回滚段并管理区（extents）。然而，9i 引入了一种新类型的回滚表空间来取代传统的回滚段。事实上，Oracle 文档指出，创建回滚段的传统方法正在废弃，并强烈建议使用回滚表空间。

回滚表空间执行传统回滚段的核心功能。它们提供了回滚段的三个 R 功能：

- SQL 语句的回滚（Rollback）
- 读取一致性（Read consistency）
- 崩溃后的恢复（Recovery）

遗憾的是，在编写本文时，Oracle 尚未解释解释回滚表空间内部是如何工作的，以及它们与传统回滚段有何区别。基本上，我们知道如何创建它们以及 Oracle 会自动管理它们，但细节尚未发布。根据对 `DBA_ROLLBACK_SEGS` 的查询，似乎使用了某种类型的段，但这些与传统回滚段的区别仍不可知。因此，本节侧重于它们的作用，而不是其实现方式。

9i 实例可以使用传统的回滚段或新的回滚表空间运行。在这些方法之间进行切换需要修改 `UNDO_MANAGEMENT` 参数并重启实例（bounce）。`UNDO_MANAGEMENT` 具有以下设置：

| 设置 | 描述 |
|---|---|
| `UNDO_MANAGEMENT = ''` | 未设置，默认使用回滚段 |
| `UNDO_MANAGEMENT = MANUAL` | 使用传统的回滚段 |
| `UNDO_MANAGEMENT = AUTO` | 使用新的回滚表空间 |

![](img/0735bb12e1d45128c662b4b409eb1bf1_520_0.png)

# Unix 和 Linux 上的 Oracle DBA

如果你不设置 `UNDO_MANAGEMENT` 或将其设置为 `MANUAL`，你可以像往一样使用和管理回滚段。但是，如果你决定使用回滚表空间，必须执行以下操作：

- 1. 决定是在数据库创建时创建表空间还是在数据库创建后。这里，我们在数据库创建后创建一个回滚表空间。创建此回滚表空间与其他任何类型表空间的关键区别在于 `UNDO` 子句。

```sql
SQL> create undo tablespace auto_undo_tbs
2 datafile /u02/app/oracle/oradata/demo/auto_undo_tbs01.dbf
3 size 100M;
```

表空间已创建。

```
SQL>
```

在这里，你现在有了一个名为 `AUTO_UNDO_TBS` 的回滚表空间。如果你让 Oracle 在数据库创建时创建它，默认名称为 `UNDOTBS`。

- 2. 当前，你设置为手动（传统）回滚表空间。由于你有多个表空间，你必须识别你将使用哪一个。一旦开始使用回滚表空间，将数据库设置为使用 `AUTO_UNDO_TBS` 回滚表空间。

```sql
SQL> alter system
2 set undo_tablespace = auto_undo_tbs
3 scope = spfile;
```

系统已更改。

```
SQL>
```

一旦你设置数据库使用回滚表空间，你就可以动态更改 `UNDO_TABLESPACE` 以在不同的表空间之间切换。新将在指定的表空间中进行，而现有事务将继续在之前的表空间执行。然而，你不能动态更改 `UNDO_TABLESPACE`，因为数据库仍然处于手动回滚模式。因此，你在 `SPFILE` 中使用 `SCOPE` 子句对其进行设置，以便在下次重启实例时生效。

- 3. 接下来，你必须将数据库设置为使用回滚表空间方法而非手动方法。此参数不是动态的，因此你必须在 `SPFILE` 中设置它，以便在重启实例时生效。

```sql
SQL> alter system
2 set undo_management = auto
3 scope = spfile;
```

系统已更改。

```
SQL>
```

- 4. 重启数据库使更改生效。

```
SQL> shutdown;
...
SQL> startup
ORACLE instance started.
```

| Total System Global Area | 42024270 bytes |
| Fixed Size | 279820 bytes |
| Variable Size | 335544320 bytes |
| Database Buffers | 83886080 bytes |
| Redo Buffers | 532480 bytes |
| Database mounted. | |
| Database opened. | |

```
SQL>
```

- 5. 验证数据库是否正在使用回滚表空间。

```
SQL> show parameter undo
```

| NAME | TYPE | VALUE |
| undo_management | string | auto |
| undo_retention | integer | 900 |
| undo_suppress_errors | boolean | FALSE |
| undo_tablespace | string | auto |

```sql
SQL> select segment_name, tablespace_name, status from dba_rollback_segs;
```

| SEGMENT_NAME | TABLESPACE_NAME | STATUS |
|---|---|---|
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |
| SYSTEM | UNDOTBS | ONLINE |

11行 selected。

```
SQL>
```
