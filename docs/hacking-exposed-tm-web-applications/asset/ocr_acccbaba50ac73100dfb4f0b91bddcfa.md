# Hacking Exposed Web Applications

# Stored Procedures for Enumerating SQL Server (continued)

| Stored Procedure | Description |
| --- | --- |
| sp_helpextext <object> | Describes the object. This is more useful for identifying areas where you can execute stored procedures. It rarely executes successfully. |
| sp_helpextextproc | Lists all extended stored procedures. |
| sp_spaceused [object] | With no parameters, returns the database name(s), size, and unallocated space. If an object is specified it will describe rows and other information as appropriate. |
| sp_who2 [username] (and sp_who) | Displays usernames, the host from which they've connected, the application used to connect to the database, the current command executed in the database, and several other pieces of information. Both procedures accept an optional username. This is an excellent way to enumerate SQL database's users as opposed to application users. |

# MS SQL Parameterized Extended Stored Procedures

| Extended Stored Procedure | Description |
| --- | --- |
| xp_cmdshell <command> | The equivalent of cmd.exe—in other words, full command-line access to the database server. Cmd.exe is assumed, so you would only need to enter 'dir' to obtain a directory listing. The default current directory is the %SYSTEMROOT%\System32. |