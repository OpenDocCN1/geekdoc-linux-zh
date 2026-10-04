We evaluate some of the ways that SQL Servers can be discovered from the Internet or from within the Enterprise. Whether an attacker is targeting a certain IP range or randomly scanning for low-hanging fruit, the tools and techniques they use for SQL Server discovery remain the same. Try some of the techniques and see how many SQL Servers you can find. The techniques we outline the following:

+   - Understanding and getting information from the SQL Server Resolution Service
- Performing OsqL -L probes to list servers
- Sc.exe sweeping of services
- Port scanning
- Using commercial alternatives

# Understanding the SQL Server Resolution Service

When Microsoft introduced the multiple instance capabilities of SQL Server 2000, they ran into a bit of a conundrum: How does a user who knows the name of an instance get connected to the proper TCP port (besides the default instance, which by default listeners on TCP 1433) are assigned dynamically?) Microsoft addressed this issue by creating a listener on UDP 1434, which refers to as the SQL Server Resolution Service. This service is responsible for sending a response packet that contains details to clients who send a specially requested format. This packet has all of the details to allow the client to connect to the desired instance, including the TCP port of each instance, the other reported netlibs, and which the server is clustered.

If you'd like to see the listener service in action, you can download the SQLPing at www.sqlsecurity.com to send that special request and see the results for yourself. The following is a sample request for any SQL Servers on your local subnet:

```
c:\sqlping 192.168.1.255
SQL-Ping 192.168.1.255
Listening...
ServerName:BRUTUS
InstanceName:MSSQLSERVER
IsClustered:No
```

![](bbox=[0.711, 0.946, 0.932, 0.966])