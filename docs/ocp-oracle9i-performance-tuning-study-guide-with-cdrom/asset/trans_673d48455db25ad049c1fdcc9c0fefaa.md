

-   如果在服务第 2 级需求后仍有剩余资源，可以最多启动两个额外的查询进程。
-   如果前一级别仍有剩余资源，可以为每个剩余的级别启动一个额外的查询进程。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_561_0.png)

资源管理器（Resource Manager）只能管理由服务器操作系统分配给实例的资源（即 CPU）。如果其他操作系统资源管理工具已经在操作系统层面管理资源到 Oracle 的分配，则资源管理器的有效性可能会受到限制。

除非在系统层面这些资源稀缺，否则 CPU 和并行查询（Parallel Query）资源限制不会影响处理。例如，如果您的服务器上存在过剩的 CPU 资源，那么 CPU 资源管理将不会起作用。这将允许通过计划指令（Plan Directive）被分配很少或没有资源的进程能够获取其所需的任何数量的 CPU 资源——甚至超过其分配指令中指定的数量。

## 管理撤销资源（Managing Undo Resources）

Oracle9i 引入了一种称为 UNDO_PLAN 的新计划指令。使用此计划指令，您可以在执行大型 DML 事务时控制用户允许消耗的撤销段（undo segment）空间量。对撤销段使用施加的限制以整个资源组的配额形式实现。如果撤销段空间的配额被超出，导致配额超出的用户执行 UPDATE 的操作，其 UPDATE 语句将被终止。在资源组的另一名成员释放撤销资源之前，该用户或用户资源组的任何其他成员都无法执行额外的 DML。

## 管理工作负载资源（Managing Workload Resources）

通过一种称为活动会话池（Active Session Pool）的机制，Oracle9i 允许您限制特定资源组的活跃并发会话数量。一旦资源组的成员达到允许的活跃并发会话数量，任何后续的活跃会话请求将由资源管理器排队，而不是立即处理。通过这种方式，活动会话池允许您保证每个资源组获得最低数量的资源，而又不允许单个资源组独占服务器的可用资源。任何排队的会话将在现有会话之一完成或变为非活动状态后执行。每个资源消费者组都有一个队列。排队的会话按先进先出（first-in first-out）原则分配资源。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_562_0.png)

> V$SESSION 动态性能视图中 CURRENT_QUEUE_DURATION 列的非零值表示该会话当前正由资源管理器排队。V$RSRC_CONSUMER_GROUP 的 QUEUE_LENGTH 列也包含用于监控特定资源组排队会话总数的有用信息。

允许的最大会话数和排队的最大会话数都可以在创建资源组时指定。最大会话数使用 ACTIVE_SESS_POOL_P1 资源管理器参数指定。会话在放弃之前排队的最长时间（以秒为单位）使用 QUEUING_P1 资源管理器参数指定。ACTIVE_SESS_POOL_P1 和 QUEUING_P1 参数的默认值均为 1,000,000。这意味着每个资源组允许的最大会话数为 1,000,000，且每个会话在放弃前可以排队长达 1,000,000,000 秒。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_563_0.png)

如果当前正在参与 DML 事务、执行查询或某些其他并行操作，则视为该会话处于活动状态。

## 管理执行时长（Managing Execution Duration）

使用新的 Oracle9i 资源计划指令 MAX_ESTIMATED_EXEC_TIME，您可以指定数据库操作完成所需的最大时长。一旦设置，资源管理器将使用 CBO（成本基于优化器）中的统计信息为每个数据库操作生成预计完成时间。然后将此估计值与此指定的最大允许时间进行比较。如果操作耗时将超过指定时长，则该操作将不会启动。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_563_1.png)

如果资源消费者组被分配了多个竞争的 maximum execution time（最大执行时间）指令，则将使用最短的最大时间。

现在您已对资源组、资源计划和资源计划指令如何用于管理 CPU、并行查询、会话、撤销和执行时间资源有了了解，接下来的部分将介绍实现这些资源管理功能的机制。

## 配置资源管理（Configuring Resource Management）

为了使用 Oracle9i 的资源管理功能，您必须先执行几个简单的配置操作。这些操作包括向正确的用户授予资源管理权限，创建资源管理对象，将这些资源分配给个人用户，以及设置实例的整体资源目标。

| **Oracle 目标** | | 设置数据库资源管理器 |
| :--- | :--- | :--- |

### 授予资源管理器权限（Granting Resource Manager Privileges）

将被允许管理资源组、计划和指令的用户必须被授予 ADMINISTER_RESOURCE_MANAGER 权限。与传统的系统权限不同（传统系统权限可以使用 GRANT ... TO ... 命令授予），ADMINISTER_RESOURCE_MANAGER 权限必须使用 Oracle 提供的名为 DBMS_RESOURCE_MANAGER_PRIVS 的 PL/SQL 包来授予。该包需要三个参数：GRANTEE_NAME、PRIVILEGE_NAME 和 ADMIN_OPTION。GRANTEE_NAME 是被授予权限的 Oracle 用户名称。PRIVILEGE_NAME 是被授予的权限名称（即 DBMS_RESOURCE_MANAGER_PRIVS）。ADMIN_OPTION 指示接收权限的用户是否可以将该权限传递给其他用户。图 10.7 展示了如何使用此包将带有 ADMIN 选项的 ADMINISTER_RESOURCE_MANAGER 权限授予用户 Regi。

**图 10.7** 授予资源管理器权限

```
SQL> EXECUTE dbms_resource_manager_privs.grant_system_privilege (grantee_name => "REGI", privilege_name => "ADMINISTER_RESOURCE_MANAGER", admin_option => TRUE);
PL/SQL procedure successfully completed.
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_564_0.png)

图 10.7 中的 -> 是执行 DBMS_RESOURCE_MANAGER_PRIVS 包的实际语法的一部分。为了使包成功执行，您还必须将所有参数输入在同一行，如图 10.7 所示。

如果需要撤销管理资源管理器的权限，请使用 DBMS_RESOURCE_MANAGER_PRIVS 包中的 REVOKE_SYSTEM_PRIVILEGE 过程。该过程接受两个参数：REVOKEE_NAME 和 PRIVILEGE_NAME。图 10.8 展示了如何撤销用户 Regi 的资源管理器权限。

**图 10.8** 撤销资源管理器权限

```
SQL> EXECUTE dbms_resource_manager_privs.revoke_system_privilege (revokee_name => "REGI", privilege_name => "ADMINISTER_RESOURCE_MANAGER");
PL/SQL procedure successfully completed.
```

一旦用户被分配了 ADMINISTER_RESOURCE_MANAGER 权限，该用户就可以创建其他资源管理器对象。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_565_0.png)

DBA_RSRC_MANAGER_SYSTEM_PRIVS 数据字典视图可用于显示哪些数据库用户被授予了 ADMINISTER_RESOURCE_MANAGER 权限。

### 创建资源管理器对象（Creating the Resource Manager Objects）

一旦适当的权限已被分配给将管理资源管理器的用户，您必须构建资源管理器所需的数据库对象。设置资源管理器需要以下步骤：

-   创建挂起区（pending area）
-   创建一个或多个资源消费者组
-   创建一个或多个资源计划
-   创建一个或多个资源计划指令
-   验证资源消费者组、计划和指令
-   将资源消费者组、计划和指令保存到数据库

#### 创建挂起区（Creating the Pending Area）

每当创建新的资源消费者组、计划或指令时，它将暂时存储在挂起区中，直到被验证并写入数据库。挂起区的目的是让 DBA 有机会在实施之前确认每个消费者组、计划和指令的定义是正确的。挂起区使用 DBMS_RESOURCE_MANAGER 包和 CREATE_PENDING_AREA 过程创建：

```
SQL> EXECUTE dbms_resource_manager.create_pending_area;
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_565_1.png)

数据库一次只能有一个挂起区。

