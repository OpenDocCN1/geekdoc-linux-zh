# Chapter 8: Attacking Web Datastores

| Extended Stored Procedure | Description |
|---|---|
| xp_cmdshell <command> | The equivalent of cmd.exe—in other words, full command-line access to the database server. Cmd.exe is assumed, so you would only need to enter 'dir' to obtain a directory listing. The default current directory is %SYSTEMROOT%\System32. Reads a registry from the Hive. |
| xp_regread <rootkey>, <key>, <value> | There are several other registry-related procedures. Reading a value is the most useful. |
| xp_servicecontrol <action>, <service> | STARTs or STOPs a Windows service. |
| xp_terminate_process <PID> | Kills a process based on its process ID. |

**Table 9-5.** Parameterized Stored Procedures

database configurations. A SELECT from one of these tables usually requires the “master.." indication:

```
SELECT * FROM master..sysdevices
```

| System Table Object | Description |
|---|---|
| syscolumns | All column names and stored procedures for the current database, not just the master. |
| syssobjects | Every object (as stored procedures) in the database. |
| sysusers | All of the users who can manipulate the database. |
| sysfiles | The file name and path for the current database and its log file. |
| systypes | Data types defined by SQL or new types defined by users. |

**Table 9-6.** System Table Objects