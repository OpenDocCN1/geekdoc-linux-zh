
在这里，在成功执行 `UPDATE` 语句后，系统将向 A 和 B 发出 `COMMIT` 语句。暴露发生在 A 的 `COMMIT` 之后且 B 的 `COMMIT` 之前发生故障时。这会导致严重的完整性丢失，且无法自动恢复。解决此问题的唯一方法是终止事务并手动回滚 A 和 B 的更新。

可以使用以下技术来释放数据库中的锁：

- 使用命令杀死持有锁的会话：`ALTER SYSTEM KILL SESSION 'sid,serial#';`
- 要求锁持有者执行 `COMMIT`（提交）或 `ROLLBACK`（回滚）。
- 在 UNIX 提示中使用 `kill -9 <UserID>` 杀死用户 ID。
- 在两阶段提交事务中，使用 `ROLLBACK FORCE` 或 `COMMIT FORCE`。
- 从服务器管理器（Server Manager）模式或企业管理器（Enterprise Manager）杀死用户会话。

## 详细锁信息脚本

列表 25.9 一个详细锁信息脚本提供了有关数据库当前持有锁的完全解码信息。

### 列表 25.9 获取数据库锁的解码信息

```sql
set lines 200

set pages 66

break on Kill on sid on username on terminal

column Kill heading 'Kill String' format a13

column res heading 'Resource Type' format 999

column id1 format 999999

column id2 format 999999

column Lock heading 'Lock Held/Lock Requested' format a40

column mode heading 'Lock Held' format a20

column request heading 'Lock Requested' format a20

column serial# format 99999

column username format a10 heading "Username"

column terminal heading Term format a6
```

## 锁与分布式数据库

```sql
column tab format a30 heading Name "Table Name"

column owner format a9

column Laddr heading "ID1 - ID2" format a18

column Lockt heading "Lock Type" format a40

column command format a25

column sid format 990

rem L.SID||''||S.SERIAL# Kill,

select

nvl(S.USERNAME,'Internal') username,

l.SID,

nvl(S.TERMINAL,'None') terminal,

decode(command,
0,'None',decode(1.id2,0,U1.NAME||''))substr(T1.NAME,1,20),'None')) tab,

decode(command,
0,'BACKGROUND',
1,'Create Table',
2,'INSERT',
3,'SELECT',
4,'CREATE CLUSTER',
5,'ALTER CLUSTER',
6,'UPDATE',
7,'DELETE',
8,'DROP',
9,'CREATE INDEX',
10,'DROP INDEX',
11,'ALTER INDEX',
12,'DROP TABLE',
13,'--',
14,'--',
15,'ALTER TABLE',
16,'--',
17,'GRANT',
18,'REVOKE',
19,'CREATE SYNONYM',
20,'DROP SYNONYM',
21,'CREATE VIEW',
22,'DROP VIEW',
23,'--',
24,'--',
25,'--',
26,'LOCK TABLE',
27,'NO OPERATION',
28,'RENAME',
29,'COMMENT',
30,'AUDIT',
31,'NOAUDIT',
32,'CREATE EXTERNAL DATABASE',
33,'DROP EXTERNAL DATABASE',
34,'CREATE DATABASE',
35,'ALTER DATABASE',
36,'CREATE ROLLBACK SEGMENT',
37,'ALTER ROLLBACK SEGMENT',
38,'DROP ROLLBACK SEGMENT',
39,'CREATE TABLESPACE',
40,'ALTER TABLESPACE',
41,'DROP TABLESPACE',
42,'ALTER SESSION',
```

### 列表 25.9 延续

```sql
43, 'ALTER USER',
44, 'COMMIT',
45, 'ROLLBACK',
46, 'SAVEPOINT',
47, 'PL/SQL EXECUTE',
48, 'SET TRANSACTION',
49, 'ALTER SYSTEM SWITCH LOG',
50, 'EXPLAIN',
51, 'CREATE USER',
52, 'CREATE ROLE',
53, 'DROP USER',
54, 'DROP ROLE',
55, 'SET ROLE',
56, 'CREATE SCHEMA',
57, 'CREATE CONTROL FILE',
58, 'ALTER TRACING',
59, 'CREATE TRIGGER',
60, 'ALTER TRIGGER',
61, 'DROP TRIGGER',
62, 'ANALYZE TABLE',
63, 'ANALYZE INDEX',
64, 'ANALYZE CLUSTER',
65, 'CREATE PROFILE',
66, 'DROP PROFILE',
67, 'ALTER PROFILE',
68, 'DROP PROCEDURE',
70, 'ALTER RESOURCE COST',
71, 'CREATE SNAPSHOT LOG',
72, 'ALTER SNAPSHOT LOG',
73, 'DROP SNAPSHOT LOG',
74, 'CREATE SNAPSHOT',
75, 'ALTER SNAPSHOT',
76, 'DROP SNAPSHOT',
84,
85, 'TRUNCATE TABLE',
86, 'TRUNCATE CLUSTER',
87,
88, 'ALTER VIEW',
89,
90,
91, 'CREATE FUNCTION',
92, 'ALTER FUNCTION',
93, 'DROP FUNCTION',
94, 'CREATE PACKAGE',
95, 'ALTER PACKAGE',
96, 'DROP PACKAGE',
97, 'CREATE PACKAGE BODY',
98, 'ALTER PACKAGE BODY',
99, 'DROP PACKAGE BODY',
100, 'CREATE TYPE',
```
