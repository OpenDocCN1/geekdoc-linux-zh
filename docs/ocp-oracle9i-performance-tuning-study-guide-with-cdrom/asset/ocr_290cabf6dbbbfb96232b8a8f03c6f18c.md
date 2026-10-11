and QUEUING_P1 parameters is 1,000,000. This means that a maximum of 1,000,000 sessions are allowed for each resource group and each session can be queued for up to 1,000,000,000 seconds before aborting.

![](bbox=[0.17, 0.19, 0.27, 0.25])

A session is considered active if it is currently participating in a DML transaction, performing a query, or some other parallel operation.

# Managing Execution Duration

Using the new Oracle9i resource plan directive called MAX_ESTIMATED_EXEC_TIME, you can specify the maximum length of time that a database operation can take to complete. Once set, Resource Manager will use the statistics in the CBO to generate an estimated completion time for each database operation. This estimate is then compared to this specified maximum allowed time. If the operation is going to take longer than the specified duration, then the operation will not be started.

![](bbox=[0.17, 0.48, 0.27, 0.54])

If a resource consumer group has several competing maximum execution time directives assigned to it, then the shortest maximum time will be used.

Now that you have a sense of how resource groups, resource plans, and resource plan directives can be used to manage CPU, Parallel Query, session, undo, and execution time resources, the following section explains the mechanics of implementing these Resource Management features.

# Configuring Resource Management

In order to use the resource management features of Oracle9i, you must first perform a few simple configuration operations. These operations include granting resource management privileges to the proper users, creating the resource management objects, assigning those resources to individual users, and setting the overall resource objectives for the instance.

| **Oracle Objective** | | Set up Database Resource Manager |
| :--- | :--- | :--- |