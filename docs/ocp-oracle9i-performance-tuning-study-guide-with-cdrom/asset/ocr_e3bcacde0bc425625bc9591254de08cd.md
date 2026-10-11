# **FIGURE 9.6** Example of Oracle's locking mechanism

![](bbox=[0.35, 0.14, 0.8, 0.49])

> The `init.ora` parameter **ROW_LOCKING** can be set to a value of **INTENT** if more restrictive, table-level locking is desired. The default value for this parameter is **ALWAYS**, which results in row-level locking.

Oracle uses two lock types to perform its locking operations: a *DML or data lock* and a *DDL or dictionary lock*. When performing these locking functions, Oracle also uses two different locking modes to achieve its goals of data concurrency and data consistency. The first mode, *exclusive*, is the most restrictive. An *exclusive lock* locks a resource until the transaction that took out the lock is complete. No other user can modify the resource while it is locked in exclusive mode. The second lock mode, *share lock*, is the least restrictive. A *share lock* locks the resource, but allows other users to also obtain additional share locks on the same resource. Each of these lock types and modes is discussed in the following sections.

# **Oracle Objective**

Define levels of locking