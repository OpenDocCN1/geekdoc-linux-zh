
实例启动。因此，分配给用户 BETTY 的任何资源消费者组，其资源计划指令中第 1 级别的 CPU 分配比例应为 25%，以便她能够继续享受她习惯的性能体验。

## 监控资源管理器

在创建资源消费者组、资源计划和计划指令后，您可以在多个位置监控与资源管理器相关的话题，例如哪些消费者组存在、哪个计划处于活动状态，以及每个用户被分配了哪些计划。这些位置包括动态性能视图、DBA 数据字典视图和 Oracle Enterprise Manager。

### 资源管理器动态性能视图

包含与资源管理器相关信息的三个动态性能视图如下：

- V$SESSION
- V$RSRC_CONSUMER_GROUP
- V$RSRC_PLAN

![](img/832fbc6aca8b6075843ca6f2356c0a8d_575_0.png)

另外两个与资源管理器相关的 V$ 视图是 V$RSRC_PLAN_CPU_MTH 和 V$RSRC_CONSUMER_GROUP_CPU_MTH。这两个视图仅包含一列 NAME，分别显示资源消费者组和资源计划可用的资源分配方法。默认情况下，使用的方法分别是 EMPHASIS 和 ROUND-ROBIN。

#### V$SESSION

V$SESSION 中的 RESOURCE_CONSUMER_GROUP 列显示每个会话当前的资源消费者组。以下对 V$SESSION 的查询显示了该列的内容：

```sql
SQL> SELECT username, resource_consumer_group
  2  FROM v$session
  3  WHERE username IS NOT NULL;
```

| USERNAME | RESOURCE_CONSUMER_GROUP |
| :--- | :--- |
| DBSNMP | DEFAULT_CONSUMER_GROUP |
| SYSTEM | SYS_GROUP |
| APPS | POWER_USERS |
| BETTY | POWER_USERS |

此查询的输出显示，已为连接的数据库用户分配了三个资源消费者组：DEFAULT_CONSUMER_GROUP、SYS_GROUP 和 POWER_USERS。

#### V$RSRC_CONSUMER_GROUP

V$RSRC_CONSUMER_GROUP 动态性能视图包含有关已分配给活动资源消费者组的资源分配详细信息。表 10.8 描述了这个视图的内容。

**表 10.8 V$RSRC_CONSUMER_GROUP 视图的内容**

| 列 | 描述 |
| :--- | :--- |
| NAME | 资源消费者组的名称 |
| ACTIVE_SESSIONS | 当前分配给此资源消费者组的会话数 |
| EXECUTION_WAITERS | 分配给此资源消费者组、在可以执行前正在等待资源分配的会话数 |
| REQUESTS | 此资源消费者组中的用户已执行的数据库请求总数 |
| CPU_WAIT_TIME | 此资源消费者组中的用户等待访问 CPU 的总时间（以百分之一秒为单位） |
| CPU_WAITS | 资源消费者组中的用户等待访问 CPU 的总次数 |
| CONSUMED_CPU_TIME | 此资源消费者组中的用户消耗的总 CPU 时间（以百分之一秒为单位） |
| YIELDS | 此资源消费者组中的用户被迫将 CPU 让给具有更高优先级的其他资源消费者组中用户的次数 |
| SESSIONS_QUEUED | 分配给此资源消费者组且正在等待变为活动状态的用户会话数 |

理想情况下，如果您的用户被有效地分配到了资源消费者组，数据库中具有高优先级的用户应该很少遇到 CPU 等待（*EXECUTION_WAITERS* 和 *CPU_WAIT_TIME*），并且没有很多未服务的会话（*SESSIONS_QUEUED*）。如果并非如此，您可能需要重新审视您创建的资源分配，以尝试最小化这些事件的发生。

#### V$RSRC_PLAN

*V$RSRC_PLAN* 动态性能视图显示所有当前活动的资源计划的名称。此视图中仅有一列，*NAME*，其中包含在实例级别活动的资源计划的名称。以下查询展示了如何使用 *V$RSRC_PLAN* 来确定活动的资源计划：

```sql
SQL> SELECT *
  2  FROM v$rsrc_plan;

NAME
--------------------------------
TECHNICAL
```

此查询的输出显示 *TECHNICAL* 资源计划当前在数据库中处于活动状态。这可能是由于 `init.ora` 参数 *RESOURCE_MANAGER_PLAN* 被设置为 *TECHNICAL*，或者是因为发出了 *ALTER SYSTEM SET RESOURCE_MANAGER_PLAN = 'TECHNICAL'* 命令。

## 资源管理器数据字典视图

有六个数据字典视图包含与资源管理器相关的信息：

- DBA_RSRC_CONSUMER_GROUPS
- DBA_RSRC_CONSUMER_GROUPS_PRIVS
- DBA_RSRC_PLANS
- DBA_RSRC_PLAN_DIRECTIVES
- DBA_RSRC_MANAGER_SYSTEM_PRIVS
- DBA_USERS

### **DBA_RSRC_CONSUMER_GROUPS**

DBA_RSRC_CONSUMER_GROUPS 视图包含数据库中每个资源消费者组的信息。这些参数与创建资源消费者组时指定的参数相同。表 10.9 列出了此视图的内容。

**表 10.9 DBA_RSRC_CONSUMER_GROUPS 视图的内容**

| 列 | 描述 |
|:-------------|:-------------------------------------------------------------------|
| CONSUMER_GROUP | 资源消费者组的名称。 |
| CPU_METHOD | 用于向此消费者组分配 CPU 资源的 CPU 分配方法。 |
| COMMENTS | 创建资源消费者组时指定的注释（如果有）。 |
| STATUS | 资源消费者组的状况。新的、未提交的 RCG 状态为 PENDING。已提交的 RCG 状态为 ACTIVE。 |
| MANDATORY | 指示资源消费者组是否强制。强制 RCG 不能删除或修改。 |

以下对 DBA_RSRC_CONSUMER_GROUPS 的查询展示了如何检查之前创建的 POWER_USERS 资源消费者组的摘要信息：

```sql
SQL> SELECT consumer_group, cpu_method,
   2    status, mandatory
   3  FROM dba_rsrc_consumer_groups
   4 WHERE consumer_group = 'POWER_USERS';

CONSUMER_GROUP    CPU_METHOD STATUS     MANDATORY
---------------------------------------------------
POWER_USERS       ROUND-ROBIN ACTIVE     NO
```

### **DBA_RSRC_CONSUMER_GROUP_PRIVS**

DBA_RSRC_CONSUMER_GROUP_PRIVS 视图显示数据库中哪些用户或角色已被授予每个资源消费者组。表 10.10 列出了此视图中包含的列。

**表 10.10 DBA_RSRC_CONSUMER_GROUP_PRIVS 视图的内容**

| 列 | 描述 |
| :--- | :--- |
| GRANTEE | 被授予资源消费者组的用户名或角色 |
| GRANTED_GROUP | 授予给用户或角色的资源消费者组的名称 |
| GRANT_OPTION | 指示用户是否有能力将通过资源消费者组分配的权限传递给其他用户 |
| INITIAL_GROUP | 指示资源消费者组是否是用户的默认 RCG |

以下查询显示两个用户 **Apps** 和 **Betty** 的资源消费者组权限，这两个用户在之前的示例中被引用：

```sql
SQL> SELECT *
  2  FROM dba_rsrc_consumer_group_privs;

GRANTEE    GRANTED_GROUP          GRANT_OPT INITIAL_GROUP
---------  -------------------    --------- -------------
APPS       POWER_USERS            NO          NO
BETTY      POWER_USERS            NO          YES
PUBLIC     DEFAULT_CONSUMER_GROUP YES         YES
PUBLIC     LOW_GROUP              NO          NO
SYSTEM     SYS_GROUP              NO          YES
```

### DBA_RSRC_PLANS

DBA_RSRC_PLANS 视图显示数据库中已创建的所有资源计划。表 10.11 显示了此视图的内容。

**表 10.11 DBA_RSRC_PLANS 视图的内容**

| 列 | 描述 |
| :--- | :--- |
| PLAN | 计划的名称。 |
| NUM_PLAN_DIRECTIVES | 计划内的指令数量。 |
| CPU_METHOD | 用于向该计划分配 CPU 资源的方法（Emphasis 方法）。 |
| ACTIVE_SESS_POOL_MTH | 用于活动会话池资源的分配方法。 |
| PARALLEL_DEGREE_LIMIT_MTH | 用于向该计划分配并行资源的方法（Absolute 方法）。 |
| QUEUEING_MTH | 用于排队会话资源的分配方法。 |
| COMMENTS | 在计划创建时定义的注释（如果有）。 |
| STATUS | 资源计划的状态。新的未提交计划的状态为 PENDING。已提交计划的状态为 ACTIVE。 |
| MANDATORY | 指示资源计划是否强制。强制计划不能修改或删除。 |

以下查询显示了之前示例中创建的 TECHNICAL 和 FUNCTIONAL 资源计划的 DBA_RSRC_PLANS 输出。它还显示了一个未提交的资源计划，名为 AR_CLERK：

```sql
SQL> SELECT plan, status, mandatory
  2  FROM dba_rsrc_plans;
```

