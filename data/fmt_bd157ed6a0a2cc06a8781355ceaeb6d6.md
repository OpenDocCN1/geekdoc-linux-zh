
> William Page 的第 90 条提示：某些提供的包可能依赖于其他包。重新编译包头会导致任何依赖包失效。请检查重新编译后其他包是否仍然有效。如果只重新编译包体，依赖包不会失效。任何用户编写的存储程序和包也可能受到这种影响。

# 使用 ORACLE8I 提供的包

现在是实操阶段了。我将通过一些简单且实用的示例，阐述每个提供的包中一些有趣的内容。

## 使用 DBMS_APPLICATION_INFO 进行监控

此包允许开发者在 `Vssqlarea` 和 `Vsession` 视图中添加应用程序跟踪信息。可以跟踪的数据类型如下：

- 模块（使用当前运行应用程序的名称），一个最多 48 字节的 `VARCHAR2` 字符串，存储在 `Vssqlarea.module` 和 `Vsession.module` 中。
- 当前操作（例如，“更新客户信息”），最多 32 字节的 `VARCHAR2` 字符串，存储在 `Vssqlarea.action` 和 `Vsession.action` 中。
- 任何客户端特定信息，最多 64 字节的 `VARCHAR2` 字符串，存储在 `Vsession.client_info` 中。

Oracle8 不处理这些信息；这些信息供 DBA 对每个应用程序和组件操作运行统计。超过支持长度的字符串会被截断。列表 29.12 显示了一个简单的示例。

### 列表 29.12 APPINFO.SQL-设置并读取应用程序信息

```sql
DECLARE

module VARCHAR2(48);          -- 应用程序信息

action VARCHAR2(32);

client VARCHAR2(64);

ldate VARCHAR2(30);           -- 获取系统日期

BEGIN

DBMS_OUTPUT.enable;

module := 'CLAIMING ELIBILITY';

action := 'VERIFY ELIGIBILITY';

DBMS_APPLICATION_INFO.set_module(module, action);

DBMS_APPLICATION_INFO.set_client_info(USER);

DBMS_APPLICATION_INFO.read_module(module, action);

DBMS_APPLICATION_INFO.read_client_info(client);

DBMS_OUTPUT.put_line(client || ' is running ' || module || ' ' || action || ' ');

SELECT TO_CHAR(SYSDATE, 'YYYY-MON-DD HH:MI:SS') INTO ldate

FROM DUAL;

END;
```

我得到的响应如下：

SCOTT is running CLAIMING ELIBILITY: VERIFY ELIGIBILITY

在会话开启期间，DBA 可以通过以下命令检查谁在做什么：

- `COLUMN module FORMAT A20`
- `COLUMN action FORMAT A20`
- `COLUMN client_info FORMAT A20`
- `SELECT client_info, module, action`
- `FROM Vsession`
- `WHERE client_info IS NOT NULL`

得到的结果如下：

| CLIENT_INFO | MODULE | ACTION | PART |
|---|---|---|---|
| SCOTT | CLAIM TRACKING | VERIFY ELIGIBILITY | CH 29 |

DBA 随后可以通过以下命令看到所有人运行此模块和操作的效果：

```sql
SELECT
sql_text, SUM(sharable_mem) mem, SUM(persistent_mem) pmem,
SUM(runtime_mem) remem, SUM(sorts) sorts, SUM(loads) loads,
SUM(disk_reads) rdisk, SUM(buffer_gets) bget,
SUM(rows_processed) prows
FROM Vssqlarea
WHERE module = 'CLAIM TRACKING' AND action = 'VERIFY ELIBILITY';
```

结果非常有意思：

| SMEM | PMEM | RMEM | SORTS | LOADS | RDISK | BGET | PROWS |
|---|---|---|---|---|---|---|---|
| SELECT TO_CHAR(SYSDATE, 'YYYY-MON-DD HH:MI:SS') FROM DUAL | | | | | | |
| 4267 | 508 | 792 | 0 | 1 | 4 | | |
| SELECT USER FROM SYS.DUAL | | | | | | | |
| 3596 | 688 | 0 | 1 | 0 | 4 | 1 |
| begin dbms_output.put_lines(:lines);4317 592 420 0 1 |

显式进行的查询只有第一个，但 SQL 显然在后台执行了一些工作。开发者应该通过适当调用 `set_action()` 来通过查询、模块或用户组收集某些统计信息。注意：断开连接后，`Vssqlarea` 中的条目仍然存在。

## 使用 DBMS_DD 重新编译包

使用此包可以两件事：

- 使用 `alter_compile()` 重新编译存储程序和包。
- 使用 `analyze_object()` 分析表、索引或簇。

`alter_compile()` 的简单用法是找到无效的存储对象并重新编译它们。列表 29.13 阐释了这一点。

### 列表 29.13 RECOMP.SQL-- 重新编译无效对象

```sql
-- 重新编译存储对象
-- 注意：未考虑包依赖
DECLARE
  CURSOR invalid_prog_obj IS
    SELECT object_name, object_type
    FROM user_objects
    WHERE status = 'INVALID';
  rec invalid_prog_obj%ROWTYPE;
  status NUMERIC;
BEGIN
  DBMS_OUTPUT.enable;
  OPEN invalid_prog_obj;
  LOOP
    -- 重新编译每个存储对象
    FETCH invalid_prog_obj INTO rec;
    EXIT WHEN invalid_prog_obj%NOTFOUND;
    DBMS_OUTPUT.put_line('Recompile ' || rec.object_type || ' ' || rec.object_name);
    DBMS_OUTPUT.alter_compile(rec.object_type, NULL, rec.object_name);
    DBMS_OUTPUT.put_line(' SUCCESSFUL
');
    -- 重新编译成功
  END LOOP;
  -- 无效对象
  CLOSE invalid_prog_obj;
EXCEPTION
  WHEN OTHERS THEN
    BEGIN
      status := SQLCODE;
      DBMS_OUTPUT.put_line(' FAILED with ' || SQLERRM(status));
      IF (invalid_prog_obj%ISOPEN) THEN
        CLOSE invalid_prog_obj;
      END IF;
    EXCEPTION WHEN OTHERS THEN
      NULL;
    END;
END;
/
```

这可能会返回类似的内容：

Recompile FUNCTION TABLE SUCCESS
Program Objects Recompiled
PL/SQL procedure successfully completed.

> 如果存储对象重新编译失败，`alter_compile` 不提示！运行 `alter_compile` 后，你应该检查包的状态以确保编译成功。

如果你提供的存储对象名称不存在或类型错误，你会得到：

```
ORA-20000: Unable to compile PACKAGE 'BLICK', insufficient privileges or does not exist
```
