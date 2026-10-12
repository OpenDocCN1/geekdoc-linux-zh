```
[oracle@ptc6 oracle]$ $ORACLE_HOME/bin/gencinstt
Created  /opt/oracle/product/10.1.0/db_1/lib/libcnlt10.a
```

This procedure assumes that the *oracle_home* environment variable has been set already. If it hasn't, you will need to set it or use the actual path name.

# Setting Up Oracle Net

Another important task is to set up Oracle Net so your database server can be accessed by Oracle client systems. Oracle Net can be configured by editing the following files.

+   ■ Listener file $ORACLE_HOME/network/admin/listener.ora

+   ■ Names file $ORACLE_HOME/network/admin/tnsnames.ora

In addition to manually editing the network configuration files, the network can be configured by using the graphical Net Configuration Assistant or netca. netca is invoked by running the program $ORACLE_HOME/bin/netca. You will then see the Java application shown in Figure 6-3.

Once the network has been configured, you are ready to start testing.

![](bbox=[0.14, 0.65, 0.88, 0.88])

**FIGURE 6-3.** *The Oracle Net Configuration Assistant*