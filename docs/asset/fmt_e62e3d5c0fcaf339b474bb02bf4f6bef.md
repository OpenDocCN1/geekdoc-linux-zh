
# 使用 ORACLE8i 提供的包

你可以程序化地为表、索引和簇分析统计信息。例如，你可以分析模式中所有或选定的对象，如列表 29.14 所示。

## 列表 29.14 runstats.sql—程序化运行统计信息

```sql
-- 分析模式下的所有表、索引和簇

-- 计算统计信息

SET OFF ECHO

ACCEPT PROMPT 'ANALYZE Method [[COMPUTE]:ESTIMATE,DELETE]: '

ACCEPT PROMPT 'IF Analyze Method is ESTIMATE, #Rows (0-n) [100]: '

ACCEPT PROMPT 'IF Analyze Method is ESTIMATE, %Rows (0-99) [20]: '

DECLARE

-- 定义的异常
bad_method_EXCEPTION; -- 用户输入无效的方法
bad_estrow_EXCEPTION; -- 用户输入无效的估计行数
bad_estpct_EXCEPTION; -- 用户输入无效的估计百分比

CURSOR analyze_obj IS
SELECT object_name, object_type
FROM user_objects
WHERE object_type = ANY ('TABLE', 'INDEX', 'CLUSTER');

-- 常量
METHOD CONSTANT VARCHAR(30) := NVL(UPPER('&&method'), 'COMPUTE');

-- 变量
estrow := NVL('&&est', '100'); -- 用户输入的估计行数
estpct := NVL('&&estpct', '20'); -- 用户输入的估计百分比

rec analyze_obj%ROWTYPE;
status NUMERIC := 0;
cnt NUMERIC := 0;

BEGIN
DBMS_OUTPUT.PUT_LINE('

-- 验证用户输入
IF (method NOT IN ('COMPUTE', 'ESTIMATE', 'DELETE')) THEN
  RAISE bad_method;
ELSIF (method IN ('COMPUTE', 'DELETE')) THEN -- 忽略估计行
estrow := NULL;
estpct := NULL;
ELSE
-- 选择了 estrow 输入：必须提供估计行数或百分比
IF (estrow < 1 AND estpct = 0) THEN
  RAISE bad_estrow;
ELSIF (estpct NOT BETWEEN 1 AND 99) THEN
  RAISE bad_estpct;
END IF;
-- -- 验证输入
OPEN analyze_obj;
LOOP
-- 分析模式对象
FETCH analyze_obj INTO rec;
EXIT WHEN analyze_obj%NOTFOUND;
-- 仅为此模式计算统计信息
DBMS_OUTPUT.PUT_LINE('Analyze ' || method || ' ' || rec.object_type || ' ' || rec.object_name || '\');
DBMS_ODL.analyze_object(rec.object_type, NULL, rec.object_name, 'COMPUTE');
DBMS_OUTPUT.PUT_LINE(' SUCCESSFUL!
');
ncnt := cnt + 1;
END LOOP;
-- 分析模式对象
CLOSE analyze_obj;
```

## 684 | 第 29 章 使用存储程序、程序包和提供的程序

### 列表 29.14 续

```sql
DBMS_OUTPUT.put_line(TO_CHAR(cnt)) || ' objects analyzed');

EXCEPTION
WHEN bad_method THEN
  DBMS_OUTPUT.put_line('Invalid Method! Must be COMPUTE, ESTIMATE or DELETE
  only);
WHEN bad_estrow THEN
  DBMS_OUTPUT.put_line('Invalid Est. #Rows! Must be >= 1');
WHEN bad_estpct THEN
  DBMS_OUTPUT.put_line('Invalid Est. %Rows! Must be between 1 and 99');
WHEN OTHERS THEN
  BEGIN
    status := SQLCODE;
    DBMS_OUTPUT.put_line(' FAILED with ' || SQLERRM(status));
    IF (analyze_obj%ISOPEN) THEN
      CLOSE analyze_obj;
    END IF;
  EXCEPTION WHEN OTHERS THEN
    NULL;
  END;
//
```

注意你必须进行的所有输入验证。部分原因是因为 `analyze_object` 自身做的工作非常少。例如，如果你使用 `COMPUTE` 方法提供行估算，你会得到以下结果：

`Analyze TABLE <table> failed with ORA-01490: invalid ANALYZE command.`

当我通过选择所有默认值来计算信息时，我的运行如下：

```
ANALYZE Method ([COMPUTE]|ESTIMATE|DELETE):
  IF Analyze Method IS ESTIMATE, #Rows (1-n) [1]:
IF Analyze Method IS ESTIMATE, %Rows (1-99) [20]:
old 12: METHOD CONSTANT VARCHAR2(30) := NVLUPPER('&method'), 'COMPUTE');
new 12: METHOD CONSTANT VARCHAR2(30) := NVLUPPER('&method'), 'COMPUTE');
old 14: estrow := NVLUPPER('&estrow', 'estrow'); -- user input expr. #rows
new 14: estrow := NVLUPPER('1', '1'); -- user input expr.
old 15: estpct := NVLUPPER('&estpct', '20'); -- user input expr. pct
new 15: estpct := NVLUPPER('20', '20'); -- user input expr. pct
```

`Analyze TABLE BONUS SUCCESSFUL`
`Analyze Compute TABLE EMP SUCCESSFUL`
`Analyze Compute INDEX PK_EMP SUCCESSFUL`
`Analyze Compute INDEX EMP SUCCESSFUL`
`Analyze Compute INDEX SALGRADE SUCCESSFUL`
`6 objects analyzed`
`PL/SQL procedure successfully completed.`

如果你输入了一个无效的方法，它的执行结果如下：

`Invalid Method! Must be COMPUTE, ESTIMATE or delete only`

这如你所愿。尝试运行一下并看看效果如何。

## 使用 ORACLE 8I 提供的程序包

此 `ANALYZE` 命令的实现并没有验证结构（VALIDATE STRUCTURE）或列出链表（LIST CHAINED ROWS）。从这方面来说，它是一个不完整的实现，但仍然非常有用。

如果你一直在跟着教程学习，已经熟悉该程序包中的 `put_line` 过程了。以下是关于程序包实现的一些细节：

- 每行都以换行符结束。
- 每行长度最多为 255 字节，包括换行符。
- 每行都存储在 PL/SQL 表中。
- 除非首先调用 `DBMS_OUTPUT.ENABLE`，否则什么都不会存储。
- 缓冲区大小必须在 2,000 到 1,000,000 范围范围内指定。

你使用该过程来开启输出功能。如果输出未先启用，则 `put_line` 调用将被忽略。当你启用输出时，也可以像下面一样指定缓冲区大小：

```sql
DBMS_OUTPUT.enable(1000000); -- 100 万字节是最大值
```

相反，你可以使用 `disable` 关闭输出，如下所示：

```sql
DBMS_OUTPUT.disable; -- 关闭输出
```
