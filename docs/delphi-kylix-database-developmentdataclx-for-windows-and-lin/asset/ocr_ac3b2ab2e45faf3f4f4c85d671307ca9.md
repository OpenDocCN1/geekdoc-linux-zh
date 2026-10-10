# ## Summary

This chapter introduced you to the `TSQLConnection` component, which is used to establish and maintain a connection to an SQL database. Specifically, you learned:

+   * You can create either named or unnamed database connections.
+   * `TSQLConnection` surfaces a small number of events that are useful in allowing or preventing connections to, and disconnections from, a database.
+   * You can easily retrieve schema information (also called metadata) from a database connection, including table, field, index, and procedure data.
+   * `TSQLConnections` can be used to execute both DDL and DML commands against a database.
+   * If a database server supports transactions, you can control those transactions through the connection component.
+   * Several mechanisms are available for you to report feedback while performing operations against a database.

The next chapter introduces unidirectional datasets, which enable you to retrieve result sets from an SQL connection.

# ### ESTABLISHING AND USING DATABASE CONNECTIONS

# #### 1