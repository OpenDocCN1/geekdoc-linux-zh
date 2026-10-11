# # Increasing the Number of Shared Servers

Whenever the allocated Shared Servers are unable to service the incoming requests for database activity, the PMON background process will dynamically start additional Shared Server processes, up to the limit specified by the MAX_SHARED_SERVERS value in init.ora. You can also explicitly add additional Shared Server processes either dynamically or manually.

# ## Oracle Objective

Diagnose and resolve performance issues with Oracle Shared Server processes

# ### Dynamically Adding Additional Shared Servers

Additional Shared Server processes can be added, up to the maximum specified by the init.ora parameter MAX_SHARED_SERVERS, by using the ALTER SYSTEM command:

```
SQL> ALTER SYSTEM SET shared_servers = 10;
```

This command will dynamically increase the number of Shared Servers to a total of 10.

# ### Manually Adding Additional Shared Servers

Additional Shared Servers can also be added by increasing the value for SHARED_SERVERS in the init.ora. Once the value has been changed, the instance must be shut down and restarted for the changes to take effect.

# ## Increasing the Number of Dispatchers

Unlike Shared Server processes, Dispatcher processes are not dynamically started by the PMON background process when user requests are coming in faster than they can be serviced. If the queries shown in the previous section reveal contention for Dispatchers, you can add additional Dispatchers dynamically or manually.

![](bbox=[0.15, 0.8, 0.25, 0.84])

User Processes remain tied to their original Dispatcher process for the duration of their session. Therefore, any newly added Dispatcher processes go unused by preexisting client connections. Only new connections to the instance will use the new Dispatchers.