When adjusting the size of the Shared Pool, the total size of the new Shared Pool, Database Buffer Cache and Redo Log Buffer cannot exceed the value specified by **SGA_MAX_SIZE**.

![](bbox=[0.13, 0.19, 0.23, 0.27])

Attempting to increase the size the Shared Pool past the limit imposed by the **SGA_MAX_SIZE** parameter in the `init.ora` will cause an **ORA-04033: Insufficient memory to grow pool** error.

# Manually Increasing the Shared Pool Size

The Shared Pool can also be resized by shutting down the instance, changing the value for **SHARED_POOL_SIZE**, and then restarting the instance. This technique is required whenever you need to increase the value of **SGA_MAX_SIZE** so that a larger value for **SHARED_POOL_SIZE** can be specified.

![](bbox=[0.12, 0.44, 0.23, 0.53])

Shutting down and then restarting the instance will produce artificially low Shared Pool hit ratios until the instance “warms up” and the Shared Pool has reloaded application SQL statements.

# Real World Scenario

# How Big Should I Make the Shared Pool on My New Server?

When setting up a new server where no previous statistics are available, you are forced to take educated guesses at the sizing of SGA components like the Shared Pool. While Oracle provides some suggested values (small, medium, and large) for the various SGA components in its sample `init.ora`, these are rarely useful since “small, medium, and large” are only relative terms.

# Initial SGA Size Calculation

Instead of using the Oracle sample values, I use the following rule of thumb when setting the SGA size for a new system:

+   - Server Physical Memory × .55 = Total Amount of Memory to Allocate to All SGAs (TSGA)
+   - TSGA/Number of Oracle Instances on the Server = Total SGA Size Per Instance (TSAGI)