In order to set the shared pool size on one node in the RAC cluster, use the following syntax:

```
SQL> ALTER SYSTEM SET shared_pool_size=150M COMMENT='6/2/2004
Set shared pool size
To 150M' SCOPE=BOTH SID='RAC1';
```

The ALTER SESSION command can be used to set session variables, not initialization parameters. In the case of the ALTER SYSTEM command with the parameters shown in the preceding table, the order of the parameters is important in some cases.

# When to Use a PFILE

Even though the spfile is the recommended method of tuning the Oracle instance, the use of a pfile is sometimes a convenient way of setting parameters. Some reasons that a pfile might be more convenient include the following:

+   Several parameters need to be set. When you are setting a number of parameters, you can change them in the pfile, start up the instance, and then create the spfile from the pfile.

+   The instance can’t start. If memory has been removed from the system, you might have trouble starting the instance. By using a pfile, you can restart the instance with new parameters.

Regardless of whether you use a pfile or an spfile, the result is the same. The characteristics of the instance are changed.

# Monitoring the Oracle Instance

So, how do you actually know what to tune? There are a number of different Oracle parameters that can be set (over 200 in Oracle 10g). Which ones you need to set and how to set them can fill up an entire book, and often does. In this book, you will not learn all of the Oracle initialization parameters that can be set, or how to set them. Rather, you will learn how to monitor and interpret some performance data in Oracle and Linux, and how to set some of the most common parameters.

# Monitoring the Instance with v$ and gv$ Views

There are many different ways to monitor the Oracle instance, including a number of excellent third-party tools. Most of these tools get their data from the same place: the v$ views. Oracle maintains a set of views that are a window into the performance of the Oracle instance. These views are known as the v$ views or the *dynamic performance* views. These views appear to be normal table data but in fact are dynamic values that keep track of the performance of the Oracle instance since the last time it was started.